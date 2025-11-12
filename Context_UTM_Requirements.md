
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

