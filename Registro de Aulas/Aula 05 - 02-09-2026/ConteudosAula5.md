# ⚙️ GitHub Actions e Pipelines Automatizadas

> **Disciplina:** DevOps — FATEC
> **Atividade:** GitHub Actions e Automação de Pipelines
---

## 📌 Sobre a Aula

Durante esta aula, aprendi sobre o **GitHub Actions** e como ele pode ser utilizado para automatizar diferentes processos dentro de um projeto.

Inicialmente, o professor apresentou o funcionamento do GitHub Actions e suas principais ferramentas, mostrando como podemos criar **workflows automatizados** diretamente dentro de um repositório do GitHub.

A partir disso, entendi que é possível automatizar várias etapas do desenvolvimento, evitando a necessidade de realizar determinados processos manualmente.

---

## 🚀 GitHub Actions

O GitHub Actions permite criar automações que são executadas a partir de determinados eventos no repositório.

Por exemplo, posso configurar uma pipeline para ser executada automaticamente quando realizo:

* 📤 `push` em uma branch;
* 🔀 abertura de um `pull request`;
* 🏷️ criação de uma `tag`;
* ▶️ execução manual do workflow.

Isso permite integrar diferentes ferramentas e processos diretamente ao fluxo de desenvolvimento.

---

## 🔄 Pipelines Automatizadas

Um dos principais conceitos apresentados durante a aula foi a utilização de **pipelines**.

Entendi que uma pipeline pode possuir várias etapas e que essas etapas podem ser organizadas e até mesmo **encadeadas**, fazendo com que uma etapa dependa do resultado de outra.

Um exemplo de fluxo que posso utilizar é:

```text
Alteração no código
       │
       ▼
      Push
       │
       ▼
GitHub Actions
       │
       ▼
   Instalação
       │
       ▼
     Testes
       │
       ▼
 Validação do código
       │
       ▼
      Build
       │
       ▼
     Deploy
```

Dessa forma, consigo criar um processo em que o código só avança para a próxima etapa caso a etapa anterior seja concluída corretamente.

---

## 🧪 Automação de Testes

Outro ponto que considerei importante foi a possibilidade de utilizar o GitHub Actions para **testes automatizados**.

Posso configurar a pipeline para executar os testes sempre que uma alteração for enviada para o repositório.

Isso é útil porque consigo verificar automaticamente se uma alteração introduziu algum problema no projeto.

Um possível fluxo seria:

```text
Push
 │
 ▼
Executar testes
 │
 ├── ❌ Falhou → Pipeline interrompida
 │
 └── ✅ Passou
       │
       ▼
      Build
       │
       ▼
     Deploy
```

Assim, os testes funcionam como uma etapa de validação antes que o código continue pelo restante da pipeline.

---

## 🧩 GitHub Marketplace

Durante a aula, também conheci o **GitHub Marketplace**, onde existem diversas Actions prontas que podem ser utilizadas nos workflows.

Isso facilita bastante a criação das pipelines, pois não preciso desenvolver todas as automações do zero.

As Actions disponíveis podem ser utilizadas para diferentes finalidades, como:

* 🧪 Testes automatizados;
* 🔍 Análise de código;
* 🔐 Segurança;
* 📦 Gerenciamento de dependências;
* 🐳 Docker;
* 🚀 Deploy;
* ⚙️ Configuração de ambientes;
* 📊 Verificações e validações.

---

## 🛠️ Atividade Proposta

A atividade desta aula consiste em escolher **3 Actions disponíveis no GitHub Marketplace** e utilizá-las em um projeto através de uma **pipeline automatizada no GitHub Actions**.

A ideia é utilizar cada Action em uma etapa adequada do processo, fazendo com que elas trabalhem em conjunto dentro do workflow.

O fluxo da atividade pode ser representado da seguinte maneira:

```text
                 Projeto
                    │
                    ▼
             GitHub Actions
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
       Action 1            Action 2
          │                   │
          └─────────┬─────────┘
                    ▼
                 Action 3
                    │
                    ▼
              Resultado
```

---

## 🔧 Actions Utilizadas

Para realizar a atividade, utilizei três Actions do **GitHub Marketplace**, cada uma responsável por uma etapa diferente da pipeline.

| Action      | Função                              | Etapa       |
| ----------- | ----------------------------------- | ----------- |
| 🔧 Action 1 | Configuração/preparação do ambiente | Preparação  |
| 🧪 Action 2 | Execução das verificações/testes    | Testes      |
| 🚀 Action 3 | Processo final da aplicação         | Finalização |

A utilização de Actions diferentes em cada etapa permitiu compreender melhor como podemos **combinar ferramentas dentro de uma mesma pipeline**.

---

## 📋 Organização do Workflow

O workflow foi configurado dentro do próprio repositório utilizando um arquivo localizado em:

```text
.github/
└── workflows/
    └── pipeline.yml
```

Essa organização permite manter os workflows separados do restante do código da aplicação.

A estrutura básica utilizada segue a ideia:

```text
.github
   │
   └── workflows
          │
          └── pipeline.yml
                    │
                    ├── Action 1
                    ├── Action 2
                    └── Action 3
```

Manter essa estrutura organizada é importante porque, conforme o projeto cresce, posso ter diferentes workflows para diferentes finalidades.

---

## ▶️ Execução da Pipeline

Depois de configurar o workflow, realizei a execução da pipeline pelo **GitHub Actions**.

Durante a execução, foi possível acompanhar cada etapa separadamente e verificar se as Actions foram executadas corretamente.

O processo ficou organizado da seguinte maneira:

```text
Workflow iniciado
       │
       ▼
Action 1
       │
       ▼
Action 2
       │
       ▼
Action 3
       │
       ▼
Pipeline concluída
```

A execução das etapas permitiu verificar na prática como o GitHub Actions consegue automatizar processos que anteriormente precisariam ser executados manualmente.

---

## 💡 O que eu aprendi

Com esta aula, entendi melhor como o **GitHub Actions** pode ser utilizado dentro de um fluxo real de desenvolvimento.

O principal aprendizado foi perceber que posso criar pipelines com diversas etapas e utilizar diferentes ferramentas dentro delas.

Também entendi que as pipelines podem ser **encadeadas**, principalmente quando existe uma dependência entre processos, como executar os testes antes de permitir que uma aplicação avance para uma etapa de build ou deploy.

Além disso, o GitHub Marketplace facilita bastante esse processo porque disponibiliza Actions prontas para diversas necessidades.

---

## 📈 Aplicação em Projetos Reais

Consigo aplicar esse conhecimento em projetos futuros para automatizar boa parte do meu fluxo de desenvolvimento.

Um projeto maior poderia possuir uma pipeline como:

```text
       Desenvolver
            │
            ▼
          Commit
            │
            ▼
           Push
            │
            ▼
    ┌─────────────────┐
    │ GitHub Actions   │
    └────────┬────────┘
             │
             ▼
        Testes
             │
             ▼
       Análise/Validação
             │
             ▼
           Build
             │
             ▼
          Deploy
```

Dessa forma, consigo reduzir processos manuais e tornar o desenvolvimento mais organizado, automatizado e confiável.

---

## 📝 Considerações Finais

Nesta aula, aprendi que o **GitHub Actions** pode ser utilizado para muito mais do que executar um simples comando automaticamente.

Posso utilizar diferentes Actions para criar um fluxo completo de desenvolvimento, conectando **testes, validações, builds e deploys** dentro de uma única pipeline.

A possibilidade de encadear essas etapas também mostra como o conceito de automação pode crescer junto com o projeto.

> ⚙️ **Código → GitHub → Actions → Testes → Validação → Build → Deploy**

Para mim, o principal aprendizado desta aula foi entender como transformar tarefas que seriam realizadas manualmente em um **processo automatizado e organizado dentro do próprio GitHub**.
