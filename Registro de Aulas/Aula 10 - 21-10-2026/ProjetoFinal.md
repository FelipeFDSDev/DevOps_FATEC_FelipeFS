# Aula 10 — Projeto Final DevOps

> **Data:** 21/10/2026<br>
> **Tema:** integração das práticas de DevOps em um projeto de software<br>
> **Projeto final:** [RateMedia](https://github.com/LuisGlauser/RateMedia)<br>
> **Equipe:** Luís Felipe Glauser Lucas, Felipe Ferreira de Souza, Gabriel da Silva, Giovanni Camargo Maruccio e Arthur Gaspare Camzano

## Objetivo

Consolidar os conteúdos da disciplina em um projeto de software documentado, versionado e preparado para validação e entrega contínuas. O RateMedia aplica práticas de CI/CD, testes automatizados, containerização, segurança e documentação ao desenvolvimento de uma aplicação web colaborativa.

## Projeto e problema

O RateMedia centraliza o acompanhamento, as avaliações e as resenhas de animes, mangás, séries e filmes. Também permite que a comunidade publique e avalie campanhas de RPG de mesa.

O problema que orienta o projeto é a fragmentação da experiência dos fãs entre diferentes serviços para cada tipo de mídia, além da falta de um espaço integrado para descobrir campanhas de RPG. O projeto reúne esses recursos em uma aplicação web, com biblioteca pessoal, busca, listas, perfis e ferramentas de administração.

## Escopo

### Funcionalidades incluídas

- Cadastro, autenticação e gerenciamento de sessão.
- Busca de obras e campanhas com filtros, ordenação e paginação.
- Biblioteca pessoal com status, progresso, notas e resenhas com indicação de spoilers.
- Listas públicas ou privadas e perfil de usuário.
- Criação, publicação e avaliação de campanhas de RPG.
- Painel administrativo para curadoria do catálogo, importação de metadados, moderação e gestão de papéis.
- Integração com AniList, Jikan e TMDB para consultar metadados externos.
- Central de documentação e diagramas acessível pela aplicação.

### Fora do escopo documentado

A versão descrita no projeto não inclui aplicativo móvel nativo, chat, notificações em tempo real, recomendações por inteligência artificial ou upload de imagens. Esses limites ajudam a delimitar a entrega e orientar possíveis evoluções.

## Requisitos principais

### Requisitos funcionais

| ID | Requisito resumido |
|---|---|
| RF01 | Permitir cadastro, autenticação e encerramento de sessão. |
| RF02 | Buscar obras por texto e tipo, com filtros, ordenação e paginação. |
| RF03 | Exibir detalhes da obra, metadados, notas médias e resenhas da comunidade. |
| RF04 | Permitir ao usuário organizar a biblioteca, atualizar progresso, avaliar e escrever resenhas. |
| RF05 | Criar listas públicas ou privadas e gerenciar as obras incluídas. |
| RF06 | Criar, editar, excluir e avaliar campanhas de RPG conforme as permissões do usuário. |
| RF07 | Disponibilizar funções administrativas de catálogo, importação, moderação e gestão de usuários. |
| RF08 | Exibir a documentação técnica e os diagramas do projeto. |

### Requisitos não funcionais

- **Segurança:** Row Level Security (RLS) no PostgreSQL, validação no servidor e credenciais fora do código versionado.
- **Desempenho e resiliência:** cache, timeout e novas tentativas nas integrações externas, com fallback entre AniList e Jikan.
- **Usabilidade:** interface responsiva em português brasileiro.
- **Manutenibilidade:** TypeScript estrito, lint e testes automatizados organizados por nível.
- **Portabilidade:** execução local, em contêiner Docker e na Vercel.
- **Qualidade de entrega:** CI para validar alterações antes do merge e verificação pós-deploy.

## Tecnologias

| Área | Tecnologias e responsabilidades |
|---|---|
| Aplicação web | Next.js 16, React 19, TypeScript e Tailwind CSS 4. |
| Dados e autenticação | Supabase Auth e PostgreSQL com políticas RLS. |
| Integrações externas | AniList GraphQL, Jikan REST e TMDB. |
| Testes | Vitest para testes unitários e de integração, Playwright para E2E e script Node.js para performance. |
| CI/CD | GitHub Actions para CI e verificações; Vercel para previews e produção. |
| Contêiner | Docker multi-stage e Docker Compose. |
| Segurança | gitleaks, `npm audit`, CodeQL, variáveis de ambiente e privilégios mínimos. |

## Arquitetura

O projeto é um monólito Next.js: interface e lógica de servidor ficam na mesma aplicação. As páginas usam Server Components; as alterações são processadas por Server Actions. O Supabase oferece autenticação e persistência PostgreSQL, enquanto as políticas RLS restringem o acesso às linhas conforme o usuário.

```text
Navegador
   │
   ▼
Next.js — App Router / Server Components
   ├── Server Actions ──► validação e regras de negócio
   ├── Integrações ─────► AniList / Jikan / TMDB
   └── Cliente Supabase ─► Auth + PostgreSQL + RLS

GitHub Actions ─► lint, tipos, testes, build, segurança e Docker
Vercel ─────────► preview por pull request e produção após merge na main
```

### Organização dos componentes

- `src/app/`: rotas da aplicação, páginas, layouts e Server Actions.
- `src/components/`: componentes reutilizáveis da interface.
- `src/lib/`: acesso a dados, busca, formatação, validações e integrações externas.
- `src/lib/supabase/`: clientes Supabase para servidor e navegador.
- `supabase/`: schema do banco e migrações.
- `tests/`: testes unitários, de integração, E2E e performance.
- `public/docs/`: documentação Markdown, diagramas e versões em PDF e Word.
- `.github/workflows/`: workflows de CI, segurança, deploy e verificações pós-deploy.

## Testes e qualidade

O projeto organiza a validação em níveis distintos:

| Tipo | Ferramenta | Objetivo |
|---|---|---|
| Unitário | Vitest | Verificar regras, filtros, formatação, permissões e clientes de APIs em isolamento. |
| Integração | Vitest | Validar Server Actions, middleware e camada de dados com Supabase simulado. |
| Ponta a ponta | Playwright | Cobrir fluxos de navegação e uso no navegador. |
| Performance | Script Node.js | Medir latência, vazão e taxa de erros em perfis de carga. |
| Contêiner | Docker | Construir a imagem e verificar que o serviço inicia e responde. |

O repositório também descreve testes manuais de aceitação, como cadastro, autenticação, avaliação de obras, privacidade de listas e acesso administrativo.

## Integração e entrega contínuas

O workflow principal [`ci.yml`](https://github.com/LuisGlauser/RateMedia/blob/main/.github/workflows/ci.yml) é acionado por `push` e pull request em `main` e `develop`, além de permitir execução manual. Os jobs cobrem lint, checagem de tipos, testes unitários e de integração, builds em modos demo e configurado, E2E, performance, Docker, varredura de segredos e auditoria de dependências. Um job final `CI OK` consolida os resultados.

A entrega usa a integração Git da Vercel: pull requests recebem previews e o merge na branch `main` publica em produção. O workflow [`deploy.yml`](https://github.com/LuisGlauser/RateMedia/blob/main/.github/workflows/deploy.yml) executa smoke tests nas rotas principais depois do deploy.

## Containerização e execução

O Dockerfile usa etapas de dependências, build e execução final, com usuário sem privilégios. O Compose define a aplicação e um healthcheck HTTP. O projeto documenta a configuração local por `.env.local`, baseada em [`.env.example`](https://github.com/LuisGlauser/RateMedia/blob/main/.env.example), com variáveis para Supabase e, opcionalmente, TMDB.

O README do projeto orienta a instalar dependências com `npm install`, preencher a configuração local, preparar o schema e as migrações no Supabase e iniciar o ambiente de desenvolvimento com `npm run dev`. O Compose pode subir a versão em contêiner com `docker compose --env-file .env.local up --build`.

Credenciais reais devem permanecer em variáveis de ambiente e não devem ser adicionadas ao Git. O projeto informa que não utiliza chave `service_role` no cliente.

## Documentação e resultado do projeto

O repositório contém um README de entrada, uma Wiki com guias de instalação e operação, documentação técnica em Markdown, diagramas UML/DER e materiais em PDF e Word. A central de documentação também está disponível na aplicação pela rota `/docs`.

Como projeto final, o RateMedia reúne desenvolvimento de produto e práticas operacionais: requisitos e arquitetura documentados, testes em diferentes níveis, automação de CI, deploy contínuo, contêiner e verificações de segurança. Esta descrição segue o estado documentado no README e nos arquivos técnicos do repositório; ela não representa uma execução local ou auditoria independente do sistema.

## Equipe e contribuições registradas

O README do projeto lista os cinco integrantes e as frentes de trabalho: telas, Supabase e integrações; containerização; testes unitários, integração, E2E e performance; pipeline, segurança e pós-deploy; documentação e padronização.

## Referências

- [Repositório RateMedia](https://github.com/LuisGlauser/RateMedia) — README, aplicação e documentação do projeto final.
- [Visão geral](https://github.com/LuisGlauser/RateMedia/blob/main/public/docs/md/01-visao-geral.md) e [requisitos](https://github.com/LuisGlauser/RateMedia/blob/main/public/docs/md/02-requisitos.md).
- [Arquitetura](https://github.com/LuisGlauser/RateMedia/blob/main/public/docs/md/05-arquitetura.md), [DevOps](https://github.com/LuisGlauser/RateMedia/blob/main/public/docs/md/10-devops.md) e [estratégia de testes](https://github.com/LuisGlauser/RateMedia/blob/main/public/docs/md/11-testes.md).
- [Material da Aula 10 — Projeto DevOps](../../Documenta%C3%A7%C3%A3o%20dos%20conte%C3%BAdos/Aula%2010%20-%20Projeto%20DevOps.pdf).

> **Endereço do projeto:** o repositório público localizado no perfil de Luís Glauser usa o slug `RateMedia`. O endereço com `RateMediaNão` não corresponde ao nome publicado; por isso, os links deste registro apontam para `LuisGlauser/RateMedia`.

---

[← Aula 09](../Aula%2009%20-%2023-09-2026/DocumentacaoSoftware.md) · [Índice das aulas](../README.md) · [Início](../../README.md)
