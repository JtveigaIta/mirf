# Roteiro de Desenvolvimento do MIRF (ROADMAP)

Este documento descreve o roteiro de desenvolvimento para o **Mission Intelligence & Reconfiguration Framework (MIRF)**. Ele detalha as metas de curto, médio e longo prazo, alinhadas com os objetivos de pesquisa do projeto.

O roteiro é um documento vivo e pode ser ajustado com base nas descobertas da pesquisa e nas contribuições da comunidade.

---

### Fase 1: Fundação e Prototipagem (Concluído/Em Andamento)

**Objetivo:** Estabelecer a arquitetura conceitual e desenvolver um protótipo funcional integrado ao simulador PlaNAR UTM.

-   [x] **Formalização da Arquitetura Conceitual:**
    -   Definição das camadas estratégica, tática e operacional.
    -   Modelagem baseada em grafos conceituais.
    -   Criação do `README.md` e documentação inicial.

-   [x] **Integração com o Simulador PlaNAR UTM:**
    -   Desenvolvimento do MIRF como um plugin/extensão.
    -   Estabelecimento da comunicação entre o MIRF e o núcleo do simulador.

-   [ ] **Módulo de Injeção de Falhas (v1.0):**
    -   Implementação de injeção de falhas determinísticas (ex: perda de comunicação, falha de bateria em tempo pré-definido).
    -   Criação de uma API para acionar falhas durante a simulação.

-   [ ] **Mecanismo de Reconfiguração Tática (Baseado em Regras):**
    -   Implementação de um planejador de coalizão simples (baseado em MAS/Contract Net) para redistribuição de tarefas após uma falha.
    -   Uso de Behavior Trees (BTs) para a execução de planos reativos.

---

### Fase 2: Inteligência e Aprendizado

**Objetivo:** Integrar módulos de aprendizado de máquina para tornar a tomada de decisão mais robusta e adaptativa.

-   [ ] **Controle Híbrido (Residual RL):**
    -   Integrar uma política de RL que atue como um corretor para um controlador clássico (PID/MPC), melhorando a performance em cenários não modelados.

-   [ ] **Gêmeos Digitais (Digital Twins) dos Provedores (USS):**
    -   Modelar as políticas, restrições e capacidades dos provedores de serviço como gêmeos digitais.
    -   Utilizar os gêmeos no planejador de coalizão para simulações *what-if* antes de tomar decisões.

-   [ ] **Aprendizado Guiado por Conhecimento (Knowledge-Guided RL):**
    -   Incorporar restrições de segurança e regras de voo (conhecimento especialista) na função de recompensa do RL para acelerar o treinamento e garantir comportamentos seguros.

-   [ ] **Módulo de Injeção de Falhas (v2.0):**
    -   Adicionar falhas não-determinísticas e ambientais (ex: degradação de sensor, zonas de interferência de comunicação).

---

### Fase 3: Validação, Generalização e Segurança

**Objetivo:** Validar a arquitetura em cenários complexos, garantir a segurança e trabalhar na generalização dos modelos.

-   [ ] **Validação Experimental e Métricas:**
    -   Executar baterias de testes de estresse com injeção massiva de falhas.
    -   Coletar e analisar métricas de resiliência, como *Mean Time To Reconfigure (MTTR)* e percentual de sucesso da missão.
    -   Comparar o desempenho do MIRF com a abordagem baseline (MRCF sem reconfiguração estratégica).

-   [ ] **Verificação em Tempo de Execução (Runtime Verification):**
    -   Implementar *Safety Shields* que monitorem a execução e previnam a violação de invariantes de segurança (ex: separação mínima, geofences).

-   [ ] **Generalização com Meta-Learning (MAML/PEARL):**
    -   Pesquisar o uso de Meta-RL para permitir que as políticas de controle se adaptem rapidamente a tipos de falhas ou missões nunca vistos antes.

-   [ ] **Publicação e Sim-to-Real:**
    -   Publicar os resultados da metodologia e dos experimentos em conferências e periódicos de relevância (AIAA, JATM, etc.).
    -   Planejar os primeiros passos para a transferência *sim-to-real*, calibrando os modelos com dados de voos reais em um ambiente controlado.

---
Espero que estes documentos ajudem a estruturar e impulsionar seu projeto.

Podemos prosseguir com mais alguma etapa? Por exemplo, criar o arquivo `CODE_OF_CONDUCT.md` ou detalhar um dos itens do roteiro em uma especificação técnica.
