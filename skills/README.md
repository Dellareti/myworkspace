# Skills

Skills customizadas do Claude Code (cada uma numa pasta com `SKILL.md`).

## Disponíveis aqui
| Skill | Quando dispara |
|-------|----------------|
| [deploy-checklist](deploy-checklist/SKILL.md) | Antes de deploy/release: testes, migrations, rollback, env, observabilidade |
| [api-scaffold](api-scaffold/SKILL.md) | Criar endpoint completo seguindo as convenções do projeto |
| [stack-conventions](stack-conventions/SKILL.md) | Convenções do seu stack (Svelte/Next/Django/Go/Rust/Nest) — arquivo vivo, preencher TODOs |
| [incident-debug](incident-debug/SKILL.md) | Debug de incidente em produção: sintoma → evidência → causa raiz |

> Já cobertos por plugins (não recriar): superpowers (TDD, systematic-debugging, writing-plans…),
> searchfit-seo (11 skills de SEO), chrome-devtools-mcp (a11y, LCP), frontend-design, claude-mem.

## Instalar
Global (qualquer projeto):
```bash
mkdir -p ~/.claude/skills
for d in "$(pwd)"/skills/*/; do ln -sf "$d" ~/.claude/skills/; done
```
Por projeto: copie/symlink para `.claude/skills/` do repositório alvo.
