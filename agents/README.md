# Agentes

Catálogo flat de subagentes do Claude Code — **83 agentes**, cada um um `.md` com frontmatter
`name`/`description`. Arquivos reais no repo. Nomes do arsenal são prefixados com o plugin de
origem (`<plugin>-<agente>`) — assim o filename casa com o `name:` interno e não há colisão
(vários plugins têm `security-auditor`, `code-reviewer`, etc., e cada variante é mantida).

Lista exaustiva: `ls agents/`.

## Customizados (autoria própria)
| Agente | Quando usar |
|--------|-------------|
| [backend-api-reviewer](backend-api-reviewer.md) | Revisar design/implementação de endpoints REST/GraphQL |
| [db-migration-reviewer](db-migration-reviewer.md) | Revisar migrations/schema: locks, índices, reversibilidade |
| [infra-iac-reviewer](infra-iac-reviewer.md) | Revisar Terraform/K8s/Docker/CI: segurança, custo, confiabilidade |
| [appsec-auditor](appsec-auditor.md) | Auditoria de segurança (OWASP) — uso defensivo |

## Arsenal wshobson (79, prefixados `<plugin>-<agente>`)
Vêm dos 24 plugins do marketplace `claude-code-workflows` (ver `setup/claude-setup-manifest.md` §8a).
Guia por domínio (prefixo = plugin de origem):

| Domínio | Prefixos de plugin |
|---------|--------------------|
| Arquitetura | c4-architecture-*, full-stack-orchestration-* |
| Backend/API | backend-development-*, api-scaffolding-*, database-design-*, database-migrations-*, backend-api-security-* |
| Frontend/UI | frontend-mobile-development-*, ui-design-* (e ex.: accessibility-expert) |
| Linguagens | python-development-*, javascript-typescript-*, systems-programming-*, jvm-languages-* |
| DevOps/Cloud | cloud-infrastructure-*, kubernetes-operations-*, cicd-automation-*, observability-monitoring-*, incident-response-* |
| Segurança | security-scanning-*, reverse-engineering-* |
| Qualidade/fluxo | comprehensive-review-*, tdd-workflows-*, debugging-toolkit-*, git-pr-workflows-* |

> Variantes do "mesmo" agente em plugins diferentes (ex.: `security-auditor` aparece em 4) são
> **mantidas separadas** porque o conteúdo difere por plugin. O prefixo as distingue.

## Como usar numa máquina
Customizados (global):
```bash
mkdir -p ~/.claude/agents
ln -sf "$PWD"/agents/*.md ~/.claude/agents/
```
> Cópias do arsenal aqui = backup. A fonte viva dos agentes wshobson é o **plugin instalado**
> (atualizável via `claude plugin update`); para uso real numa máquina nova, instalar os
> plugins (§8a) em vez de copiar estes arquivos.
