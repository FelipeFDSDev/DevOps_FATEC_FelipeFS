# Aula 07 — Testes automatizados e CI

> **Data:** 16/09/2026<br>
> **Tema:** testes unitários, de integração e de performance em uma pipeline CI<br>
> **Projeto utilizado:** [tipos-de-testes](https://github.com/FelipeFDSDev/tipos-de-testes)

## Conteúdo da aula

A aula abordou três tipos de teste automatizado e o uso de uma pipeline para executá-los de forma recorrente. Também foram discutidos o GitHub Marketplace e ferramentas de qualidade e padronização, como o ESLint.

- **Teste unitário:** verifica uma unidade pequena do sistema de forma isolada.
- **Teste de integração:** verifica a interação entre componentes ou serviços.
- **Teste de performance:** observa o comportamento do sistema sob carga ou condições definidas.

## Atividade proposta

1. Criar um projeto que integre testes unitários, de integração e de performance.
2. Organizar cada tipo de teste para que possa ser executado e analisado separadamente.
3. Criar uma pipeline de CI em YAML no GitHub Actions.
4. Configurar a pipeline para executar automaticamente em cada `push` na branch `main`.
5. Instalar as dependências, executar os três tipos de teste e apresentar os resultados.

## Projeto utilizado

O projeto desenvolvido para a atividade é [FelipeFDSDev/tipos-de-testes](https://github.com/FelipeFDSDev/tipos-de-testes). Ele implementa uma API CRUD de pedidos em Python, usando Flask e SQLite, e organiza os testes em `tests/unit`, `tests/integration` e `tests/performance`.

### Requisitos e execução local

O README do projeto informa **Python 3.11 ou superior**. Na raiz do repositório, a instalação documentada é:

```bash
python -m pip install -e ".[test]"
```

Para iniciar a API:

```bash
python -m test_types_demo
```

Ela fica disponível em `http://127.0.0.1:5000`. As rotas documentadas são `GET /orders` e `POST /orders` para listar e criar pedidos, `GET /orders/<id>` e `PUT /orders/<id>` para consultar e atualizar, e `DELETE /orders/<id>` para remover.

### Suítes de teste

O README separa a execução dos três tipos de teste:

```bash
python -m pytest tests/unit -m unit -v
python -m pytest tests/integration -m integration -v
python -m pytest tests/performance -m performance -v --benchmark-columns=min,mean,median,max
```

- **Unitários:** `tests/unit/test_orders.py`.
- **Integração:** `tests/integration/test_order_repository.py`.
- **Performance:** `tests/performance/test_orders_performance.py`, com `pytest-benchmark`.

A execução completa também está documentada com `python -m pytest -v`.

## Pipeline de integração contínua

O workflow [`ci.yml`](https://github.com/FelipeFDSDev/tipos-de-testes/blob/main/.github/workflows/ci.yml) executa em cada `push` para `main`. O job roda em Ubuntu, limita o token a `contents: read`, prepara Python 3.12 e instala as dependências de `requirements.txt`.

| Etapa | Configuração | Resultado esperado |
|---|---|---|
| Preparar o código | `actions/checkout@v4` | Código disponível no runner. |
| Preparar Python | `actions/setup-python@v5`, Python 3.12 e cache pip | Ambiente Python configurado. |
| Instalar dependências | `python -m pip install -r requirements.txt` | Dependências necessárias instaladas. |
| Teste unitário | `pytest tests/unit -m unit -v` | Resultado da suíte unitária nos logs. |
| Teste de integração | `pytest tests/integration -m integration -v` | Resultado da suíte de integração nos logs. |
| Teste de performance | `pytest tests/performance -m performance -v --benchmark-columns=min,mean,median,max` | Testes e métricas do benchmark nos logs. |

Cada conjunto é executado em uma etapa própria, facilitando identificar qual grupo falhou. Os resultados são consultados nos logs de cada execução do workflow na aba **Actions** do repositório.

> A configuração de desenvolvimento documenta `Python 3.11+`, enquanto o workflow fixa Python 3.12. O README recomenda instalar a aplicação com o extra `[test]`; a CI instala `requirements.txt`. Esses são os comandos descritos pelas respectivas fontes do projeto.

## Resultado e aprendizado

O projeto atende à estrutura solicitada: separa os três tipos de teste em diretórios e comandos próprios e possui uma CI acionada por `push` em `main`, com uma etapa dedicada para cada suíte. A documentação do repositório também informa como instalar as dependências, iniciar a API e consultar as rotas.

A separação permite rodar e analisar cada categoria individualmente durante o desenvolvimento, enquanto a pipeline repete as verificações de forma automatizada. A performance é apresentada como benchmark; seus números dependem do ambiente em que os testes são executados.

### Verificação posterior do workflow

O histórico público do GitHub Actions registra uma execução `push` em `main` concluída com sucesso em **21/10/2026** ([execução bem-sucedida](https://github.com/FelipeFDSDev/tipos-de-testes/actions/runs/39536361887)). Há também uma execução anterior, em **21/10/2026**, que terminou com falha ([execução com falha](https://github.com/FelipeFDSDev/tipos-de-testes/actions/runs/39535351092)). São resultados posteriores à aula e demonstram que a CI foi executada; os detalhes das etapas e os logs estão disponíveis em cada execução.

## Referências do projeto

- [Repositório tipos-de-testes](https://github.com/FelipeFDSDev/tipos-de-testes)
- [README com instalação, rotas e comandos de testes](https://github.com/FelipeFDSDev/tipos-de-testes/blob/main/README.md)
- [Workflow de CI](https://github.com/FelipeFDSDev/tipos-de-testes/blob/main/.github/workflows/ci.yml)

---

[← Aula 06](../Aula%2006%20-%2009-09-2026/Aula06-ProjetoPipeline.md) · [Índice das aulas](../README.md) · [Início](../../README.md)

