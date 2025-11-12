---

### Plano de Simulação e Desenho de Experimentos (DoE) para o MIRF

**Objetivo Principal:** Validar quantitativamente a capacidade do framework MIRF de melhorar a resiliência e a eficiência de missões de UAS quando submetido a falhas de alto nível (táticas e estratégicas), em comparação com uma abordagem de linha de base (baseline).

**Ferramentas:**
*   **Simulador:** PlaNAR UTM
*   **Módulo sob Teste:** MIRF (em comparação com o MRCF sem reconfiguração estratégica)
*   **Agentes:** Drones simulados com modelos de voo e comunicação realistas.

---

#### 1. Definição da Linha de Base (Baseline)

Para medir o ganho proporcionado pelo MIRF, é crucial definir um comportamento de referência.

*   **Sistema Baseline:** O simulador PlaNAR UTM utilizando apenas o **MRCF (Mission Replanning and Control Framework)** com sua capacidade de replanejamento local.
*   **Comportamento Baseline:** Em caso de falha que impede a continuação da missão (ex: perda de GPS, violação de geofence), o agente autônomo executará apenas uma ação de segurança pré-programada e terminal, como **RTH (Return to Home)** ou **pouso imediato**. Não há reconfiguração estratégica da missão ou realocação de tarefas para outros agentes.

---

#### 2. Definição das Métricas de Performance (KPIs)

Estas são as métricas que serão coletadas durante cada execução da simulação para avaliar o desempenho.

| Sigla | KPI (Key Performance Indicator) | Descrição | Unidade |
| :--- | :--- | :--- | :--- |
| **TSM** | **Taxa de Sucesso da Missão** | Percentual de objetivos da missão concluídos com sucesso ao final da simulação. | % |
| **TTR** | **Tempo para Reconfiguração** | Tempo decorrido desde a **detecção** da anomalia pelo sistema até a **execução** da primeira ação de reconfiguração estratégica (ex: envio de novo plano a um drone substituto). | Segundos (s) |
| **DLD** | **Degradação da Latência de Decisão** | Aumento no tempo de resposta do sistema para tomar decisões táticas sob condições de falha. | % ou ms |
| **AIS** | **Impacto no Espaço Aéreo** | Volume de espaço aéreo adicional (4D) consumido pelo plano de reconfiguração em comparação com o plano original. Mede a eficiência espacial da solução. | m³·s |
| **NSI** | **Número de Intervenções de Segurança** | Quantidade de vezes que uma ação de segurança de último recurso (ex: *Safety Shield*) foi acionada. Um número menor indica melhor prevenção. | Contagem |

---

#### 3. Fatores e Níveis do Experimento

Estes são os parâmetros que serão variados para criar diferentes cenários de teste.

*   **Fator 1: Complexidade da Missão**
    *   **Nível 1 (Simples):** Voo BVLOS ponto a ponto com 1 UAS.
    *   **Nível 2 (Complexa):** Missão de cobertura de área com uma coalizão de 3 UAS.

*   **Fator 2: Tipo de Falha (Estímulo)**
    *   **Nível 1 (Espacial):** Fechamento de Zona Aérea (NOTAM súbito) que invalida parte da rota planejada.
    *   **Nível 2 (Sistêmica):** Perda de serviço GNSS em uma área específica, afetando um ou mais UAS.
    *   **Nível 3 (Emergência Externa):** Surgimento de tráfego tripulado em rota de colisão, exigindo evacuação imediata de um corredor aéreo.

*   **Fator 3: Arquitetura de Controle (o objeto do teste)**
    *   **Nível 1 (Baseline):** MRCF com ação de segurança terminal (RTH).
    *   **Nível 2 (MIRF):** MIRF com replanejamento estratégico e re-coalizão.

---

#### 4. Matriz de Desenho de Experimentos (DoE)

A combinação dos fatores e níveis acima gera a seguinte matriz de cenários a serem executados. Cada cenário deve ser executado múltiplas vezes (ex: N=10 execuções) para garantir significância estatística.

| ID do Cenário | Complexidade da Missão | Tipo de Falha | Arquitetura | Hipótese / O que Observar |
| :--- | :--- | :--- | :--- | :--- |
| **C1.1** | Simples (1 UAS) | Espacial (Zona) | Baseline | **Hipótese:** Missão falhará (TSM=0%). Drone executará RTH. |
| **C1.2** | Simples (1 UAS) | Espacial (Zona) | **MIRF** | **Hipótese:** MIRF replanejará a rota. TSM > 90%. Medir TTR e AIS. |
| **C2.1** | Simples (1 UAS) | Sistêmica (GNSS) | Baseline | **Hipótese:** Missão falhará (TSM=0%). Drone executará pouso de emergência. |
| **C2.2** | Simples (1 UAS) | Sistêmica (GNSS) | **MIRF** | **Hipótese:** MIRF usará navegação inercial/alternativa para RTH seguro. TSM=0%, mas NSI=0. |
| **C3.1** | Complexa (3 UAS) | Espacial (Zona) | Baseline | **Hipótese:** Um drone fará RTH. Cobertura da missão será incompleta (TSM < 70%). |
| **C3.2** | Complexa (3 UAS) | Espacial (Zona) | **MIRF** | **Hipótese:** MIRF redistribuirá a área do drone afetado entre os outros dois. TSM > 90%. Medir TTR. |
| **C4.1** | Complexa (3 UAS) | Sistêmica (GNSS) | Baseline | **Hipótese:** O drone afetado será perdido. Cobertura da missão será incompleta (TSM < 70%). |
| **C4.2** | Complexa (3 UAS) | Sistêmica (GNSS) | **MIRF** | **Hipótese:** MIRF substituirá o drone afetado (se houver um sobressalente) ou reconfigurará a coalizão. TSM > 80%. |
| **C5.1** | Complexa (3 UAS) | Emergência Ext. | Baseline | **Hipótese:** Todos os drones executarão RTH por segurança, falhando a missão (TSM=0%). |
| **C5.2** | Complexa (3 UAS) | Emergência Ext. | **MIRF** | **Hipótese:** MIRF coordenará uma evacuação ordenada do corredor e retomará a missão após a passagem. TSM > 80%. |

---

#### 5. Procedimento de Execução

1.  **Configuração:** Para cada ID de Cenário, configurar o simulador PlaNAR UTM com a missão, o número de agentes e a arquitetura de controle correspondente.
2.  **Execução e Injeção:** Iniciar a simulação. Em um tempo de simulação pré-determinado (ex: t=120s), injetar o evento de falha correspondente.
3.  **Coleta de Dados:** O simulador deve registrar em um log todos os eventos, decisões e mudanças de estado, com carimbos de tempo precisos. Os nós do Grafo de Fluxo de Falhas (FFG) são os pontos ideais para a instrumentação e coleta dos KPIs.
4.  **Finalização:** A simulação termina quando a missão é concluída, todos os objetivos falharam, ou um tempo máximo é atingido.
5.  **Repetição:** Repetir o processo N vezes para cada cenário para obter dados estatísticos robustos (média, desvio padrão) para cada KPI.

#### 6. Análise dos Resultados

Após a coleta, os dados serão analisados para validar as hipóteses:
*   **Comparação Direta:** Comparar os KPIs (TSM, TTR, etc.) entre os cenários com Baseline e MIRF (ex: C1.1 vs. C1.2).
*   **Análise Estatística:** Usar testes de hipóteses (como o teste t de Student) para confirmar se a melhoria observada com o MIRF é estatisticamente significativa.
*   **Visualização:** Gerar gráficos de barras (para TSM), box plots (para TTR) e mapas de calor (para AIS) para ilustrar claramente os resultados.

Este plano de simulação fornece um caminho claro e rigoroso para demonstrar o valor e a inovação do MIRF, gerando resultados concretos para sua pesquisa e publicações.

---
