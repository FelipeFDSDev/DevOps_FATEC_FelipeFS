# Aula 09 — Documentação de software

> **Data:** 23/09/2026  
> **Tema:** documentar um projeto de software  
> **Projeto escolhido:** [MiltonProject — API de agendamento e envio de mensagens](https://github.com/FelipeFDSDev/MiltonProject)

## Objetivo da aula

Praticar a documentação de um sistema a partir de um projeto real. A atividade propõe explicar o propósito da aplicação, o problema que resolve, seu escopo, requisitos, tecnologias, arquitetura e organização do código. Também orienta a criar ou atualizar o `README.md` do projeto com informações suficientes para que outra pessoa possa configurá-lo e executá-lo.

## Atividade proposta

A documentação do projeto deveria apresentar:

1. **Objetivo e problema:** explicar para quem o sistema foi pensado e qual necessidade atende.
2. **Escopo:** delimitar o que faz parte da solução e o que fica fora dela.
3. **Requisitos:** registrar os comportamentos esperados e as qualidades importantes do sistema.
4. **Tecnologias e arquitetura:** descrever a stack, o fluxo da aplicação e a responsabilidade dos principais componentes.
5. **README de execução:** informar pré-requisitos, instalação, configuração, execução e, quando aplicável, testes e deploy.
6. **Interfaces e dados:** documentar APIs, banco de dados e variáveis de ambiente quando fizerem parte do projeto.

## Projeto utilizado

O [MiltonProject](https://github.com/FelipeFDSDev/MiltonProject) é uma API REST para gerenciar contatos e mensagens. A descrição e o README do repositório apresentam recursos de envio de mensagens por e-mail e WhatsApp, agendamento para data e hora específicas, processamento automático das mensagens agendadas e documentação interativa da API.

O projeto foi escolhido como estudo de caso porque reúne vários elementos que precisam ser explicados em uma documentação técnica: endpoints, persistência, processamento assíncrono, integrações externas, configuração local e execução de serviços auxiliares.

## Problema e objetivo do sistema

O sistema busca centralizar o cadastro de contatos e o envio de mensagens, permitindo tanto o envio imediato quanto o agendamento. A automação do processamento reduz a necessidade de acompanhar manualmente cada mensagem até o horário previsto.

## Escopo documentado

### Incluído

- Gerenciar contatos por operações de criação, consulta, atualização e remoção, além de importação e exportação CSV, conforme descrito no README do projeto.
- Enviar mensagens imediatamente por e-mail e, quando configurado, por WhatsApp.
- Criar e consultar agendamentos e cancelar um agendamento pelo identificador.
- Processar mensagens agendadas usando Celery, Celery Beat e Redis.
- Persistir dados em SQLite usando SQLAlchemy.
- Expor documentação interativa da API por meio do FastAPI.

### Fora do escopo deste registro

Este material resume a documentação pública do projeto e a proposta da aula. Não é uma auditoria do código, não confirma que todos os cenários estão cobertos por testes e não descreve um processo de deploy em produção que não esteja especificado nas fontes consultadas.

## Requisitos funcionais

Os requisitos abaixo foram organizados a partir das funções e dos endpoints descritos no README público do MiltonProject.

| ID | Requisito |
|---|---|
| RF01 | O sistema deve permitir cadastrar, consultar, atualizar e remover contatos. |
| RF02 | O sistema deve permitir importar e exportar contatos em CSV. |
| RF03 | O sistema deve enviar uma mensagem imediatamente por um canal configurado. |
| RF04 | O sistema deve permitir agendar uma mensagem com destinatário, conteúdo, canal e data/hora. |
| RF05 | O sistema deve listar agendamentos e permitir filtrar ou consultar seu status quando suportado pela API. |
| RF06 | O sistema deve permitir cancelar um agendamento existente. |
| RF07 | O sistema deve processar automaticamente as mensagens cujo horário de envio foi alcançado. |
| RF08 | O sistema deve disponibilizar documentação navegável das rotas da API. |

## Requisitos não funcionais

Estes requisitos são recomendações pertinentes ao sistema e à atividade de documentação. Não devem ser interpretados como resultados de testes ou garantias já comprovadas pelo projeto.

| ID | Requisito recomendado | Como documentar ou verificar |
|---|---|---|
| RNF01 | **Configurabilidade:** credenciais e opções de execução devem ficar em configuração externa ao código. | Listar variáveis de ambiente, finalidade e obrigatoriedade; nunca publicar valores secretos. |
| RNF02 | **Manutenibilidade:** componentes devem ter responsabilidades identificáveis. | Explicar a organização de rotas, serviços, modelos e inicialização. |
| RNF03 | **Confiabilidade do agendamento:** a execução deve distinguir mensagens pendentes, processadas e com falha. | Documentar estados, tentativas e comportamento em falhas conforme implementado. |
| RNF04 | **Segurança:** credenciais de e-mail e WhatsApp devem ser protegidas. | Usar variáveis de ambiente e instruir a criação local de `.env` sem versioná-lo. |
| RNF05 | **Usabilidade para desenvolvimento:** uma pessoa deve conseguir reproduzir a execução local seguindo o README. | Fornecer pré-requisitos, comandos por serviço e endereços de documentação. |
| RNF06 | **Observabilidade:** falhas e execução dos serviços devem produzir informações úteis para diagnóstico. | Informar como acompanhar logs da API, do worker, do Beat e do Redis. |

## Tecnologias e responsabilidades

Conforme o README público do projeto:

| Tecnologia | Papel descrito |
|---|---|
| Python | Linguagem da aplicação. |
| FastAPI | Construção da API REST e documentação OpenAPI interativa. |
| SQLAlchemy | Mapeamento e acesso aos dados. |
| SQLite | Persistência dos dados da aplicação. |
| Celery | Execução das tarefas de processamento em segundo plano. |
| Celery Beat | Agendamento periódico da verificação de mensagens pendentes. |
| Redis | Broker usado na comunicação entre o agendador e os workers. |
| SMTP | Envio de e-mails. |
| Twilio | Integração opcional para envio por WhatsApp. |

## Arquitetura em alto nível

```text
Cliente / consumidor da API
          │ HTTP
          ▼
      FastAPI ───────────────► SQLite
          │                    SQLAlchemy
          │ tarefa de envio
          ▼
      Redis (broker)
          ▲
          │ tarefa agendada
    Celery Beat
          │
          ▼
    Celery Worker ───────────► SMTP / Twilio
```

O fluxo representa a arquitetura descrita no README do projeto: a API recebe operações e persiste dados; tarefas de processamento são encaminhadas pelo Redis; Celery Beat coordena a verificação periódica; e o worker realiza o envio pelo serviço externo configurado. A implementação deve ser consultada para confirmar detalhes operacionais.

## Componentes principais

A estrutura apresentada no README do projeto inclui a pasta `API Base - Python`, com `main.py` como entrada da aplicação, `routes/` para endpoints, `service/` para lógica de negócio, `models.py` para modelos de dados e `celery_app.py` para configuração do processamento assíncrono. O arquivo `requirements.txt` lista dependências Python. A pasta `Documentação/` e o arquivo `RELATORIO_COMPLETO.md` complementam o guia principal.

Essa divisão torna mais fácil localizar as responsabilidades: as rotas recebem as requisições, os serviços concentram operações da aplicação, os modelos representam os dados e a configuração do Celery prepara as tarefas em segundo plano.

## API e dados

O README do MiltonProject lista como rotas principais:

| Método | Rota | Finalidade documentada |
|---|---|---|
| `POST` | `/agendamentos/` | Criar um agendamento. |
| `GET` | `/agendamentos/` | Consultar agendamentos. |
| `DELETE` | `/agendamentos/{id}` | Cancelar um agendamento. |
| `POST` | `/mensagem/enviar/` | Enviar uma mensagem imediatamente. |
| `POST` | `/contacts/` | Criar contato. |
| `GET` | `/contacts/` | Listar contatos. |

A lista é um resumo, não substitui o esquema OpenAPI. Depois de iniciar a aplicação, o README aponta a interface Swagger em `http://localhost:8000/docs` e a ReDoc em `http://localhost:8000/redoc`.

O banco informado é SQLite, acessado por SQLAlchemy. Para documentação de dados completa, o projeto deve descrever as entidades, campos, relacionamentos, restrições e forma de inicialização do banco conforme os modelos e migrações existentes.

## Instalação e execução documentadas

O README do projeto informa Python 3.8 ou superior, Redis 6 ou superior, uma conta Gmail para e-mail e uma conta Twilio opcional para WhatsApp. O fluxo de execução descrito é:

1. Entrar na pasta `API Base - Python`.
2. Criar e ativar um ambiente virtual Python.
3. Instalar as dependências de `requirements.txt`.
4. Configurar as credenciais de e-mail e, se necessário, de Twilio em um arquivo `.env` local.
5. Iniciar o Redis (o exemplo do README usa Docker).
6. Executar a API, o worker Celery e o Celery Beat em processos separados.
7. Acessar `/docs` ou `/redoc` para consultar e experimentar a API.

A configuração publicada inclui `EMAIL_USER`, `EMAIL_PASS`, `TWILIO_ACCOUNT_SID` e `TWILIO_AUTH_TOKEN`. Os valores devem ser preenchidos localmente; credenciais reais não devem ser adicionadas ao repositório.

> Os comandos exatos podem variar conforme sistema operacional e versão do projeto. Consulte o [README do MiltonProject](https://github.com/FelipeFDSDev/MiltonProject) e o [relatório completo](https://github.com/FelipeFDSDev/MiltonProject/blob/main/RELATORIO_COMPLETO.md) antes de executar.

## Testes e deploy

O README público menciona scripts de teste e fornece um exemplo de teste do fluxo de agendamento, mas este registro não afirma cobertura, resultado de execução ou pipeline de CI. Para completar essa parte da documentação do projeto, devem ser indicados os comandos de teste realmente disponíveis, os cenários cobertos e os serviços necessários.

A atividade pede deploy **quando aplicável**. As fontes consultadas para este registro descrevem execução local da API e dos serviços auxiliares, mas não especificam um procedimento de deploy em produção; por isso, nenhum passo de publicação foi presumido.

## Resultado e aprendizado

A atividade mostra que um README útil precisa orientar dois públicos: quem quer entender o sistema e quem precisa executá-lo. Uma boa documentação começa pelo propósito, delimita funcionalidades, explica as peças da arquitetura e oferece passos reproduzíveis de configuração e uso. Também deve separar aquilo que o sistema implementa daquilo que ainda é recomendação ou informação a confirmar.

## Fontes

- [Repositório MiltonProject](https://github.com/FelipeFDSDev/MiltonProject) — README, descrição, recursos e instruções do projeto.
- [Relatório completo do MiltonProject](https://github.com/FelipeFDSDev/MiltonProject/blob/main/RELATORIO_COMPLETO.md).
- [Material da Aula 09 — Documentação de Software](../../Documenta%C3%A7%C3%A3o%20dos%20conte%C3%BAdos/Aula%2009%20-%20Documenta%C3%A7%C3%A3o%20de%20Software.pdf).

---

[← Aula 07](../Aula%2007%20-%2016-09-2026/ConteudoAula07.md) · [Índice das aulas](../README.md) · [Início do repositório](../../README.md)
