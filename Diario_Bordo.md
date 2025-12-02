PESQUISA 02.12.2025 (Foi compilado o texto, agora preciso)
---
( ) Separar só o que interessa para apresentar - Dez Slides
( ) Rodar o template com conteudo e formato 
(v) Colocar os dizeres da propriedade intelectual;
(v) Colocar o material do artigo MRCF online;
( ) Colocar o material do word escrito do DOC;
( ) Colocar o material do word escrito do SAC;

PESQUISA 28.11.2025 (Compilar os textos relevantes para o Template Overleaft da QUALIS)
---
Basicamente o compilado da secao proposta que fiz hoje:

\chapter{Research Proposal (Work Plan and Timeline)}

%\section{Detailed Dissertation Proposal}
%Com base na lacuna de pesquisa que eu estabeleci no capítulo anterior, vou detalhar aqui exatamente o que farei no restante do meu mestrado. Vou apresentar minha proposta (de solução, framework, método, etc.) para preencher essa lacuna.

%\section{Future Research Methodology}
%Aqui, eu vou descrever a metodologia que usarei para desenvolver e avaliar minha proposta. Esta pode ser, por exemplo, Design Science Research, um estudo de caso, um experimento, etc.

%\section{Work Plan and Timeline}
%Vou apresentar um cronograma detalhado com todas as etapas futuras até a minha defesa. Um Gráfico de Gantt eu curto bastante e acho ideal para esta seção, para visualizar as atividades e os prazos.

%\section{Expected Contributions}
%Para finalizar, vou listar de forma clara e objetiva quais serão as contribuições originais esperadas do meu trabalho para a academia e/ou para a indústria.
%OS ITENS ACIMA SAO PARA ADEQUAR

\subsection{Documentos Elaborados e Artefatos de Arquitetura}

Foram desenvolvidas duas arquiteturas de software para o Sistema de Simulação UTM, conforme os módulos e requisitos fornecidos, além da análise de alinhamento com recomendações internacionais (ICAO, CANOPs e FAA). Os resultados encontram-se organizados nos seguintes anexos:

\begin{itemize}
    \item \textbf{Arquitetura de Software para Sistema de Simulação UTM -- Contexto Geral} (\textit{arquitetura\_geral.md}):  
    Documento que descreve a arquitetura em alto nível, com foco na separação de responsabilidades entre os módulos principais do sistema.
    
    \item \textbf{Código PlantUML -- Arquitetura Geral} (\textit{arquitetura\_geral\_plantuml.txt}):  
    Código-fonte utilizado para a visualização do diagrama de componentes relacionados ao contexto geral da arquitetura.
    
    \item \textbf{Arquitetura de Software para Sistema de Simulação UTM -- Detalhada (Nível de Implementação)} (\textit{arquitetura\_detalhada.md}):  
    Documento que apresenta a arquitetura em nível de microsserviços, módulos internos e componentes do motor de simulação.
    
    \item \textbf{Código PlantUML -- Arquitetura Detalhada} (\textit{arquitetura\_detalhada\_plantuml.txt}):  
    Código para geração do diagrama de componentes detalhado correspondente ao nível de implementação.
    
    \item \textbf{Análise de Alinhamento com Normas Internacionais} (\textit{analise\_conformidade.md}):  
    Documento que descreve como a arquitetura proposta se alinha às normas e diretrizes da ICAO, CANOPs e FAA para UTM, destacando também os elementos que permanecem fora desse escopo por se tratarem de funcionalidades específicas do ambiente de simulação.
\end{itemize}

\section{Arquitetura de Software para Sistema de Simulação UTM -- Contexto Geral}

A arquitetura de contexto geral do sistema de simulação UTM (Unmanned Aircraft System Traffic Management) é concebida como um sistema modular e distribuído, com a separação clara das responsabilidades de \textbf{configuração}, \textbf{execução}, \textbf{visualização} e \textbf{persistência} da simulação.

\subsection{Visão Geral da Arquitetura}

O modelo arquitetural segue o paradigma de Arquitetura Orientada a Serviços (Service-Oriented Architecture -- SOA) ou microserviços, essencial para garantir \textbf{escalabilidade}, \textbf{resiliência} e \textbf{fidelidade arquitetural} em relação ao ambiente real de UTM, intrinsicamente distribuído~\cite{ref1}.

\begin{table}[h!]
\centering
\caption{Principais módulos da arquitetura e seus alinhamentos com requisitos}
\begin{tabular}{|p{4cm}|p{6cm}|p{4cm}|}
\hline
\textbf{Módulo Principal} & \textbf{Responsabilidade Primária} & \textbf{Alinhamento com Requisitos (Exemplos)} \\
\hline

\textbf{Interface de Visualização (UI/UX)} &
Interação Humano-Sistema; visualização geoespacial 4D; manutenção da consciência situacional operacional. &
1, 25, 26, 92, 93, 95, 96, 97, 98, 100, 140, 141, 150 \\
\hline

\textbf{Gestor de Cenários / Configurador} &
Criação, parametrização e gestão completa do ciclo de vida dos cenários de simulação. &
2, 6, 7, 10, 12, 14, 17, 18, 22, 23, 35, 36, 40, 44, 45, 47, 49, 52, 55, 56, 58, 59, 137, 139, 153, 154, 167, 168 \\
\hline

\textbf{Motor de Simulação / Framework} &
Núcleo de execução da simulação; aplicação de regras físicas, regulatórias e táticas; execução em tempo próximo ao real. &
5, 35, 36, 44, 52, 55, 81, 82, 105, 148, 160, 161, 162 \\
\hline

\textbf{Infraestrutura de Serviços / Backend} &
Fornecimento de APIs internas e externas; gestão de infraestrutura distribuída; suporte a execução simultânea e escalabilidade. &
15, 24, 38, 85, 86, 88, 89, 91, 138, 160, 161, 162, 163 \\
\hline

\textbf{Banco de Dados / Persistência} &
Armazenamento de cenários, resultados, logs, métricas e histórico operacional. &
31, 34, 144, 160, 161, 162 \\
\hline

\textbf{Gerador de Relatórios e Dashboards} &
Consolidação de métricas; relatórios de não conformidade; dashboards estratégicos para análise. &
4, 25, 27, 32, 33, 41, 42, 69, 141 \\
\hline

\textbf{Carregamento e Integração de Entidades} &
Interoperabilidade com APIs externas, DSS e provedores; importação de entidades e restrições operacionais. &
3, 9, 37, 41, 42, 107, 164, 165 \\
\hline

\textbf{Gestão de Usuários e Acesso} &
Autenticação, autorização, perfis de usuário e trilhas de auditoria. &
1, 16, 29, 30, 39, 102, 103, 104, 112, 142, 143, 151, 152 \\
\hline

\end{tabular}
\end{table}

\section{Diagrama de Componentes (PlantUML)}

O diagrama de componentes a seguir ilustra as interações de alto nível entre os módulos.

%\begin{lstlisting}[language={},caption={Arquitetura de Software - Contexto Geral (Simulação UTM)}]
%@startuml
%skinparam componentStyle rectangle
%skinparam monochrome true

%title Arquitetura de Software - Contexto Geral (Simulação UTM)

%' Subsistemas Principais
%component "Interface de Visualização (UI/UX)" as UI
%component "Gestor de Cenários / Configurador" as SCENARIO_MANAGER
%component "Motor de Simulação / Framework" as SIM_ENGINE
%component "Infraestrutura de Serviços / Backend" as BACKEND
%component "Banco de Dados / Persistência" as DB
%component "Gerador de Relatórios e Dashboards" as REPORT_GEN
%component "Carregamento e Integração de Entidades" as DATA_INTEGRATION
%component "Gestão de Usuários e Acesso" as USER_MANAGER

%' Relações
%UI --> SCENARIO_MANAGER : Configuração de Cenários
%UI --> SIM_ENGINE : Visualização em Tempo Real
%UI --> REPORT_GEN : Visualização de Resultados
%UI --> USER_MANAGER : Autenticação e Gestão de Perfil

%SCENARIO_MANAGER --> SIM_ENGINE : Parâmetros e Início da Simulação
%SCENARIO_MANAGER --> DB : Persistência de Cenários

%SIM_ENGINE --> DATA_INTEGRATION : Carregamento de Dados Externos
%SIM_ENGINE --> DB : Persistência de Logs e Resultados
%SIM_ENGINE --> REPORT_GEN : Geração de Métricas

%BACKEND --> SIM_ENGINE : Execução Distribuída
%BACKEND --> DB : Acesso a Dados
%BACKEND --> DATA_INTEGRATION : Serviços de API

%DATA_INTEGRATION --> BACKEND : Serviços de API
%DATA_INTEGRATION --> DB : Dados de Entidades

%REPORT_GEN --> DB : Consulta de Resultados Históricos

%USER_MANAGER --> BACKEND : Controle de Acesso

%' Módulos de Suporte (Aspectos Transversais)
%package "Segurança e Conformidade" {
%  [Módulo de Segurança] as SECURITY
%}
%package "Planejamento Estratégico e Análise" {
%  [Módulo de Análise] as ANALYSIS
%}
%package "Testes, Certificação e Auditoria" {
%  [Módulo de Testes] as TESTING
%}

%SIM_ENGINE ..> SECURITY : Aplicação de Regras
%BACKEND ..> SECURITY : Autenticação/Autorização
%DB ..> SECURITY : Proteção de Dados

%REPORT_GEN ..> ANALYSIS : Consolidação de Dados
%SIM_ENGINE ..> ANALYSIS : Dados para Avaliação

%SIM_ENGINE ..> TESTING : Logs e Resultados para Validação

%@enduml
%\end{lstlisting}

\subsection*{Referências}

[1] FAA. \textit{Unmanned Aircraft System (UAS) Traffic Management (UTM) ConOps V2.0}. Documento que descreve a arquitetura e serviços do UTM.

\section{Análise de Alinhamento com Normas Internacionais (ICAO, CANOPs, FAA)}

A arquitetura de simulação proposta foi desenhada para refletir os princípios fundamentais de um sistema UTM, conforme estabelecido por organizações reguladoras e de padronização como a Organização da Aviação Civil Internacional (ICAO), a Administração Federal de Aviação (FAA) e o CANOPs (embora o CANOPs seja um conceito mais amplo, seus princípios de segurança e interoperabilidade são aplicáveis).

\subsection{Alinhamento com Recomendações Internacionais}

O alinhamento da arquitetura com as normas internacionais é forte, especialmente nos aspectos de distribuição de serviços, interoperabilidade e segurança.

\begin{table}[h!]
\centering
\caption{Alinhamento da Arquitetura com Normas Internacionais (ICAO, FAA, CANOPs)}
\begin{tabular}{|p{3.3cm}|p{2.5cm}|p{8.5cm}|}
\hline
\textbf{Aspecto da Arquitetura} & 
\textbf{Alinhamento} & 
\textbf{Justificativa} \\ 
\hline

Arquitetura Distribuída (Microsserviços) 
& Alinhado 
& A ICAO e a FAA definem que o UTM deve operar como um ecossistema distribuído, com múltiplos provedores (USS) integrados por um Sistema de Informação Comum (CIS). A arquitetura proposta, com backend distribuído e APIs internas/externas, simula essa estrutura. Os Requisitos 88 e 89 reforçam a necessidade de fidelidade arquitetural com o UTM real. \\
\hline

Interoperabilidade
& Alinhado
& A troca de dados padronizada entre atores (USS, Autoridade, Operadores) é um dos pilares das normas internacionais. O módulo de Carregamento e Integração de Entidades, junto ao serviço de dados, simula APIs compatíveis com padrões como ASTM F3411. Os Requisitos 3, 9, 37 e 164 tratam diretamente dessa necessidade. \\
\hline

Gestão de Conflitos (CDR)
& Alinhado
& O serviço de \textit{Conflict Detection \& Resolution} simula o Desconflito Tático (Requisito 81), um dos principais serviços de segurança presentes nas normas da ICAO e FAA. A simulação de regras de separação e mitigação de conflitos está alinhada com os requisitos de segurança operacional. \\
\hline

Segurança e Auditoria
& Alinhado
& O sistema contempla autenticação, autorização e rastreabilidade por meio dos módulos de Segurança, Gestão de Usuários e Auditoria. Esses mecanismos atendem às recomendações internacionais para segurança cibernética e operacional (Requisitos 39, 108, 113). \\
\hline

Visualização Geoespacial (4D)
& Alinhado
& A visualização espaço-temporal (4D) é essencial para consciência situacional e tomada de decisão em UTM. O módulo de UI/UX e o suporte à coleta de métricas 4D (Requisito 134) atendem às recomendações da ICAO e FAA. \\
\hline

\end{tabular}
\end{table}

\begin{table}[h!]
\centering
\caption{Partes Fora do Escopo Direto das Normas Internacionais}
\begin{tabular}{|p{3.5cm}|p{3cm}|p{8cm}|}
\hline
\textbf{Aspecto da Arquitetura} &
\textbf{Relação com Normas Internacionais} &
\textbf{Justificativa} \\
\hline

Motor de Simulação (Core) 
& Fora do escopo direto 
& As normas ICAO/FAA definem os serviços UTM, mas não especificam como um motor de simulação deve ser implementado. O \textit{Scheduler} e o \textit{Rule Engine} são estruturas internas necessárias para execução em tempo próximo ao real (Requisito 35), mas não constituem serviços UTM definidos nas normas internacionais. \\
\hline

Gerador de Relatórios e Dashboards 
& Fora do escopo direto 
& As normas exigem registro e rastreabilidade de dados, mas não definem formatos de dashboards ou relatórios analíticos. O Módulo de Análise Estratégica (Requisitos 11, 124, 125) e o Gerador de Relatórios são ferramentas específicas do simulador, destinadas à avaliação e tomada de decisão, extrapolando os requisitos operacionais do UTM. \\
\hline

Módulo de Testes de Saturação 
& Fora do escopo direto 
& Embora as normas estabeleçam que o sistema deve ser seguro e robusto, o módulo de testes é uma ferramenta própria do simulador. O Requisito 121 (Avaliação de Saturação do Espaço Aéreo) representa um objetivo analítico da simulação, não um serviço UTM. O módulo que suporta essa função é uma ferramenta de engenharia e validação do sistema. \\
\hline

\end{tabular}
\end{table}

\section*{Resumo do Alinhamento}

Em resumo, a arquitetura proposta adota a estrutura de serviços e a filosofia de interoperabilidade do UTM, mantendo forte alinhamento com as recomendações internacionais. Ao mesmo tempo, o \textbf{Motor de Simulação} e os \textbf{Módulos de Análise} representam uma camada adicional de ferramentas para avaliação, própria de um sistema de simulação, e portanto \textit{fora do escopo direto} das normas operacionais estabelecidas por ICAO, FAA e documentos associados.

\section*{Referências}

\begin{enumerate}
    \item ICAO. \textit{UTM Guidance}. Documento que fornece orientação sobre a gestão do tráfego de UAS.
    \item FAA. \textit{Unmanned Aircraft System (UAS) Traffic Management (UTM) ConOps V2.0}.
    \item FAA. \textit{Uncrewed Aircraft Systems (UAS) Traffic Management (UTM) Pilot Program (UPP) Final Report}.
\end{enumerate}

\section*{Atores do Sistema de Simulação UTM}

Com base nos textos dos módulos, requisitos e nas arquiteturas de software elaboradas, os atores do sistema de simulação UTM foram identificados e classificados em duas categorias principais: \textbf{Atores Humanos (Usuários)} e \textbf{Atores de Sistema (Entidades)}. 

O documento anexo, \textit{Atores do Sistema de Simulação UTM}, detalha cada ator, seu papel no sistema, os módulos de interação primária e os requisitos associados.

\subsection*{Resumo dos Principais Atores}

\subsubsection*{Atores Humanos}
\begin{itemize}
    \item \textbf{Analista de Espaço Aéreo / Regulador}: Responsável pela configuração de cenários complexos e pela análise estratégica.
    \item \textbf{Operador de Simulação / Engenheiro de Testes}: Responsável pela execução técnica da simulação, testes de saturação e processos de validação.
    \item \textbf{Usuário de Consulta / Observador}: Focado na visualização de resultados, métricas e dashboards.
    \item \textbf{Administrador do Sistema}: Atua na gestão de acesso, segurança e governança operacional do sistema.
\end{itemize}

\subsubsection*{Atores de Sistema}
\begin{itemize}
    \item \textbf{Provedores de Serviço UTM (USS)}: Entidades simuladas que interagem diretamente com o Motor de Simulação.
    \item \textbf{Sistemas Externos / DSS}: Fontes de dados externas integradas por meio de APIs.
    \item \textbf{Entidades de Simulação (Aeronaves/Drones)}: Objetos primários representados e manipulados durante a simulação.
    \item \textbf{Módulo de Análise Estratégica}: Componente interno que atua como ator ao produzir insights e outputs analíticos.
\end{itemize}

ste documento apresenta a contextualização e o enquadramento técnico-normativo do \textbf{Sistema de Gerenciamento de Tráfego de Aeronaves Não Tripuladas (UTM) Global}, cujo cenário de aplicação inicial é o Brasil, mas cuja concepção segue as diretrizes internacionais mais avançadas em gestão de tráfego aéreo distribuído. 

O objetivo central é garantir uma solução robusta, interoperável e aderente a padrões globais, assegurando escalabilidade, certificabilidade e integração futura com infraestruturas internacionais. O projeto reconhece a transição do modelo tradicional e centralizado de \textit{Air Traffic Management (ATM)} para o paradigma distribuído, baseado em risco, de \textit{Unmanned Traffic Management (UTM)}, conforme preconizado por organismos como a \textit{ICAO}, \textit{FAA/NASA}, \textit{EASA} e \textit{JARUS}.

% ------------------------------------------------------------
\section{Referenciais Normativos e Diretrizes Internacionais}

A definição dos requisitos do simulador baseia-se em um conjunto consolidado de normas e diretrizes internacionais, que visam assegur a compatibilidade e a interoperabilidade do UTM brasileiro com o ecossistema global.

\begin{table}[H]
\centering
\caption{Referenciais normativos e diretrizes internacionais considerados.}
\label{tab:normas_internacionais}
\renewcommand{\arraystretch}{1.3}
\setlength{\tabcolsep}{6pt}
\begin{tabularx}{\textwidth}{|l|X|X|}
\hline
\textbf{Organismo / Documento} & \textbf{Descrição e Relevância para o Projeto} & \textbf{Referência Original} \\
\hline
\textbf{ICAO} & Diretrizes globais para harmonização entre ATM e UTM. O sistema deve seguir o \textit{UTM Framework} (Edição 4), assegurando aceitação internacional. & \cite{icao2019utmframework} \\
\hline
\textbf{FAA / NASA} & Arquitetura de referência baseada no \textit{UTM ConOps v2.0} e no \textit{Flight Information Management System (FIMS)}, modelos centrais para interoperabilidade e supervisão digital. & [\cite{faa_conops}][\cite{faa_utm}] \\
\hline
\textbf{EASA (U-space)} & Regulamento europeu (EU) 2021/664, com ênfase na autonomia operacional dos provedores de serviço e serviços essenciais do U-space. & [\cite{eu2021uSpace664}] \\
\hline
\textbf{ASTM F3448 / F3548} & Especificações para interoperabilidade e provedores suplementares de dados e serviços. Fundamenta o intercâmbio entre USSs e autoridades. & [\cite{astmF3448}][\cite{astm_f3548_21}] \\
\hline
\textbf{JARUS} & Diretrizes de segurança, avaliação de risco e definição de níveis de garantia (DAL) aplicáveis a sistemas UAS. & [\cite{jarusSORA}] \\
\hline
\end{tabularx}
\end{table}

% ------------------------------------------------------------
\section{Estrutura de Atores do Sistema}

O ecossistema UTM é composto por atores que interagem em um modelo distribuído de responsabilidade, interoperabilidade e supervisão digital. A Tabela~\ref{tab:atores_sistema} apresenta os principais papéis e responsabilidades.

\begin{table}[H]
\centering
\caption{Principais atores e funções no Sistema UTM}
\label{tab:atores_sistema}
\renewcommand{\arraystretch}{1.3}
\begin{tabularx}{\textwidth}{|l|X|}
\hline
\textbf{Ator} & \textbf{Papel e Responsabilidade} \\
\hline
\textbf{Autoridade Aeronáutica (ANSP/DECEA)} & Supervisão e regulação; definição de restrições estáticas e dinâmicas e manutenção da responsabilidade final pela segurança operacional. \\
\hline
\textbf{Operadores de Voo (UAS Operators)} & Planejamento, execução e conformidade das missões UAS, em interação direta com os provedores de serviço (USS). \\
\hline
\textbf{Provedores de Serviço UTM (USS)} & Coordenação tática, desconflito e sincronização de dados de intenção e posição em tempo real; execução dos serviços essenciais de U-space. \\
\hline
\textbf{Provedores de Informações Suplementares (SIPs)} & Fornecimento de dados críticos (meteorologia, topografia, multidões, emergências) que alimentam a operação dos USSs. \\
\hline
\textbf{FIMS (\emph{Flight Information Management System})} & Camada digital de supervisão e mediação entre USSs e Autoridade Aeronáutica, gerenciando planos de voo e restrições dinâmicas. \\
\hline
\end{tabularx}
\end{table}

% ------------------------------------------------------------
\section{Categorias de Requisitos e Perfis de Entrevistas}

Durante a elicitação dos requisitos, foram definidos diferentes níveis de análise, conforme a natureza dos requisitos e os perfis de especialistas entrevistados.

\begin{table}[H]
\centering
\caption{Categorias de requisitos e perfis de contribuição.}
\label{tab:categorias_requisitos}
\renewcommand{\arraystretch}{1.3}
\begin{tabularx}{\textwidth}{|l|X|}
\hline
\textbf{Categoria} & \textbf{Descrição e Origem} \\
\hline
\textbf{Requisitos de Negócio (RN)} & Derivados das entrevistas com gestores de projeto e autoridades regulatórias; refletem os objetivos estratégicos e operacionais do sistema. \\
\hline
\textbf{Requisitos de Arquitetura (RA)} & Originados da análise de padrões técnicos (FAA/NASA, ASTM, EASA); descrevem a estrutura e as interfaces do sistema. \\
\hline
\textbf{Requisitos de Processo (RP)} & Associados à engenharia de sistemas e certificação; definidos a partir de práticas recomendadas (DOORS, LDRA, Rapita). \\
\hline
\end{tabularx}
\end{table}

Os perfis de especialistas entrevistados incluem representantes de três grupos principais:  
(i) \textit{Autoridade e Fiscalização} (DECEA, ANAC),  
(ii) \textit{Desenvolvedores e Integradores de Sistemas}, e  
(iii) \textit{Operadores e Pesquisadores} em UAS e UTM.  
Essa divisão permitiu consolidar perspectivas complementares sobre requisitos, desafios e aderência normativa.

% ------------------------------------------------------------
\section{Integração com Normas e Estrutura Hierárquica}

Cada subdivisão de requisitos do UTM Global foi estruturada para garantir aderência direta aos referenciais normativos apresentados na Tabela~\ref{tab:normas_internacionais}.  
A Tabela~\ref{tab:enquadramento_normativo} mostra a relação entre as categorias de requisitos e os padrões que as sustentam.

\begin{table}[H]
\centering
\caption{Enquadramento das categorias de requisitos em normas e diretrizes internacionais.}
\label{tab:enquadramento_normativo}
\renewcommand{\arraystretch}{1.3}
\setlength{\tabcolsep}{6pt}
\begin{tabularx}{\textwidth}{|l|X|}
\hline
\textbf{Categoria de Requisito} & \textbf{Normas e Diretrizes Associadas} \\
\hline
Requisitos de Negócio (RN) & ICAO UTM Framework; FAA UTM ConOps v2.0; EASA U-space (Reg. EU 2021/664). \\
\hline
Requisitos de Arquitetura (RA) & FAA/NASA FIMS; ASTM F3448 e F3548; Open UTM; InterUSS Foundation. \\
\hline
Requisitos de Processo (RP) & JARUS (metodologia de risco e segurança); ferramentas de engenharia de sistemas (DOORS, Rapita, LDRA). \\
\hline
\end{tabularx}
\end{table}

Esta estrutura visa propiciar a rastreabilidade vertical dos requisitos — do nível conceitual (normativo) ao nível de sistema (implementação e verificação) — alinhando o projeto às boas práticas internacionais de engenharia de sistemas aplicadas à aviação não tripulada.

Este documento apresenta a contextualização e o enquadramento técnico-normativo do Sistema de Simulação UTM, com foco nas necessidades e diretrizes do ecossistema brasileiro de Gerenciamento de Tráfego de Aeronaves Não Tripuladas (BR-UTM).

O objetivo central é garantir uma solução robusta e aderente aos processos e à arquitetura de comunicação estabelecida no Brasil, utilizando as diretrizes internacionais (ICAO, FAA) como inspiração e referencial de boas práticas, mas priorizando a fidelidade arquitetural e as necessidades apontadas pelos especialistas locais.

\section{Enquadramento Normativo e Foco Local}

A definição dos requisitos do simulador baseia-se nas diretrizes estabelecidas pelos especialistas brasileiros, mas reconhece a importância de se inspirar em padrões globais para garantir a evolução e a interoperabilidade futura.

\subsection*{Referências}
\begin{enumerate}
    \item ICAO. UTM Guidance. Documento que fornece orientação sobre a gestão do tráfego de UAS.
    \item FAA. Unmanned Aircraft System (UAS) Traffic Management (UTM) ConOps V2.0.
    \item FAA. Uncrewed Aircraft Systems (UAS) Traffic Management (UTM) Pilot Program (UPP) Final Report.
\end{enumerate}

\begin{table}[h!]
\centering
\caption{Comparação entre referenciais internacionais e foco revisado para o BR-UTM}
\begin{tabular}{|p{3.3cm}|p{5.2cm}|p{6cm}|}
\hline
\textbf{Referencial} & \textbf{Foco Original (Global)} & \textbf{Foco Revisado (BR-UTM)} \\ \hline

ICAO UTM Framework &
Diretrizes globais para harmonização entre ATM e UTM. &
\textbf{Inspiração e Boas Práticas}: Base conceitual para o modelo distribuído e definição de serviços essenciais (ex.: desconflito, informações de voo). \\ \hline

FAA / NASA (ConOps, FIMS) &
Arquitetura de referência baseada no UTM ConOps v2.0 e no FIMS. &
\textbf{Referência Arquitetural}: Guia para concepção da arquitetura de serviços distribuídos, priorizando aderência à arquitetura de comunicação do BR-UTM (Requisitos 85, 89). \\ \hline

ASTM F3448 / F3548 &
Especificações para interoperabilidade e provedores suplementares de dados. &
\textbf{Interoperabilidade Lógica}: Definição dos padrões de troca de dados e APIs do simulador, refletindo a interoperabilidade entre Provedores e Autoridades no contexto brasileiro. \\ \hline

JARUS &
Diretrizes de segurança, avaliação de risco e níveis de garantia (DAL). &
\textbf{Metodologia de Risco}: Base para análise de risco e avaliação de segurança operacional nos cenários simulados. \\ \hline

\end{tabular}
\end{table}

\begin{table}[h!]
\centering
\caption{Estrutura de Atores Prioritária no Contexto BR-UTM}
\begin{tabular}{|p{4cm}|p{10cm}|}
\hline
\textbf{Ator} & \textbf{Papel e Responsabilidade no Contexto da Simulação} \\ \hline

Autoridade Aeronáutica (ANSP/DECEA) &
Ator principal responsável por definir restrições, supervisionar a conformidade regulatória e analisar os resultados da simulação. \\ \hline

Provedores de Serviço UTM (USS) &
Entidades simuladas responsáveis pela coordenação tática, desconflito e gerenciamento operacional, sendo o foco principal da avaliação de desempenho e comportamento. \\ \hline

Operadores de Voo (UAS Operators) &
Entidades simuladas que interagem com os USSs, representando a demanda de tráfego e a execução de missões. \\ \hline

Provedores de Informações Suplementares (SIPs) &
Fontes de dados externas — simuladas ou integradas — que fornecem informações críticas para a execução e a consistência dos cenários. \\ \hline

\end{tabular}
\end{table}

\begin{table}[h!]
\centering
\caption{Categorias de Requisitos e Origem Local}
\begin{tabular}{|p{4cm}|p{10cm}|}
\hline
\textbf{Categoria} & \textbf{Descrição e Origem} \\ \hline

Requisitos de Negócio (RN) &
Derivados das entrevistas com gestores de projeto e autoridades regulatórias brasileiras; refletem os objetivos estratégicos e operacionais do sistema no contexto do BR-UTM. \\ \hline

Requisitos de Arquitetura (RA) &
Originados da análise da arquitetura de comunicação do BR-UTM e de padrões técnicos internacionais (ICAO, FAA, ASTM) utilizados como referência para garantir a fidelidade da simulação. \\ \hline

Requisitos de Processo (RP) &
Associados à engenharia de sistemas, testes e certificação; definidos a partir de práticas recomendadas para assegurar robustez, verificabilidade e validade dos resultados da simulação. \\ \hline

\end{tabular}
\end{table}

\subsection{Conclusão do Enquadramento}

Esta estrutura visa propiciar a rastreabilidade dos requisitos, alinhando o projeto às necessidades reais e imediatas dos especialistas brasileiros, ao mesmo tempo em que mantém a coerência com os princípios de um sistema UTM distribuído e seguro, conforme a inspiração das diretrizes internacionais. O foco é na aplicabilidade prática e na validação de cenários relevantes para a evolução do gerenciamento de tráfego não tripulado no Brasil.

\subsection{Arquitetura Modular e Priorização para o MVP}

A arquitetura modular do Sistema de Simulação UTM foi concebida para permitir extensibilidade, independência entre componentes e capacidade de execução em escala. A estrutura proposta divide o sistema em módulos especializados, que podem ser ativados, combinados e avaliados de forma isolada ou integrada. Para demonstrar rapidamente valor operacional e aderência aos requisitos de especialistas — especialmente no contexto militar — é necessário priorizar um conjunto mínimo de módulos que viabilizem campanhas de teste robustas e auditáveis.

\subsection{Campaign Orchestrator (Prioridade Máxima)

O Campaign Orchestrator é o núcleo operacional do simulador no que se refere à execução massiva de experiências. Ele controla o disparo, agendamento e paralelização de cenários por meio de um mecanismo de jobs associado a um worker pool, permitindo que milhares de execuções sejam processadas em lote. Sua capacidade de replay garante rastreabilidade e repetibilidade dos experimentos, fundamentais para inspeção regulatória e auditoria técnica.
Esse módulo fornece a espinha dorsal da simulação e deve ser implementado primeiro para viabilizar o restante dos testes.

\subsection{Traffic Synthesizer com Perfis Militares e Ameaças}

O gerador de tráfego é responsável pela criação de missões, rotas, eventos e comportamentos plausíveis. Para uso no contexto militar, é essencial que o módulo suporte perfis especiais, como aeronaves kamikaze, comportamentos de spoofing ou jamming, formações coordenadas e tráfego hostil adversarial.
Esse módulo alimenta o motor de simulação com estímulos ricos, permitindo avaliar resiliência do UTM e respostas do sistema em cenários extremos.

\subsection{Conflict Detection & Resolution (CDR) Instrumentado}

O módulo de CDR representa um dos pilares da arquitetura UTM e deve ser completamente instrumentado para registrar latência, estado interno, decisões e justificativas. Ele deve garantir: detecção de conflitos com medição de atraso, resolução automática com diferentes estratégias, suporte a operador no ciclo (man-in-the-loop). Os principais KPIs derivados deste módulo — T_detect, T_resolve e success_rate — são fundamentais para demonstrar conformidade com requisitos internacionais.

\subsection{Decision Support System (DSS) Mínimo}

O DSS atua como uma camada inteligente de suporte à decisão, combinando um rule engine configurável com um risk scorer baseado em ML. A função desse módulo é produzir recomendações explicadas de manobras ou alternativas de desconflito, justificando cada ação.
Este componente aproxima a simulação de um ambiente operacional onde decisões precisam ser rastreáveis e justificáveis perante autoridades.

\subsection{Provider Federation Manager}

Este módulo simula o comportamento de múltiplos USSPs com SLAs distintos e políticas próprias de priorização de tráfego. Ele permite testar interações federadas, troca indireta de informações e interoperabilidade entre provedores — aspectos essenciais do BR-UTM.
A federação de provedores é crítica para analisar gargalos, conflitos de estratégia e comportamento cooperativo ou competitivo.

\subsection{Forensics Store e Evidence Generator (Pacotes SORA)}

A camada de forense garante integridade e verificabilidade dos resultados de cada execução. Esse componente gera evidências criptograficamente assinadas (per-run packages) contendo logs, estados, métricas e trilhas de auditoria — seguindo princípios do SORA.
Este módulo é indispensável para avaliações regulatórias e certificação de cenários de risco.

\subsection{Test Suites Regulamentares}

Um conjunto de testes padronizados deve ser incorporado ao simulador, incluindo: conflict primitives, handover, perda de comunicação, falhas GNSS. Esses cenários refletem diretrizes da ICAO para testes em campo e garantem que a simulação respeite eventos críticos previstos pelo UTM.

\subsection{KPIs and SLA Dashboard + Exportação}

Por fim, o dashboard agrega métricas de campanhas, SLAs e KPIs operacionais. Deve suportar exportação em CSV, PDF e compilação de pacotes de submissão para entidades reguladoras.
Esse módulo fecha o ciclo de avaliação, fornecendo ao especialista uma visão consolidada de desempenho, falhas e tendências.

\subsection{Métricas e KPIs Recomendados para a Arquitetura do Simulador}

Para que o simulador opere como uma plataforma confiável de avaliação técnica, ele deve medir e registrar um conjunto consistente de métricas que reflitam eficácia, segurança e desempenho do sistema.

\subsection{Taxa de Detecção de Conflito (TPR)}

Reflete a eficiência do módulo de CDR na identificação de eventos perigosos. É a razão entre conflitos detectados e conflitos injetados. Criticamente importante para avaliar a qualidade de algoritmos e SLAs.

\subsection{Tempo Médio de Identificação (T_detect)}

Corresponde ao intervalo entre a ocorrência de um evento de conflito e sua detecção pelo sistema. Deve ser registrado em milissegundos ou segundos.
Baixos valores indicam maior consciência situacional.

\subsection{Tempo Médio de Resolução (T_resolve)}

Mede o tempo necessário para que uma ação corretiva seja aplicada após a identificação do conflito. Essa métrica está diretamente relacionada à eficácia das estratégias automáticas e da interação humano-máquina.

\subsection{Taxa de Resoluções Bem-Sucedidas (success_rate)}

Indica o percentual de conflitos solucionados sem violar restrições operacionais ou comprometer missões. É um indicador chave de confiabilidade do UTM.

\subsection{Falsos Positivos e Falsos Negativos}

Essas métricas avaliam como o sistema equilibra sensibilidade e precisão, permitindo identificar cenários onde operadores podem ser sobrecarregados (muitos falsos positivos) ou onde o sistema falha em alertar (falsos negativos).

\subsection{Throughput de Simulação}

Quantidade de execuções por hora ou por cluster computacional. Mede a escalabilidade do modelo e a eficiência do Campaign Orchestrator.

\subsection{Latência CIS (Publicação → Propagação)}

Avalia o tempo necessário para que mensagens e estados sejam distribuídos aos participantes, essencial para validar SLAs baseados na ED-318.

\subsection{Robustez Frente a Ameaças (resilience_score)}

Percentual de missões críticas que permanecem operacionais sob condições adversas, como spoofing, jamming ou tráfego hostil.
Fundamental para cenários militares e experimentos de resiliência.

\subsection{Tempo Médio de Recuperação (MTTR)}

Mede quanto tempo o sistema leva para retornar ao funcionamento normal após uma falha. Conecta-se diretamente à robustez da federação de provedores e do DSS.

\subsection{Métodos de Teste Recomendados para o Simulador UTM}

A arquitetura modular do simulador UTM possibilita a aplicação de uma variedade de técnicas avançadas de teste, essenciais para validar robustez, segurança operacional, comportamento sob ameaça e conformidade regulatória. Cada método abaixo desempenha um papel complementar na avaliação do sistema.

\subsection{Monte-Carlo e Latin Hypercube Sampling}

Esses métodos permitem explorar grandes espaços de variáveis através de amostragem estatística. Ao variar parâmetros como densidade de tráfego, padrões de vento, latência de comunicação ou probabilidade de falha, é possível identificar limites operacionais e sensibilidades do sistema.
O uso de Latin-Hypercube aumenta a cobertura de combinações, gerando cenários mais diversificados e reduzindo o risco de lacunas estatísticas.

\subsection{Fuzzing de Inputs}

O fuzzing insere entradas inesperadas ou malformadas — como planos de voo corrompidos, mensagens incompletas ou valores fora de faixa — com o objetivo de revelar vulnerabilidades de parsing, validação e resiliência do sistema.
Esse método é particularmente eficaz na detecção de falhas silenciosas e comportamentos imprevisíveis, sobretudo em módulos críticos como ingestão de dados e APIs do CIS.

\subsection{Adversarial Scenario Injection (Threat Feed)}

Esse método insere eventos hostis deliberados, como spoofing de posição, jamming de sinais, mensagens falsas de USSP ou comportamentos maliciosos de aeronaves.
O objetivo é avaliar a capacidade do sistema de detectar, desacoplar ou mitigar ameaças, fornecendo insumos para métricas de resiliência e para geração de pacotes de evidência em contextos de segurança.

\section{Red-Team / Blue-Team Exercises}

Nesse tipo de exercício, operadores humanos (Blue Team) interagem com agentes adversariais simulados (Red Team).
Esse teste permite avaliar a sobrecarga cognitiva, a eficácia do suporte à decisão, e o comportamento do sistema em situações de ataque coordenado ou saturação intencional.
Ele também fornece dados qualitativos sobre o desempenho do DSS e da interface humano-máquina.

\subsection{Stress e Saturation Tests}

Esses testes exploram os limites físicos e lógicos do sistema:

densidade máxima de tráfego 4D,

taxas elevadas de atualização,

degradação proposital de latências e perdas de pacotes.
O objetivo é identificar gargalos, falhas de escalabilidade e comportamentos emergentes sob carga extrema – fundamentais para validar a robustez do simulador e dos módulos de federação de provedores.

\subsection{Regression Testing e Deterministic Replay}

A capacidade de reproduzir exatamente um cenário — através de seeds fixas — é essencial para depuração e análise forense.
O replay determinístico permite validar correções com segurança, comparando comportamento antes/depois de alterações e garantindo que novas funcionalidades não introduzam regressões.
Esse mecanismo também é indispensável para geração de evidências verificáveis para autoridades reguladoras.

\section{Formato das Evidências Geradas pelo Simulador}

Para atender às necessidades de certificação, conformidade técnica e auditoria regulatória, o simulador deve produzir evidências estruturadas, assinadas e rastreáveis. Essas evidências compõem o material que será submetido a autoridades aeronáuticas ou entidades de avaliação.

Pacote SORA-Like (JSON + PDF)

O pacote principal consolida todos os elementos necessários para análise técnica de um cenário ou campanha:

definição completa do cenário e parâmetros de entrada,

classificação iGRC e ARC,

mitigações aplicadas,

trilhas de auditoria e logs assinados,

resultados da campanha (KPIs, incidentes, análises).
O objetivo é fornecer uma documentação coerente, auditável e compatível com processos inspirados no SORA.

Relatórios de SLA

Esses relatórios oferecem uma visão quantitativa sobre desempenho e disponibilidade:

latência de publicação e propagação no CIS,

disponibilidade e responsividade dos USSP simulados,

violação de janelas de tempo críticas.
Eles são especialmente importantes para autoridades que buscam validar limites de operação e identificar fragilidades no ecossistema UTM.

Replay Package

Conjunto de arquivos contendo:

traces completos,

telemetria detalhada,

marcações de tempo das decisões (com assinatura).
Esse pacote garante reprodutibilidade e permite reconstruir o comportamento do sistema quadro-a-quadro, usado em investigações, auditorias ou validação de regressões.

Lista de Incidents

Documento estruturado que relaciona:

todos os eventos que violaram regras, SLAs ou separação,

condições que levaram ao incidente,

ações tomadas,

eficácia das respostas tanto automáticas quanto humanas.
Essa lista é fundamental para processos de análise de segurança e para verificar aderência a padrões operacionais.

OBs AUTOR em 25.11.2025:
gostei, porem nao noitei muito alinhamento com a minha arquitetura de necessidade dos especialistas militares de voo ATM que estao pensando nos gargalos do utm , para as diretrizes UTM fornecidas. Principalmente nos pontos iniciais que estamos que diZ respeito a testar os cenarios simulados dos testes de prova e em campo, conforme proposato pela ICAO, principalmente com relação a confluto, desconflito, gestão de provedores e DSS. Porem eles demonstram que todos estes dados precisa ir a um simulador robusto que possa prever milhares de caso de testes para efetivar e mehlrara a acertabilidade de resposta dos orgaos de fiscalizacao, frente aos grandes desafios, no que diz respeito ao compartilhamento do espaço, segurança, ataques voos conflitosos, tarifação, operações no espaço 4D , gestão das diferentes operações para autorizar, priorização de espaço, entre outros.

\section{Mapeamento de Normas para Componentes da Arquitetura}

Esta seção descreve como cada regulamentação internacional de UTM/U-Space foi mapeada para componentes específicos do simulador. Também são apresentados os princípios, diretrizes e obrigações de cada norma, destacando quais partes foram incorporadas ao modelo e quais ainda exigem extensão.

\subsection{ICAO UTM Framework}
O \textit{ICAO UTM Framework} define diretrizes globais para gestão do tráfego não tripulado, enfatizando:
\begin{itemize}
    \item Catálogo mínimo de serviços UTM (UDM, conformance monitoring, strategic deconfliction).
    \item Integração operacional com o sistema ATM existente.
    \item Segurança operacional como princípio norteador.
    \item Necessidade de registro auditável, rastreabilidade e mecanismos para incident reporting.
\end{itemize}

\noindent
\textbf{Componentes mapeados:}
\begin{itemize}
    \item \textbf{Simulation Engine}: modelagem dos serviços UTM obrigatórios.
    \item \textbf{ATM Adapter}: coordenação entre UTM simulado e procedimentos ATM.
    \item \textbf{SORA Module}: suporte à avaliação de risco seguindo diretrizes ICAO.
    \item \textbf{Audit \& Evidence Store}: registro auditável conforme requisitos ICAO.
\end{itemize}

\subsection{FAA UTM ConOps}
O \textit{FAA UTM Concept of Operations} estabelece:
\begin{itemize}
    \item Modelo federado de USS (similar ao USSP europeu), com responsabilidade dividida entre FAA e indústria.
    \item Princípios de interoperabilidade entre provedores.
    \item Troca de informações via APIs padronizadas.
    \item Foco na autonomia do UTM para operações BVLOS e missões densas.
\end{itemize}

\noindent
\textbf{Componentes mapeados:}
\begin{itemize}
    \item \textbf{USSP/USS Adapter}: representação de múltiplos provedores federados.
    \item \textbf{API Gateway}: abstração para troca de mensagens inter-USSP.
    \item \textbf{Auth \& Access Control}: aderência ao modelo FAA de responsabilidade compartilhada.
\end{itemize}

\subsection{SESAR / EUROCAE ED-318 (U-Space)}
A especificação \textit{EUROCAE ED-318} é a referência técnica mais detalhada em termos de:
\begin{itemize}
    \item Definição formal de zonas geográficas (geozones) e suas propriedades.
    \item Formatos de mensagens para o \textit{Common Information Service} (CIS).
    \item Protocolos para intercâmbio entre USSPs e serviços U-Space.
    \item Requisitos de latência, SLA e consistência de dados.
\end{itemize}

\noindent
\textbf{Componentes mapeados:}
\begin{itemize}
    \item \textbf{CIS Service}: implementação dos modelos de dados e trocas ED-318.
    \item \textbf{GeoZone Manager}: ingestão, validação e aplicação de zonas U-Space.
\end{itemize}

\subsection{JARUS SORA}
A metodologia \textit{JARUS SORA} fornece o processo internacionalmente aceito para avaliação de risco em operações RPAS:
\begin{itemize}
    \item Cálculo de risco inicial (\textit{iGRC}).
    \item Determinação do nível de robustez requerido (\textit{SAIL}).
    \item Conjunto de mitigadores técnicos e organizacionais.
    \item Exigência de documentação estruturada, justificativas e evidências para autoridades.
\end{itemize}

\noindent
\textbf{Componente mapeado:}
\begin{itemize}
    \item \textbf{Risk Assessment (SORA Module)}: cálculo automatizado de iGRC, SAIL e mitigadores, além de geração de pacotes de evidência.
\end{itemize}

\section{Cobertura Atual da Arquitetura}
A arquitetura atual do simulador cobre:
\begin{itemize}
    \item Blocos explícitos para CIS/ED-318.
    \item Pipeline SORA para avaliação de risco.
    \item Abstração para múltiplos USSP/USS no modelo federado.
    \item Camada de segurança operacional e auditoria.
\end{itemize}

\section{Pontos que Requerem Extensão}
Os seguintes itens ainda exigem desenvolvimento adicional:
\begin{itemize}
    \item Implementação completa dos esquemas ED-318 (JSON/XML) e validadores.
    \item Testes documentados de desempenho (SLA de latência, disponibilidade).
    \item Geração automatizada de pacotes SORA com justificativas formais.
    \item Mecanismos de certificação: logs assinados, retenção, timestamps confiáveis.
\end{itemize}

\section{Recomendações Práticas e Próximos Passos}

\subsection{1. Validar ED-318 no CIS Service}
Implementação completa dos esquemas ED-318 no serviço CIS, incluindo:
\begin{itemize}
    \item Validadores estruturais (JSON/XML).
    \item Conjunto de testes (\textit{test harness}) para cenários CIS.
\end{itemize}

\subsection{2. Pipeline SORA automatizado}
Construção de pipeline end-to-end contendo:
\begin{itemize}
    \item Templates Annex A (\textit{ConOps}).
    \item Cálculo automatizado de iGRC/SAIL.
    \item Geração do pacote final de evidência.
\end{itemize}

\subsection{3. Testes de integração USS}
\begin{itemize}
    \item Execução de cenários com USSPs em modo \textit{mock}.
    \item Medição de latências e ajustes de cache.
\end{itemize}

\subsection{4. Fortalecimento de Segurança}
\begin{itemize}
    \item Uso de HSM para chaves críticas.
    \item Assinatura de logs e política de retenção.
    \item Rotina de pentest orientada às recomendações ICAO.
\end{itemize}

\subsection{5. Painel Unificado de KPIs}
Desenvolver dashboard com KPIs padronizados:
\begin{itemize}
    \item Latência CIS.
    \item Disponibilidade USSP.
    \item Tempo de detecção e resolução de conflitos.
\end{itemize}

\section{Fontes Primárias Consultadas}
\begin{itemize}
    \item \textbf{ICAO}: UTM Framework / Guidance Material.
    \item \textbf{FAA}: UTM Concept of Operations v2.0.
    \item \textbf{EUROCAE}: ED-318 Technical Specification.
    \item \textbf{SESAR}: U-Space ConOps.
    \item \textbf{JARUS}: SORA v2.x.
\end{itemize}

\section{Resumo da Proposta de Adequação Normativa da Arquitetura}

A arquitetura do simulador foi revisada e aprimorada para alinhar-se às principais referências regulatórias internacionais: ICAO UTM Framework, FAA UTM ConOps, EUROCAE ED-318 (U-Space), SESAR e JARUS SORA. As mudanças afetam diretamente os componentes centrais do sistema, seus fluxos de dados, requisitos funcionais e evidências regulatórias associadas.

\subsection{Principais Alterações Implementadas}

\paragraph{1. CIS como Serviço Explícito (ED-318)}
O \textit{Common Information Service} foi isolado como serviço dedicado, com schemas formais para geozonas, mensagens de espaço aéreo e informações tipo NOTAM. A estrutura segue diretamente os modelos e formatos exigidos pela norma ED-318, garantindo compatibilidade com U-Space e padronização das trocas de dados.

\paragraph{2. Interfaces USSP/USS Padronizadas (ICAO/FAA/SESAR)}
Foram definidas interfaces separadas para comunicação entre provedores de serviço UTM (USSP/USS), mediadas por um \textit{API Gateway}. Esse modelo segue o conceito federado estabelecido pelo FAA UTM ConOps e a delimitação de papéis entre operador, provedor e autoridade proposta em ICAO/SESAR. A arquitetura agora explicita responsabilidades e pontos de delegação.

\paragraph{3. Módulo SORA Automatizado (JARUS)}
O pipeline SORA foi incorporado, permitindo processamento automático do fluxo \textit{CONOPS → iGRC → mitigations → SAIL}. O módulo gera evidências exportáveis (JSON/PDF), aderentes às exigências do \textit{JARUS SORA v2.x}. Este componente suporta análises repetíveis e documentação técnica para submissão a autoridade.

\paragraph{4. Segurança, Auditoria e Cadeia de Custódia (ICAO/EASA)}
Foram incluídos mecanismos de segurança compatíveis com recomendações ICAO/EASA:
\begin{itemize}
    \item Autenticação forte (OAuth2 e mTLS).
    \item Proteção de chaves via HSM.
    \item Logs imutáveis com assinaturas digitais (WORM/append-only).
    \item Política de retenção e rastreabilidade completa para fins regulatórios.
\end{itemize}
Essas medidas garantem integridade, auditabilidade e conformidade com requisitos de investigação operacional.

\paragraph{5. Interoperabilidade ATM/ATC (ICAO/FAA)}
A arquitetura inclui adaptadores para formatos aeronáuticos amplamente utilizados (AIXM, ASTERIX, FIXM), permitindo troca de informações entre o núcleo UTM e sistemas ATM simulados. Foram definidos limites de delegação, incluindo critérios para handover para ATC durante cenários de contingência.

\paragraph{6. Medição de SLAs e KPIs Regulamentares}
A solução incorpora um módulo de coleta e análise de indicadores:
\begin{itemize}
    \item Latência de serviços CIS (ED-318).
    \item Disponibilidade e responsividade de USSPs (FAA/SESAR).
    \item Tempos de detecção e resolução de conflitos.
\end{itemize}
Esses dados alimentam dashboards padronizados e servem como evidências para ensaios regulatórios e ambientes sandbox.

\subsection{Conjuntos de Artefatos Gerados}
A proposta inclui ainda um conjunto completo de diagramas e representações:
\begin{itemize}
    \item Diagramas PlantUML revisados para arquitetura geral e detalhada.
    \item UMLs específicos para CIS/Geozonas (ED-318), USSP/USS (FAA/ICAO), módulo SORA (JARUS), integração ATM e segurança/auditoria.
    \item Mapeamento direto norma → componente, destacando aderência e lacunas remanescentes.
\end{itemize}

\subsection{Recomendações e Próximos Passos Prioritários}

\paragraph{1. Validação Completa ED-318}
Implementar validadores automáticos (JSON/XML) para todos os schemas ED-318, além de adaptadores robustos no serviço CIS, assegurando fidelidade aos formatos oficiais.

\paragraph{2. SORA Automatizado e Geração de Evidência}
Concluir pipeline de geração de artefatos de risco (iGRC, mitigations, SAIL), exportação em PDF/JSON e templates baseados no Annex A. Este fluxo deve permitir submissão direta às autoridades.

\paragraph{3. Ensaios de Performance com SLAs}
Executar testes de carga e latência, com coleta contínua de KPIs e estruturação de dashboards conforme requisitos EASA/FAA para ambientes de certificação e sandbox.

\paragraph{4. Fortalecimento de Segurança e Auditoria}
Expandir mecanismos de segurança com logs imutáveis, HSM, monitoramento contínuo e práticas de gestão de risco alinhadas ao guidance cibernético da EASA.

\subsection{Síntese Geral}
As alterações propostas elevam o simulador ao nível das referências regulatórias mais importantes, garantindo compatibilidade estrutural com U-Space, ICAO e FAA, e incorporando uma base robusta de avaliação de risco via SORA. A arquitetura resultante é modular, auditável, interoperável e pronta para sustentação de ensaios regulatórios, experimentação controlada e comprovação de conformidade técnica em sandbox.

\section{Grau de Alinhamento Normativo da Arquitetura}

A arquitetura revisada do simulador apresenta diferentes níveis de aderência às normas e guias internacionais, variando entre conformidade forte, conformidade parcial e funções propositalmente fora do escopo regulatório. A seguir descrevem-se os principais pontos de alinhamento.

\subsection{Alinhamento Forte com Normas Internacionais}

A solução demonstra alto grau de conformidade nas áreas relacionadas à modelagem de serviços compartilhados e gestão de informação. Em particular, foram implementados de forma explícita os seguintes elementos:
\begin{itemize}
    \item \textbf{Serviços CIS e Estruturas de Intercâmbio}: alinhados às diretrizes de EASA, SESAR e FAA, que definem estruturas equivalentes para troca de informações críticas no ecossistema UTM/U-Space.
    \item \textbf{Representação de Geozonas}: compatível com os requisitos funcionais e operacionais estabelecidos por ED-318 e pelos projetos SESAR.
    \item \textbf{Monitoramento Operacional e Interface para Operador}: coerente com os padrões de vigilância, supervisão e transparência exigidos em ambientes regulados.
\end{itemize}
Essas partes da arquitetura obedecem de forma clara ao modelo europeu de U-Space, ao guidance da EASA e às práticas do FAA UTM ConOps para serviços federados e informações compartilhadas.

\subsection{Pontos Parcialmente Atendidos}

Alguns elementos apresentam boa estrutura arquitetural, mas ainda requerem implementação normativa detalhada para atender plenamente aos padrões oficiais. Entre os principais pontos parcialmente cobertos estão:
\begin{itemize}
    \item \textbf{Conformidade formal de USSP/USS}: embora os adaptadores e fluxos estejam definidos, faltam requisitos específicos de certificação, testes de conformidade e mecanismos padronizados de evidência.
    \item \textbf{Workflow SORA e Formalização Completa de Risco}: o módulo SORA está previsto e parcialmente implementado, mas necessita de justificativas de mitigação, templates oficiais e integração completa do fluxo \emph{iGRC → SAIL}.
    \item \textbf{Requisitos de SLA, Métricas Normativas e Schemas ED-318}: a arquitetura já contém componentes de medição e coleta, porém ainda carece dos esquemas completos, métricas exatas e relatórios padronizados exigidos pelas normas europeias.
\end{itemize}
Esses itens representam áreas em que a estrutura existe e está corretamente posicionada, mas depende de desenvolvimento adicional para demonstrar conformidade formal em processos de auditoria ou certificação.

\subsection{Funcionalidades Fora do Escopo das Normas}

Determinadas capacidades do simulador não são exigidas pelas normas internacionais, mas são mantidas por sua utilidade operacional e valor técnico para ensaios. Estas funcionalidades não conflitantes incluem:
\begin{itemize}
    \item \textbf{Motor de Dinâmica de Voo}: não regulado por ICAO/EASA/FAA para fins de UTM, mas essencial para representar comportamentos realistas.
    \item \textbf{Geração de Tráfego Sintético}: não normatizada, porém crítica para cargas de teste, cenários adversariais e modelagem estatística.
    \item \textbf{Visualizações Avançadas}: úteis para análise exploratória, mas sem exigências formais em guidelines internacionais.
    \item \textbf{Testes de Estresse e Saturação}: práticas recomendadas em engenharia, porém não especificadas em documentos U-Space/FAA.
\end{itemize}

\noindent Essas funções estão deliberadamente fora do escopo regulatório, mas são cruciais para validar comportamentos, gerar campanhas experimentais e produzir evidências consistentes para ambientes sandbox e avaliações técnicas.

\section{Análise de Conformidade por Requisito}

A seguir apresenta-se a análise descritiva de cada requisito técnico da arquitetura, indicando se é exigido pelas regulações internacionais (EASA, FAA, SESAR, ICAO), o grau de cobertura atual na arquitetura e as principais observações necessárias para atingir conformidade plena.

\subsection{Serviços CIS e Troca de Dados (ED-318)}

As regulações europeias e documentos SESAR/ED-318 exigem modelos de dados padronizados, endpoints bem definidos e requisitos de desempenho para serviços CIS.  
Na arquitetura atual, o suporte é \textbf{parcial}: existem os módulos \texttt{CIS\_MOCK} e \texttt{CIS\_SVC}, capazes de emular o intercâmbio conforme ED-318.  
Entretanto, ainda é necessária a implementação completa dos schemas ED-318/ED-269, além de testes formais de temporização e conformidade.  
Os reguladores exigem SLAs explícitos, formatos oficiais e validadores automáticos.

\subsection{Certificação e Requisitos de USSP / Provedor U-Space}

As normas EASA U-Space definem requisitos de responsabilidade, desempenho, disponibilidade e acesso seguro para provedores USSP.  
A arquitetura cobre o tema de forma \textbf{parcial}: USSP e ATC são emulados, mas não há módulo formal de certificação, geração de relatórios de SLA ou auditoria automatizada.  
Para conformidade plena são necessários logs imutáveis, trilhas de evidência e relatórios padronizados para autoridades.

\subsection{Avaliação de Risco (SORA / ICAO)}

A ICAO e o JARUS SORA exigem processos formais de análise de risco, mitigação e níveis equivalentes de confiabilidade operacional.  
O ambiente atual fornece \texttt{REPORTS} e \texttt{STRATEGIC\_ANALYSIS}, porém a conformidade é apenas \textbf{parcial}.  
Faz-se necessário um módulo SORA completo com workflow: entrada do cenário, cálculo de \textit{intrinsic risk}, definição das mitigations e produção de documentação final estruturada.

\subsection{Geo-awareness, Geozones e Zonas Dinâmicas}

ED-318, EAR e SESAR exigem suporte a geozonas dinâmicas, atualizações em tempo real e consistência entre provedores.  
A arquitetura atende \textbf{plenamente} o requisito: os módulos \texttt{ADAPTERS} e \texttt{CIS\_MOCK} já oferecem suporte a zonas dinâmicas.  
Permanece necessária a validação de reconfigurações em tempo real e testes de latência/distribuição.

\subsection{Segurança da Informação e Cibersegurança}

As regulações EASA exigem práticas de gestão de risco, proteção criptográfica e integridade operacional.  
A solução cobre o tema de forma \textbf{parcial}: os módulos \texttt{AUTH} e \texttt{AUDIT} existem, porém recomenda-se reforço com HSM, criptografia ponta-a-ponta, políticas de retenção e testes de segurança.  
A conformidade requer evidências formais e cadeia de custódia.

\subsection{Monitoramento, Desempenho e KPIs Operacionais}

EASA e SESAR exigem SLAs claros e métricas de desempenho para serviços U-Space.  
A arquitetura oferece \textbf{cobertura completa}: os módulos \texttt{METRICS}, \texttt{REPORT\_SVC} e \texttt{DW} atendem a coleta e monitoramento.  
Falta incorporar KPIs específicos exigidos pelas normas (latência CIS, disponibilidade USSP, tempos de detecção e resolução).

\subsection{Interoperabilidade com Sistemas ATM / ATC}

A FAA e a ICAO determinam processos de intercâmbio com sistemas ATM, incluindo formatação, segurança e limites de delegação.  
A arquitetura possui \textbf{cobertura parcial}: módulos como \texttt{ATC\_EMU} e \texttt{ADAPTERS} viabilizam a integração, mas o uso com ATC real exige certificação, formatos completos (AIXM, CIDIN, ASTM) e validação operacional.

\subsection{Auditabilidade e Logs Imutáveis}

Regulações EASA e ICAO exigem rastreabilidade completa e registros à prova de adulteração.  
O módulo \texttt{AUDIT} atende parcialmente ao requisito.  
Para conformidade completa, recomenda-se WORM storage, assinaturas digitais, retenção regulatória e capacidade de exportação de logs assinados.

\subsection{Procedimentos Operacionais e Operador no Loop}

Normas SESAR e FAA exigem workflows operacionais claros, responsabilidades definidas e suporte a operações com humano no loop.  
A arquitetura atende \textbf{plenamente}: componentes como \texttt{UI}, \texttt{Operator CLI} e \texttt{Scenario Manager} suportam testes e operações H-in-the-loop.  
Sugere-se adicionar checklists operacionais padronizados.

\subsection{Funcionalidades Específicas de Simulação}

Aspectos como testes de estresse, replays determinísticos, tráfego sintético e telemetria enriquecida não são regulamentados.  
A arquitetura cobre esses itens \textbf{totalmente}, com \texttt{SAT\_SVC}, \texttt{Scenario Service} e módulos de telemetria.  
Apesar de não obrigatórios, esses recursos são importantes para ensaios e demonstração de conformidade em cenários controlados.

\section{Referências Técnicas e Arquiteturais}

Documentos públicos de referência influenciam o desenho da arquitetura. As principais fontes incluem:

\begin{itemize}
    \item \textbf{EASA U-Space (EAR \& Regulamentos)}: conjunto consolidado de regras e diretrizes para serviços U-Space na União Europeia.
    \item \textbf{EUROCAE ED-318 e Projetos Sandbox}: especificações técnicas de geozonas, formatos de dados e intercâmbio.
    \item \textbf{SESAR U-Space CONOPS}: princípios arquiteturais para organização de serviços, CIS e interoperabilidade.
    \item \textbf{NASA UTM ConOps v1.0 / NTRS}: definição dos blocos USS, troca de dados, responsabilidades e níveis TCL.
    \item \textbf{FAA UTM ConOps v2.0}: arcabouço regulatório e operacional dos EUA para serviços UTM e federated USS.
    \item \textbf{Protótipos Airbus/EUROCONTROL e Relatórios de Demonstração}: úteis para padrões de integração e simulação de riscos.
\end{itemize}

\section{Referências Técnicas e Documentos Normativos}

\subsection{Documentos Regulamentares e Técnicos}

\begin{description}

    \item[EASA – U-Space Regulation (EU) 2021/664] 
    Conjunto de regras europeias que definem os serviços U-Space, responsabilidades dos U-Space Service Providers (USSP), requisitos de desempenho, SLAs, segurança operacional e interfaces de informação. Contém o material consolidado conhecido como Easy Access Rules (EAR).

    \item[EUROCAE ED-318] 
    Especificação técnica oficial para modelos de dados, geozonas, mensagens, requisitos de troca de informação e padrões de interoperabilidade para serviços U-Space. Inclui formatos de dados, semântica, endpoints e regras de sincronização.

    \item[EUROCAE ED-269]
    Documento complementar ao ED-318 que detalha estruturas para serviços U-Space, incluindo requisitos de desempenho, consistência e validação de dados.

    \item[SESAR – U-Space Concept of Operations (CONOPS)] 
    Blueprint conceitual europeu para definição de serviços U-Space, CIS (Common Information Services), padrões de integração com ATM e princípios de operação.

    \item[JARUS SORA v2.x (Specific Operations Risk Assessment)]
    Metodologia padronizada internacionalmente para avaliação de risco operacional de operações com RPAS/UAS. Define iGRC, mitigations, SAIL, requisitos de assurance e documentação obrigatória para submissão à autoridade.

    \item[NASA UTM – ConOps v1.0 / NTRS Material]
    Arquitetura conceitual do ecossistema UTM (UAS Traffic Management) contendo componentes USS, provedores de serviço, intercâmbio de dados, reserva de volumes de espaço aéreo e responsabilidades operacionais.

    \item[FAA – UTM ConOps v2.0]
    Descrição oficial da Arquitetura UTM nos Estados Unidos, incluindo serviços USS, UAS Volume Reservations, requisitos de segurança, responsabilidades do operador e do provedor e integração com o sistema ATC.

    \item[U-Space Sandbox Standards and Services (Transpordiamet)]
    Documentação pública que descreve a arquitetura de referência para sandboxes U-Space, incluindo serviços CIS, geozonas, requisitos de latência, disponibilidade, schemas ED-318 e indicadores regulatórios.

    \item[Airbus / EUROCONTROL Prototypes]
    Relatórios de demonstrações e protótipos de simulações U-Space utilizados para validação de requisitos de integração, desempenho, segurança e coordenação multi-USSP.

\end{description}

\section{Lista de Siglas e Definições}

\begin{description}

    \item[ATM] Air Traffic Management — Gerenciamento do tráfego aéreo.
    \item[ATC] Air Traffic Control — Controle de tráfego aéreo.
    \item[AIXM] Aeronautical Information Exchange Model — Modelo para troca de informação aeronáutica.
    \item[ASTERIX] All Purpose Structured Eurocontrol Surveillance Information Exchange — Padrão de vigilância EUROCONTROL.
    \item[FIXM] Flight Information Exchange Model — Modelo para troca de informação de voo.
    \item[CIS] Common Information Services — Serviço de informação comum para U-Space/UTM.
    \item[CIS\_SVC / CIS\_MOCK] Versões simuladas/implementadas de CIS usadas no simulador.
    \item[CONOPS] Concept of Operations — Documento conceitual de operação.
    \item[DAL] Design Assurance Level — Nível de garantia de projeto.
    \item[EASA] European Union Aviation Safety Agency — Agência Europeia de Segurança da Aviação.
    \item[ED-318 / ED-269] Documentos EUROCAE que definem dados, geozonas e troca de informação U-Space.
    \item[FAA] Federal Aviation Administration — Administração Federal de Aviação (EUA).
    \item[EAR] Easy Access Rules — Consolidação de regras EASA.
    \item[HSM] Hardware Security Module — Equipamento de segurança para gestão de chaves criptográficas.
    \item[iGRC] Intrinsic Ground Risk Class — Classe intrínseca de risco ao solo (SORA).
    \item[JARUS] Joint Authorities for Rulemaking on Unmanned Systems — Grupo internacional para réglementation de UAS/RPAS.
    \item[KPI] Key Performance Indicator — Indicador-chave de desempenho.
    \item[LHS] Latin Hypercube Sampling — Técnica estatística de amostragem.
    \item[mTLS] Mutual TLS — Autenticação mútua via certificados.
    \item[PAS] Provider Agent System — Componente do MAS no simulador.
    \item[MAS] Multi-Agent System — Sistema multiagente.
    \item[MRA] Mission Resource Agent — Agente de recursos do simulador.
    \item[USSP / USS] U-Space Service Provider / UTM Service Supplier (EUA) — Fornecedores de serviços U-Space/UTM.
    \item[SAT\_SVC] Serviço de saturação e estresse do simulador.
    \item[SAIL] Specific Assurance and Integrity Level — Nível de integridade/garantia SORA.
    \item[SLAs] Service Level Agreements — Acordos de desempenho de serviços.
    \item[SORA] Specific Operation Risk Assessment — Metodologia internacional de avaliação de risco operacional.
    \item[TCL] Technical Capability Level — Níveis do programa de testes UTM da NASA.
    \item[UI] User Interface — Interface do Operador.
    \item[UTM] Unmanned Aircraft System Traffic Management.
    \item[U-Space] Ecossistema europeu equivalente ao UTM.
    \item[WORM] Write-Once Read-Many — Armazenamento imutável para logs/auditoria.

\end{description}



---
Neste dia estou compilando todos os textos que estão separados entre os trabalhos do SAC, MRCF, PLANAR e outros sobre UTM e ultimos feitos sobre regulacao e arquitetura de BVLOS, nas semanas entre 18 á 28.11

Compilei a maquina das arquiteturas até chegar no seguinte:
ocê está correto ao notar que o PlantUML, embora excelente para diagramas de texto simples, tem limitações na representação 3D e na exibição de detalhes mais avançados de forma nativa.
No contexto de ferramentas de diagramação de arquitetura, existem plataformas mais avançadas que oferecem visualizações 3D ou que permitem uma organização visual mais rica e interativa, embora a geração a partir de um código simples como o PlantUML seja um desafio.
A ferramenta mais próxima do que você descreve, que permite uma visualização de arquitetura em camadas (o que simula o "3D" ou a profundidade) e com maior detalhe, é o Diagrama C4.
O Modelo C4 é uma abordagem para visualização de arquitetura de software que foca em diferentes níveis de abstração (Contexto, Contêineres, Componentes e Código). Embora o PlantUML suporte a sintaxe C4, outras ferramentas oferecem uma renderização mais sofisticada.
Ferramentas que oferecem visualização mais avançada:
Structurizr: É uma ferramenta que implementa o Modelo C4. Ela permite definir a arquitetura em código (DSL) e renderiza diagramas interativos que podem ser navegados em diferentes níveis de detalhe. Embora não seja 3D no sentido literal, a separação em camadas C4 (Contexto, Contêiner, Componente) oferece a profundidade de detalhe que você busca.
Mermaid.js / Kroki: São alternativas ao PlantUML que, embora ainda sejam baseadas em texto, oferecem diferentes estilos de renderização que podem ser mais limpos ou modernos.
Ferramentas de Modelagem Gráfica (Ex: draw.io, Lucidchart): Estas permitem a criação manual de diagramas 3D ou em perspectiva, mas perdem a vantagem da geração automática a partir de código.
Avançando com o PlantUML (Melhor Opção no Nosso Ambiente):
Como estamos limitados ao ambiente de sandbox e ao PlantUML, a melhor maneira de simular o "3D" e o detalhe é através da sintaxe C4-PlantUML.
O C4-PlantUML permite que eu defina os pacotes e componentes em diferentes níveis de abstração (Contexto, Contêiner, Componente), o que organiza a informação de forma hierárquica e detalhada, simulando a profundidade.
Proposta:
Vou reescrever o diagrama utilizando a sintaxe C4-PlantUML para criar um Diagrama de Contêineres (que é o nível logo abaixo do Contexto), o que dará a visão detalhada e organizada que você busca, mantendo a clareza e a estrutura top-down.
Você gostaria que eu gerasse o diagrama usando a sintaxe C4-PlantUML? (O resultado ainda será uma imagem 2D, mas com a organização lógica de profundidade do C4).

Objetivo específico de hoje:
--
 ( ) Inserir todos os textos no Overleaft
 ( ) Após os textos, inserir no prisma para monitorar revisoes e inserir no github, em seguida iniciar a lapidação da QUALIS
 ( ) Após lapidar, finalizar os SLIDs e enviar para os Orientadores.

PESQUISAS 18.11.2025 (Objetivo, planejamento para Apresentacao e Estruturacao da QUALIS)
---
Nesse dia, eu fiz os textos tanto para apresentação dos PITCH Planar, quanto PITCH da QUALIS. Após estes planos, tambem comecei o template em .ppt para QUALIS, porem resolvi rodar o exemplo fornecido pelo programa, e tambem, começar o preenchimento do docuemnto FAPESP. Algumas coisas que pensei em conjunto foi como divulgar e escolha de busca de alunos e orientação, para meta de gerar dez trabalhos relacionados em 2026.

( ) Rodar e Iniciar a divisão do documento QUALIS
( ) Fazer a Introducao e Contexto para o MIRF
( ) Elencar possiveis parceiros: ENCITA, e outros programas tanto no ITA, IFAL, ITA-CE, Federal de SP, etc. Buscar de novo contato com o colega que possui base de dados dos alunos e programas internos
( ) Programar os artigos resumo para forum, para divulgação e amplicar o alcance: Minicurso, Artigo MRCF, Site PlaNAR, projeto Planar, DEV do MIRF e inserir nos programas de UAS o PlaNAR UTM.
---
MIRF — *Mission Intelligence & Reconfiguration Framework*, parte da sua linha de pesquisa/projeto de doutorado — alinhado à integração com o MRCF e o PlaNAR UTM / artefato físico correspondente. Vou propor para cada slide: título, conteúdo chave (bullet-points) e sugestão visual. Você pode adaptar conforme o estilo da apresentação (PowerPoint, Keynote, Beamer etc).

---

### Slide 1 – Título / Gancho

**Título**: MIRF - Mission Intelligence & Reconfiguration Framework
**Conteúdo**:

* Sua assinatura (nome, instituição, doutorado)
* “Apresentação para … (ex: banca, patrocinador, conferência)”
* Frase de impacto: “Resiliência ativa para operações BVLOS no ecossistema UTM”
  **Visual**: Logo ou banner do projeto (com o “MIRF”), ou um drone em ambiente BVLOS, para atrair atenção.

---

### Slide 2 – Contexto e Problema

**Título**: Desafio nas operações BVLOS / UTM
**Conteúdo**:

* Crescente uso de UAS (drones) em missões além da linha de visada (BVLOS)
* Ecossistemas de tráfego de UAS (UTM) demandam robustez e adaptabilidade
* Falhas possíveis: hardware, sensores, comunicações, ambiente externo
* Problema: projetos tradicionais focam no planejamento ou no voo — e pouco em reconfiguração ativa frente a falhas
  **Visual**: Gráfico ou diagrama ilustrando falha de drone, ambiente UTM, múltiplos drones operando.

---

### Slide 3 – Visão Geral da Solução MIRF

**Título**: O que é o MIRF?
**Conteúdo**:

* Framework de controle avançado, plugin para o simulador PlaNAR UTM. ([GitHub][1])
* Objetivo: fortalecer a resiliência e inteligência de missões de UAS, especialmente BVLOS. ([GitHub][1])
* Abordagem híbrida: aprendizado profundo, redes de conhecimento especialistas, sistemas multiagentes. ([GitHub][1])
  **Visual**: Esquema da arquitetura conceitual (por ex. camadas Estratégica-Tática-Operacional) retirada do README ou adaptada.

---

### Slide 4 – Integração com o ecossistema (PlaNAR + MRCF)

**Título**: Como o MIRF se conecta ao PlaNAR UTM e ao MRCF
**Conteúdo**:

* O ecossistema:

  * PlaNAR UTM → núcleo do simulador para UTM. ([GitHub][1])
  * MRCF → Mission Replanning and Control Framework, módulo de replanejamento tático. ([GitHub][1])
  * MIRF → módulo de injeção e recuperação de falhas, reconfiguração de missão em face de eventos adversos. ([GitHub][1])
* Benefício: fluxo de missão completo desde planejamento, execução, falha e reconfiguração.
  **Visual**: Diagrama de blocos com PlaNAR → MRCF → MIRF, com setas mostrando função de cada.

---

### Slide 5 – Arquitetura Conceitual do MIRF

**Título**: Arquitetura Conceitual
**Conteúdo**:

* Camadas de decisão: Estratégica, Tática, Operacional. ([GitHub][1])
* Autonomia e reconfiguração dinâmica: realocação de recursos, formação de novas coalizões. ([GitHub][1])
* Feedback contínuo: monitoramento, análise de status, ajuste em tempo real. ([GitHub][1])
  **Visual**: O diagrama “flowchart TD” do README (ou adaptado para slide) mostrando as camadas e o loop de realimentação.

---

### Slide 6 – Inovações Técnicas e Diferenciais

**Título**: Inovações & Diferenciais Técnicos
**Conteúdo**:

* Controle híbrido: model-based + learning-based. ([GitHub][1])
* Aprendizado guiado por conhecimento (knowledge-guided ML) para incorporar regras de segurança. ([GitHub][1])
* Gêmeos digitais (digital twins) do ambiente e agentes para simulação what-if. ([GitHub][1])
* Sistemas multiagentes (MAS) e teoria de coalizões para robustez distribuída. ([GitHub][1])
* Verificação em tempo de execução (runtime verification) via escudos de segurança. ([GitHub][1])
  **Visual**: Ícones ou mini-gráficos para cada inovação técnica, talvez com um “radar” dos diferenciais.

---

### Slide 7 – Caso de Uso & Cenário de Aplicação

**Título**: Cenário de Aplicação – BVLOS & UTM
**Conteúdo**:

* Exemplo: operação de múltiplos drones em ambiente urbano/complexo com tráfego UTM, evento de falha de comunicação ou sensor.
* Como o MIRF intervém: simula a falha, detecta, reconfigura missão, redistribui tarefas.
* Benefício operacional: aumento da resiliência, menor tempo de inatividade, maior robustez.
  **Visual**: Ilustração de drone em ambiente urbano, falha marcada, e redistribuição de missão – talvez animação simplificada ou sequência de três frames.

---

### Slide 8 – Status, Progresso e Próximos Passos

**Título**: Progresso Atual & Roadmap
**Conteúdo**:

* Repositório disponível: README com descrição da proposta. ([GitHub][1])
* Estado atual: módulo de software em desenvolvimento (versão de tese); validação em ambiente simulado com PlaNAR UTM.
* Próximos passos: integração completa com MRCF, testes em cenário real ou HiL, publicação de resultados, prototipagem física (se aplicável).
* Cronograma ou roadmap (por exemplo: Q1 2025 simulação completa; Q2 integração; Q3 testes de campo; Q4 publicação/patente).
  **Visual**: Linha do tempo (timeline) com marcos chave.

---

### Slide 9 – Impacto, Mercado, Potencial de Aplicação

**Título**: Impacto & Potencial de Mercado
**Conteúdo**:

* Relevância acadêmica: contribui para controle autônomo de missões UAS, resiliência, multiagentes, UTM.
* Relevância industrial / operacional: uso em operadores de UAS, serviços UTM, defesa, logística, inspeção crítica.
* Potencial de comercialização/licenciamento da tecnologia de reconfiguração de missão.
* Alinhamento estratégico com regulamentação de tráfego de UAS (ex: no Brasil, projeto BR‑UTM). ([jtveigaita.github.io][2])
  **Visual**: Gráfico de mercado de drones, UTM ou infográfico de aplicação (defesa, logística, inspeção).

---

### Slide 10 – Conclusão & Chamada à Ação

**Título**: Conclusão & Próximos Passos para Colaboração
**Conteúdo**:

* Recapitulação breve: O que o MIRF faz, por que importa, como está conectado ao MRCF e ao PlaNAR.
* Convite para: colaboração institucional, financiamento de protótipo ou testes de campo, parcerias acadêmicas/industriais.
* Informação de contato: seu email, instituição, GitHub (link para o repositório).
* Slide de “Obrigado” com logotipos (ITA, etc).
  **Visual**: Imagem de drone ou simulação futurista + “Obrigado / Perguntas?” + QR-code para repositório, se possível.

---

[1]: https://github.com/JtveigaIta/mirf "GitHub - JtveigaIta/mirf: Repositório destinado ao SW gerado com a proposta de Tese do Doutorado do ITA"
[2]: https://jtveigaita.github.io/planar/ "PlaNAR - Planador Autônomo para Ressuprimento Logístico"

----------
INSERIR NO REPO CORRETO:
Pitch PLANAR, alinhado a PROPOSTA DE QUALIFICACAO, COMO??

-----------------------------------------------------------
CAPA: Projeto PlaNAR

Planador Autônomo para Ressuprimento Logístico

Duração: 6 meses

Outubro de 2025
----------------------------------------------
1. Abertura/ Titulo Impactante (30s):
* Nome do projeto (ex.: PLANAR - Planador para Navegação Autonoma)
* Uma frase forte: 
"Transformamos telemetria, missão e segurança em um único 
cérebro operacional para sistemas remotos de alto risco."

----------------------------------------------
----------------------------------------------
2. Resumo Executivo/ Visão Geral (1 min):
Explique em 4 pontos:
1. Problema central - caótico, caro, manual, risco elevado.
2. Solução - plataforma inteligente de gestão PLANAR + módulo UTM (nao é isso ainda)
4. Impacto esperado - redução de custos, mais segurança, automação.
5. Aplicações - foguetes, UAS, cargas autonomas, ensaios estruturais, laboratorios, redes plug-and-play.

Dica: aqui você cria o gancho emocional que prende a banca.

----------------------------------------------
----------------------------------------------
3. Oportunidade Tecnológica e TRL Pretendido (1 min):

* Mostre em que TRL o projeto está hoje (ex,: TRL 3-4)
* Mostre onde quer chegar ao final da pesquisa (ex.: TRL 6 demonstrado em ambiente relevante)
* Explique o salto tecnológico que o recurso de fomento torna possível.

Objetivo: transmitir que você entende a trajetória completa da tecnologia
----------------------------------------------
----------------------------------------------
4. Revisão Científica / Estado da Arte (1min):

Em Pitch, essa parte deve ser simples, mas sólida:
 * O que já existe no mundo (UTM internacional, ESA, sistemas distribuídos, Digital Twins)
 * Onde os modelos atuais falham:
	* pouca modularidade
        * operação difícil
 	* não são plug-and-play
	* pouca interoperabilidade
	* frameworks não integrados
* Onde o PLANAR avança:
	* visão holística
	* arquitetura orientada a componentes
	* digital assets para reconfiguração
	* automação dos testes / telemetria
	* convergência ar-terra-epaço

Objetivo: deixar claro que você está acima do estado da arte 
----------------------------------------------
----------------------------------------------
5. Diferencia, Concorrência PI (1min):

Explique:
	* Quem são os concorrentes diretos/ indiretos.
	* Qual diferencial disruptivo do PLANAR:
	  * orquestração de alto nível
	  * reconfiguração de ativos
	  * UTM aplicável a naves leves / cargas
	  * integração com sistemas de Test Bench e telemetria
	* Se existe liberdade para operar (FTO)
	* Estratégia de PI:
	  * registro de software
	  * métodos, fluxos, processos
          * blockchain para certificações (POA, etc.)
----------------------------------------------
----------------------------------------------
6. Plano de Pesquisa (2min):
Aqui você conquista a banca com clareza de execução.

Monte em três etapas:

Fase 1 - Arquitetura e MVP (TRL 3 -> 4)
   * Modelagem PFS
   * Camadas do PLANAR
   * Protótipo do orquestrador
   * Simulação UTM / Digital Assets

Fase 2 - Demonstrações (TRL 4 -> 5)
   * Testes em ambiente semi-controlado
   * Integração com telemetria real (foguetes, LASC, drones, etc)

Fase 3 - Validação em Ambiente Relevante (TRL 5 -> 6)
   * Missões reais
   * Ensaios de testes automatizados
   * Reconfiguração de ativos
   * Relatórios, métricas, maturação para produto
----------------------------------------------
----------------------------------------------
7. Potencial Comercial e Inovação (1min):

Aqui a banca quer saber: Isso vira produto? Dá retorno?

Fale sobre:
	* Mercado-alvo:
		* aeroespacial
		* defesa
		* UAS (logística, agro, inspeções)
		* educação e laboratórios
		* telemetria e ensaios
	* Modelos de negócio:
		* SaaS
 		* licenças institucionais
		* kits de simulação
		* consultoria e integração
	* Parceiros potenciais:
		* universidades, parques tecnológicos, laboratórios espaciais
	* Projeção de receita (não presa número exato, apenas "comportamento").
----------------------------------------------
----------------------------------------------
8. Orçamento Justificado (45s):
Mostre:
	* Em que o dinheiro será gasto:
		* equipe
		* infraestrutura de testes
		* equipamentos
		* desenvolvimento
	* Justifique cada bloco.
	* Mostre maturidade e transparência (não precisa valor em Pitch)
----------------------------------------------
----------------------------------------------
9. Nossas Realizações e Contribuições:
Conte:
	* Quem você é
	* Experiências prévias (telemetria, artigos, laboratórios, projetos)
	* Competências da equipe
	* Parceiros e co-operação
	* Capacidade de execução

Objetivo: transmitir confiança
----------------------------------------------
----------------------------------------------
10. Outras Propostas Relacionadas (30s)
Mostre: 
	* Como este projeto não é duplicado
	* Como se conecta com outros projetos ou ideias do ecossistema
	* Como traz sinergia e não sobreposição
----------------------------------------------
----------------------------------------------
10. Fechamento e Chamada para Ação (30s)
Finalize com:
	* Impacto direto do investimento
	* O futuro possível com a tecnologia
	* Convite para a banca apoiar o desenvolvimento

Ex.: "Com o apoio desta instituição, o PLANAR se torna o primeiro 
orquestrador brasileiro de sistemas distribuídos aeroespaciais. Um salto tecnológico que posiciona o Brasil no cenário Space 4.0"
----------------------------------------------
----------------------------------------------
O Projeto PlaNAR vai além do hardware. Nossas construções atuais estabelecem uma base de conhecimento e tecnologia fundamental para o futuro do tráfego aéreo não tripulado no Brasil.

01
Mini Curso sobre UTM e UAS
Formação essencial sobre Gerenciamento de Tráfego Aéreo Não Tripulado (UTM) e Sistemas de Aeronaves Não Tripuladas (UAS). Capacitação de profissionais e alinhamento com a regulamentação BR-UTM.

02
Artigo Científico (MRCF)
Publicação técnica sobre o Sistema de Simulação de Drones com Multi-Agent System (MAS) e Behavior Trees (BT). Validação acadêmica e avanço na coordenação autônoma de múltiplos drones.

03
Propriedade Intelectual (MRCF)
Registro de tecnologia (ex: algoritmos de navegação e controle) desenvolvida para o PlaNAR. Proteção e comercialização da tecnologia nacional.

04
Validação PIPE-1
Conclusão da fase de Validação Funcional por Simulação Integrada (HiL + SiL) do design do planador. Redução de riscos e otimização do design antes da prototipagem física (PIPE-2).
----------------------------------------------
----------------------------------------------
10. Próximos Passos:

* Ser reconhecido como especialista em Capacitações em UTM e UAS;
* Fornecer meios para  integrar sua tecnologia ao ecossistema BR-UTM? Agende uma consulta com nossa equipe.
* Submissão da proposta para financiamento PIPE-2 para prototipagem e testes de voo em ambiente controlado.
----------------------------------------------
----------------------------------------------
11. Parceiros:

* ITA: Instituto Tecnológico de Aeronáutica - Base de excelência acadêmica e tecnológica em engenharia aeroespacial;
* BR-UTM / DECEA: Alinhamento com o Projeto BR-UTM e o Departamento de Controle do Espaço Aéreo. Implementação a partir de 2026.
* Aviação do Amanhã: Entidade que promove o debate e o avanço da aviação de nova geração no Brasil.
* DECEA: Órgão regulador que define o futuro operacional de sistemas como o PlaNAR.
----------------------------------------------
12. Realizações:

( ) Artigo MRCF
( ) Mini Curso
( ) Participação Ensaio II DCEA
( ) Projeto Aviação do Amanha
( ) Participação do III Encontro
----------------------------------------------
13. Entre em Contato:

Tem dúvidas ou interesse em colaborar? Fale conosco!
📍 Localização
Incubaero - Fundação Casimiro Montenegro Filho
DCTA, São José dos Campos - SP
📧 Email
contato@planar.org
📱 Telefone
+55 (11) 99999-9999
🌐 Redes Sociais
LinkedIn | Twitter | GitHub

==================================================================

PESQUISAS 12.11.2025 (Objetivo, produzir uma linha de AÇÃO e DoE Mínimo Conceitual)
---
A ultima etapa da pesquisa, dando algums passos atraz foi buscar colocar minha abordagem no contexto global:

Com certeza. Preparar uma revisão da literatura que conecte esses trabalhos e normas é fundamental para posicionar o MIRF academicamente e demonstrar sua relevância.

A seguir, apresento uma revisão discursiva e simplificada, como solicitado, que tece uma narrativa coesa sobre o tratamento e a propagação de falhas no contexto UTM, utilizando os documentos e frameworks que você mencionou como pilares.

---

### Revisão da Literatura: Resiliência e Tratamento de Falhas em Ecossistemas UTM

A garantia de operações seguras e eficientes com Veículos Aéreos Não Tripulados (UAS), especialmente em cenários Além da Linha de Visada Visual (BVLOS), depende fundamentalmente da capacidade do sistema de gerenciar falhas. A literatura recente tem se afastado da simples tolerância a falhas em nível de componente para uma abordagem mais holística de **resiliência operacional**. Esta revisão conecta conceitos-chave de documentos da NASA, SESAR e trabalhos acadêmicos para construir o alicerce teórico que justifica uma arquitetura como o MIRF.

#### 1. O Fluxo de Decisão e a Necessidade de um "Cérebro" Cognitivo: NASA UTM CONOPS

O **Conceito de Operações (CONOPS) do UTM da NASA (2018)** estabelece a base para um ecossistema de gerenciamento de tráfego distribuído. Ele define os papéis e as responsabilidades entre os diversos atores: operadores de UAS, Provedores de Serviço UTM (USS) e a autoridade de tráfego aéreo (ATM). O ponto crucial do CONOPS é que a segurança não é garantida por um controle centralizado, mas por uma **troca de informações e uma negociação de intenções de voo**.

No contexto de falhas, o CONOPS prevê que os operadores são responsáveis por gerenciar suas próprias contingências. No entanto, ele deixa uma lacuna clara: *como* um operador, especialmente um que gerencia uma frota de drones autônomos, deve tomar decisões ótimas em tempo real quando uma falha ocorre? Uma falha não afeta apenas o drone, mas também o plano de voo compartilhado com o USS e, por consequência, todo o ecossistema. É aqui que o MIRF se encaixa: ele atua como o **módulo cognitivo** que preenche essa lacuna, permitindo que um operador cumpra suas responsabilidades de forma inteligente e automatizada, analisando a propagação da falha no nível tático (a missão imediata) e pré-tático (o impacto futuro na operação e no espaço aéreo).

#### 2. O Ciclo de Resiliência e a Propagação de Falhas: ADACORSA e SESAR

Enquanto a NASA define "quem faz o quê", os projetos europeus focam em "como fazer de forma segura". O **Modelo Conceitual do ADACORSA** inspira a compreensão da **propagação de falhas**. Uma falha em um sensor, por exemplo, não é um evento isolado; ela se propaga, degradando a capacidade de navegação, que por sua vez pode invalidar um plano de voo e gerar um conflito. O MIRF pega essa ideia e a eleva do nível do veículo para o nível da missão multiagente. Uma falha em um drone de uma coalizão se propaga, degradando a capacidade da *coalizão* de cumprir um objetivo estratégico (como a cobertura de uma área).

Essa visão é fortemente corroborada pelo **Framework de Resiliência do U-space (SESAR, 2023-2024)**. Este trabalho introduz formalmente o conceito de **“operational resilience loop” (ciclo de resiliência operacional)**, um processo contínuo de **Detectar, Reagir, Adaptar e Aprender**. Este ciclo é praticamente um sinônimo da arquitetura do MIRF:
*   **Detectar:** O MIRF monitora a telemetria e os dados do ecossistema para identificar anomalias.
*   **Reagir:** O MIRF executa ações imediatas para garantir a segurança (o *Safety Shield*).
*   **Adaptar:** Esta é a fase estratégica, onde o MIRF replaneja a missão, reconfigura coalizões e negocia novos planos com o USS, mantendo a operação viável mesmo em modo degradado.
*   **Aprender:** Os dados coletados durante o ciclo alimentam os modelos de aprendizado para melhorar futuras respostas.

O MIRF, portanto, não é apenas um sistema de tratamento de falhas, mas uma implementação prática do ciclo de resiliência operacional proposto pelo SESAR para o U-space.

#### 3. O Ambiente de Teste e Validação: Gêmeos Digitais e Co-Simulação

Validar um sistema complexo como o MIRF em voos reais é caro e arriscado. A literatura recente converge na solução: **co-simulação e Gêmeos Digitais**.

O **Framework de Gêmeo Digital de Cranfield (2023)** demonstra como conectar diferentes simuladores (um para a física do drone, outro para o tráfego aéreo) com dados do mundo real para criar um ambiente de teste de alta fidelidade. Esta abordagem permite testar cenários de falha complexos que seriam impossíveis de replicar fisicamente. Por exemplo, é possível simular como a degradação do sinal GNSS (dado real) afeta um modelo de voo (simulador de física) dentro de um corredor de tráfego aéreo movimentado (simulador ATM). O testbed que você planeja construir para o PlaNAR UTM segue exatamente essa filosofia, integrando modelos de falha, modelos de voo e a lógica de decisão do MIRF em um único ambiente.

Para a camada de aprendizado de máquina, o **BlueSky e o BlueSky-Gym (SESAR, 2024)** oferecem a peça final. Eles fornecem um ambiente de simulação de tráfego aéreo de código aberto, projetado especificamente para treinar e testar algoritmos de decisão baseados em Aprendizado por Reforço (RL). A existência de um framework como o BlueSky-Gym valida a abordagem de usar RL para otimizar decisões táticas em UTM. O MIRF pode ser treinado e validado neste tipo de ambiente, onde suas políticas de replanejamento podem ser comparadas com outras abordagens de forma padronizada e reprodutível.

### Conclusão da Revisão

A literatura forma uma narrativa clara e convergente. A **NASA** estabelece a necessidade de tomada de decisão distribuída. O **ADACORSA** e o **SESAR** definem o que essa decisão deve fazer: seguir um ciclo de resiliência para gerenciar a propagação de falhas em nível de missão. Finalmente, **Cranfield** e os criadores do **BlueSky** mostram *como* validar essa capacidade: através de Gêmeos Digitais em ambientes de co-simulação.

O **MIRF** se posiciona de forma única na interseção de todos esses conceitos. Ele não reinventa uma peça isolada, mas sim **integra** essas ideias em uma arquitetura coesa que serve como o cérebro cognitivo para um operador de frota autônoma, implementando o ciclo de resiliência em um ambiente de simulação de alta fidelidade, exatamente como preconizado pelo estado da arte.

-------------------------------------------------------------------------------------------------------------------
Agora que tenho o DoE, estou obserrvando que talvez está um pouco fora do que pensei, a abordagem no que diz respeito " falhas de alto nível e pre/tático em ambientes multi-UAS, recomendo um *co-simulation* stack que permita testar comportamento tático, interdependências e integração ATM" está correto, tambem sobre a arquitetura gerada, quanto as considerações dos módulos principais:

A Arquitetura GERAL DO SISTEMA
------------
TERMOS ACâDEMICOS ÚTEIS para PESQUISA:
---
1) modelo ODAA (Observe–Decide–Act–Adapt) ou o loop OODA.

2) Excelente — seu direcionamento está perfeito: o **MIRF** como estrutura cognitiva de **resiliência e replanejamento em missões BVLOS**, equivalente conceitualmente a modelos como o **OODA loop** e **ODDA (Observe–Detect–Decide–Act)**, mas aplicado ao contexto **UTM / U-space**.

Com base nas referências que você trouxe — **ADACORSA [1]**, **NASA UTM CONOPS [2]**, **BlueSky e BlueSky-Gym [3,5]**, **Cranfield Digital Twin [4]**, **SESAR [7]**, e **hierarchical mission replanning [6]** —, seguem **termos de pesquisa e estruturas teóricas correlatas** que você pode usar para fundamentar o MIRF como **metodologia global de resposta a falhas**:

---

## 🔹 1. Termos conceituais equivalentes ao ODDA/OODA aplicáveis ao MIRF

| Categoria           | Termo de pesquisa                         | Descrição / Aplicação em UTM e MIRF                                                                                                                                                             |
| ------------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ciclo cognitivo** | **OODA Loop (Observe–Orient–Decide–Act)** | Modelo clássico de tomada de decisão em sistemas dinâmicos — base conceitual para agentes autônomos e replanejamento tático em tempo real (usado pela NASA e SESAR para autonomia distribuída). |
|                     | **ODDA (Observe–Detect–Decide–Act)**      | Versão mais orientada à **detecção de falhas e reconfiguração**; aplicável ao MIRF como fluxo de resposta a eventos anômalos.                                                                   |
|                     | **Sense–Detect–Respond–Recover (SDRR)**   | Usado em **segurança cibernética e sistemas resilientes** (ver aplicações em U-space resiliente). Se alinha ao ciclo do MIRF: perceber → diagnosticar → agir → medir impacto.                   |
|                     | **Monitor–Analyze–Plan–Execute (MAPE-K)** | Modelo de controle de sistemas autônomos da engenharia de software e IA — base para arquiteturas de **autonomic computing** e **digital twins** (referência direta com [4]).                    |
|                     | **Perceive–Comprehend–Project (Endsley)** | Modelo de **situational awareness**, usado pela NASA e SESAR no contexto de UTM para avaliar estados críticos do espaço aéreo e projetar consequências.                                         |
|                     | **Detect–Diagnose–Recover (DDR)**         | Estrutura formal de sistemas **fault-tolerant**, aplicável a falhas de alto nível (missões, rotas, zonas).                                                                                      |

---

## 🔹 2. Termos de pesquisa técnicos relacionados a falhas, autonomia e UTM

| Tema                               | Termos recomendados                                                                                                                               | Relevância                                                                                             |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Gestão de falhas e resiliência** | “Resilient U-space”, “Fault management architecture for UTM”, “Autonomous contingency management”                                                 | Estudos da **SESAR** e **ADACORSA** sobre segurança operacional distribuída.                           |
| **Planejamento e replanejamento**  | “Hierarchical mission replanning for multiple UAVs” [6], “Adaptive trajectory management”, “Multi-agent reconfiguration strategies”               | Correlato direto ao **núcleo decisório do MIRF** (fase 3 do seu grafo).                                |
| **Monitoramento e diagnóstico**    | “Anomaly detection in UTM”, “Digital twin for UAS fault testing” [4], “Telemetry-based diagnostics”, “MAS observability”                          | Mostra como sistemas de simulação (como **BlueSky**) podem gerar observações e diagnósticos dinâmicos. |
| **Tomada de decisão autônoma**     | “Autonomous decision-making loop”, “Reinforcement learning for airspace management” [5], “Policy-based control”, “Self-organizing U-space agents” | Aplica-se à etapa “Decisão → Ação” do MIRF.                                                            |
| **Simulação e teste**              | “Co-simulation Digital Twin framework”, “Agent-based airspace simulation”, “Hybrid UTM testbed”, “BlueSky U-space integration”                    | Fundamentos técnicos para o **giga de teste e simulação** que você pretende estruturar.                |
| **Métricas de impacto e KPIs**     | “Mission success rate (TSM)”, “Time to react (TTR)”, “Airspace load impact”, “Resilience metrics for U-space”                                     | Usadas para medir a eficácia da resposta MIRF (fase 5 do seu grafo).                                   |

---

## 🔹 3. Estruturas metodológicas compatíveis com o MIRF

1. **ADACORSA Conceptual Model of Fault Propagation and Recovery**
   → Inspira o MIRF no nível conceitual, mas o seu é aplicado ao **nível tático e pré-tático BVLOS** (cenários multi-drone, integração UTM).

2. **NASA UTM CONOPS (2018)**
   → Define papéis e fluxos de decisão entre **UTM, operadores e veículos** — excelente base para formalizar o MIRF como **módulo cognitivo dentro de um sistema UTM distribuído**.

3. **BlueSky + BlueSky-Gym (SESAR, 2024)**
   → Framework aberto para testar **algoritmos de decisão baseados em aprendizado**. Pode servir para implementar o MIRF em ambiente de co-simulação.

4. **Cranfield Digital Twin Framework (2023)**
   → Mostra como conectar **modelos de simulação + dados reais de sistemas ATM/UTM** para testar comportamentos de falha e recuperação.
   Isso corresponde ao **testbed que você planeja construir**.

5. **U-space Resilience Framework (SESAR 2023–2024)**
   → Apresenta o conceito de **“operational resilience loop”** — altamente alinhado ao propósito do MIRF: detectar, reagir, adaptar e manter a operação.

---

## 🔹 4. Sugestão de termos combinados para pesquisa avançada

Você pode usar expressões como:

* “UTM resilience loop”
* “Autonomous contingency management for U-space”
* “Fault-tolerant decision-making for multi-UAS missions”
* “Resilient digital twin for BVLOS simulation”
* “MAPE-K based UTM autonomy architecture”
* “Operational fault cycle in U-space environments”
* “OODA-inspired planning for distributed UAS missions”
* “MAS coordination under UTM contingencies”
* “Anomaly detection and route reconfiguration in U-space”

---
o MIRF como estrutura cognitiva de resiliência e replanejamento em missões BVLOS, equivalente conceitualmente a modelos como o OODA loop e ODDA (Observe–Detect–Decide–Act), mas aplicado ao contexto UTM / U-space.
--
| Categoria           | Termo de pesquisa                         | Descrição / Aplicação em UTM e MIRF                                                                                                                                                             |
| ------------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ciclo cognitivo** | **OODA Loop (Observe–Orient–Decide–Act)** | Modelo clássico de tomada de decisão em sistemas dinâmicos — base conceitual para agentes autônomos e replanejamento tático em tempo real (usado pela NASA e SESAR para autonomia distribuída). |
|                     | **ODDA (Observe–Detect–Decide–Act)**      | Versão mais orientada à **detecção de falhas e reconfiguração**; aplicável ao MIRF como fluxo de resposta a eventos anômalos.                                                                   |
|                     | **Sense–Detect–Respond–Recover (SDRR)**   | Usado em **segurança cibernética e sistemas resilientes** (ver aplicações em U-space resiliente). Se alinha ao ciclo do MIRF: perceber → diagnosticar → agir → medir impacto.                   |
|                     | **Monitor–Analyze–Plan–Execute (MAPE-K)** | Modelo de controle de sistemas autônomos da engenharia de software e IA — base para arquiteturas de **autonomic computing** e **digital twins** (referência direta com [4]).                    |
|                     | **Perceive–Comprehend–Project (Endsley)** | Modelo de **situational awareness**, usado pela NASA e SESAR no contexto de UTM para avaliar estados críticos do espaço aéreo e projetar consequências.                                         |
|                     | **Detect–Diagnose–Recover (DDR)**         | Estrutura formal de sistemas **fault-tolerant**, aplicável a falhas de alto nível (missões, rotas, zonas).                                                                                      |

| Tema                               | Termos recomendados                                                                                                                               | Relevância                                                                                             |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Gestão de falhas e resiliência** | “Resilient U-space”, “Fault management architecture for UTM”, “Autonomous contingency management”                                                 | Estudos da **SESAR** e **ADACORSA** sobre segurança operacional distribuída.                           |
| **Planejamento e replanejamento**  | “Hierarchical mission replanning for multiple UAVs” [6], “Adaptive trajectory management”, “Multi-agent reconfiguration strategies”               | Correlato direto ao **núcleo decisório do MIRF** (fase 3 do seu grafo).                                |
| **Monitoramento e diagnóstico**    | “Anomaly detection in UTM”, “Digital twin for UAS fault testing” [4], “Telemetry-based diagnostics”, “MAS observability”                          | Mostra como sistemas de simulação (como **BlueSky**) podem gerar observações e diagnósticos dinâmicos. |
| **Tomada de decisão autônoma**     | “Autonomous decision-making loop”, “Reinforcement learning for airspace management” [5], “Policy-based control”, “Self-organizing U-space agents” | Aplica-se à etapa “Decisão → Ação” do MIRF.                                                            |
| **Simulação e teste**              | “Co-simulation Digital Twin framework”, “Agent-based airspace simulation”, “Hybrid UTM testbed”, “BlueSky U-space integration”                    | Fundamentos técnicos para o **giga de teste e simulação** que você pretende estruturar.                |
| **Métricas de impacto e KPIs**     | “Mission success rate (TSM)”, “Time to react (TTR)”, “Airspace load impact”, “Resilience metrics for U-space”                                     | Usadas para medir a eficácia da resposta MIRF (fase 5 do seu grafo).                                   |



--
modelo FFPN oferece uma base formal para especificar, simular e validar o comportamento do MIRF: Neste caso nao aceitei bem, acredito que Resumir Tudo a eventos discretos, para representacao Conceitual, replicacao e simulação das Redes de Conhecimento: Pois agora estamos numa abordagem orientado a dados, e o contexto será complexo, o que quero dizer, se analizarmos o arquivo DoE e o código fornecido, se limita e eventos do tipo Broker por meio da camada de comunicação - A questão que fica, serão estes TIPOS de FALHA que desejo tratar?
------------
de forma técnica, o **processo completo de detecção e resposta a uma falha de alto nível** no contexto de missões BVLOS dentro do MIRF.
Abaixo está uma **descrição em linguagem humana, explicativa e simples**, mostrando passo a passo o **comportamento e funcionamento do módulo de falha**.

---

## 🧩 Explicação simples do processo do Módulo de Falha (MIRF)

O módulo de falhas do MIRF atua como um “sistema nervoso” do simulador: ele observa o ambiente, identifica quando algo anormal acontece e decide a melhor forma de reagir.
O processo ocorre em **cinco etapas principais**:

---

### **1. Estímulo – Injeção de Falha**

Tudo começa com um **evento externo** que provoca uma situação inesperada.
Exemplo: o sistema ATM (Gerenciamento de Tráfego Aéreo) **ativa uma Zona de Exclusão Aérea**, onde nenhum drone pode entrar.

➡️ Isso é o **estímulo inicial** — algo que muda as condições do espaço aéreo e exige uma resposta.

---

### **2. Propagação e Observação**

O sistema percebe que, com essa mudança, o **plano de voo atual do drone se tornou inválido**.
Em outras palavras, o drone agora está prestes a voar para dentro de uma área proibida.

O MIRF transforma isso em uma **observação**:

> “O plano de voo atual viola uma geofence ativa.”

➡️ Aqui o módulo apenas observa e registra o problema, sem ainda decidir nada. É a **fase de percepção da falha**.

---

### **3. Análise e Decisão (Núcleo do MIRF)**

O MIRF analisa o que observou e tenta **entender a causa e a gravidade**.
Ele diagnostica:

> “Há um conflito espacial crítico entre a rota planejada e uma zona restrita.”

Com base nesse diagnóstico, o sistema toma uma **decisão inteligente**:

> “É necessário replanejar a rota para contornar a zona de exclusão.”

➡️ Essa é a **fase cognitiva** do processo — o cérebro do MIRF entra em ação, raciocinando sobre o que fazer.

---

### **4. Ação e Execução**

Depois de decidir o que fazer, o sistema **executa a ação** correspondente.
O MIRF **gera um novo plano de voo** e envia essa atualização para o agente (drone).

O resultado é que o **drone passa a seguir a nova rota**, agora ajustada e segura.

➡️ Essa é a fase **de reação e controle ativo** — o MIRF aplica a solução no sistema em tempo real.

---

### **5. Medição de Impacto (KPIs)**

Por fim, o MIRF **mede o impacto da sua decisão** usando indicadores de desempenho (KPIs):

* **Latência de Decisão (TTR):** quanto tempo o sistema levou para perceber e reagir à falha.
* **Impacto no Espaço Aéreo:** quanto espaço adicional foi usado para o desvio.
* **Sucesso da Missão (TSM):** o drone conseguiu completar sua missão, mesmo com o imprevisto?

➡️ Essa etapa fecha o ciclo de aprendizado — o MIRF **avalia o quanto sua resposta foi eficiente**, permitindo melhorar continuamente.

---

## 🧠 Em resumo

| Etapa                 | O que acontece                                 | Resultado                       |
| --------------------- | ---------------------------------------------- | ------------------------------- |
| 1️⃣ Estímulo          | Um evento externo muda as condições de voo     | Uma falha é injetada            |
| 2️⃣ Observação        | O sistema percebe um estado inválido           | Falha é reconhecida             |
| 3️⃣ Análise e decisão | O MIRF entende o problema e decide o que fazer | Estratégia definida             |
| 4️⃣ Execução          | O sistema envia o novo plano de voo            | Drone reconfigura a rota        |
| 5️⃣ Medição           | O MIRF avalia o resultado da ação              | Aprendizado e melhoria contínua |

---

Posso complementar este texto com uma **versão acadêmica**, mostrando como esse processo se encaixa no **ciclo de resiliência do MIRF** (detecção, decisão, ação, aprendizado) — citando também referências como o modelo **ODAA (Observe–Decide–Act–Adapt)** ou o **loop OODA**.
Quer que eu faça isso?

-------------
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
