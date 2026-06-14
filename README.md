# myworkspace

Meu repositório pessoal de ambiente: plugins, MCPs, agentes, skills e links de ferramentas.

## Estrutura

```
myworkspace/
├── setup/          # Como reconstruir meu ambiente Claude Code
│   └── claude-setup-manifest.md   # Plugins, MCPs, agentes, skills + comandos de instalação
├── links/          # Ferramentas e serviços úteis, por categoria
│   ├── seo.md
│   ├── performance.md
│   ├── security.md
│   └── agents.md
├── agents/         # Agentes customizados (defs .md) — adicionar conforme criar
└── skills/         # Skills customizadas — adicionar conforme criar
```

## Índice de links

| Categoria | Arquivo | Descrição |
|-----------|---------|-----------|
| SEO | [links/seo.md](links/seo.md) | Análise de SEO, backlinks, tráfego, SERP, keywords |
| Performance | [links/performance.md](links/performance.md) | Velocidade e Core Web Vitals |
| Segurança & Info | [links/security.md](links/security.md) | IP, infra, tech stack, threat intel |
| Agents / IA | [links/agents.md](links/agents.md) | Prontidão de sites para agentes de IA |

## Setup do ambiente

Ver [setup/claude-setup-manifest.md](setup/claude-setup-manifest.md) para reinstalar todo o
ambiente Claude Code numa máquina nova:
- **Plugins** (17 base) + marketplaces
- **MCPs** (21 globais: cloud, design, DB, devops, scraping, LLM)
- **Arsenal** (seção 8): marketplace `claude-code-workflows` com 24 plugins curados
  (**79 agentes + 79 skills**: arquitetura, backend, frontend, linguagens, devops, cloud,
  segurança) + skills standalone (Vercel/Anthropics/Glaucia) e o gotcha do `known_marketplaces.json`.
- **Agentes/skills customizados** deste repo (`agents/`, `skills/`)
