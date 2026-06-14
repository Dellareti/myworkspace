# Skills

Catálogo de skills do Claude Code (cada uma numa pasta com `SKILL.md`).
Arquivos reais versionados no repo (não só symlinks):
- **72 skills standalone** (raiz de `skills/`) — custom + importadas via `npx skills`/clones
- **79 skills do arsenal wshobson** em `skills/wshobson/<plugin>/` — vêm dos 24 plugins instalados

## Como usar numa máquina
Copiar/symlinkar todas pro Claude Code:
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

## Importadas (arsenal — fontes na seção 8 do setup/)
Agrupadas por domínio:

- **Arquitetura/refactor:** improve-codebase-architecture, handoff, review-to-release-workflow,
  implementation-readiness-gate, task-clarification-harness, implementation-contract-review-harness
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
  django-expert, django-security
- **Go:** golang-pro, golang-patterns, golang-testing, golang-code-style
- **Rust:** rust-best-practices, rust-mcp-server-generator, actix-web
- **Ruby:** rails-expert
- **Deploy/Vercel:** deploy-to-vercel, vercel-optimize
- **QA/test/MCP:** webapp-testing, mcp-builder, code-review-analysis, agent-browser
- **Segurança/infra:** security-best-practices, cybersecurity-analyst,
  anthropic-cybersecurity-skills (754 skills MITRE/NIST), secure-linux-web-hosting,
  github-actions-docs
- **Documentos:** pdf, docx, xlsx, pptx
- **Descoberta:** find-skills

> As importadas vieram via `npx skills add` / clones (ver `setup/claude-setup-manifest.md` §8).
> Aqui ficam vendorizadas (cópia dos arquivos) para backup e replicação offline; para atualizar
> à versão upstream, reinstalar pela fonte.

## Skills do arsenal wshobson — `skills/wshobson/<plugin>/` (79 skills)
Vêm dentro dos 24 plugins do marketplace `claude-code-workflows` (ver `setup/` §8a).
Organizadas por plugin para preservar proveniência e evitar colisão de nomes.

| Domínio | Plugins (nº skills) |
|---------|---------------------|
| Backend/API | backend-development (9), api-scaffolding (1), database-design (1) |
| Frontend/UI | frontend-mobile-development (4), ui-design (9) |
| Linguagens | python-development (16), javascript-typescript (4), systems-programming (3) |
| DevOps/Cloud | cloud-infrastructure (8), kubernetes-operations (4), cicd-automation (4), observability-monitoring (4), incident-response (3) |
| Segurança | security-scanning (5), reverse-engineering (4) |

> Fonte viva = plugin instalado (atualizável via `claude plugin`). Cópias aqui = backup.
> Para uso real numa máquina nova, instalar os plugins (§8a) em vez de copiar estes arquivos.
