PESQUISAS 12.11.2025 (Objetivo, produzir uma linha de AÇÃO e DoE Mínimo Conceitual)
---

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
