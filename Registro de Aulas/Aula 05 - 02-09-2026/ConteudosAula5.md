Aula — GitHub Actions e Pipelines Automatizadas

Disciplina: DevOps — FATEC
Tema: GitHub Actions e automação de pipelines
Atividade: Utilização de Actions do GitHub Marketplace

📚 Resumo da Aula

Nesta aula, aprendi mais sobre o GitHub Actions e como ele pode ser utilizado para automatizar diversas etapas do desenvolvimento de um projeto.

Inicialmente, o professor explicou o funcionamento do GitHub Actions e apresentou suas principais ferramentas e possibilidades. Entendi que ele permite criar workflows automatizados, que são executados a partir de determinados eventos dentro do repositório, como um push, pull request ou até mesmo de forma manual.

O ponto que mais chamou minha atenção foi perceber que não precisamos utilizar o GitHub Actions apenas para uma tarefa específica. Podemos criar pipelines completas, com várias etapas acontecendo de maneira organizada e automática.

⚙️ O que entendi sobre GitHub Actions

O GitHub Actions permite automatizar processos que normalmente precisaríamos executar manualmente.

Um workflow pode ser dividido em diferentes etapas, chamadas de jobs e steps, permitindo que cada parte da pipeline tenha uma responsabilidade específica.

Por exemplo, posso criar uma pipeline que:

Baixa o código do repositório;
Configura o ambiente necessário;
Instala as dependências;
Executa testes;
Realiza análises no código;
Gera uma build;
Faz o deploy da aplicação.

Dessa forma, consigo transformar várias tarefas manuais em um processo automatizado.

🔄 Pipelines e etapas encadeadas

Uma das coisas mais importantes que entendi durante a aula foi a possibilidade de encadear etapas dentro de uma pipeline.

Isso significa que uma etapa pode depender do sucesso de outra.

Por exemplo:

Código enviado
      ↓
Instalação das dependências
      ↓
Testes automatizados
      ↓
Análise do código
      ↓
Build
      ↓
Deploy

Se os testes falharem, por exemplo, posso impedir que as etapas seguintes sejam executadas.

Isso é muito importante porque evita que um código com problemas avance para outras etapas do processo.

🧪 GitHub Actions aplicado a testes

Também compreendi como o GitHub Actions pode ser utilizado para trabalhar com testes automatizados.

Posso configurar uma pipeline para que, sempre que realizar um push ou abrir um pull request, os testes sejam executados automaticamente.

Dessa forma, não preciso depender apenas de testes manuais para verificar se uma alteração que fiz quebrou alguma parte do projeto.

Um fluxo possível seria:

Push / Pull Request
        ↓
GitHub Actions
        ↓
Instalação das dependências
        ↓
Execução dos testes
        ↓
 ┌───────────────┐
 │ Testes passaram? │
 └───────────────┘
      ↓       ↓
     SIM     NÃO
      ↓       ↓
    Build    Pipeline para
      ↓
    Deploy

Essa abordagem ajuda bastante na qualidade do projeto, principalmente quando várias pessoas trabalham no mesmo repositório.

🧩 GitHub Marketplace

Durante a aula, também conheci o GitHub Marketplace, onde podemos encontrar diversas Actions prontas para serem utilizadas nos nossos workflows.

Isso é interessante porque não precisamos desenvolver todas as automações do zero.

Podemos encontrar Actions desenvolvidas para diferentes finalidades, como:

Configuração de ambientes;
Execução de testes;
Análise de código;
Docker;
Deploy;
Segurança;
Gerenciamento de dependências;
Integração com serviços externos.

Assim, conseguimos montar uma pipeline aproveitando ferramentas que já existem e foram desenvolvidas especificamente para determinadas tarefas.

🛠️ Atividade Prática

A proposta da atividade foi escolher 3 Actions disponíveis no GitHub Marketplace e desenvolver um projeto que utilizasse essas ferramentas dentro de uma pipeline automatizada.

A ideia foi não apenas adicionar as Actions ao projeto, mas entender em qual etapa cada uma delas deveria ser utilizada.

O fluxo que devo seguir é:

Projeto
   ↓
GitHub Actions
   ↓
Action 1
   ↓
Action 2
   ↓
Action 3
   ↓
Resultado da Pipeline

Cada Action deve possuir uma função específica dentro do processo.

Por exemplo, posso utilizar uma Action para configurar o ambiente, outra para executar testes e uma terceira para realizar uma análise ou publicação do projeto.

📋 Organização do Workflow

Um dos pontos que considero mais importantes nessa atividade é a organização do workflow.

Não basta fazer a pipeline funcionar. Preciso conseguir entender facilmente o que cada etapa está fazendo.

Por isso, considero importante utilizar nomes claros para os jobs e steps e separar corretamente cada responsabilidade.

Um workflow pode seguir uma estrutura semelhante a:

name: Pipeline

on:
  push:
  pull_request:

jobs:

  build:
    name: Build
    runs-on: ubuntu-latest

    steps:
      - name: Baixar código
        uses: ...

      - name: Configurar ambiente
        uses: ...

      - name: Executar testes
        uses: ...

      - name: Gerar build
        run: ...

A estrutura pode mudar de acordo com o projeto e com as Actions escolhidas, mas a ideia principal é manter o processo organizado e fácil de entender.

🎯 O que aprendi com a aula

Com essa aula, consegui entender que o GitHub Actions pode ser muito mais do que simplesmente executar comandos automaticamente.

Ele pode ser utilizado para criar um processo completo de integração e entrega contínua, conectando diferentes ferramentas e etapas.

Também entendi que podemos criar pipelines mais complexas, inclusive com jobs independentes ou encadeados, dependendo das necessidades do projeto.

A possibilidade de executar testes automaticamente foi um dos pontos que considerei mais importantes, pois permite verificar alterações antes que elas avancem para outras etapas.

💡 Minha visão sobre a aplicação

Vejo bastante utilidade do GitHub Actions em projetos reais.

Em um projeto desenvolvido por várias pessoas, por exemplo, posso configurar o repositório para que cada alteração passe automaticamente por testes e verificações antes de ser integrada.

Isso reduz tarefas repetitivas e ajuda a evitar erros causados por processos manuais.

Também consigo imaginar pipelines maiores, onde cada etapa possui uma responsabilidade:

Desenvolvimento
      ↓
Commit
      ↓
Push
      ↓
Testes
      ↓
Validação
      ↓
Build
      ↓
Deploy

Dessa maneira, o processo de desenvolvimento fica mais padronizado e previsível.

📝 Conclusão

Nesta aula, aprendi como o GitHub Actions pode ser utilizado para automatizar diferentes processos dentro de um projeto.

Entendi principalmente a importância das pipelines, da organização das etapas e da possibilidade de encadear diferentes processos, principalmente quando trabalhamos com testes automatizados.

A atividade de utilizar três Actions do GitHub Marketplace também me ajudou a perceber que posso aproveitar ferramentas prontas para construir pipelines mais completas sem precisar desenvolver cada automação do zero.

Para mim, o principal aprendizado foi entender que DevOps não está apenas relacionado às ferramentas individualmente, mas também à forma como consigo organizar e conectar essas ferramentas em um processo automatizado.

GitHub Actions + organização + automação + testes = uma pipeline mais confiável e eficiente.