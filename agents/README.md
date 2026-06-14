# Agentes

Subagentes customizados do Claude Code (arquivos `.md` com frontmatter `name`/`description`).

## Disponíveis aqui
| Agente | Quando usar |
|--------|-------------|
| [backend-api-reviewer](backend-api-reviewer.md) | Revisar design/implementação de endpoints REST/GraphQL |
| [db-migration-reviewer](db-migration-reviewer.md) | Revisar migrations/schema: locks, índices, reversibilidade |
| [infra-iac-reviewer](infra-iac-reviewer.md) | Revisar Terraform/K8s/Docker/CI: segurança, custo, confiabilidade |
| [appsec-auditor](appsec-auditor.md) | Auditoria de segurança (OWASP) — uso defensivo |

> Já cobertos por plugins (não recriar): code-reviewer, code-simplifier, comment-analyzer,
> pr-test-analyzer, silent-failure-hunter, type-design-analyzer (pr-review-toolkit);
> seo-auditor, competitor-analyzer, content-strategist (searchfit-seo).

## Instalar
Global (qualquer projeto) — symlink mantém este repo como fonte de verdade:
```bash
mkdir -p ~/.claude/agents
ln -sf "$(pwd)"/agents/*.md ~/.claude/agents/
```
Por projeto: copie/symlink para `.claude/agents/` do repositório alvo.
