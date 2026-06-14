# Agentes

Subagentes do Claude Code (`.md` com frontmatter `name`/`description`).

## Customizados (autoria própria) — raiz de `agents/`
| Agente | Quando usar |
|--------|-------------|
| [backend-api-reviewer](backend-api-reviewer.md) | Revisar design/implementação de endpoints REST/GraphQL |
| [db-migration-reviewer](db-migration-reviewer.md) | Revisar migrations/schema: locks, índices, reversibilidade |
| [infra-iac-reviewer](infra-iac-reviewer.md) | Revisar Terraform/K8s/Docker/CI: segurança, custo, confiabilidade |
| [appsec-auditor](appsec-auditor.md) | Auditoria de segurança (OWASP) — uso defensivo |

## Arsenal wshobson — `agents/wshobson/<plugin>/` (79 agentes)
Vendorizados dos 24 plugins instalados do marketplace `claude-code-workflows`
(ver `setup/claude-setup-manifest.md` §8a). Organizados por plugin para preservar proveniência
e evitar colisão de nomes (vários plugins têm `performance-engineer`, `security-auditor`, etc.).

| Domínio | Plugins (nº agentes) |
|---------|----------------------|
| Arquitetura | c4-architecture (4), full-stack-orchestration (4) |
| Backend/API | backend-development (8), api-scaffolding (4), database-design (2), database-migrations (2), backend-api-security (2) |
| Frontend | frontend-mobile-development (2), ui-design (3) |
| Linguagens | python-development (3), javascript-typescript (2), systems-programming (4), jvm-languages (3) |
| DevOps/Cloud | cloud-infrastructure (7), kubernetes-operations (1), cicd-automation (5), observability-monitoring (4), incident-response (6) |
| Segurança | security-scanning (2), reverse-engineering (3) |
| Qualidade/fluxo | comprehensive-review (3), tdd-workflows (2), debugging-toolkit (2), git-pr-workflows (1) |

## Como usar numa máquina

**Customizados** (global):
```bash
mkdir -p ~/.claude/agents
ln -sf "$PWD"/agents/*.md ~/.claude/agents/
```

**Arsenal wshobson** — duas opções:
- *Recomendado:* instalar os plugins (mantém atualizável) — ver `setup/claude-setup-manifest.md` §8a.
- *Offline/backup:* copiar as defs vendorizadas:
  ```bash
  mkdir -p ~/.claude/agents
  cp agents/wshobson/*/*.md ~/.claude/agents/
  ```
  (Cópia flat pode colidir nomes entre plugins; preferir a via plugin para uso real.)

> Cópias aqui = backup/replicação. A fonte viva dos agentes wshobson é o plugin instalado.
