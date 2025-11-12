# Guia de Contribuição para o MIRF

Primeiramente, agradecemos seu interesse em contribuir para o **Mission Intelligence & Reconfiguration Framework (MIRF)**! Este projeto é um esforço colaborativo de pesquisa e toda contribuição, seja em código, documentação ou ideias, é muito bem-vinda.

Para garantir um ambiente colaborativo, transparente e eficiente, pedimos que siga as diretrizes abaixo.

## Código de Conduta

Este projeto e todos que participam dele são regidos pelo nosso [Código de Conduta](CODE_OF_CONDUCT.md). Ao participar, você concorda em seguir seus termos. Por favor, leia-o para entender o que esperamos de todos os membros da comunidade.

## Como Posso Contribuir?

Existem várias maneiras de contribuir para o MIRF:

### **Reportando Bugs**
Se você encontrar um bug no código-fonte ou um erro na documentação, pode nos ajudar submetendo uma **Issue** no repositório do GitHub.

Ao reportar um bug, por favor, inclua:
-   Uma descrição clara e concisa do problema.
-   Passos para reproduzir o comportamento.
-   O comportamento esperado.
-   O comportamento observado.
-   Capturas de tela, se aplicável.
-   Informações do seu ambiente (versão do simulador PlaNAR UTM, sistema operacional, etc.).

### **Sugerindo Melhorias (Features)**
Se você tem uma ideia para uma nova funcionalidade ou uma melhoria em uma já existente, abra uma **Issue** com a tag `enhancement`.

Ao sugerir uma melhoria, descreva:
-   O problema que sua sugestão resolve.
-   Uma descrição detalhada da sua solução proposta.
-   Alternativas que você considerou.
-   A relevância da melhoria para os objetivos do projeto (resiliência, autonomia, etc.).

### **Contribuindo com Código ou Documentação**
Para contribuir diretamente com o projeto, siga o fluxo de trabalho abaixo.

1.  **Faça um Fork do Repositório:**
    Clique no botão "Fork" no canto superior direito da página para criar uma cópia do repositório na sua conta do GitHub.

2.  **Clone o seu Fork:**
    ```bash
    git clone https://github.com/SEU-USUARIO/MIRF.git
    cd MIRF
    ```

3.  **Crie uma Branch:**
    Crie uma branch descritiva para sua contribuição. Use um prefixo como `feature/` para novas funcionalidades ou `fix/` para correções de bugs.
    ```bash
    # Para uma nova feature
    git checkout -b feature/hierarchical-rl-module

    # Para uma correção de bug
    git checkout -b fix/memory-leak-in-simulation
    ```

4.  **Faça suas Alterações:**
    Implemente seu código, faça as correções ou melhore a documentação. Siga as convenções de estilo de código do projeto. Se estiver adicionando uma nova funcionalidade, inclua também os testes correspondentes.

5.  **Faça o Commit das suas Alterações:**
    Escreva uma mensagem de commit clara e descritiva.
    ```bash
    git add .
    git commit -m "feat: Adiciona módulo inicial para RL Hierárquico"
    ```
    *(Usamos o padrão [Conventional Commits](https://www.conventionalcommits.org/ ) para mensagens de commit).*

6.  **Envie suas Alterações para o seu Fork:**
    ```bash
    git push origin feature/hierarchical-rl-module
    ```

7.  **Abra um Pull Request (PR):**
    Vá para o repositório original e abra um Pull Request da sua branch para a branch `main` do projeto. No PR, forneça uma descrição detalhada das suas alterações, conectando-o à Issue correspondente, se houver.

Aguarde a revisão do seu PR. Os mantenedores do projeto irão analisar suas alterações e podem solicitar ajustes.

## Questões e Contato

Se tiver dúvidas, pode abrir uma Issue ou entrar em contato diretamente com o mantenedor do projeto:

-   **Jackson T. Veiga**
-   📧 `jackson.veiga.101422@ga.ita.br`

Obrigado por sua contribuição!
