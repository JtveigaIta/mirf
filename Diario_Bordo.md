PESQUISAS 12.11.2025 (Objetivo, produzir uma linha de AÇÃO e DoE Mínimo Conceitual)
---

Compreendido. A sua necessidade é por um modelo conceitual que vá além de uma simples Rede de Petri, focando em **falhas de alto nível (táticas e estratégicas)** e que seja diretamente aplicável a um simulador como o PlaNAR UTM. O objetivo é permitir a execução de **Testes de Missão e Desenho de Experimentos (DoE)**, onde eventos do mundo ATM/UTM (como fechamento de zonas) são os estímulos, e os resultados são medidos por KPIs operacionais (latência de decisão, impacto no espaço aéreo, etc.).

A inspiração no projeto ADACORSA é perfeita, pois ele foca na resiliência e certificação, que são os pilares do MIRF.

A seguir, apresento um modelo conceitual para um **Grafo de Fluxo de Falhas (Fault Flow Graph - FFG)**, projetado para ser o núcleo do motor de simulação de falhas do MIRF. Este modelo é mais rico que uma Rede de Petri, pois incorpora semântica, hierarquia e contratos.

---

### Modelo Conceitual: Grafo de Fluxo de Falhas (FFG) para o MIRF

Este modelo descreve como um **evento adverso** (a falha) se propaga através das camadas de decisão do sistema, desde sua origem até a execução de uma resposta e a avaliação de seu impacto.

#### 1. Elementos do Grafo (Ontologia Mínima)

O grafo é composto por nós e arestas com significados bem definidos (semântica).

**Nós (Nodes):** Representam estados, entidades, eventos ou informações no sistema.

| Tipo de Nó | Descrição | Exemplo |
| :--- | :--- | :--- |
| `Event` | Um estímulo externo ou interno que inicia um fluxo de falha. | Perda de sinal GNSS, Notificação de Zona Restrita (NOTAM). |
| `SystemState` | O estado atual de um componente ou do sistema. | `GNSS_DEGRADED`, `COALITION_INCOMPLETE`. |
| `Observation` | A percepção de uma mudança de estado pelo MIRF. | "Telemetria indica desvio de rota > 50m". |
| `Diagnosis` | A conclusão do MIRF sobre a causa raiz do evento. | `ROOT_CAUSE: GPS_JAMMING`. |
| `Decision` | Uma escolha estratégica ou tática feita pelo MIRF. | `DECISION: INITIATE_RTH`. |
| `Action` | Um comando concreto enviado a um agente ou ao simulador. | `COMMAND: SET_MODE('RTH')`. |
| `KPI_Metric` | Um indicador de performance a ser medido. | `Decision_Latency`, `Airspace_Impact`. |

**Arestas (Edges):** Representam a relação causal ou temporal entre os nós.

| Tipo de Aresta | Descrição | Exemplo |
| :--- | :--- | :--- |
| `triggers` | Um evento que causa uma mudança de estado. | `Event` --triggers--> `SystemState` |
| `is_observed_as` | Um estado do sistema que é percebido pelo MIRF. | `SystemState` --is_observed_as--> `Observation` |
| `leads_to` | Uma observação que leva a um diagnóstico ou decisão. | `Observation` --leads_to--> `Diagnosis` |
| `results_in` | Uma decisão que resulta em uma ação concreta. | `Decision` --results_in--> `Action` |
| `impacts` | Uma ação ou estado que afeta um KPI. | `Action` --impacts--> `KPI_Metric` |

---

#### 2. Diagrama do Grafo de Fluxo de Falhas (FFG)

Este diagrama mostra o fluxo completo, desde a injeção do evento até a medição do impacto.

```mermaid
graph TD
    subgraph "1. Estímulo (Injeção de Falha)"
        A[E: Evento ATM <br/> 'Zona de Exclusão Aérea Ativada']
    end

    subgraph "2. Propagação e Observação"
        A -- triggers --> B(S: Estado do Sistema <br/> 'Rota Atual Inválida')
        B -- is_observed_as --> C(O: Observação <br/> 'Plano de Voo viola Geofence Ativa')
    end

    subgraph "3. Análise e Decisão (Núcleo do MIRF)"
        C -- leads_to --> D(D: Diagnóstico <br/> 'Conflito Espacial Crítico')
        D -- leads_to --> E(De: Decisão <br/> 'Replanejar Rota para Contornar Zona')
    end

    subgraph "4. Ação e Execução"
        E -- results_in --> F(A: Ação <br/> 'Enviar Novo Plano de Voo ao Agente')
        F -- impacts --> G(S: Estado do Sistema <br/> 'Drone em Rota Replanejada')
    end

    subgraph "5. Medição de Impacto (KPIs)"
        E -- impacts --> KPI1(K: KPI <br/> 'Latência de Decisão (TTR)')
        F -- impacts --> KPI2(K: KPI <br/> 'Impacto no Espaço Aéreo (Volume Adicional)')
        G -- impacts --> KPI3(K: KPI <br/> 'Sucesso da Missão (TSM)')
    end

    %% Styling
    style A fill:#ffcdd2,stroke:#b71c1c
    style B fill:#ffe0b2,stroke:#333
    style C fill:#fff9c4,stroke:#333
    style D fill:#c5cae9,stroke:#333
    style E fill:#b3e5fc,stroke:#333
    style F fill:#dcedc8,stroke:#333
    style G fill:#e1f5fe,stroke:#333
    style KPI1 fill:#f8bbd0,stroke:#333
    style KPI2 fill:#f8bbd0,stroke:#333
    style KPI3 fill:#f8bbd0,stroke:#333
```

---

#### 3. Como Este Modelo Permite Testes de Missão e DoE

Este grafo não é apenas um desenho; ele é um **modelo executável** para a simulação. Veja como ele atende aos seus requisitos:

1.  **Injeção de Eventos ATM como Estímulos:**
    *   O ponto de partida do grafo é sempre um nó do tipo `Event`. Para o seu DoE, você pode criar uma biblioteca de eventos:
        *   `Event(type='AirspaceClosure', details={polygon: [...], start_time: '...', end_time: '...'})`
        *   `Event(type='GNSS_Outage', details={area: '...', level: 'degraded'})`
        *   `Event(type='MannedAircraft_Emergency', details={trajectory: [...], corridor: '...'})`
    *   O simulador PlaNAR UTM simplesmente "injeta" esses nós no grafo em tempos de simulação específicos para iniciar o fluxo.

2.  **Registro de KPIs Operacionais:**
    *   Os nós do tipo `KPI_Metric` são "coletores" de dados. Cada vez que uma aresta `impacts` aponta para um deles, um valor é registrado com um carimbo de tempo.
    *   **TSM (Taxa de Sucesso da Missão):** O nó `KPI3` é atualizado no final da simulação, verificando se o objetivo final da missão foi cumprido, mesmo após a falha.
    *   **TTR (Tempo para Reconfigurar / Latência de Decisão):** O nó `KPI1` calcula a diferença de tempo entre o carimbo de tempo do nó `Observation` (quando o problema foi notado) e o do nó `Decision` (quando a solução foi decidida).
    *   **Impacto no Espaço Aéreo:** O nó `KPI2` pode calcular o volume de espaço aéreo adicional necessário para a nova rota em comparação com a original, uma métrica crucial para operações em larga escala.

3.  **Integração com a Arquitetura do MIRF:**
    *   **Camada de Observação (`Observation`):** Corresponde aos monitores de telemetria e conformidade.
    *   **Camada de Análise (`Diagnosis`):** É onde a base de conhecimento especialista e os modelos de ML do MIRF atuam para classificar a falha.
    *   **Camada de Decisão (`Decision`):** Representa o planejador de coalizão (MAS) e o motor de replanejamento estratégico.
    *   **Camada de Ação (`Action`):** É a interface que traduz a decisão em um comando para o agente (via Behavior Tree, por exemplo) ou para o simulador.

### Próximos Passos Práticos

Com base neste modelo conceitual, podemos avançar para:

1.  **Definir o Esquema de Dados (YAML/JSON):** Formalizar a estrutura de cada tipo de nó e aresta em um formato de dados, criando um "dicionário" para o seu simulador.
2.  **Esboçar um Plano de Simulação (DoE):** Criar uma matriz de experimentos. Por exemplo:
    *   **Cenário 1:** Voo BVLOS simples. **Injetar:** `AirspaceClosure`. **Medir:** TTR, Sucesso da Missão.
    *   **Cenário 2:** Missão de cobertura com 3 drones. **Injetar:** `GNSS_Outage` em um drone. **Medir:** TTR para re-coalizão, degradação da cobertura, latência de decisão.
3.  **Produzir uma Bibliografia em BibTeX:** Fornecer as referências acadêmicas que fundamentam este tipo de modelo (grafos semânticos, DoE em simulação, etc.) para fortalecer sua pesquisa.

Este modelo FFG lhe dá a estrutura conceitual necessária para construir um motor de simulação de falhas robusto e alinhado com os objetivos da sua pesquisa.

Gostaria de prosseguir com a definição do **esquema de dados em YAML (item 1)** e o **plano de simulação (item 2)**?

---------------------------------------------------------------------------------------------------------------------------
# Visão geral curta (alinhada ao ADACORSA)

ADACORSA trata da preparação técnica, sensoriamento e integração para viabilizar BVLOS de forma resiliente e certificável — excelente base de inspiração para MIRF porque enfatiza redundância, integração de sensores e alinhamento regulatório. ([adacorsa.eu][1])

Paralelamente, o conceito UTM / U-space (NASA, SESAR) fornece o *contexto operacional* e os serviços esperados (conflito, coordenação, notificações, restrições de espaço) que o MIRF deve consumir/usar para decisões tático-estratégicas. Recomendo tratar o MIRF como um módulo de inteligência **acoplável** à infraestrutura UTM/U-space. ([NASA][2])

---

# O que significa “falhas de alto nível” (pré-tático / tático) — definição operacional

Falhas de alto nível são eventos que **afetam a missão ou a fruição do espaço aéreo**, não apenas um sensor ou atuador isolado. Exemplos:

* perda de aceitação de espaço (zona temporariamente restrita pela autoridade ATM);
* degradação da capacidade da coalizão (número de UAS disponíveis < exigido pela missão);
* perda de serviço de posicionamento seguro (integridade GNSS para missão tática);
* congestão de espectro/comunicação que reduz banda disponível e impede coordenação;
* conflito com tráfego tripulado que exige replanejamento tático imediato.

Essas categorias exigem **representação semântica no grafo** (nós que representam políticas, contratos, restrições espaciais), não apenas estados de hardware.

---

# Como modelar o grafo conceitual do MIRF para esses níveis

1. **Vocabulário mínimo (ontologia leve)** — nós semânticos:

   * `MissionIntent`, `MissionPlan`, `SpaceConstraint`, `CoalitionState`, `ServiceIntegrity(GNSS/C2)`, `TrafficConflict`, `PolicyConstraint`, `ReconfigurationPlan`.
2. **Arestas semânticas** (direcionadas + guards):

   * `violates`, `triggers_replan`, `requires_coalition_change`, `low_integrity`, `notifies_ATM`.
3. **Guards e contratos**:

   * cada aresta tem *precondição* (ex.: `mission_loss_margin > 0.2`) e *postcondição* (ex.: `plan_validated == true`).
4. **Atributos por nó**:

   * `confidence` (0..1), `latency_budget_ms`, `authority_source` (UTM, operator, C2), `impact_score` (missão, segurança).
5. **Hierarquia temporal**:

   * níveis pré-tático (planejamento de slot/intent), tático (replanejamento em tempo real), operacional (safety shield locais).
6. **Eventos externos**:

   * modelar inputs vindos de ATM legada como *streams* ou *snapshots* (p.ex. NOTAMs, TIS-B analogs, zones), com carimbo UTC e proveniência.

> Técnica recomendada: persistir o grafo canônico em YAML/JSON-LD (metadados + esquema JSON-Schema). Isso facilita validação e tradução para qualquer tecnologia (MAS, RL, orquestrador centralizado).

---

# Integração com sistemas legados ATM (espaços críticos, modelos avionics, tratamento de falhas)

1. **Interfaces/contratos**:

   * definir *schema* de mensagens para: `SpaceConstraint` (polygon + temporal window + priority), `TrafficSnapshot` (tracks + confidence), `AirspaceStatus` (restrictions), `AvionicsModelSpec` (capabilities & failure modes).
   * usar formatos de longa vida: GeoJSON (espaços), OpenAPI/Protobuf para mensagens.
2. **Normalização / Fusion**:

   * criar camada de *adapter* que transforma formatos ATM legados (ex.: ASTERIX, SWIM feeds, NOTAM strings) para o grafo canônico.
3. **Modelos avionics**:

   * representar capacidades como atributos: `RNP`, `integrity_levels`, `RTH_capability`, `time_on_station`.
   * falhas avionics de alto nível mapeadas para `impact_score` no grafo (p.ex. perda de “mission-critical navigation” → impact_score alto).
4. **Espaços críticos / zonas**:

   * representar zonas com prioridades e regras de entrada/evacuação; conectá-las ao nó `PolicyConstraint`.
5. **Verificação de conformidade**:

   * cada plano de reconfiguração deve ser validado contra `PolicyConstraint` (regras de ATM) antes de execução automatizada.

Essas abordagens progridem a visão ADACORSA de integração sensor/automotive e o encaixe no UTM/UTM services. ([adacorsa.eu][1])

---

# Simulação e testbed — recomendações práticas

Para validar falhas de alto nível e pre/tático em ambientes multi-UAS, recomendo um *co-simulation* stack que permita testar comportamento tático, interdependências e integração ATM:

* **BlueSky** (simulador de tráfego/ATM open) para modelagem de tráfego e interfaces ATM. ([ResearchGate][3])
* **Airsim / Gazebo / simuladores de veículo** para dinâmica do UAS e modelos avionics; usar co-sim (ex.: BlueSky + AirSim) para conectar fluxo de tráfego com sensores e modelos de falha. Há trabalhos mostrando esse approach (co-simulation Digital Twin). ([dspace.lib.cranfield.ac.uk][4])
* **Ambientes para RL/benchmarks UTM**: BlueSky-Gym facilita pesquisa em ATC/UTM com RL e experimentos reprodutíveis. Útil para treinar políticas de replanejamento tático. ([sesarju.eu][5])
* **Testes de missão e DoE**: injete eventos ATM (fechamento de zona, emergência tripulada, perda de serviço GNSS) como estímulos e registre KPIs (TSM, TTR, latência de decisão, impacto de espaço).

Também há literatura e frameworks recentes sobre *hierarchical mission replanning* e *resilient mission planning* que descrevem abordagens para reatribuição e replanejamento entre múltiplos UAVs — úteis para estruturar a camada tática/estratégica do MIRF. ([ScienceDirect][6])

---

# Referências acadêmicas e técnicas (selecionadas — leitura recomendada)

Eu priorizei trabalhos e documentos que legitimam abordagem UTM / U-space e mission-level replanning:

1. ADACORSA — dissemination & goals (BVLOS, sensores, integração regulatória). ([adacorsa.eu][1])
2. NASA UTM Concept of Operations (UTM CONOPS v1.0) — base conceitual UTM e serviços esperados. ([NASA][2])
3. SESAR U-space pages — serviços U-space e requisitos operacionais para drones. ([sesarju.eu][7])
4. Wu, Y., "Hierarchical mission replanning for multiple UAV" (2023) — métodos para replanejamento hierárquico em formações/UAV multi. Útil para estruturar níveis tático/estratégico. ([ScienceDirect][6])
5. BlueSky/BlueSky-Gym + co-simulation trabalhos (BlueSky, AirSim integration) — para construção de testbeds reprodutíveis. ([ResearchGate][3])

(se quiser, eu posso fornecer uma bibliografia em BibTeX/EndNote formatada com essas e outras referências adicionais, incluindo papers sobre coalition formation, MAS e diagnósticos táticos.)

---

# Artefatos que eu posso gerar agora (práticos)

Sem precisar de mais dados, eu já posso:

1. Gerar o **grafo conceitual canônico** (nós/arestas/atributos/contratos) em **YAML** com níveis (pré-tático/tático/operacional) e exemplos de contratos.
2. Gerar um **mapa de integração** (JSON) que descreve adaptadores para: NOTAM/NOTAM-like, tracks (ASTRIX/GeoJSON), AvionicsModel schema, e espaço crítico (GeoJSON).
3. Esboçar um **plano de simulação / DoE** para MRCF que injeta falhas de alto nível (com matrizes de cenário e KPIs a coletar).
4. Produzir uma **lista BibTeX** com as referências acima + papers sobre coalition planning / resilient mission planning.

Quer que eu gere agora o **grafo conceitual em YAML** (item 1) e o **plano de simulação** (item 3)? Se preferir, já gero também a bibliografia em BibTeX junto.

---

[1]: https://adacorsa.eu/?utm_source=chatgpt.com "ADACORSA - About"
[2]: https://www.nasa.gov/wp-content/uploads/2024/04/2018-utm-conops-v1-0-508.pdf?emrc=94dcbb&utm_source=chatgpt.com "Unmanned Aircraft System (UAS) Traffic Management (UTM)"
[3]: https://www.researchgate.net/publication/304490055_BlueSky_ATC_Simulator_Project_an_Open_Data_and_Open_Source_Approach?utm_source=chatgpt.com "(PDF) BlueSky ATC Simulator Project: an Open Data and ..."
[4]: https://dspace.lib.cranfield.ac.uk/bitstreams/07f58210-082b-4f05-9241-2b048d8c2ee5/download?utm_source=chatgpt.com "Co-simulation Digital Twin Framework for Testing Future ..."
[5]: https://www.sesarju.eu/sites/default/files/documents/sid/2024/papers/SIDs_2024_paper_021%20final.pdf?utm_source=chatgpt.com "BlueSky-Gym: Reinforcement Learning Environments for ..."
[6]: https://www.sciencedirect.com/science/article/abs/pii/S0140366423000191?utm_source=chatgpt.com "Hierarchical mission replanning for multiple UAV ..."
[7]: https://www.sesarju.eu/U-space?utm_source=chatgpt.com "U-space and urban air mobility"
