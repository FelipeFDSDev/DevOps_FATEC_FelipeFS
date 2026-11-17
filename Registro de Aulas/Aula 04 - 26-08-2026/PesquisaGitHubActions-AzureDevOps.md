# GitHub Actions ou Azure DevOps?

> **Aula 04 · 26/08/2026**  
> **Tema:** comparação de plataformas para automação CI/CD

## Em poucas palavras

GitHub Actions e Azure Pipelines automatizam integração e entrega de software. A diferença principal está no contexto em que cada ferramenta se encaixa: Actions trabalha de forma integrada ao GitHub; Azure Pipelines faz parte da suíte Azure DevOps, que também oferece planejamento, repositórios, testes e pacotes.

## O que é CI/CD?

- **Integração contínua (CI):** cada alteração passa por verificações automáticas, como compilação e testes.
- **Entrega contínua (continuous delivery):** o software fica pronto para publicação, que pode depender de aprovação.
- **Implantação contínua (continuous deployment):** alterações aprovadas pelos testes são publicadas automaticamente.

Um fluxo comum é:

```text
Alteração → build → testes → artefato → aprovação (opcional) → publicação
```

## Comparação rápida

| Aspecto | GitHub Actions | Azure Pipelines |
|---|---|---|
| Integração principal | Repositórios, pull requests e eventos do GitHub | Serviços do Azure DevOps; também pode usar repositórios GitHub |
| Configuração | Workflows em YAML, normalmente em `.github/workflows/` | Pipelines em YAML ou configuração clássica |
| Execução | Runners hospedados ou próprios | Agents hospedados ou próprios |
| Ponto forte | Começar rápido quando o projeto já está no GitHub | Integrar pipelines a processos e serviços corporativos do Azure DevOps |
| Ecossistema | Actions e workflows reutilizáveis | Boards, Repos, Test Plans, Artifacts e Pipelines |

As duas ferramentas suportam automação, execução paralela, ambientes, segredos e integração com diferentes plataformas de nuvem. A escolha depende do fluxo da equipe, dos controles necessários e dos serviços já utilizados.

## Como escolher

**GitHub Actions** tende a ser uma escolha direta quando o código e a colaboração já acontecem no GitHub e a equipe quer validar pull requests e automatizar builds no mesmo lugar.

**Azure Pipelines** pode ser mais conveniente quando a organização já usa Azure DevOps e precisa conectar a automação a planejamento, testes, pacotes ou aprovações centralizados.

Também é possível combinar GitHub como repositório com Azure Pipelines como mecanismo de CI/CD. As plataformas não precisam ser tratadas como opções mutuamente exclusivas.

## Segurança e custos

Em qualquer plataforma, conceda ao pipeline apenas as permissões necessárias, proteja credenciais, revise componentes de terceiros e restrinja publicação em ambientes sensíveis. Runners e agents próprios oferecem controle sobre a infraestrutura, mas exigem manutenção e isolamento pela equipe.

Custos e limites variam conforme plano, sistema operacional, tempo de execução e uso de agentes próprios. Como esses valores mudam, consulte as páginas oficiais antes de tomar uma decisão comercial; esta comparação não fixa preços.

## Conclusão

Para um projeto acadêmico hospedado no GitHub, Actions costuma reduzir a configuração inicial e facilitar a visualização do processo. Em uma organização que já depende dos serviços e controles do Azure DevOps, Azure Pipelines pode oferecer melhor encaixe. Em ambos os casos, a decisão deve partir das necessidades do projeto, e não de uma lista isolada de funcionalidades.

## Referências

- Manolov, V.; Gotseva, D.; Hinov, N. [Practical Comparison Between the CI/CD Platforms Azure DevOps and GitHub](https://doi.org/10.3390/fi17040153). *Future Internet*, 2025, 17(4), 153.
- [Documentação do GitHub Actions](https://docs.github.com/actions)
- [Documentação do Azure Pipelines](https://learn.microsoft.com/azure/devops/pipelines/)
- [Integração entre Azure Pipelines e GitHub](https://learn.microsoft.com/azure/devops/pipelines/repos/github)

---

[← Aula 03](../Aula%2003%20-%2019-08-2026/Atividade_sobre_Landing_Pages/README.md) · [Índice das aulas](../README.md) · [Aula 05 →](../Aula%2005%20-%2002-09-2026/ConteudosAula5.md)
