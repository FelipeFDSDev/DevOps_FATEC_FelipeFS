GitHub Actions e Azure DevOps: análise comparativa de plataformas CI/CD

    Pesquisa acadêmica sobre integração e entrega contínuas (CI/CD), automação DevOps, segurança, escalabilidade, governança e custos

Resumo

A adoção de práticas de DevOps transformou os processos tradicionais de desenvolvimento, integração, teste e entrega de software. Nesse contexto, plataformas de integração e entrega contínuas (CI/CD) passaram a desempenhar um papel central na automação do ciclo de vida das aplicações. Entre as soluções mais relevantes do ecossistema Microsoft encontram-se o GitHub Actions, integrado nativamente ao GitHub, e o Azure DevOps, conjunto de serviços que inclui o Azure Pipelines, além de ferramentas para planejamento, versionamento, testes e gerenciamento de artefatos.

Este estudo apresenta uma análise comparativa aprofundada entre GitHub Actions e Azure DevOps, tomando como referência principal o trabalho de Manolov, Gotseva e Hinov (2025), intitulado Practical Comparison Between the CI/CD Platforms Azure DevOps and GitHub. O artigo compara as duas plataformas considerando capacidades de CI/CD, escalabilidade, segurança, preços, usabilidade, integração com ambientes de nuvem, automação e adequação a diferentes perfis de equipe.

A análise é ampliada neste documento por meio da documentação oficial atual das duas plataformas. São investigados conceitos arquiteturais, workflows e pipelines, runners e agents, execução paralela, estratégias de matriz, artefatos, ambientes, aprovações, secrets, identidades federadas, integração com GitHub e Azure, reutilização de configurações, governança, rastreabilidade, modelos de cobrança e cenários de adoção.

A principal conclusão é que GitHub Actions e Azure DevOps não são simplesmente duas implementações equivalentes de CI/CD. O GitHub Actions apresenta uma abordagem fortemente centrada no repositório GitHub e na automação orientada a eventos, enquanto o Azure DevOps apresenta uma abordagem mais abrangente de plataforma DevOps, particularmente adequada a organizações que necessitam de governança, pipelines complexos, ambientes controlados, integração empresarial e componentes especializados como Azure Boards e Azure Artifacts. Ao mesmo tempo, as fronteiras entre as plataformas diminuíram significativamente: Azure DevOps pode executar pipelines sobre repositórios GitHub, enquanto GitHub Actions possui integração profunda com Azure e mecanismos modernos de segurança e deployment.

Palavras-chave: DevOps; CI/CD; GitHub Actions; Azure DevOps; Azure Pipelines; GitHub; Continuous Integration; Continuous Delivery; Continuous Deployment; Cloud Computing; DevSecOps; automação de software.
1. Introdução

O desenvolvimento moderno de software caracteriza-se por ciclos de entrega cada vez menores, maior frequência de alterações e necessidade de disponibilização contínua de novas funcionalidades. Esse cenário tornou insuficientes processos baseados em integração manual, testes executados apenas ao final do desenvolvimento e implantações realizadas de maneira pouco automatizada.

A cultura DevOps surgiu, entre outros objetivos, para reduzir a distância entre desenvolvimento e operações. Nesse modelo, práticas de integração contínua (Continuous Integration — CI), entrega contínua (Continuous Delivery — CD) e implantação contínua (Continuous Deployment — CD) são utilizadas para automatizar e tornar repetíveis etapas que anteriormente dependiam de intervenção humana.

Nesse contexto, plataformas CI/CD fornecem mecanismos para:

    detectar alterações no código;
    executar builds;
    instalar dependências;
    executar testes;
    realizar análise estática;
    gerar artefatos;
    armazenar resultados;
    publicar pacotes;
    implantar aplicações;
    controlar ambientes;
    aplicar políticas de segurança;
    registrar logs;
    controlar aprovações;
    realizar rollback ou estratégias de deployment;
    integrar ferramentas externas.

O artigo de Manolov, Gotseva e Hinov parte justamente desse problema: como comparar duas plataformas pertencentes ao ecossistema Microsoft, mas construídas em torno de modelos conceituais diferentes? Os autores observam que Azure DevOps e GitHub constituem soluções relevantes, com características, públicos-alvo e modelos de utilização distintos.

Embora o artigo utilize a comparação entre Azure DevOps e GitHub em sentido mais amplo, esta pesquisa concentra a análise técnica principalmente em:

    GitHub Actions, como mecanismo de automação CI/CD do GitHub;
    Azure Pipelines, como componente de CI/CD do Azure DevOps.

Essa delimitação é importante porque comparar “GitHub” inteiro com “Azure DevOps” inteiro produziria uma comparação assimétrica. GitHub é uma plataforma centrada em hospedagem e colaboração sobre código, enquanto Azure DevOps é uma suíte formada por múltiplos serviços.
2. Referência principal

A referência acadêmica central deste estudo é:

    MANOLOV, Vladislav; GOTSEVA, Daniela; HINOV, Nikolay. Practical Comparison Between the CI/CD Platforms Azure DevOps and GitHub. Future Internet, v. 17, n. 4, 2025, p. 153. DOI: 10.3390/fi17040153.

O artigo foi submetido em 7 de março de 2025, revisado em 24 de março, aceito em 28 de março e publicado em 31 de março de 2025.

A pesquisa dos autores aborda:

    capacidades de CI/CD;
    escalabilidade;
    segurança;
    preços;
    usabilidade;
    integração com ambientes de nuvem;
    automação;
    adequação a equipes de diferentes tamanhos;
    custo-efetividade;
    tendências industriais;
    cenários reais de utilização.

A escolha desse trabalho como referência é particularmente adequada porque ele não limita a comparação à sintaxe de pipelines, mas considera também fatores organizacionais e estratégicos.
3. Objetivos
3.1 Objetivo geral

Realizar uma investigação comparativa aprofundada entre GitHub Actions e Azure DevOps/Azure Pipelines, analisando suas características técnicas, arquiteturais, operacionais, econômicas e organizacionais para determinar em quais contextos cada plataforma apresenta maiores vantagens.
3.2 Objetivos específicos

Este estudo busca:

    explicar os fundamentos de CI/CD;
    apresentar a arquitetura do GitHub Actions;
    apresentar a arquitetura do Azure Pipelines;
    comparar workflows e pipelines;
    comparar runners e agents;
    analisar modelos de execução;
    comparar estratégias de paralelismo;
    analisar mecanismos de build e teste;
    comparar artefatos;
    analisar ambientes e deployments;
    comparar secrets e mecanismos de identidade;
    analisar OIDC e autenticação federada;
    investigar mecanismos de governança;
    comparar reutilização de pipelines/workflows;
    analisar integração com GitHub e Azure;
    estudar escalabilidade;
    comparar modelos de cobrança;
    analisar segurança;
    comparar usabilidade;
    identificar vantagens e limitações;
    determinar cenários em que cada plataforma é mais apropriada;
    estabelecer uma matriz de decisão para projetos acadêmicos e profissionais.

4. Fundamentos de CI/CD
4.1 Continuous Integration

Continuous Integration (CI), ou integração contínua, consiste na integração frequente das alterações produzidas pelos desenvolvedores em uma base de código compartilhada.

Em uma implementação CI típica:

Developer
   |
   v
Commit / Pull Request
   |
   v
Source Repository
   |
   v
Build
   |
   v
Unit Tests
   |
   v
Static Analysis
   |
   v
Integration Tests
   |
   v
Artifact

O objetivo é detectar problemas de integração o mais cedo possível.

Entre os benefícios estão:

    redução do custo de correção de defeitos;
    feedback rápido;
    redução de divergências entre branches;
    automatização de testes;
    maior previsibilidade do processo de build.

5. Continuous Delivery e Continuous Deployment

Embora os termos sejam frequentemente utilizados como sinônimos, existe uma diferença importante.
Continuous Delivery

No Continuous Delivery, o software é mantido em um estado potencialmente implantável.

Code
  |
  v
Build
  |
  v
Test
  |
  v
Package
  |
  v
Artifact
  |
  v
Production-ready

A implantação em produção pode exigir uma aprovação humana.
Continuous Deployment

No Continuous Deployment, uma alteração que satisfaz todas as condições automatizadas pode chegar à produção sem aprovação manual.

Commit
  |
  v
Build
  |
  v
Test
  |
  v
Security
  |
  v
Deploy
  |
  v
Production

A diferença é principalmente operacional:
Modelo	Produção
CI	Não necessariamente
Continuous Delivery	Pronta para implantação
Continuous Deployment	Implantação automática

Tanto GitHub Actions quanto Azure Pipelines podem implementar esses modelos, embora utilizem mecanismos diferentes para controle de ambientes, aprovações e deployment.
6. GitHub Actions
6.1 Definição

GitHub Actions é o mecanismo de automação integrado ao GitHub. Ele permite criar workflows automatizados diretamente dentro do repositório.

A documentação oficial descreve Actions como uma plataforma para automatizar, personalizar e executar workflows de desenvolvimento diretamente no repositório. Os workflows podem implementar CI/CD e combinar actions individuais para executar diferentes tarefas.

A configuração é normalmente armazenada em:

.github/
└── workflows/
    ├── ci.yml
    ├── cd.yml
    └── release.yml

Essa característica é importante do ponto de vista de Infrastructure as Code: a própria definição do processo de CI/CD pode ser versionada junto ao código da aplicação.
7. Conceitos fundamentais do GitHub Actions

Os principais componentes são:

Workflow
   |
   +-- Event
   |
   +-- Job
        |
        +-- Runner
        |
        +-- Step
             |
             +-- Action
             |
             +-- Shell command

7.1 Workflow

É o processo automatizado definido em YAML.

Exemplo:

name: CI

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v6

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test

A documentação do GitHub define um workflow como um processo automatizado composto por um ou mais jobs e configurado por meio de YAML.
8. Events

Workflows podem ser disparados por diferentes eventos, como:

    push;
    pull_request;
    workflow_dispatch;
    schedule;
    release;
    workflow_call;
    eventos relacionados a issues;
    eventos de deployment;
    eventos provenientes de outros sistemas.

Exemplo:

on:
  push:
    branches:
      - main

  pull_request:
    branches:
      - main

Essa abordagem baseada em eventos é uma das características mais marcantes do GitHub Actions.
9. Jobs

Um workflow pode conter vários jobs.

jobs:

  build:
    runs-on: ubuntu-latest
    steps:
      - run: npm run build

  test:
    runs-on: ubuntu-latest
    steps:
      - run: npm test

  deploy:
    needs:
      - build
      - test
    runs-on: ubuntu-latest
    steps:
      - run: ./deploy.sh

Por padrão, jobs independentes podem executar em paralelo. Dependências podem ser estabelecidas com needs.
10. Steps

Steps são unidades individuais de execução dentro de um job.

Podem:

    executar comandos;
    utilizar actions;
    configurar variáveis;
    produzir outputs;
    fazer checkout do código;
    publicar artefatos;
    executar testes.

Exemplo:

steps:
  - uses: actions/checkout@v6

  - name: Install
    run: npm ci

  - name: Test
    run: npm test

11. Actions

Actions são componentes reutilizáveis.

Exemplos conceituais:

- uses: actions/checkout@v6

ou:

- uses: actions/upload-artifact@v4

Uma action pode encapsular lógica complexa e ser reutilizada em diferentes workflows.

Isso cria um ecossistema em que organizações podem:

    consumir actions públicas;
    criar actions próprias;
    criar actions compostas;
    centralizar automações.

12. Runners do GitHub Actions

Um runner é o ambiente responsável pela execução de um job.

Existem dois modelos principais:
GitHub-hosted runner

A infraestrutura é fornecida e gerenciada pelo GitHub.
Self-hosted runner

A organização fornece e administra a infraestrutura.

Arquiteturalmente:

GitHub
   |
   | dispatch
   v
Runner
   |
   +-- checkout
   +-- build
   +-- test
   +-- deploy

O uso de runners hospedados reduz a necessidade de administração de infraestrutura.

Runners self-hosted fornecem maior controle, mas transferem responsabilidades operacionais e de segurança para a organização.
13. Matrix Strategy

Uma característica importante do GitHub Actions é a estratégia de matriz.

Exemplo:

jobs:
  test:
    strategy:
      matrix:
        os:
          - ubuntu-latest
          - windows-latest
        node:
          - 20
          - 22

    runs-on: ${{ matrix.os }}

    steps:
      - uses: actions/checkout@v6
      - run: npm ci
      - run: npm test

Isso pode produzir combinações:

Ubuntu + Node 20
Ubuntu + Node 22
Windows + Node 20
Windows + Node 22

A documentação atual informa que uma matriz pode gerar até 256 jobs por workflow run.

Esse mecanismo é especialmente útil para testes multiplataforma.
14. Concurrency no GitHub Actions

O GitHub Actions permite controlar concorrência por meio da propriedade concurrency.

Exemplo:

concurrency:
  group: production
  cancel-in-progress: true

Isso é útil quando várias execuções não podem modificar simultaneamente o mesmo ambiente.

Exemplos:

    deployments;
    migrações de banco;
    publicação de pacotes;
    atualização de infraestrutura.

O GitHub permite controlar concorrência em nível de workflow ou job.
15. Artefatos no GitHub Actions

Artefatos são arquivos produzidos por uma execução que precisam ser preservados ou compartilhados com jobs posteriores.

Exemplo:

- name: Build
  run: npm run build

- name: Upload artifact
  uses: actions/upload-artifact@v4
  with:
    name: application
    path: dist/

Outro job pode realizar o download.

- uses: actions/download-artifact@v4
  with:
    name: application

Artefatos podem conter:

    binários;
    arquivos compilados;
    logs;
    screenshots;
    resultados de testes;
    relatórios de cobertura;
    pacotes.

A documentação do GitHub também relaciona artefatos a mecanismos de provenance e artifact attestations.
16. Reusable Workflows

GitHub Actions permite reutilizar workflows.

Isso é importante para organizações com muitos repositórios.

Exemplo conceitual:

Repository A ─┐
Repository B ─┼──> Reusable CI Workflow
Repository C ─┘

Em vez de duplicar:

build
test
security scan
package

em dezenas de arquivos, uma organização pode centralizar a implementação.

A documentação oficial define reusable workflows como mecanismo para centralizar lógica determinística e repetível.
17. Segurança no GitHub Actions

Segurança é um dos pontos mais importantes da comparação.

A documentação do GitHub destaca mecanismos como:

    secrets;
    GITHUB_TOKEN;
    OIDC;
    artifact attestations;
    proteção contra script injection;
    segurança dos runners;
    permissões granulares.

18. GITHUB_TOKEN

Cada execução pode utilizar um token específico para interagir com o GitHub.

A prática recomendada é limitar permissões.

Exemplo:

permissions:
  contents: read

Em jobs específicos:

jobs:
  release:
    permissions:
      contents: write

A documentação do GitHub permite definir permissões em nível de workflow e job, incluindo read, write e none para diferentes capacidades.

Esse mecanismo implementa o princípio de:

    least privilege

ou princípio do menor privilégio.
19. OIDC no GitHub Actions

Um dos mecanismos mais importantes para segurança moderna é o OpenID Connect.

Tradicionalmente, uma pipeline poderia armazenar uma credencial de longa duração:

GitHub
   |
   | secret
   v
Azure credential

Com OIDC:

GitHub Actions
      |
      | OIDC token
      v
Cloud Identity Provider
      |
      v
Short-lived credential
      |
      v
Azure

Isso reduz a necessidade de armazenar credenciais permanentes.

A documentação oficial mostra que o GitHub Actions pode utilizar OIDC para autenticação no Azure sem armazenar credenciais Azure de longa duração como GitHub Secrets.
20. OIDC e reusable workflows

OIDC pode ser combinado com reusable workflows.

Isso permite criar uma política organizacional como:

Repository
     |
     v
Reusable deployment workflow
     |
     v
OIDC
     |
     v
Cloud

A confiança pode considerar informações como:

    repositório;
    organização;
    workflow;
    branch;
    environment;
    commit;
    runner.

A documentação do GitHub descreve mecanismos de confiança baseados em claims como repository, workflow, ref, environment e referências do workflow reutilizável.
21. Azure DevOps

Azure DevOps é uma plataforma mais abrangente que GitHub Actions.

Os principais serviços incluem:

    Azure Boards;
    Azure Repos;
    Azure Pipelines;
    Azure Test Plans;
    Azure Artifacts.

Assim:

Azure DevOps
|
+-- Boards
+-- Repos
+-- Pipelines
+-- Test Plans
+-- Artifacts

Consequentemente, uma comparação entre GitHub Actions e Azure DevOps deve reconhecer que Azure Pipelines é apenas uma parte da plataforma Azure DevOps.
22. Azure Pipelines

Azure Pipelines fornece funcionalidades de CI/CD para diferentes linguagens, plataformas e ambientes.

A documentação oficial descreve suporte a build, deploy e teste para diferentes ecossistemas, incluindo .NET, Java, JavaScript/Node.js, Python, PHP, Android, containers e Kubernetes.

Uma estrutura conceitual é:

Azure Pipeline
|
+-- Stage
    |
    +-- Job
        |
        +-- Step
            |
            +-- Task

23. YAML no Azure Pipelines

Azure Pipelines suporta pipelines definidos em YAML.

Exemplo:

trigger:
  - main

pool:
  vmImage: ubuntu-latest

steps:
  - script: npm ci
    displayName: Install dependencies

  - script: npm test
    displayName: Run tests

A Microsoft recomenda pipelines YAML em vez de pipelines Classic em vários cenários de segurança e governança, destacando as vantagens de tratar o pipeline como código.
24. Stages no Azure Pipelines

Azure Pipelines possui uma abstração explícita de stages.

Exemplo:

stages:

- stage: Build
  jobs:
    - job: Build

- stage: Test
  jobs:
    - job: Test

- stage: Production
  jobs:
    - deployment: Deploy

Essa estrutura representa diretamente fases do processo:

Build
  |
  v
Test
  |
  v
Staging
  |
  v
Production

Isso é particularmente interessante para ambientes corporativos.
25. Agents do Azure Pipelines

Os agents são equivalentes conceituais aos runners do GitHub Actions.

Um agent executa os jobs definidos no pipeline.

Podem existir:

    Microsoft-hosted agents;
    self-hosted agents.

Arquiteturalmente:

Azure DevOps
     |
     v
Agent
     |
     +-- Checkout
     +-- Build
     +-- Test
     +-- Package
     +-- Deploy

26. Tasks no Azure Pipelines

Azure Pipelines possui uma biblioteca extensa de tasks.

Exemplo:

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '22.x'

- script: npm ci

- script: npm test

Tasks podem abstrair operações complexas de:

    Azure;
    Docker;
    Kubernetes;
    Terraform;
    testes;
    publicação;
    artefatos;
    cloud providers.

27. Azure Pipelines e ambientes

Ambientes são um conceito importante do Azure Pipelines.

Exemplo:

Development
     |
     v
Testing
     |
     v
Staging
     |
     v
Production

Ambientes podem ter:

    permissões;
    aprovações;
    checks;
    histórico de deployments;
    rastreabilidade.

A documentação oficial permite controlar quem pode criar, visualizar, utilizar e administrar ambientes e também estabelecer aprovações antes da execução de etapas de deployment.
28. Approvals and Checks

Um dos recursos importantes do Azure Pipelines é o sistema de approvals and checks.

Exemplo:

Pipeline
   |
   v
Build
   |
   v
Test
   |
   v
Approval
   |
   v
Production

Uma implantação pode ser bloqueada até que:

    uma pessoa aprove;
    uma condição seja satisfeita;
    uma janela de horário seja alcançada;
    uma branch autorizada seja utilizada.

A Microsoft documenta approvals e checks como mecanismos para validar que requisitos sejam atendidos antes da execução de um pipeline ou stage.
29. Recursos protegidos no Azure Pipelines

O Azure Pipelines permite proteger recursos como:

    repositories;
    environments;
    service connections;
    agent pools;
    secure files;
    secret variables.

Permissões, approvals e checks podem ser utilizados para restringir o acesso.

A documentação da Microsoft recomenda explicitamente não conceder acesso aberto quando não for necessário e utilizar autorização explícita para pipelines confiáveis.
30. Templates no Azure Pipelines

Azure Pipelines permite reutilização por meio de templates.

Estrutura:

templates/
├── build.yml
├── test.yml
├── security.yml
└── deploy.yml

Um pipeline pode utilizar:

steps:
- template: templates/build.yml

Isso permite padronizar processos entre projetos.
31. GitHub Actions versus Azure Pipelines: comparação conceitual

A comparação fundamental pode ser representada assim:

GitHub Actions

GitHub Repository
       |
       v
   Workflow
       |
       v
      Jobs
       |
       v
     Runner
       |
       v
     Steps
       |
       v
     Actions

Enquanto:

Azure Pipelines

Repository
    |
    v
Pipeline
    |
    v
Stages
    |
    v
Jobs
    |
    v
Agent
    |
    v
Steps / Tasks

As duas plataformas são semelhantes em capacidade, mas apresentam diferentes abstrações.
32. Tabela comparativa geral
Característica	GitHub Actions	Azure Pipelines
Plataforma principal	GitHub	Azure DevOps
Configuração	YAML	YAML / Classic
Unidade principal	Workflow	Pipeline
Execução	Jobs	Jobs
Executor	Runner	Agent
Unidade operacional	Step	Step/Task
Automação orientada a eventos	Muito forte	Forte
Integração com GitHub	Nativa	Excelente, mas externa
Integração com Azure	Excelente	Nativa
Repositório	GitHub	Azure Repos/GitHub/alguns outros
Matrix	Sim	Sim
Paralelismo	Sim	Sim
Reusable workflows	Sim	Templates
Ambientes	Sim	Sim
Aprovação de deployment	Sim	Sim
Secrets	Sim	Sim
OIDC	Sim	Sim, por mecanismos de service connection/identidade
Artefatos	Workflow artifacts	Pipeline artifacts / Azure Artifacts
Boards	GitHub Issues/Projects	Azure Boards
Pacotes	GitHub Packages	Azure Artifacts
Test management	Integrações e ferramentas	Azure Test Plans
Governança empresarial	Forte	Muito forte
GitHub-native workflow	Excelente	Boa
Azure-native workflow	Excelente	Excelente
Ecossistema marketplace	Muito forte	Muito forte
Infraestrutura self-hosted	Sim	Sim
YAML como código	Sim	Sim
Escopo natural	Repositório	Organização/projeto
33. Diferença filosófica

A diferença mais importante não está na sintaxe.

Está no centro de gravidade da plataforma.
GitHub Actions

O centro de gravidade é:

Código
  |
  v
GitHub Repository
  |
  v
Pull Request
  |
  v
Workflow
  |
  v
Deployment

Ou seja, o GitHub Actions é fortemente Git-native.
Azure DevOps

O centro de gravidade é:

Projeto
 |
 +-- Work Items
 |
 +-- Repository
 |
 +-- Pipeline
 |
 +-- Tests
 |
 +-- Artifacts
 |
 +-- Environments

O Azure DevOps é mais orientado à gestão integrada do ciclo de vida de desenvolvimento.
34. Integração entre GitHub e Azure DevOps

É incorreto afirmar que escolher Azure DevOps significa abandonar GitHub.

Azure Pipelines pode utilizar repositórios GitHub.

A integração permite:

    build automático;
    testes;
    deployments;
    status updates;
    rastreabilidade;
    integração com GitHub Pull Requests;
    integração com GitHub Enterprise.

A documentação oficial da Microsoft descreve a integração de Azure Pipelines com GitHub e GitHub Enterprise.

Portanto:

GitHub Repository
       |
       v
Azure Pipelines
       |
       v
Azure / AWS / GCP / Kubernetes / etc.

é uma arquitetura perfeitamente válida.
35. Azure Boards + GitHub

Também é possível combinar GitHub com Azure Boards.

Nesse cenário:

GitHub
  |
  +-- Commits
  +-- Branches
  +-- Pull Requests
          |
          v
     Azure Boards
          |
          v
      Work Items

A integração pode vincular commits, branches e pull requests a itens de trabalho do Azure Boards.

Isso demonstra que as plataformas não precisam ser utilizadas de maneira mutuamente exclusiva.
36. GitHub Actions com Azure

O inverso também é verdadeiro.

Uma organização pode manter:

Source Code
   |
 GitHub
   |
GitHub Actions
   |
OIDC
   |
Azure

O GitHub documenta explicitamente o uso de OIDC para autenticação de workflows no Azure.

Isso cria uma combinação particularmente interessante:

    GitHub como plataforma de desenvolvimento + GitHub Actions como CI/CD + Azure como infraestrutura de execução.

37. Segurança: comparação
Aspecto	GitHub Actions	Azure Pipelines
Secrets	Sim	Sim
Token automático	GITHUB_TOKEN	System Access Token
OIDC	Sim	Sim
Permissões granulares	Sim	Sim
Ambientes protegidos	Sim	Sim
Aprovações	Sim	Sim
Controle de branches	Sim	Sim
Self-hosted execution	Sim	Sim
Artifact provenance	Sim	Sim
Service connections	Integrações externas	Recurso central
Governança de recursos	Forte	Muito forte
Segurança de pipeline	Forte	Muito forte

A conclusão não deve ser que uma plataforma “não possui segurança”.

As duas possuem mecanismos avançados.

A diferença está na forma de modelar e administrar a segurança.
38. GitHub Actions: principal risco

O ecossistema aberto de Actions é uma vantagem, mas também introduz risco.

Um workflow pode utilizar:

uses: alguma-organizacao/alguma-action@...

Isso cria uma dependência externa.

Riscos incluem:

    action comprometida;
    alteração inesperada;
    dependência de terceiros;
    supply-chain attack;
    permissões excessivas;
    secrets expostos.

Por isso, organizações devem:

    fixar versões;
    avaliar actions utilizadas;
    reduzir permissões;
    controlar secrets;
    utilizar OIDC;
    revisar workflows;
    proteger branches.

39. Azure Pipelines: principal risco

No Azure Pipelines, riscos importantes estão relacionados a:

    service connections;
    permissões excessivas;
    agents;
    secrets;
    acesso a repositórios;
    templates;
    scripts;
    pipelines Classic;
    recursos compartilhados.

A Microsoft recomenda restringir acesso de pipelines a recursos protegidos e evitar conceder acesso indiscriminado.
40. Supply Chain Security

A segurança moderna de CI/CD não termina no pipeline.

Uma cadeia típica é:

Source Code
     |
     v
Dependencies
     |
     v
Build
     |
     v
Artifact
     |
     v
Registry
     |
     v
Deployment

Um atacante pode explorar qualquer etapa.

Portanto, uma plataforma CI/CD moderna deve considerar:

    dependency scanning;
    secret scanning;
    SAST;
    SCA;
    SBOM;
    artifact signing;
    provenance;
    least privilege;
    isolated runners;
    protected environments.

41. Artifact Attestations no GitHub

O GitHub oferece artifact attestations.

Uma attestation pode estabelecer informações sobre a origem e o processo de construção de um artefato.

Conceitualmente:

Source
   |
   v
Workflow
   |
   v
Build
   |
   v
Artifact
   |
   +---- Attestation

A documentação do GitHub indica que attestations podem registrar informações como workflow, repositório, organização, ambiente, commit SHA e dados associados ao OIDC. Também podem ser associadas a SBOMs.
42. Escalabilidade

Escalabilidade possui pelo menos quatro dimensões:

    quantidade de repositórios;
    quantidade de pipelines;
    quantidade de execuções simultâneas;
    complexidade dos processos.

Uma plataforma pode ser tecnicamente capaz de executar milhares de jobs, mas ainda apresentar desafios administrativos.

Portanto:

Technical scalability
        !=
Organizational scalability

Uma organização grande necessita também de:

    governança;
    padrões;
    auditoria;
    permissões;
    templates;
    observabilidade;
    controle de custos.

43. Escalabilidade do GitHub Actions

GitHub Actions é especialmente conveniente quando uma organização possui muitos repositórios GitHub e deseja manter os workflows próximos do código.

Exemplo:

Organization
|
+-- repo-a
|    └── .github/workflows/
|
+-- repo-b
|    └── .github/workflows/
|
+-- repo-c
|    └── .github/workflows/

Reusable workflows podem reduzir duplicação.
44. Escalabilidade do Azure DevOps

Azure DevOps permite organizar projetos, equipes, repositories, pipelines, environments e permissões.

Um modelo conceitual:

Organization
|
+-- Project A
|    +-- Teams
|    +-- Repos
|    +-- Pipelines
|    +-- Boards
|
+-- Project B
     +-- Teams
     +-- Repos
     +-- Pipelines
     +-- Boards

Esse modelo pode ser especialmente interessante em ambientes corporativos que necessitam de separação organizacional.
45. Usabilidade
GitHub Actions

Pontos fortes:

    integração imediata com GitHub;
    configuração próxima do código;
    interface familiar para desenvolvedores GitHub;
    marketplace de Actions;
    forte integração com Pull Requests;
    workflows orientados a eventos.

Possíveis dificuldades:

    YAML pode ficar complexo;
    grande dependência do ecossistema de Actions;
    governança de workflows distribuídos pode exigir disciplina;
    pipelines complexos podem se tornar difíceis de manter.

Azure Pipelines

Pontos fortes:

    modelo robusto de stages;
    templates;
    environments;
    approvals;
    integração com Azure DevOps;
    recursos corporativos.

Possíveis dificuldades:

    maior complexidade inicial;
    maior número de conceitos;
    Azure DevOps possui curva de aprendizado maior;
    integração GitHub não é tão transparente quanto GitHub Actions.

46. Complexidade conceitual

Uma comparação simplificada:

GitHub Actions

Repository
  |
Workflow
  |
Job
  |
Step

Azure Pipelines:

Project
  |
Pipeline
  |
Stage
  |
Job
  |
Step
  |
Task

Isso não significa que Azure Pipelines seja necessariamente pior.

Significa que ele possui mais abstrações explícitas para representar processos complexos.
47. Modelo de custos

O custo deve ser analisado considerando:

Custo total
=
licença
+
execução
+
armazenamento
+
infraestrutura
+
administração
+
segurança
+
manutenção

Uma comparação baseada apenas no preço por minuto é insuficiente.
48. GitHub Actions — custos atuais

A documentação atual do GitHub informa diferentes cotas conforme o plano.

Para repositórios privados, a tabela atual inclui, por exemplo:
Plano	Minutos/mês	Armazenamento de artifacts
GitHub Free	2.000	500 MB
GitHub Pro	3.000	1 GB
GitHub Team	3.000	2 GB
GitHub Enterprise Cloud	50.000	50 GB

Runners padrão hospedados pelo GitHub são gratuitos para repositórios públicos, enquanto repositórios privados utilizam as cotas associadas ao plano.

Esses valores devem ser tratados como dados temporais, pois o modelo comercial pode ser alterado pelo GitHub.
49. Azure Pipelines — custos atuais

A página oficial de preços do Azure DevOps atualmente informa:

    um job paralelo Microsoft-hosted gratuito;
    até 1.800 minutos mensais para esse job;
    um job self-hosted gratuito com minutos ilimitados;
    possibilidade de aquisição de jobs paralelos adicionais.

A página também apresenta preços para jobs paralelos adicionais.

Assim, a comparação de custo deve considerar o perfil de execução.
50. Comparação de custos
Fator	GitHub Actions	Azure Pipelines
Repositório público	Muito favorável	Pode ser favorável
Repositório privado pequeno	Depende do plano	Depende do uso
Self-hosted	Disponível	Disponível
Minutos incluídos	Dependem do plano	Modelo próprio de jobs/minutos
Artefatos	Cota por plano	Pipeline/Azure Artifacts
Grande organização	Enterprise	Azure DevOps Enterprise/serviços
Custos indiretos	Administração do GitHub	Administração do Azure DevOps
Previsibilidade	Depende da utilização	Depende de paralelismo e execução

Conclusão: preço isolado não determina a escolha.
51. GitHub Actions em projetos acadêmicos

Para projetos acadêmicos hospedados no GitHub, GitHub Actions frequentemente apresenta vantagens significativas.

Uma arquitetura típica:

GitHub Repository
       |
       v
GitHub Actions
       |
       +-- Build
       +-- Test
       +-- Lint
       +-- Coverage
       +-- Documentation
       |
       v
Artifact

O pipeline pode ser versionado juntamente com o projeto.

Isso é particularmente interessante para:

    trabalhos acadêmicos;
    TCCs;
    projetos de pesquisa;
    projetos open source;
    experimentos reprodutíveis;
    bibliotecas;
    trabalhos de disciplinas.

52. Reprodutibilidade acadêmica

CI/CD pode contribuir para a reprodutibilidade científica.

Um projeto pode possuir:

src/
tests/
docs/
.github/
  workflows/
    ci.yml
requirements.txt
Dockerfile
README.md

O workflow pode verificar automaticamente:

clone
  |
install dependencies
  |
build
  |
test
  |
coverage
  |
artifact

Isso permite que cada alteração seja validada automaticamente.
53. Azure DevOps em contexto acadêmico

Azure DevOps pode ser especialmente interessante quando o projeto acadêmico pretende estudar:

    ambientes corporativos;
    gerenciamento de requisitos;
    planejamento ágil;
    pipelines complexos;
    Azure Cloud;
    governança;
    testes empresariais;
    deployment controlado.

Uma estrutura possível:

Azure DevOps Project
|
+-- Azure Boards
+-- Azure Repos
+-- Azure Pipelines
+-- Azure Test Plans
+-- Azure Artifacts

54. DevSecOps

DevSecOps amplia DevOps incorporando segurança desde o início.

Uma pipeline moderna pode ser:

Commit
  |
  v
Build
  |
  +--> Unit Tests
  |
  +--> SAST
  |
  +--> Dependency Scan
  |
  +--> Secret Scan
  |
  +--> Container Scan
  |
  v
Package
  |
  v
SBOM
  |
  v
Artifact Signing
  |
  v
Deploy

GitHub Actions e Azure DevOps podem implementar arquiteturas desse tipo.
55. GitHub Actions: modelo DevSecOps

Uma implementação pode combinar:

    GitHub Advanced Security;
    secret scanning;
    code scanning;
    dependency analysis;
    Actions;
    OIDC;
    artifact attestations;
    protected environments.

A arquitetura pode ser:

GitHub
 |
 +-- Source
 +-- Pull Request
 +-- Code Security
 |
 v
GitHub Actions
 |
 +-- Build
 +-- Test
 +-- Security
 +-- Attestation
 |
 v
Azure

56. Azure DevOps: modelo DevSecOps

No Azure DevOps:

Azure Repos / GitHub
       |
       v
Azure Pipelines
       |
       +-- Build
       +-- Test
       +-- Security
       +-- Artifact
       |
       v
Environment
       |
       +-- Approval
       +-- Check
       |
       v
Production

A Microsoft recomenda restringir acesso a projetos, repositórios e service connections, utilizar YAML, proteger agents, controlar variáveis e utilizar templates para práticas de segurança.
57. Infrastructure as Code

GitHub Actions:

.github/workflows/*.yml

Azure Pipelines:

azure-pipelines.yml
templates/*.yml

Nos dois casos, o pipeline pode ser versionado.

Isso proporciona:

    histórico;
    code review;
    rollback;
    auditoria;
    colaboração;
    reprodutibilidade.

58. Pull Requests

GitHub Actions possui uma vantagem natural em cenários orientados a Pull Requests.

Exemplo:

on:
  pull_request:
    branches:
      - main

Isso permite executar automaticamente:

Pull Request
     |
     v
CI
     |
     +-- Build
     +-- Test
     +-- Lint
     +-- Security
     |
     v
Status Check

Esse modelo está profundamente integrado ao fluxo de desenvolvimento GitHub.
59. Azure Pipelines e Pull Requests

Azure Pipelines também pode ser integrado a GitHub Pull Requests.

A diferença é que a pipeline é executada pelo Azure DevOps, enquanto o código pode permanecer no GitHub.

GitHub PR
    |
    v
Azure Pipeline
    |
    v
Build/Test
    |
    v
GitHub Status

A Microsoft documenta essa integração e os mecanismos de conexão entre Azure Pipelines e GitHub.
60. Ambientes de produção

Um dos pontos mais importantes para CD é o controle de produção.
GitHub Actions

Pode utilizar:

    environments;
    environment secrets;
    protection rules;
    reviewers;
    deployment history;
    concurrency.

Azure Pipelines

Pode utilizar:

    environments;
    approvals;
    checks;
    branch control;
    business hours;
    resource permissions.

A Microsoft documenta approvals e checks como mecanismos para bloquear uma etapa até que requisitos de segurança e governança sejam satisfeitos.
61. Exemplo GitHub Actions — CI

name: CI

on:
  push:
    branches:
      - main

  pull_request:

permissions:
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v6

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test

      - name: Build
        run: npm run build

Esse exemplo representa um pipeline CI mínimo.
62. Exemplo GitHub Actions — matriz

name: Matrix CI

on:
  pull_request:

jobs:
  test:
    strategy:
      matrix:
        os:
          - ubuntu-latest
          - windows-latest
        node:
          - 20
          - 22

    runs-on: ${{ matrix.os }}

    steps:
      - uses: actions/checkout@v6

      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}

      - run: npm ci
      - run: npm test

63. Exemplo GitHub Actions — artifact

name: Build

on:
  push:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v6

      - run: npm ci
      - run: npm run build

      - name: Upload build
        uses: actions/upload-artifact@v4
        with:
          name: application
          path: dist/

64. Exemplo GitHub Actions — deployment

name: CD

on:
  push:
    branches:
      - main

permissions:
  contents: read
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest

    environment:
      name: production

    steps:
      - uses: actions/checkout@v6

      - name: Authenticate
        run: echo "OIDC authentication configured here"

      - name: Deploy
        run: ./deploy.sh

65. Exemplo Azure Pipelines — CI

trigger:
  - main

pool:
  vmImage: ubuntu-latest

steps:

- checkout: self

- script: npm ci
  displayName: Install dependencies

- script: npm test
  displayName: Run tests

- script: npm run build
  displayName: Build

66. Exemplo Azure Pipelines — stages

trigger:
  - main

stages:

- stage: Build
  jobs:
  - job: Build
    pool:
      vmImage: ubuntu-latest

    steps:
    - script: npm ci

    - script: npm test

    - script: npm run build

- stage: Deploy
  dependsOn: Build

  jobs:
  - deployment: Production
    environment: production

    strategy:
      runOnce:
        deploy:
          steps:
          - script: ./deploy.sh

67. Equivalência conceitual
GitHub Actions	Azure Pipelines
Workflow	Pipeline
Event	Trigger
Job	Job
Runner	Agent
Step	Step
Action	Task
Matrix	Strategy/Matrix
Environment	Environment
Secrets	Secret variables
Reusable workflow	Template
Artifact	Pipeline artifact
GitHub Packages	Azure Artifacts
GitHub Issues/Projects	Azure Boards

Essa tabela deve ser interpretada como analogia conceitual, e não como equivalência funcional perfeita.
68. GitHub Actions — vantagens

As principais vantagens são:

    integração nativa com GitHub;
    excelente experiência com Pull Requests;
    configuração diretamente no repositório;
    forte modelo orientado a eventos;
    grande ecossistema de Actions;
    workflows reutilizáveis;
    integração forte com cloud;
    OIDC;
    artifacts e attestations;
    facilidade de adoção;
    grande comunidade;
    excelente adequação para open source.

69. GitHub Actions — limitações

Possíveis limitações:

    workflows complexos podem ficar difíceis de manter;
    dependência de Actions de terceiros;
    governança pode exigir configuração organizacional;
    custos podem crescer com uso intensivo;
    runners self-hosted exigem administração;
    funcionalidades empresariais podem depender do plano;
    a plataforma é naturalmente centrada no GitHub.

70. Azure DevOps — vantagens

Principais vantagens:

    suíte DevOps integrada;
    Azure Pipelines robusto;
    Azure Boards;
    Azure Repos;
    Azure Test Plans;
    Azure Artifacts;
    environments;
    approvals;
    checks;
    governança empresarial;
    integração nativa com Azure;
    suporte a cenários complexos;
    boa integração com GitHub;
    grande capacidade de customização.

71. Azure DevOps — limitações

Possíveis limitações:

    maior curva de aprendizado;
    maior quantidade de conceitos;
    experiência menos GitHub-native;
    administração pode ser mais complexa;
    pipelines Classic podem gerar dívida técnica;
    service connections exigem governança cuidadosa;
    custos podem crescer com paralelismo e uso.

72. GitHub Actions ou Azure DevOps?

A resposta depende do problema.
Escolha GitHub Actions quando:

    o código está no GitHub;
    Pull Requests são o centro do desenvolvimento;
    o projeto é open source;
    deseja-se configuração próxima ao código;
    a equipe quer começar rapidamente;
    o workflow é predominantemente CI/CD;
    integração com GitHub é prioridade.

Escolha Azure DevOps quando:

    a organização já utiliza Azure DevOps;
    Azure Boards é importante;
    há necessidade de governança complexa;
    ambientes e approvals são centrais;
    existem processos empresariais estruturados;
    Azure DevOps é usado como plataforma completa;
    há necessidade de forte integração entre planning, source, test e deployment.

73. Quando utilizar os dois?

Não é necessário escolher apenas um.

Uma arquitetura híbrida pode ser:

GitHub
 |
 +-- Source
 +-- Pull Requests
 +-- GitHub Actions
 |
 +------------------+
                    |
                    v
              Azure Cloud

Ou:

GitHub
 |
 +-- Source
 |
 v
Azure Pipelines
 |
 +-- Build
 +-- Test
 +-- Deploy
 |
 v
Azure

Também é possível utilizar:

GitHub
 |
 +-- Source Control
 +-- Pull Requests
 |
 v
Azure Boards
 |
 v
Azure Pipelines
 |
 v
Azure

74. Critérios de decisão

Uma organização pode avaliar as plataformas utilizando os seguintes critérios:
Critério	Peso sugerido
Integração com SCM	15%
CI/CD	15%
Segurança	15%
Governança	10%
Escalabilidade	10%
Usabilidade	10%
Integração cloud	10%
Custos	10%
Ecossistema	5%

A ponderação deve ser adaptada ao contexto.
75. Matriz qualitativa

Escala:

    ★ = baixa;
    ★★ = moderada;
    ★★★ = boa;
    ★★★★ = muito boa;
    ★★★★★ = excelente.

Critério	GitHub Actions	Azure Pipelines
GitHub integration	★★★★★	★★★★
Azure integration	★★★★★	★★★★★
Simplicidade inicial	★★★★★	★★★
CI	★★★★★	★★★★★
CD	★★★★	★★★★★
Governança	★★★★	★★★★★
Pull Requests	★★★★★	★★★★
Environments	★★★★	★★★★★
Approvals	★★★★	★★★★★
Marketplace/ecossistema	★★★★★	★★★★
Gestão integrada DevOps	★★★★	★★★★★
Projetos acadêmicos GitHub	★★★★★	★★★
Ambiente corporativo complexo	★★★★	★★★★★

Essa matriz é qualitativa e não deve ser interpretada como resultado estatístico do artigo de Manolov et al. Trata-se de uma síntese analítica construída a partir das características das plataformas.
76. Comparação arquitetural
GitHub Actions

                    GitHub
                       |
        +--------------+--------------+
        |              |              |
     Repository      Issues        Pull Request
        |
        v
   GitHub Actions
        |
   +----+----+
   |         |
 Job       Job
   |         |
Runner     Runner
   |         |
Steps      Steps
   |         |
Actions    Commands

Azure DevOps

                 Azure DevOps
                      |
       +--------------+--------------+
       |              |              |
     Boards         Repos         Test Plans
                      |
                      v
                 Pipelines
                      |
                  Pipeline
                      |
                +-----+-----+
                |           |
              Stage       Stage
                |           |
              Jobs         Jobs
                |           |
              Agents      Agents

77. Comparação de governança

GitHub Actions possui mecanismos de governança em:

    organizações;
    repositórios;
    environments;
    permissions;
    secrets;
    reusable workflows;
    policies.

Azure DevOps possui mecanismos adicionais em:

    organizações;
    projetos;
    equipes;
    repositories;
    service connections;
    environments;
    variable groups;
    agent pools;
    permissions;
    approvals;
    checks.

Por isso, em ambientes muito regulados, Azure DevOps pode apresentar uma estrutura administrativa particularmente atraente.
78. Observabilidade

Uma plataforma CI/CD deve permitir entender:

    o que foi executado;
    quando foi executado;
    por quem;
    sobre qual commit;
    em qual runner/agent;
    qual etapa falhou;
    quais artefatos foram gerados;
    qual deployment foi realizado.

GitHub Actions fornece logs, histórico de workflow runs, jobs, artifacts e deployment information.

Azure Pipelines fornece logs de execução, stages, jobs, artifacts, environments e deployment history.
79. Rastreabilidade

A rastreabilidade ideal é:

Requirement
    |
    v
Work Item
    |
    v
Commit
    |
    v
Pull Request
    |
    v
Pipeline
    |
    v
Artifact
    |
    v
Deployment
    |
    v
Production

Azure DevOps possui uma vantagem estrutural quando o projeto utiliza Boards + Repos + Pipelines + Artifacts.

GitHub possui uma vantagem natural quando o processo é fortemente centrado em:

Issue
 |
 v
Branch
 |
 v
Pull Request
 |
 v
Actions
 |
 v
Release

80. Integração com Kubernetes

As duas plataformas podem participar de pipelines Kubernetes.

Fluxo:

Git
 |
 v
Build Container
 |
 v
Container Registry
 |
 v
Security Scan
 |
 v
Kubernetes

GitHub Actions pode utilizar actions específicas para Kubernetes e cloud providers.

Azure Pipelines possui tasks e integrações para Azure Kubernetes Service e outras tecnologias.

A escolha depende mais da arquitetura organizacional do que da capacidade básica de executar Kubernetes deployments.
81. Containers

CI/CD moderno frequentemente utiliza containers.

Pipeline:

Source
 |
 v
Docker Build
 |
 v
Docker Test
 |
 v
Security Scan
 |
 v
Registry
 |
 v
Deploy

GitHub Actions e Azure Pipelines podem executar Docker e publicar imagens em registries.

No Azure:

GitHub Actions
       |
       v
Azure Container Registry
       |
       v
AKS

No Azure DevOps:

Azure Pipelines
       |
       v
Azure Container Registry
       |
       v
AKS

82. Multi-cloud

Uma falsa premissa comum é associar:

GitHub Actions = apenas GitHub
Azure DevOps = apenas Azure

Isso é incorreto.

GitHub Actions pode realizar deployments em:

    Azure;
    AWS;
    Google Cloud;
    Kubernetes;
    servidores próprios;
    outros provedores.

Azure Pipelines também pode atuar em ambientes além do Azure.

Portanto, ambas são plataformas de automação e não simplesmente “deploy tools” específicas de um cloud provider.
83. Lock-in

O lock-in deve ser avaliado em diferentes níveis.
GitHub Actions

Possíveis dependências:

    GitHub;
    GitHub Actions syntax;
    Actions externas;
    GitHub environments;
    GitHub secrets;
    GitHub APIs.

Azure DevOps

Possíveis dependências:

    Azure DevOps YAML;
    Azure service connections;
    Azure Artifacts;
    Azure Boards;
    Azure environments;
    Azure-specific tasks.

Quanto mais funcionalidades específicas forem utilizadas, maior pode ser o custo de migração.
84. Portabilidade

YAML não significa automaticamente portabilidade.

Por exemplo:

run: npm test

é relativamente portátil.

Já:

- task: AzureWebApp@1

é específico do ecossistema Azure DevOps.

Da mesma maneira:

- uses: actions/specific-action@vX

é específico do GitHub Actions.

Portanto:

    Pipeline as Code aumenta versionamento, mas não elimina lock-in.

85. Portabilidade entre GitHub Actions e Azure Pipelines

Uma parte pode ser compartilhada:

npm ci
npm test
npm run build

Mas a camada de orquestração muda.

GitHub:

jobs:
  test:

Azure:

stages:
- stage: Test

Assim, uma migração frequentemente exige separar:

Application logic
        |
        v
CI/CD orchestration

Quanto mais a lógica da aplicação estiver separada da lógica específica da plataforma, mais fácil será a migração.
86. Boas práticas comuns às duas plataformas

Independentemente da plataforma:

    utilizar YAML;
    versionar pipelines;
    utilizar code review;
    reduzir permissões;
    proteger branches;
    utilizar secrets;
    evitar credenciais permanentes;
    utilizar OIDC quando possível;
    fixar dependências;
    validar artefatos;
    utilizar ambientes protegidos;
    evitar scripts excessivamente complexos;
    registrar logs;
    implementar testes automatizados;
    monitorar custos.

87. Anti-patterns
Pipeline monolítico

Build + Test + Deploy + Migration + Notification

em um único job.

Problemas:

    difícil manutenção;
    pouca reutilização;
    baixa observabilidade;
    falhas difíceis de isolar.

Secret hardcoded

run: deploy --password=SUPER_SECRET

Nunca utilizar esse padrão.
Permissões excessivas

permissions:
  contents: write

quando apenas leitura é necessária.
Action/task não confiável

Utilizar componentes externos sem avaliação.
Agent compartilhado sem isolamento

Pode causar riscos de segurança.
88. Princípio do menor privilégio

Uma pipeline deve receber apenas as permissões necessárias.

Exemplo:

Build
 |
 +-- read repository
 |
 +-- read dependencies
 |
 +-- write artifact

Não deveria possuir automaticamente:

delete repository
admin organization
production credentials

se essas permissões não forem necessárias.
89. Credenciais de longa duração versus identidade federada

Modelo antigo:

Pipeline
   |
   v
Long-lived Secret
   |
   v
Cloud

Modelo moderno:

Pipeline
   |
   v
OIDC
   |
   v
Short-lived Identity
   |
   v
Cloud

O segundo modelo reduz o impacto de vazamento de credenciais persistentes.

O GitHub documenta especificamente esse padrão para Azure.
90. Considerações sobre runners e agents

Runners/agents self-hosted fornecem:

    software customizado;
    hardware específico;
    acesso a redes privadas;
    GPUs;
    ferramentas proprietárias;
    controle do ambiente.

Mas introduzem responsabilidades:

Patch management
Security
Monitoring
Isolation
Credentials
Network access
Lifecycle

Assim:

    Self-hosted não significa automaticamente mais seguro.

Significa maior controle e maior responsabilidade.
91. Performance

Performance de CI/CD depende de:

Pipeline performance
=
Queue time
+
Provisioning time
+
Build time
+
Test time
+
Artifact transfer
+
Deployment time

O tempo total não depende exclusivamente da plataforma.

Também depende de:

    código;
    dependências;
    cache;
    número de testes;
    tamanho dos artefatos;
    região;
    runner;
    arquitetura de pipeline.

92. Caching

Caching pode reduzir significativamente o tempo de CI.

Exemplo:

First run
  |
download dependencies
  |
cache

Next run
  |
restore cache
  |
build

Isso reduz:

    tráfego;
    tempo;
    custo.

Porém, caches incorretos podem causar builds não determinísticos.

Portanto, cache deve ser tratado como otimização, não como fonte de verdade.
93. Determinismo

Uma boa pipeline deve produzir resultados previsíveis.

Evitar:

latest
unversioned dependencies
random external state

Preferir:

version pinning
lock files
immutable artifacts
reproducible environments

Isso é particularmente importante em pesquisa acadêmica.
94. CI/CD e reprodutibilidade científica

Uma aplicação acadêmica pode utilizar:

Commit SHA
    |
    v
Workflow version
    |
    v
Dependency lock
    |
    v
Build
    |
    v
Test
    |
    v
Artifact

Isso permite responder:

    “Qual código e quais dependências produziram este resultado?”

Essa característica aproxima CI/CD dos princípios de ciência reprodutível.
95. GitHub Actions para pesquisa científica

Pode ser utilizado para:

    executar testes;
    validar notebooks;
    construir documentação;
    compilar LaTeX;
    gerar datasets derivados;
    executar benchmarks;
    gerar relatórios;
    publicar releases;
    validar experimentos.

Exemplo:

Push
 |
 v
Build paper
 |
 v
Run experiments
 |
 v
Generate figures
 |
 v
Generate PDF
 |
 v
Artifact

96. Azure DevOps para pesquisa científica

Pode ser interessante em projetos que necessitam:

    múltiplas equipes;
    planejamento;
    controle de requisitos;
    aprovação;
    rastreabilidade;
    ambientes;
    testes formais;
    integração com Azure.

97. Relação com o artigo de Manolov, Gotseva e Hinov

A abordagem desta pesquisa mantém as dimensões destacadas pelos autores:

                  Comparison
                      |
     +----------------+----------------+
     |                |                |
    CI/CD         Security         Scalability
     |                |                |
   Pricing        Usability        Integration
                      |
                Cloud / Automation
                      |
                 Team suitability

O artigo enfatiza que a escolha entre Azure DevOps e GitHub deve considerar não somente recursos técnicos, mas também contexto organizacional, custo, segurança, escalabilidade e adequação à equipe.

Esta pesquisa acrescenta uma decomposição específica entre GitHub Actions e Azure Pipelines, tornando a comparação mais adequada para análise de mecanismos de CI/CD.
98. Síntese crítica

Não é adequado afirmar simplesmente:

    “GitHub Actions é melhor.”

Também não é adequado afirmar:

    “Azure DevOps é mais completo, portanto é melhor.”

A pergunta correta é:

    Qual plataforma apresenta melhor adequação ao contexto técnico e organizacional considerado?

Para um repositório GitHub acadêmico:

GitHub
 +
GitHub Actions

normalmente oferece uma experiência extremamente integrada.

Para uma organização empresarial que necessita de:

Boards
+
Repos
+
Pipelines
+
Tests
+
Artifacts
+
Environments
+
Governance

o Azure DevOps pode fornecer uma solução mais abrangente.
99. Cenários de escolha
Cenário A — Projeto acadêmico simples

GitHub
  |
  v
Actions
  |
  +-- Build
  +-- Test
  +-- Documentation

Escolha recomendada: GitHub Actions.
Cenário B — Projeto open source

GitHub
 |
 +-- Issues
 +-- Pull Requests
 +-- Actions
 +-- Releases

Escolha recomendada: GitHub Actions.
Cenário C — Aplicação empresarial Azure

Azure DevOps
 |
 +-- Boards
 +-- Repos
 +-- Pipelines
 +-- Artifacts
 |
 v
Azure

Escolha recomendada: Azure DevOps.
Cenário D — GitHub + Azure

GitHub
 |
 v
GitHub Actions
 |
 v
OIDC
 |
 v
Azure

Escolha recomendada: GitHub Actions + Azure.
Cenário E — GitHub + governança empresarial

GitHub
 |
 v
Azure Pipelines
 |
 +-- Approvals
 +-- Environments
 +-- Governance
 |
 v
Cloud

Escolha possível: GitHub + Azure Pipelines.
100. Arquiteturas recomendadas
Arquitetura GitHub-native

Developer
   |
   v
GitHub
   |
Pull Request
   |
   v
GitHub Actions
   |
   +-- Build
   +-- Test
   +-- Security
   +-- Package
   |
   v
Artifact
   |
   v
Deployment

Arquitetura Azure DevOps-native

Developer
   |
   v
Azure DevOps
   |
   +-- Boards
   +-- Repos
   +-- Pipelines
   |
   v
Build
   |
   v
Test
   |
   v
Artifact
   |
 Approval
   |
   v
Production

Arquitetura híbrida

GitHub
 |
 +-- Source
 +-- Pull Requests
 |
 v
Azure Pipelines
 |
 +-- Build
 +-- Test
 +-- Security
 +-- Deployment
 |
 v
Azure

101. Avaliação final

A comparação pode ser sintetizada da seguinte forma:
Dimensão	GitHub Actions	Azure DevOps
Filosofia	Git-native	DevOps suite
CI/CD	Excelente	Excelente
GitHub	Nativo	Integrado
Azure	Excelente	Nativo
Simplicidade	Excelente	Moderada
Governança	Muito boa	Excelente
Planning	Boa	Excelente
Testing management	Boa	Excelente
Artifacts/packages	Muito boa	Excelente
Enterprise workflows	Muito boa	Excelente
Open source	Excelente	Boa
PR-centric development	Excelente	Muito boa
Complexidade	Menor inicialmente	Maior
Flexibilidade	Muito alta	Muito alta
Ecossistema	Muito grande	Muito grande
Segurança	Muito forte	Muito forte
Hybrid cloud	Excelente	Excelente
102. Conclusão

GitHub Actions e Azure DevOps representam duas abordagens maduras para automação do ciclo de vida de software.

O GitHub Actions possui uma vantagem estrutural quando o GitHub é o centro do processo de desenvolvimento. A proximidade entre código, Pull Requests, issues, releases e workflows reduz o atrito operacional e facilita a adoção de CI/CD. O modelo orientado a eventos, o ecossistema de Actions, os reusable workflows, a estratégia de matrix, os environments, o OIDC e os mecanismos de artifact provenance tornam a plataforma adequada tanto para projetos pequenos quanto para ambientes empresariais.

O Azure DevOps, por outro lado, oferece uma visão mais ampla do ciclo de vida de desenvolvimento. Azure Pipelines constitui apenas uma parte da plataforma, que também engloba Boards, Repos, Test Plans e Artifacts. Essa integração pode ser particularmente valiosa em organizações que necessitam de planejamento estruturado, rastreabilidade, governança, ambientes controlados, aprovações e processos de deployment mais formais.

A análise também demonstra que a tradicional oposição:

GitHub versus Azure DevOps

é cada vez menos precisa.

Atualmente, é perfeitamente possível utilizar:

GitHub + GitHub Actions + Azure

ou:

GitHub + Azure Pipelines + Azure

ou ainda:

GitHub + Azure Boards + Azure Pipelines + Azure

A Microsoft mantém integrações oficiais entre GitHub e Azure DevOps, incluindo a possibilidade de utilizar Azure Pipelines sobre repositórios GitHub.

Portanto, a escolha deve ser baseada em requisitos.

Para projetos acadêmicos, open source e equipes fortemente centradas no GitHub, GitHub Actions apresenta uma proposta particularmente natural.

Para organizações que desejam uma plataforma DevOps integrada com forte governança, planejamento, testes, artifacts, environments e processos empresariais, Azure DevOps pode apresentar vantagens significativas.

Para organizações que utilizam GitHub como SCM e Azure como cloud, a combinação GitHub Actions + Azure, especialmente com OIDC, constitui uma arquitetura moderna e coerente.

A principal conclusão deste estudo é, portanto:

    GitHub Actions e Azure DevOps não devem ser avaliados apenas pela quantidade de recursos disponíveis, mas pela adequação entre o modelo operacional da plataforma e o modelo de desenvolvimento da organização.

103. Recomendações práticas

Para um projeto acadêmico hospedado no GitHub, recomenda-se começar com:

.github/
└── workflows/
    ├── ci.yml
    ├── security.yml
    └── release.yml

O ci.yml deve inicialmente executar:

Checkout
   |
Install
   |
Lint
   |
Unit tests
   |
Build

Posteriormente podem ser adicionados:

SAST
Dependency scanning
Container scanning
Coverage
Artifact
SBOM
Attestation
Deployment

Essa evolução gradual evita transformar o pipeline em um sistema excessivamente complexo antes que exista necessidade real.
104. Checklist de avaliação
GitHub Actions

    O código está hospedado no GitHub?
    Pull Requests são parte central do processo?
    O projeto precisa de CI simples?
    É necessário testar múltiplas versões?
    O projeto é open source?
    É desejável utilizar reusable workflows?
    OIDC será utilizado?
    Os ambientes de deployment precisam de proteção?
    Os custos de Actions foram analisados?
    Actions de terceiros foram avaliadas?

Azure DevOps

    A organização utiliza Azure DevOps?
    Azure Boards é necessário?
    Azure Test Plans é necessário?
    Azure Artifacts é necessário?
    Existem múltiplos ambientes?
    São necessárias aprovações formais?
    Existem requisitos fortes de governança?
    Service connections serão utilizadas?
    Os pipelines serão YAML?
    Recursos protegidos serão configurados?

105. Checklist de segurança

    Aplicar least privilege.
    Evitar secrets hardcoded.
    Reduzir permissões dos tokens.
    Utilizar OIDC quando aplicável.
    Proteger ambientes de produção.
    Revisar Pull Requests que alterem pipelines.
    Avaliar Actions/tasks de terceiros.
    Fixar versões de dependências críticas.
    Utilizar secret scanning.
    Utilizar dependency scanning.
    Considerar SBOM.
    Considerar artifact provenance.
    Isolar runners/agents self-hosted.
    Atualizar runners/agents.
    Limitar acesso a service connections.
    Evitar acesso aberto a recursos protegidos.

106. Referências
Referência acadêmica principal

MANOLOV, Vladislav; GOTSEVA, Daniela; HINOV, Nikolay. Practical Comparison Between the CI/CD Platforms Azure DevOps and GitHub. Future Internet, v. 17, n. 4, 2025, p. 153. DOI: 10.3390/fi17040153.
Documentação oficial do GitHub

GitHub. GitHub Actions Documentation. Documentação oficial do GitHub Actions.

GitHub. Workflows and actions reference. Documentação oficial.

GitHub. Workflow syntax for GitHub Actions. Documentação oficial.

GitHub. Using jobs in a workflow. Documentação oficial.

GitHub. Reusing workflow configurations. Documentação oficial.

GitHub. Concurrency. Documentação oficial.

GitHub. Security in GitHub Actions. Documentação oficial.

GitHub. OpenID Connect reference. Documentação oficial.

GitHub. Configuring OpenID Connect in Azure. Documentação oficial.

GitHub. Using OpenID Connect with reusable workflows. Documentação oficial.

GitHub. Workflow artifacts. Documentação oficial.

GitHub. Billing and usage. Documentação oficial.

GitHub. Product usage included with each plan. Documentação oficial.
Documentação oficial da Microsoft

Microsoft. Azure Pipelines documentation. Microsoft Learn.

Microsoft. Key Azure Pipelines concepts. Microsoft Learn.

Microsoft. YAML vs Classic Pipelines. Microsoft Learn.

Microsoft. Secure your Azure Pipelines. Microsoft Learn.

Microsoft. Pipeline resource security. Microsoft Learn.

Microsoft. Create and target Azure DevOps environments for pipelines. Microsoft Learn.

Microsoft. GitHub integration overview — Azure DevOps. Microsoft Learn.

Microsoft. Build GitHub repositories — Azure Pipelines. Microsoft Learn.

Microsoft. Access repositories from pipelines. Microsoft Learn.

Microsoft. Azure DevOps Services pricing. Microsoft Azure.
107. Fontes oficiais para consulta contínua

Como recursos técnicos e comerciais de plataformas SaaS mudam com frequência, recomenda-se que este arquivo não seja considerado um registro permanente de preços ou limites. Para trabalhos acadêmicos que dependam desses valores, deve-se registrar a data da consulta.

    GitHub Actions — documentação oficial.
    GitHub Actions — cobrança e uso.
    Azure Pipelines — documentação oficial.
    Azure DevOps — preços.

108. Conclusão resumida
Pergunta	GitHub Actions	Azure DevOps
Melhor para GitHub-native?	Sim	Não é o foco principal
Melhor para suíte DevOps integrada?	Parcial	Sim
Melhor para open source?	Sim	Possível
Melhor para Azure-native enterprise?	Muito bom	Excelente
Melhor para Pull Requests?	Excelente	Muito bom
Melhor para governança complexa?	Muito bom	Excelente
Mais simples para começar?	Sim	Geralmente não
Melhor escolha universal?	Não existe	Não existe

A escolha final deve considerar arquitetura, equipe, governança, segurança, custos, cloud, maturidade DevOps e modelo de desenvolvimento, e não apenas a quantidade de funcionalidades oferecidas por cada plataforma.
Referência temporal da pesquisa

Data de atualização: 26 de agosto de 2026.

Observação: preços, limites de execução, versões de actions/tasks, recursos experimentais e políticas comerciais podem mudar. Para reprodução acadêmica, recomenda-se registrar a data da consulta e, quando necessário, arquivar as páginas oficiais utilizadas.