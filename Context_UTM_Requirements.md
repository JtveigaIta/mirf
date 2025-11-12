
# Diretrizes e Boas Práticas para a Especificação de Requisitos de Sistemas UTM

## Introdução

O Gerenciamento de Tráfego de Sistemas de Aeronaves Não Tripuladas (**UTM - Unmanned Aircraft Systems Traffic Management**) é um ecossistema de serviços digitais e procedimentos que visa garantir a segurança e a eficiência das operações de drones em baixas altitudes, separadamente, mas em coordenação com o sistema tradicional de Gerenciamento de Tráfego Aéreo (**ATM - Air Traffic Management**). A especificação de requisitos para um sistema UTM é um desafio complexo, dada a natureza distribuída, digital e altamente dinâmica das operações.

Para garantir a interoperabilidade e a aceitação global, a especificação de requisitos deve estar alinhada com as diretrizes e normas estabelecidas pelos principais órgãos reguladores e de padronização internacionais. Este documento detalha as diretrizes e boas práticas para a especificação de requisitos de sistemas UTM, com base nos referenciais normativos da **ICAO**, **FAA/NASA**, **EASA**, **ASTM** e **JARUS**, e apresenta uma comparação estruturada entre as abordagens regulatórias dos Estados Unidos e da Europa.

## 1. Referenciais Normativos e Diretrizes Internacionais

A base para a especificação de requisitos de um sistema UTM reside em um conjunto de documentos e normas que definem o *framework* operacional, a arquitetura de referência, os serviços essenciais e os padrões de segurança.

| Organismo / Documento | Descrição e Relevância para Requisitos UTM | Foco Principal |
| :--- | :--- | :--- |
| **ICAO** / UTM Framework (Edição 4) | Fornece um **framework comum** e **princípios centrais** para a harmonização global entre ATM e UTM. O sistema deve seguir estes princípios para assegurar a aceitação internacional e a interoperabilidade. | Harmonização Global e Princípios de Alto Nível |
| **FAA / NASA** / UTM ConOps v2.0 e FIMS | Define a **arquitetura de referência** dos EUA. O **FIMS (Flight Information Management System)** é o modelo central para a supervisão digital e mediação de dados entre a FAA e os Provedores de Serviço (USSs). | Arquitetura de Referência, Supervisão Digital e Interoperabilidade (EUA) |
| **EASA** / Regulamento (UE) 2021/664 (U-space) | Estabelece o **quadro regulatório europeu** para o U-space, um espaço aéreo definido. Define os **serviços essenciais** (e.g., Identificação de Rede, Consciência Geográfica, Autorização de Voo) e a autonomia operacional dos Provedores de Serviço U-space (USSP). | Serviços Essenciais, Autonomia Operacional e Regulamentação (Europa) |
| **ASTM** / F3448 / F3548 | Especificações técnicas detalhadas para a **interoperabilidade** e o **intercâmbio de dados** entre USSs e autoridades. A F3548 é o padrão para interoperabilidade de sistemas UTM/USS. | Padronização Técnica e Interoperabilidade USS-USS/USS-Autoridade |
| **JARUS** / SORA (Specific Operations Risk Assessment) | Diretrizes de **segurança** e **avaliação de risco** operacional específico. Fundamental para a definição de **Níveis de Garantia (DAL)** e requisitos de mitigação de risco. | Segurança Operacional, Avaliação de Risco e Níveis de Garantia |

## 2. Comparação de Abordagens: EUA (FAA/NASA) vs. Europa (EASA U-space)

Embora ambas as abordagens busquem a gestão segura do tráfego de UAS em baixas altitudes, elas diferem significativamente em sua arquitetura e filosofia regulatória. A especificação de requisitos deve refletir a escolha de um ou outro modelo, ou buscar a compatibilidade entre eles.

| Característica | Abordagem EUA (FAA/NASA) | Abordagem Europa (EASA U-space) |
| :--- | :--- | :--- |
| **Modelo Central** | **FIMS (Flight Information Management System)**. Atua como um *hub* centralizado de dados, mediando a troca de informações entre a FAA e os USSs. | **Modelo Distribuído (U-space)**. Foco na interoperabilidade direta entre os Provedores de Serviço U-space (USSP), com a Autoridade Aeronáutica (ANSP) definindo o espaço aéreo e as restrições. |
| **Supervisão** | **Supervisão Digital Centralizada**. A FAA, via FIMS, tem acesso e controle centralizado sobre os dados de intenção de voo e restrições. | **Supervisão Descentralizada**. A ANSP/DECEA mantém a responsabilidade final, mas a coordenação tática e a deconflição são realizadas pelos USSPs. |
| **Regulamentação** | Baseada no **UTM ConOps v2.0** e em regras de operação específicas. Foco na **interoperabilidade** e no acesso a dados para a FAA. | Baseada no **Regulamento (UE) 2021/664**. Criação de um **espaço aéreo definido (U-space)** com serviços obrigatórios. |
| **Interoperabilidade** | Foco na interoperabilidade entre **USSs e FIMS**. Padrões ASTM (F3548) são cruciais para a comunicação entre USSs. | Foco na interoperabilidade entre **USSPs**. Os USSPs são os principais responsáveis pela coordenação tática. |
| **Exemplo Prático** | Validação de sistemas UTM (e.g., ANRA Technologies) contra a **ASTM F3548-21** para aprovação da FAA. | Implementação dos **Serviços Essenciais do U-space** (e.g., Identificação de Rede, Consciência Geográfica) em países como Espanha e Alemanha. |

A escolha da arquitetura (centralizada via FIMS ou distribuída via U-space) impacta diretamente os requisitos de interface, segurança e responsabilidade do sistema UTM a ser especificado.

## 3. Estrutura de Requisitos de Sistemas UTM

A especificação de requisitos deve ser dividida em escopos claros, refletindo as funções críticas do sistema e os atores envolvidos. Uma estrutura de requisitos eficaz deve abranger as seguintes categorias, fornecendo a rastreabilidade necessária entre a necessidade regulatória e a implementação técnica:

### 3.1. Requisitos Funcionais (Serviços Essenciais)

Estes requisitos definem o que o sistema deve fazer para suportar as operações de UAS. Eles são a espinha dorsal do sistema UTM e estão intimamente ligados aos serviços definidos no U-space da EASA e nas capacidades do ConOps da FAA.

| Categoria | Descrição e Requisitos Chave | Referência Normativa |
| :--- | :--- | :--- |
| **Registro e Identificação** | O sistema deve registrar UAS, operadores e missões. Deve suportar a **Identificação Remota (Remote ID)**, permitindo que o UAS transmita sua identidade e posição em tempo real. | EASA (Serviço de Identificação de Rede), FAA (Requisitos de Remote ID) |
| **Consciência Geográfica (Geo-awareness)** | O sistema deve fornecer aos operadores e USSs informações atualizadas sobre **restrições estáticas e dinâmicas** do espaço aéreo (e.g., zonas proibidas, temporariamente restritas). | EASA (Serviço de Consciência Geográfica), FAA (FIMS para disseminação de restrições) |
| **Autorização de Voo** | O sistema deve processar, validar e autorizar planos de voo (ou intenções de voo) em tempo real, garantindo que a operação esteja em conformidade com as restrições do espaço aéreo. | EASA (Serviço de Autorização de Voo), FAA (ConOps para coordenação de intenção) |
| **Informação de Tráfego** | O sistema deve fornecer informações de tráfego em tempo real (posição e intenção de outros UAS) para permitir a **deconflição tática** e a separação segura. | EASA (Serviço de Informação de Tráfego), FAA (USSs para troca de dados) |
| **Monitoramento de Conformidade** | O sistema deve monitorar a execução do voo em relação ao plano autorizado e às restrições, gerando alertas em caso de desvio (non-conformance). | FAA (Supervisão via FIMS), EASA (Responsabilidade do USSP) |

### 3.2. Requisitos Não Funcionais (Qualidade e Segurança)

Estes requisitos definem como o sistema deve operar, com foco em atributos de qualidade essenciais para um sistema de segurança crítica.

| Categoria | Descrição e Requisitos Chave | Referência Normativa |
| :--- | :--- | :--- |
| **Interoperabilidade** | O sistema deve ser capaz de trocar dados de intenção, posição e restrições com outros USSs e com a Autoridade Aeronáutica (via FIMS ou diretamente). Deve aderir aos padrões de interface definidos. | **ASTM F3548** (Interoperabilidade USS-USS), FAA (FIMS Interface), ICAO (Harmonização) |
| **Segurança (Safety)** | O sistema deve ser projetado para mitigar riscos operacionais. A especificação de requisitos deve ser validada por uma **Avaliação de Risco Operacional Específico (SORA)**, definindo o **Nível de Garantia (DAL)** necessário para cada componente. | **JARUS SORA** (Avaliação de Risco), EASA (Requisitos de segurança operacional) |
| **Cibersegurança** | O sistema deve proteger a integridade, confidencialidade e disponibilidade dos dados críticos (planos de voo, posições, identidade do operador). Requisitos de gerenciamento de riscos de segurança da informação são mandatórios. | EASA (Regulamento 2023/203), Padrões ISO/IEC 27001 (mencionado em documentos relacionados à ASTM F3548) |
| **Desempenho e Escalabilidade** | O sistema deve ser capaz de processar um grande volume de dados em tempo real (e.g., latência de processamento de autorização de voo, taxa de atualização de posição). | Requisitos operacionais definidos no ConOps e nas necessidades do ANSP/DECEA. |

## 4. Exemplos Práticos e Sistemas Existentes: O "Como Fazer"

A implementação de sistemas UTM já é uma realidade global, com diferentes modelos em operação:

*   **EUA (FIMS-centric):** O modelo dos EUA está em fase de transição para a implementação completa do FIMS. Empresas como a **ANRA Technologies** e a **AirMap** (antes de sua aquisição) foram pioneiras, validando seus sistemas USS contra os padrões **ASTM F3548-21** para garantir a interoperabilidade com o futuro ecossistema da FAA. O foco é na troca de dados padronizada para que a FAA possa manter a supervisão. Um exemplo prático de requisito derivado desta abordagem é: **"O USS DEVE implementar a API de Interoperabilidade conforme a ASTM F3548-21 para troca de dados de intenção de voo com outros USSs e DEVE fornecer acesso de leitura ao FIMS para dados de voo autorizados."** [4] [2]

*   **Europa (U-space):** O U-space está sendo implementado em diversos países, como **Espanha**, **Alemanha** e **França**. Nesses sistemas, os **USSPs** (e.g., ENAIRE em Espanha, DFS em Alemanha) fornecem os serviços essenciais (Identificação, Geo-awareness, Autorização) de forma distribuída, mas coordenada. O projeto **CORUS-XUAM** (Concept of Operations for European UTM systems) é um referencial prático que detalha como esses serviços interagem no contexto da Mobilidade Aérea Urbana (UAM). Um exemplo prático de requisito derivado desta abordagem é: **"O USSP DEVE fornecer o Serviço de Consciência Geográfica, garantindo que as informações de restrições estáticas e dinâmicas sejam atualizadas e distribuídas aos operadores de UAS com uma latência máxima de 5 segundos."** [3] [1]

## Referências Bibliográficas

1.  **ICAO.** *Unmanned Aircraft Systems Traffic Management (UTM) – A Common Framework with Core Principles for Global Harmonization (Edition 4).* Disponível em: https://www.icao.int/sites/default/files/left-menu-pdfs/UTM%20Framework%20Edition%204.pdf
2.  **FAA / NASA.** *Unmanned Aircraft System (UAS) Traffic Management (UTM) Concept of Operations (ConOps) v2.0.* Disponível em: https://www.faa.gov/sites/faa.gov/files/2022-08/UTM_ConOps_v2.pdf
3.  **EASA.** *Commission Implementing Regulation (EU) 2021/664 of 22 April 2021 on a regulatory framework for the U-space.* Disponível em: https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32021R0664
4.  **ASTM International.** *Standard Specification for UAS Traffic Management (UTM) UAS Service Supplier (USS) Interoperability (F3548).* Disponível em: https://www.astm.org/f3548-21.html
5.  **JARUS.** *Specific Operations Risk Assessment (SORA) Main Body (JAR_doc_25).* Disponível em: http://jarus-rpas.org/wp-content/uploads/2024/06/SORA-v2.5-Main-Body-Release-JAR_doc_25.pdf
6.  **Aposporis, P.** *A review of global and regional frameworks for the Unmanned Aircraft Systems Traffic Management (UTM).* ScienceDirect, 2024. https://www.sciencedirect.com/science/article/pii/S2590198224000502
7.  **World Bank.** *TRAFFIC MANAGEMENT OF THE FUTURE, TODAY A Global Perspective on UTM.* Disponível em: https://documents1.worldbank.org/curated/en/099080524233017078/pdf/P171737-95642d3c-06d6-47b6-bab5-c8c783a42462.pdf

# Diretrizes e boas-práticas (normas / órgãos) para especificação de requisitos de sistemas UTM

Abaixo você tem um guia prático — organizado por organismo normativo — com as práticas recomendadas para **especificar requisitos** de um Sistema UTM (USS / FIMS / serviços U-space / SIPs). Cada bloco traz recomendações acionáveis (requisitos, métricas, verificação) e referências bibliográficas confiáveis para consulta. Todas as afirmações que podem ser verificadas têm referência imediata.

---

## Visão rápida (resumo executivo)

* Especifique requisitos em camadas: **arquitetura**, **serviços**, **segurança & privacidade**, **interoperabilidade**, **segurança funcional / risco**, **performances/SLAs**, **monitoramento & auditoria** e **documentação / rastreabilidade**. ([OACI][1])
* Use **modelos de dados padronizados** (FIMS / USS interfaces / ED-269/ED-318 quando aplicável) e defina contratos de serviço (APIs, formatos, semântica). ([Administração Federal de Aviação][2])
* Para segurança operacional, aplique avaliação de risco baseada em SORA/JARUS e requisitos de DAL quando componentes impactam segurança aérea. ([Jarus RPAS][3])

---

## ICAO — UTM Framework (Edição 4): orientações para requisitos de alto nível

O que exigir:

* **Compatibilidade ATM/UTM**: requisitos de interface, prioridades e troca de restrições dinâmicas (NOTAM analog). Especifique necessidades de interoperabilidade com ATM local (formatos, latência, semântica). ([OACI][1])
* **Core capabilities**: planeamento de voo, serviço tático de desconfliction, registro & histórico, notificações de emergência — cada capacidade vira uma suíte de requisitos funcionais e métricas (p.ex. latência de atualização de posse de espaço). ([OACI][4])
  Boas práticas de engenharia de requisitos:
* Mapear *capability → requisito funcional → métricas (KPI) → teste de aceitação*.
* Requisitos traceáveis à segurança operacional (rastreabilidade requisitos ⇄ riscos ⇄ mitigação). ([OACI][1])

---

## FAA / NASA (UTM ConOps v2.0 & FIMS) — requisitos de integração e dados

O que exigir:

* **FIMS**: defina requisitos claros de API (endpoints, payloads), modelos de autorização/autenticação e retentividade de logs para auditoria. FIMS é o “mediador” entre USSs e autoridade — especifique latência máxima, garantia de entrega e formatos aceitos. ([Administração Federal de Aviação][2])
* **USS network**: requisitos para publicação de intenções de voo (timings, schemas), serviços de deconfliction, e interoperabilidade entre USSs. Defina SLAs (ex.: tempo máximo para atualização de posição, resolução temporal mínima). ([NASA Documentos Técnicos][5])
  Boas práticas:
* Defina **contratos de interface** (OpenAPI / JSON Schema / protobuf), políticas de versionamento e estratégia de migração.
* Especifique requisitos de telemetria mínima (frequência, precisão) e tolerâncias para sincronização entre USSs. ([Administração Federal de Aviação][2])

---

## EASA — U-Space / EU 2021/664 — requisitos regulatórios e operacionais

O que exigir:

* **Conformidade legal**: verifique os requisitos do U-Space (serviços essenciais, responsabilidades dos USSPs, níveis de automação) e traduza em requisitos contratuais e técnicos. ([EUR-Lex][6])
* **SIP/SDSP**: requisitos mínimos para provedores suplementares de dados (qualidade, latência, formatos), e políticas de certificação/aceitação pelo regulador. ([EASA][7])
  Boas práticas:
* Implementar *conformity checklist* para cada componente (USS, SIP, interface com ANSP) mapeando artigos do regulamento → requisito → evidência. ([EASA][8])

---

## ASTM (F3548, F3448) — especificações técnicas e interoperabilidade

O que exigir:

* **Requisitos de interoperabilidade**: adotar os elementos do F3548 para formatar serviços UTM, mensagens e comportamento esperado dos USS. Use a norma como *means of compliance* para requisitos de dados e serviços. ([ASTM International | ASTM][9])
  Boas práticas:
* Em requisitos de sistema, referencie cláusulas ASTM para: formatos de mensagens, requisitos de resiliência, disponibilidade e interfaces de interoperabilidade entre operadores e provedores. ([ASTM International | ASTM][9])

---

## JARUS / SORA — segurança, avaliação de risco e níveis de garantia

O que exigir:

* **Avaliação de risco**: integrar SORA (ou equivalente) ao processo de requisitos — cada requisito de segurança funcional deve mapear para controles requeridos pelo SORA (redução de risco, evidências). ([Jarus RPAS][3])
* **DAL / segurança funcional**: quando componentes UTM afetam separação/segurança, especificar critérios de confiabilidade, redundância e requisitos de falha (MTTF, MTTFd, probabilidade de perda). ([Jarus RPAS][3])
  Boas práticas:
* Produza um **Safety Requirements Specification (SRS)** que liga modos de falha a requisitos de detecção, mitigação e recuperação; inclua testes (FMEAs, FTA) e critérios de aceitação. ([Jarus RPAS][3])

---

## Checklist prática para especificação de requisitos UTM (modelo pronto para usar)

1. **Contexto & Escopo** — atores (ANSP, USS, Operators, SIPs, FIMS), restrições e fronteiras do sistema. ([OACI][4])
2. **Requisitos Funcionais** — p.ex.: registro/gerenciamento de planos de voo, serviço de deconfliction, NOTAM dinâmico, notificações de emergência. Para cada requisito: *descrição*, *entradas/saídas*, *pré-condições*, *pós-condições*, *KPI de aceitação*. ([OACI][1])
3. **Requisitos de Dados / Interfaces** — schemas (JSON/XML), contratos FIMS/USS, versionamento e tolerâncias (ex.: precisão de posição ±x m, atualização ≤ y s). ([Administração Federal de Aviação][2])
4. **Requisitos de Segurança & Privacidade** — autenticação (OAuth2 / mTLS), autorização por escopo, proteção de dados pessoais, retenção de logs, criptografia em trânsito e repouso; requisitos de GDPR/legislação local quando aplicável. ([Administração Federal de Aviação][2])
5. **Requisitos de Segurança Funcional** — DALs, requisitos de redundância, detecção de falha, comportamento em perda de link; mapear para SORA/JARUS. ([Jarus RPAS][3])
6. **Performances / SLA** — disponibilidade (ex.: 99.95%), latência (p.ex. atualização de posição < 1 s para operações críticas), tempo de recuperação. Use ASTM como referência para métricas. ([ASTM International | ASTM][9])
7. **Operação & Monitoramento** — telemetria, dashboards, alertas, retenção de dados para investigação. ([Administração Federal de Aviação][2])
8. **Verificação & Validação** — testes unitários/integrados, testes de interoperabilidade USS↔USS↔FIMS, simulações (DoE), campanhas de sandbox / trials (padrão EU U-Space sandboxes). ([EASA][7])
9. **Documentação & Rastreabilidade** — req ↔ design ↔ teste ↔ evidência certificatória; checklist de conformidade regulatória. ([EASA][8])

---

## Metodologias de verificação e evidências (o que exigir nos requisitos)

* **Testes de Interop**: cenário end-to-end envolvendo USS A ↔ USS B ↔ FIMS, com cenários de conflito, perda de dados e emergência; requisitos medem sucesso (p.ex. percentil 99 de resolução de conflito < X s). ([Administração Federal de Aviação][2])
* **Ensaios de robustez**: injetar falhas (latência, perda de mensagens) e verificar modos degradados. Documentar resultados como evidência de conformidade. ([ASTM International | ASTM][9])
* **Avaliação de risco contínua**: reavaliar SORA ao longo do ciclo de vida e after-change. ([Jarus RPAS][3])

---

## Rastreabilidade regulatória — como ligar requisitos às normas

* Para cada requisito crítico, adicione metadados: `RegulaçãoReferencia` (ex.: ICAO-UtM §X / EU 2021/664 Art-Y / ASTM F3548 §Z / JARUS SORA Step N). Isso acelera auditoria e revisão regulatória. ([OACI][1])

---

## Referências bibliográficas e leituras seguras (consultar / citar)

> Documentos oficiais (primários — **recomendado** consultar e citar diretamente)

1. ICAO — *Unmanned Aircraft Systems Traffic Management (UTM) – A Common Framework with Core Principles for Global Harmonization* (UTM Framework, Edition 4). ([OACI][1])
2. FAA / NASA — *UTM Concept of Operations Version 2.0* (inclui descrição do FIMS e USS). ([Administração Federal de Aviação][2])
3. Commission Implementing Regulation (EU) 2021/664 — *Regulatory framework for the U-space* (texto legal e Easy-Access Rules via EASA). ([EUR-Lex][6])
4. ASTM International — *F3548 (Standard Specification for UTM)* (e documentos relacionados como F3448). ([ASTM International | ASTM][9])
5. JARUS — *SORA (Specific Operations Risk Assessment)* e demais documentos técnicos (guidelines de segurança). ([Jarus RPAS][3])

> Artigos e relatórios técnicos (secundários — contexto, melhores práticas)

6. NASA / NTRS — *USS specification & related technical reports* (background de arquitetura USS). ([NASA Documentos Técnicos][5])
7. GUTMA / relatórios de readiness e sandboxes (análises de maturidade UTM / U-space). ([Autonomy Global -][10])
8. Relatórios e whitepapers de sandboxes / projetos nacionais (p.ex. documentos de U-space Sandbox Standards and Services). ([transpordiamet.ee][11])

> Como usar essas referências:

* Baixe os PDFs oficiais (ICAO, FAA, EASA, ASTM, JARUS) e use-os como *baselines* para cláusulas normativas dos seus requisitos. ([OACI][1])

---

## Sugestão prática de próximos passos (ação imediata)

1. Baixe e **mapeie**: ICAO (Edition 4), FAA UTM ConOps v2.0, EU 2021/664, ASTM F3548, JARUS SORA — crie um *matrix de conformidade* (colunas: artigo/cláusula → requisito do sistema → evidência). ([OACI][1])
2. Escreva um **template SRS** (Safety Requirements Specification) e um **Interface Control Document (ICD)** para FIMS/USS. ([Administração Federal de Aviação][2])
3. Planeje um **programa de testes de interoperabilidade** em sandbox/região piloto e inclua SORA dentro do ciclo de verificação. ([transpordiamet.ee][11])

---

[1]: https://www.icao.int/sites/default/files/left-menu-pdfs/UTM%20Framework%20Edition%204.pdf?utm_source=chatgpt.com "Unmanned Aircraft Systems Traffic Management (UTM)"
[2]: https://www.faa.gov/sites/faa.gov/files/2022-08/UTM_ConOps_v2.pdf?utm_source=chatgpt.com "Unmanned Aircraft System (UAS) Traffic Management (UTM)"
[3]: https://jarus-rpas.org/wp-content/uploads/2024/06/SORA-v2.5-Main-Body-Release-JAR_doc_25.pdf?utm_source=chatgpt.com "SORA-v2.5-Main-Body-Release-JAR_doc_25.pdf"
[4]: https://www.icao.int/utm-guidance?utm_source=chatgpt.com "UTM Guidance"
[5]: https://ntrs.nasa.gov/api/citations/20170011588/downloads/20170011588.pdf?attachment=true&utm_source=chatgpt.com "USS Specification"
[6]: https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX%3A32021R0664&utm_source=chatgpt.com "Commission Implementing Regulation (EU) 2021/664"
[7]: https://www.easa.europa.eu/en/document-library/easy-access-rules/easy-access-rules-u-space-regulation-eu-2021664?utm_source=chatgpt.com "Easy Access Rules for U-space (Regulation (EU) 2021/664)"
[8]: https://www.easa.europa.eu/en/document-library/regulations/commission-implementing-regulation-eu-2021664?utm_source=chatgpt.com "Commission Implementing Regulation (EU) 2021/664 - EASA"
[9]: https://www.astm.org/f3548-21.html?utm_source=chatgpt.com "Standard Specification for UAS Traffic Management (UTM) ..."
[10]: https://www.autonomyglobal.co/wp-content/uploads/2025/03/GUTMA-TF-Global-UTM-Ecosystems-Readiness-Index-2024-report-min.pdf?utm_source=chatgpt.com "Global UTM Ecosystems' Readiness Index 2024"
[11]: https://www.transpordiamet.ee/sites/default/files/documents/2024-09/D5.3%20-%20U-space%20Sandbox%20Standards%20and%20Services.pdf?utm_source=chatgpt.com "U-space Sandbox Standards and Services"

Sim — encontrei uma boa quantidade de referências que usam ou discutem o termo “ecosistema UTM” (ou “ecosystem UTM / U-space ecosystem”). Aqui estão as mais relevantes, com potenciais para uso no seu relatório técnico, especialmente no tema de ecossistema (atores, responsabilidades, interações, infraestrutura digital) para sistemas UTM.

---

## Principais referências sobre “ecosistema UTM”

1. Airbus – artigo “UTM is a key enabler of AAM”

   * Texto: “Unmanned Traffic Management (UTM) is a completely new ecosystem that has to deal with unmanned vehicles.” ([Airbus][1])
   * Destaque: mostra claramente a noção de “ecosistema” em que UTM faz parte de um sistema mais amplo de mobilidade aérea avançada (AAM), com múltiplos pilares (veículos, infraestruturas, serviços, UTM/ATM). ([Airbus][1])
   * Utilidade: serve para fundamentar argumentos de que o sistema UTM não é isolado, mas parte de um ecossistema distribuído com vários atores e serviços (o que encaixa muito bem no seu “estrutura de atores” e modelo de responsabilidades).

2. Artigo: “Unmanned Aerial Traffic Management System Architecture for U-Space In-Flight Services” (Applied Sciences, 2021)

   * Faz referência explícita ao “U-space ecosystem” como iniciativa europeia para UTM. ([MDPI][2])
   * Aborda arquitetura de sistema, serviços em-voo, e declara “the U-space ecosystem … offers U-space services to the different actors in the U-space ecosystem” (página resumo). ([MDPI][2])
   * Utilidade: boa para embasar a secção de especificação de requisitos referentes a atores, serviços e interfaces dentro do ecossistema.

3. National Aeronautics and Space Administration (NASA) / Federal Aviation Administration (FAA) — “Unmanned Aircraft System Traffic Management (UTM) Project”

   * Documento define UTM como um “ecosystem” para operações de muitos UAS em baixa altitude. Por exemplo: “a key attribute of the UTM ConOps is sharing of traffic, weather, and terrain information between the UTM and UAS services and the UAS operations. Analogous to the information shared by crowd-sourced traffic applications, the UTM eco-system must facilitate sharing of information between UAS operations.” ([NASA Documentos Técnicos][3])
   * Utilidade: fortalece a noção de ecossistema UTM sob a perspectiva norte-americana, útil para comparações ou para mostrar alinhamento internacional.

4. Livro: Unmanned Aircraft Systems Traffic Management: UTM (Michael Scott Baum, 2021)

   * O livro menciona “global ecosystem of players advancing UTM …” e estrutura o UTM como parte de um ecossistema global. ([Routledge][4])
   * Utilidade: boa fonte para introdução teórica, para justificar que seu trabalho trata de “ecossistema UTM” (e não apenas de “sistema UTM”) e para embasar margens de literatura.

5. Artigo “Sensors and Communication Simulation for Unmanned Traffic Management”

   * Descreve a necessidade de simular “UTM ecosystem” – “Unmanned traffic management (UTM) systems will become a key enabler to the future drone market ecosystem, enabling the safe concurrent operation of both manned and unmanned aircrafts.” ([PubMed][5])
   * Utilidade: bom para reforçar a ideia de “mercado/ecossistema de drone + UTM”, ou seja, o ecossistema se estende além da infraestrutura técnica para incluir o “mercado” ou “operações”.

---

## Como incorporar ao seu relatório técnico

Dado que seu trabalho se relaciona com sistemas UTM/UTM-SAC e arquitetura distribuída, eis como usar essas referências:

* Na seção de **estrutura de atores** (como você já tinha: ANSP/DECEA, Operadores, USS, SIPs, FIMS) — mencione que isso representa **o ecossistema UTM**, conforme a literatura, e cite as referências acima para suportar essa terminologia. Por exemplo: “Este trabalho adota o termo ‘ecossistema UTM’ para referir-se ao conjunto de atores, serviços, infraestruturas e interações distribuídas (conforme Airbus 2023; Applied Sciences 2021)”.

* Na seção de **arquitetura e serviços** — use o artigo de 2021 sobre o U-space ecosystem para fundamentar que os requisitos de serviços (pre-flight, in-flight) ocorrem no contexto de esse ecossistema, não de um sistema monolítico. Use como base para definir requisitos de interoperabilidade, modularidade, escalabilidade.

* Na seção de **normas e diretrizes** — ao mencionar International Civil Aviation Organization (ICAO) UTM Framework ou European Union Aviation Safety Agency (EASA) U-Space, inclua que essas abordagens reconhecem o UTM como ecossistema global/híbrido, o que reforça a necessidade de requisitos de interoperabilidade e governança distribuída.

* Na **discussão de desafios / limitações** — pode usar a referência que mostra que o ecossistema ainda está em evolução (ex: “ecosystem of players advancing UTM” Baum) para justificar lacunas, necessidade de maturação, integração com AAM, etc.

---

[1]: https://www.airbus.com/en/newsroom/stories/2023-10-utm-is-a-key-enabler-of-aam?utm_source=chatgpt.com "UTM is a key enabler of AAM | Airbus"
[2]: https://www.mdpi.com/2076-3417/11/9/3995?utm_source=chatgpt.com "Unmanned Aerial Traffic Management System Architecture for U-Space In-Flight Services"
[3]: https://ntrs.nasa.gov/api/citations/20190000370/downloads/20190000370.pdf?utm_source=chatgpt.com "Unmanned Aircraft System Traffic Management (UTM)"
[4]: https://www.routledge.com/Unmanned-Aircraft-Systems-Traffic-Management-UTM/Baum/p/book/9781003124689?utm_source=chatgpt.com "Unmanned Aircraft Systems Traffic Management: UTM - 1st Edition - Mich"
[5]: https://pubmed.ncbi.nlm.nih.gov/33573192/?utm_source=chatgpt.com "Sensors and Communication Simulation for Unmanned Traffic Management - PubMed"

