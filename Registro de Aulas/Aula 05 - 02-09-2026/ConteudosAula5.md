# Aula 05 — GitHub Actions e Marketplace

> **Data:** 02/09/2026<br>
> **Tema:** composição de uma pipeline com Actions reutilizáveis<br>
> **Projeto utilizado:** [fichas-de-treino](https://github.com/FelipeFDSDev/fichas-de-treino)

## Conteúdo da aula

O GitHub Actions automatiza tarefas acionadas por eventos do repositório, como `push`, abertura de pull request, criação de tag ou execução manual. Um workflow YAML reúne jobs e etapas; cada job é executado em um runner e pode usar comandos ou Actions reutilizáveis.

O GitHub Marketplace oferece Actions para tarefas como preparar ambientes, executar verificações, analisar código, publicar artefatos e realizar deploy. A escolha deve corresponder ao objetivo de cada etapa, mantendo a pipeline compreensível e útil para o projeto.

## Atividade proposta

1. Escolher **três Actions** disponíveis no GitHub Marketplace.
2. Integrá-las a um projeto em etapas adequadas de uma pipeline automatizada.
3. Configurar o workflow no GitHub Actions e executá-lo.
4. Verificar o resultado de cada etapa e documentar o nome, a função e a contribuição de cada Action.

## Projeto e workflow

A atividade foi desenvolvida no repositório [FelipeFDSDev/fichas-de-treino](https://github.com/FelipeFDSDev/fichas-de-treino). O workflow [`ci.yml`](https://github.com/FelipeFDSDev/fichas-de-treino/blob/main/.github/workflows/ci.yml) configura o job `quality` em `ubuntu-latest`, com permissão `contents: read`. Ele é disparado em `push` e pull request para `main` ou `develop`, e também pode ser iniciado manualmente.

### Actions do Marketplace utilizadas

| Action | Função na pipeline | Etapa |
|---|---|---|
| [`actions/checkout@v4`](https://github.com/marketplace/actions/checkout) | Baixa o conteúdo do repositório no runner para que os próximos comandos possam usar o código. | Checkout |
| [`actions/setup-node@v4`](https://github.com/marketplace/actions/setup-node-js-environment) | Configura o Node.js 20 e o cache do npm. | Preparação do ambiente |
| [`actions/upload-artifact@v4`](https://github.com/marketplace/actions/upload-a-build-artifact) | Publica os diretórios `src/` e `dist/` como artefato `treino-fichas-build` ao final do workflow. | Armazenamento do resultado |

Entre essas Actions, o workflow também executa comandos do projeto: `npm ci`, `npm run lint`, `npm run format:check`, `npm test -- --runInBand` e `npm run build`. Esses comandos verificam dependências, qualidade, formatação e testes, e geram o build; eles não são Actions do Marketplace.

## Fluxo automatizado

```text
Push / pull request em main ou develop (ou execução manual)
                             ↓
                     Runner Ubuntu
                             ↓
                   Checkout do código
                             ↓
              Configuração do Node.js 20
                             ↓
             npm ci → lint → format:check
                             ↓
                testes → build → artefato
```

## Registro da realização

O workflow combina as três Actions acima com verificações executadas por comandos npm. O histórico público registra execuções `push` concluídas com sucesso em **19/09/2026**, posteriores à aula: [execução 1](https://github.com/FelipeFDSDev/fichas-de-treino/actions/runs/35477469135) e [execução 2](https://github.com/FelipeFDSDev/fichas-de-treino/actions/runs/35476946801). Esses registros confirmam que o workflow foi executado com sucesso naquela data; a aba **Actions** apresenta os detalhes de cada etapa.

## Aprendizados

A atividade demonstra que uma pipeline pode combinar ações prontas do Marketplace e comandos específicos da aplicação. Cada etapa deve ter uma responsabilidade clara: preparar o código, configurar o ambiente, validar o projeto e guardar o artefato produzido.

---

[← Aula 04](../Aula%2004%20-%2026-08-2026/PesquisaGitHubActions-AzureDevOps.md) · [Índice das aulas](../README.md) · [Próxima aula →](../Aula%2006%20-%2009-09-2026/Aula06-ProjetoPipeline.md)

