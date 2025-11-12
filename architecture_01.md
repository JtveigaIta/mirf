---

### Arquitetura do Módulo de Log e Coleta de Dados (LC-Module)

**Princípios de Design:**

1.  **Estruturado e Consistente:** Todos os logs devem seguir um formato padronizado (ex: JSON), em vez de serem texto livre. Isso torna a análise automática trivial.
2.  **Assíncrono e de Baixo Impacto:** O processo de escrita dos logs não deve bloquear ou adicionar latência significativa à simulação principal.
3.  **Centralizado e Correlacionado:** Deve haver um ponto central que recebe os logs, mas cada log deve conter um `correlation_id` para rastrear um fluxo de falha específico do início ao fim.
4.  **Instrumentação Explícita:** O código não deve apenas "logar o que der", mas sim ser "instrumentado" em pontos específicos do Grafo de Fluxo de Falhas (FFG) para emitir eventos de log significativos.

---

#### 1. Componentes da Arquitetura

A arquitetura é composta por três componentes principais: o **Logger Client**, o **Log Broker** e o **Log Persistor**.

```mermaid
graph TD
    subgraph "Simulador PlaNAR UTM (Processo Principal)"
        A[Módulo de Injeção de Falhas]
        B[Agente UAS / MRCF]
        C[Módulo MIRF]
    end

    subgraph "LC-Module (Arquitetura de Log)"
        D[Logger Client API]
        E((Log Broker <br/> Fila de Eventos))
        F[(Log Persistor)]
        G{{Log File <br/> (JSON Lines)}}
    end

    A -- Emite Evento --> D
    B -- Emite Evento --> D
    C -- Emite Evento --> D
    
    D -- Envia Log (Assíncrono) --> E
    E -- Despacha Log --> F
    F -- Escreve em Disco --> G

    style A fill:#c5cae9
    style B fill:#c5cae9
    style C fill:#c5cae9
    style D fill:#b3e5fc
    style E fill:#f8bbd0
    style F fill:#dcedc8
    style G fill:#ffe0b2
```

*   **Logger Client API:** Uma interface simples e leve que os módulos do simulador (MIRF, Agentes, etc.) usam para emitir eventos de log. Sua única função é formatar a mensagem e enviá-la ao Broker.
*   **Log Broker (Fila de Eventos):** Um componente intermediário que recebe os logs do cliente. Ele funciona como uma fila (`Queue`) em memória que desacopla o simulador do processo de escrita em disco. Isso garante que, mesmo que a escrita em disco seja lenta, a simulação não será afetada.
*   **Log Persistor:** Um processo ou *thread* separado que consome os eventos da fila do Broker e os escreve de forma sequencial e eficiente no arquivo de log final.

---

#### 2. Formato do Log (Esquema JSON)

Cada entrada de log será um objeto JSON em uma única linha (formato [JSON Lines](https://jsonlines.org/)), o que facilita a leitura e o processamento por outras ferramentas.

**Esquema Base de um Evento de Log:**

```json
{
  "timestamp": "2025-11-12T15:30:15.123456Z", // Padrão ISO 8601 com alta precisão
  "simulation_id": "run_scenario_C4_2_rep_05", // ID único da execução da simulação
  "correlation_id": "fault_flow_1a2b3c4d",    // ID que agrupa todos os logs de um mesmo fluxo de falha
  "source_module": "MIRF.DecisionEngine",      // Módulo que originou o log
  "event_type": "DECISION_MADE",               // Tipo de evento, mapeado do FFG
  "log_level": "INFO",                         // Nível do log (INFO, WARN, ERROR)
  "message": "Novo plano de re-coalizão gerado para contornar falha de GNSS.", // Mensagem legível
  "data": { ... }                              // Carga útil com dados específicos do evento
}
```

---

#### 3. Instrumentação do Código para Coleta de KPIs

A chave é emitir logs específicos nos momentos exatos em que os KPIs podem ser medidos.

**Exemplo de Coleta do KPI `TTR` (Tempo para Reconfiguração):**

1.  **Momento da Detecção:** Quando o MIRF detecta a anomalia (transição `is_observed_as` no FFG), ele emite um log:

    ```json
    {
      "timestamp": "2025-11-12T15:30:15.123Z",
      "simulation_id": "sim_01",
      "correlation_id": "fault_abc",
      "source_module": "MIRF.Monitor",
      "event_type": "ANOMALY_DETECTED",
      "message": "Detectado desvio de rota do Agente UAS_02.",
      "data": { "agent_id": "UAS_02", "deviation": "75m" }
    }
    ```

2.  **Momento da Ação:** Quando o MIRF envia o comando de reconfiguração (transição `results_in` no FFG), ele emite outro log:

    ```json
    {
      "timestamp": "2025-11-12T15:30:17.456Z",
      "simulation_id": "sim_01",
      "correlation_id": "fault_abc",
      "source_module": "MIRF.ActionExecutor",
      "event_type": "RECONFIGURATION_ACTION_SENT",
      "message": "Comando de novo plano enviado ao Agente UAS_03 para assumir tarefa.",
      "data": { "affected_agent": "UAS_02", "substitute_agent": "UAS_03" }
    }
    ```

**Análise Post-Hoc:** Um script de análise pode então processar o arquivo de log, agrupar todos os eventos com o mesmo `correlation_id`, encontrar os eventos `ANOMALY_DETECTED` e `RECONFIGURATION_ACTION_SENT`, e calcular a diferença entre seus `timestamps`. O resultado é o valor do KPI `TTR` para aquele fluxo de falha.

**Coleta de outros KPIs:**

*   **TSM (Taxa de Sucesso da Missão):** No final da simulação, um evento `MISSION_COMPLETED` é logado com o status final e o percentual de objetivos alcançados.
    ```json
    "data": { "status": "PARTIAL_SUCCESS", "completion_rate": 0.85 }
    ```
*   **AIS (Impacto no Espaço Aéreo):** O evento `RECONFIGURATION_ACTION_SENT` pode incluir no campo `data` o volume do plano original e do novo plano.
    ```json
    "data": { ..., "original_airspace_volume": 50000, "new_airspace_volume": 65000 }
    ```
*   **NSI (Número de Intervenções de Segurança):** Cada vez que o *Safety Shield* é ativado, ele emite um evento `SAFETY_SHIELD_ACTIVATED`. A análise final apenas conta a ocorrência desses eventos.

---

#### 4. Implementação (Exemplo em Python)

A implementação pode usar bibliotecas padrão do Python, tornando-a leve e robusta.

```python
# Pseudocódigo da implementação

import logging
import queue
import threading
import json
import time
from datetime import datetime

# 1. Fila central para o Log Broker
log_queue = queue.Queue()

# 2. Log Persistor (executa em uma thread separada)
def log_persistor(simulation_id):
    log_filename = f"{simulation_id}.log.jsonl"
    with open(log_filename, 'w') as f:
        while True:
            log_record = log_queue.get()
            if log_record is None:  # Sinal para parar
                break
            f.write(json.dumps(log_record) + '\n')
            log_queue.task_done()

# 3. Logger Client API
class LoggerClient:
    def __init__(self, module_name, simulation_id):
        self.module_name = module_name
        self.simulation_id = simulation_id

    def emit(self, event_type, message, data, correlation_id, level="INFO"):
        log_record = {
            "timestamp": datetime.utcnow().isoformat() + "Z",
            "simulation_id": self.simulation_id,
            "correlation_id": correlation_id,
            "source_module": self.module_name,
            "event_type": event_type,
            "log_level": level,
            "message": message,
            "data": data
        }
        log_queue.put(log_record)

# --- Uso no Simulador ---
# No início da simulação:
sim_id = "run_scenario_C4_2_rep_05"
persistor_thread = threading.Thread(target=log_persistor, args=(sim_id,))
persistor_thread.start()

# Em um módulo do MIRF:
mirf_logger = LoggerClient("MIRF.Monitor", sim_id)
corr_id = "fault_xyz" # Gerado no início do fluxo de falha
mirf_logger.emit("ANOMALY_DETECTED", "...", {}, corr_id)

# No final da simulação:
log_queue.put(None)
persistor_thread.join()
```
