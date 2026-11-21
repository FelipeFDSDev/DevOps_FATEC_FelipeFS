# Aula 06 — Pipeline e análise de repositórios

> **Data:** 09/09/2026<br>
> **Tema:** CI com GitHub Actions e análise de pipelines públicas<br>
> **Projeto da primeira etapa:** [FelipeFDSDev/frases-filosofia](https://github.com/FelipeFDSDev/frases-filosofia)<br>
> **Relatório da segunda etapa:** [análise de três repositórios](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/analise%20de%203%20projetos%20com%20pipelines/analise-pipelines-github.md)

## Proposta da atividade

A atividade teve duas partes:

1. Integrar uma pipeline ao projeto e configurá-la para executar em cada `push` na branch principal (`main`).
2. Analisar pelo menos três repositórios públicos com pipelines, observando suas funcionalidades, gatilhos e histórico de evolução.

## Parte 1 — Pipeline do projeto

O projeto usado para a primeira parte foi [frases-filosofia](https://github.com/FelipeFDSDev/frases-filosofia), uma aplicação em React, TypeScript e Vite. O workflow está em [`.github/workflows/ci.yml`](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/.github/workflows/ci.yml).

A configuração executa no `push` para `main` e também em pull requests direcionados a essa branch. O workflow limita o token a `contents: read`, prepara o Node.js 20, instala as dependências com `npm ci`, roda o lint e cria o build.

| Etapa | Configuração | Finalidade |
|---|---|---|
| Checkout | `actions/checkout@v4` | Baixar o código no runner. |
| Ambiente | `actions/setup-node@v4`, Node.js 20 | Padronizar o runtime e configurar cache do npm. |
| Dependências | `npm ci` | Instalar as versões do `package-lock.json`. |
| Qualidade | `npm run lint` | Executar ESLint. |
| Build | `npm run build` | Verificar tipos e gerar o build do Vite. |

Essa pipeline valida qualidade e compilação; não realiza deploy. O `package.json` consultado no registro da atividade não definia script de testes automatizados, portanto não se deve descrever essa esteira como executora de testes unitários ou de integração.

## Parte 2 — Análise comparativa

A análise dos três repositórios é a segunda etapa da atividade e está documentada no [relatório completo](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/analise%20de%203%20projetos%20com%20pipelines/analise-pipelines-github.md), dentro do mesmo repositório da atividade. O projeto `frases-filosofia` é o objeto da primeira etapa; não é um dos três casos comparados no relatório.

| Repositório analisado | O que foi observado |
|---|---|
| [home-assistant/core](https://github.com/home-assistant/core) | CI extensa com lint, análise estática e testes paralelos; gatilhos em branches, pull requests e execução manual; evolução da estrutura de testes e das verificações de segurança. |
| [astral-sh/ruff](https://github.com/astral-sh/ruff) | Workflows reutilizáveis, filtros por caminho e publicação multiplataforma de builds e artefatos. |
| [fastapi/full-stack-fastapi-template](https://github.com/fastapi/full-stack-fastapi-template) | Integração e entrega por ambientes, validações de backend e frontend, testes e publicação em staging/produção. |

## Síntese

A comparação mostra que pipelines variam conforme o tamanho e as necessidades do projeto. O repositório de estudo usa uma CI proporcional, com lint e build; os casos analisados ilustram paralelismo, reutilização de workflows e separação de ambientes. Os gatilhos devem refletir o fluxo de colaboração e as verificações devem corresponder aos riscos reais do código.

## Fontes da atividade

- [Workflow CI de frases-filosofia](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/.github/workflows/ci.yml)
- [Histórico de commits do projeto](https://github.com/FelipeFDSDev/frases-filosofia/commits/main/)
- [Relatório de análise dos três repositórios](https://github.com/FelipeFDSDev/frases-filosofia/blob/main/analise%20de%203%20projetos%20com%20pipelines/analise-pipelines-github.md)
- [Workflow do Home Assistant](https://github.com/home-assistant/core/blob/dev/.github/workflows/ci.yaml)
- [Workflow de build do Ruff](https://github.com/astral-sh/ruff/blob/main/.github/workflows/build-binaries.yml)
- [Workflows do template FastAPI](https://github.com/fastapi/full-stack-fastapi-template/tree/master/.github/workflows)

---

[← Aula 05](../Aula%2005%20-%2002-09-2026/ConteudosAula5.md) · [Índice das aulas](../README.md) · [Próxima aula →](../Aula%2007%20-%2016-09-2026/ConteudoAula07.md)
