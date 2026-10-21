# Aula 6 — Pipeline com GitHub Actions

> **Data:** 09/09/2026  
> **Atividade:** integrar uma pipeline ao projeto e analisar três pipelines públicas do GitHub.

[← Índice das aulas](../README.md) · [Projeto analisado: frases-filosofia](https://github.com/FelipeFDSDev/frases-filosofia)

## Objetivos da atividade

1. Configurar o GitHub Actions para executar automaticamente quando houver um `push` na branch principal (`main`).
2. Pesquisar pelo menos três repositórios públicos que usam pipelines e comparar seus gatilhos, funcionalidades e histórico de evolução.

## Projeto da atividade

O projeto analisado foi [FelipeFDSDev/frases-filosofia](https://github.com/FelipeFDSDev/frases-filosofia), uma aplicação feita com React, TypeScript e Vite. A branch principal é `main`.

A pipeline está em [`.github/workflows/ci.yml`](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/.github/workflows/ci.yml). Ela atende ao requisito de executar no `push` para `main` e também valida pull requests direcionados a essa branch.

### Fluxo automatizado

```text
Push em main ou pull request para main
                  ↓
        GitHub Actions (Ubuntu)
                  ↓
           Checkout do código
                  ↓
     Configuração do Node.js 20
                  ↓
             npm ci
                  ↓
          npm run lint
                  ↓
          npm run build
            ↙          ↘
       aprovado       falhou
```

O workflow define `permissions: contents: read`, limitando o token padrão à leitura do conteúdo do repositório. Em seguida, usa `actions/checkout@v4` para obter o código e `actions/setup-node@v4` para configurar o Node.js 20 com cache do npm.

| Etapa | Comando ou Action | Finalidade |
|---|---|---|
| Preparação | `actions/checkout@v4` | Disponibiliza o código no runner. |
| Ambiente | `actions/setup-node@v4`, Node.js 20 | Padroniza a versão do Node.js e habilita cache do npm. |
| Dependências | `npm ci` | Instala as versões registradas no `package-lock.json`. |
| Qualidade | `npm run lint` | Executa o ESLint. |
| Build | `npm run build` | Executa `tsc -b` e gera a versão de produção com Vite. |

A pipeline é de **integração contínua (CI)**: verifica qualidade e se o projeto compila. Ela não faz deploy. O `package.json` também não define um script de testes automatizados; portanto, a esteira não executa testes unitários ou de integração.

## Análise de três repositórios

A análise completa, com detalhes de jobs, segurança, matrizes e referências, está no [relatório de pipelines do projeto](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/analise%20de%203%20projetos%20com%20pipelines/analise-pipelines-github.md). Abaixo está um resumo dos três casos estudados.

| Repositório | Gatilhos observados | O que a pipeline faz | Evolução registrada |
|---|---|---|---|
| [home-assistant/core](https://github.com/home-assistant/core) | `push` em `dev`, `rc` e `master`; `pull_request`; execução manual com `workflow_dispatch`. Labels em PR podem alterar a abrangência da CI. | CI de grande escala, com lint, análise estática e testes paralelos que usam diferentes bancos de dados. | A suíte cresceu de quatro para dez grupos paralelos de testes; várias ferramentas de lint foram consolidadas e foram adicionados `uv` e verificações de segurança dos workflows. |
| [astral-sh/ruff](https://github.com/astral-sh/ruff) | `workflow_call` para reutilização; `pull_request` apenas quando mudanças afetam `pyproject.toml` ou o próprio workflow. O workflow de release aceita execução manual com tag e SHA. | Build e publicação multiplataforma de wheels, binários e imagem Docker. | O fluxo de release manual evoluiu para um workflow gerado pelo `cargo-dist`, que chama um subworkflow reutilizável com a lógica específica do projeto. |
| [fastapi/full-stack-fastapi-template](https://github.com/fastapi/full-stack-fastapi-template) | `pull_request` para validação; `push` em `master` para staging; publicação de release para produção; `schedule` para automações periódicas. | CI e CD de uma aplicação web, com verificações de backend e frontend, testes e deploy por ambiente. | O histórico registra melhorias nos testes Playwright, separação do lint, uso de `uv` e cache, suporte a staging/produção e geração do SDK. |

### Comparação e aprendizados

- **Home Assistant** mostra como dividir uma CI muito grande em tarefas paralelas e deixar a execução manualmente configurável. Labels também permitem ajustar uma execução sem alterar o código.
- **Ruff** demonstra o valor de workflows reutilizáveis e de filtros por caminho: mudanças irrelevantes não precisam iniciar builds multiplataforma caros.
- **Full Stack FastAPI** conecta CI e CD. Os ambientes de staging e produção podem ter secrets e aprovações próprios, separando validação e publicação.
- **frases-filosofia** usa uma esteira proporcional ao projeto: lint e build em cada atualização da branch principal e em pull requests. Uma evolução possível é adicionar testes automatizados quando o projeto passar a ter uma suíte de testes.

A principal conclusão é que os gatilhos devem refletir o fluxo de colaboração; os jobs devem validar o que realmente pode falhar; e o histórico dos workflows ajuda a entender por que a automação mudou com o crescimento do projeto.

## Referências

- [Workflow CI do projeto frases-filosofia](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/.github/workflows/ci.yml) · [histórico de commits](https://github.com/FelipeFDSDev/frases-filosofia/commits/main/)
- [Relatório completo da análise dos três repositórios](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/analise%20de%203%20projetos%20com%20pipelines/analise-pipelines-github.md)
- [Workflow do Home Assistant](https://github.com/home-assistant/core/blob/dev/.github/workflows/ci.yaml)
- [Workflow de build do Ruff](https://github.com/astral-sh/ruff/blob/main/.github/workflows/build-binaries.yml)
- [Workflows e notas de versão do template FastAPI](https://github.com/fastapi/full-stack-fastapi-template/tree/master/.github/workflows) · [release-notes.md](https://github.com/fastapi/full-stack-fastapi-template/blob/master/release-notes.md)
- [Documentação do GitHub Actions sobre workflows e gatilhos](https://docs.github.com/en/actions/concepts/workflows-and-actions/workflows)

---

[← Anterior: Aula 5](../Aula%2005%20-%2002-09-2026/ConteudosAula5.md) | [Próxima: Aula 7 →](../Aula%2007%20-%2016-09-2026/ConteudoAula07.md)

