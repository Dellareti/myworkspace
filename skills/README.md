# Skills

Catálogo flat de skills do Claude Code — **147 skills**, cada uma numa pasta com `SKILL.md`.
Arquivos reais versionados no repo (não só symlinks). Vêm de três origens, mas vivem juntas:
custom (autoria própria), importadas via `npx skills`/clones, e as do arsenal `wshobson`
(que também chegam pelos plugins — ver `setup/claude-setup-manifest.md` §8).

Lista exaustiva: `ls skills/`.

## Como usar numa máquina
```bash
mkdir -p ~/.claude/skills
for d in "$PWD"/skills/*/; do ln -sf "${d%/}" ~/.claude/skills/; done
```
(Ou `cp -r skills/* ~/.claude/skills/` para cópias independentes do repo.)

## Customizadas (autoria própria)
| Skill | Quando dispara |
|-------|----------------|
| [api-scaffold](api-scaffold/SKILL.md) | Criar endpoint completo no padrão do projeto |
| [deploy-checklist](deploy-checklist/SKILL.md) | Go/no-go pré-deploy |
| [stack-conventions](stack-conventions/SKILL.md) | Convenções do meu stack (preencher TODOs) |
| [incident-debug](incident-debug/SKILL.md) | Debug de incidente: sintoma → causa raiz |

## Importadas — guia por domínio
(Amostra representativa; não exaustiva — há ~143 importadas no total.)

- **Arquitetura/refactor/planejamento:** improve-codebase-architecture, handoff,
  review-to-release-workflow, implementation-readiness-gate, task-clarification-harness,
  implementation-contract-review-harness, comprehensive-review-*
- **Svelte/SvelteKit:** svelte-code-writer, svelte-core-bestpractices, svelte5-best-practices,
  sveltekit-structure, svelte, shadcn-svelte
- **React/Next:** react, react-best-practices, react-components, composition-patterns,
  next-best-practices, next-cache-components, next-upgrade, next-browser,
  vercel-react-best-practices, vercel-react-native-skills, vercel-react-view-transitions
- **UI/UX & design:** ui-ux-pro-max, shadcn, web-design-guidelines, frontend-design,
  canvas-design, web-artifacts-builder, skill-creator
- **JS/TS:** javascript-mastery, javascript-typescript-jest, typescript-advanced-types,
  typescript-expert, typescript-pro, typescript-react-reviewer, nodejs-backend-patterns,
  nodejs-best-practices, fastify-best-practices
- **Python:** python-performance-optimization, python-testing-patterns, fastapi-expert,
  django-expert, django-security (+ skills do plugin python-development)
- **Go:** golang-pro, golang-patterns, golang-testing, golang-code-style
- **Rust:** rust-best-practices, rust-mcp-server-generator, actix-web
- **Ruby:** rails-expert
- **Backend/DB/API:** skills dos plugins backend-development, api-scaffolding, database-design
- **DevOps/Cloud:** skills dos plugins cloud-infrastructure, kubernetes-operations,
  cicd-automation, observability-monitoring, incident-response
- **Deploy/Vercel:** deploy-to-vercel, vercel-optimize
- **QA/test/MCP:** webapp-testing, mcp-builder, code-review-analysis, agent-browser
- **Segurança/infra:** security-best-practices, cybersecurity-analyst,
  anthropic-cybersecurity-skills (754 skills MITRE/NIST), secure-linux-web-hosting,
  github-actions-docs, security-scanning-*, reverse-engineering-*
- **Documentos:** pdf, docx, xlsx, pptx
- **Descoberta:** find-skills

> Os arquivos aqui são cópia (backup/replicação offline). Para as skills que vêm de plugins
> (`wshobson`), a fonte viva é o plugin instalado — atualizável via `claude plugin update`.
> Para reinstalar do upstream, ver `setup/claude-setup-manifest.md` §8.
