# myworkspace

Meu repositório pessoal de ambiente Claude Code: plugins, MCPs, agentes, skills e links de ferramentas.

## Inventário

| Categoria | Qtd | Onde | Replicação |
|-----------|----:|------|------------|
| Agentes customizados | 4 | [`agents/*.md`](agents/) | arquivos no repo |
| Agentes wshobson | 79 | [`agents/wshobson/`](agents/wshobson/) | arquivos no repo (fonte viva = plugin) |
| Skills | 147 | [`skills/`](skills/) | arquivos no repo |
| Plugins | 41 | [`setup/`](setup/claude-setup-manifest.md) §1-2, §8a | comandos `claude plugin install` |
| MCPs | 21 | [`setup/`](setup/claude-setup-manifest.md) §3 | comandos `claude mcp add` |
| Links de ferramentas | — | [`links/`](links/) | — |

**230 agentes+skills versionados** (83 agentes + 147 skills) + plugins/MCPs reproduzíveis por comando (~20M total).

## Estrutura

```
myworkspace/
├── README.md                          # este índice
├── setup/
│   └── claude-setup-manifest.md        # tudo p/ reconstruir o ambiente (plugins, MCPs, arsenal)
├── links/                              # ferramentas úteis por categoria
│   ├── seo.md · performance.md · security.md · agents.md
├── agents/
│   ├── *.md                            # 4 customizados (autoria própria)
│   └── wshobson/<plugin>/*.md           # 79 agentes do arsenal, por plugin
└── skills/
    └── <skill>/SKILL.md                 # 147 skills (custom + importadas + arsenal), flat
```

## Links (ferramentas)

| Categoria | Arquivo | Descrição |
|-----------|---------|-----------|
| SEO | [links/seo.md](links/seo.md) | Análise de SEO, backlinks, tráfego, SERP, keywords |
| Performance | [links/performance.md](links/performance.md) | Velocidade e Core Web Vitals |
| Segurança & Info | [links/security.md](links/security.md) | IP, infra, tech stack, threat intel |
| Agents / IA | [links/agents.md](links/agents.md) | Prontidão de sites para agentes de IA |

## Agentes & Skills

- [`agents/README.md`](agents/README.md) — catálogo de agentes (4 custom + 79 wshobson por domínio)
- [`skills/README.md`](skills/README.md) — catálogo de skills (147, por domínio)

Instalar numa máquina (global):
```bash
# agentes/skills customizados via symlink (repo = fonte de verdade)
ln -sf "$PWD"/agents/*.md ~/.claude/agents/
for d in "$PWD"/skills/*/; do [ -f "$d/SKILL.md" ] && ln -sf "${d%/}" ~/.claude/skills/; done
```

## Setup do ambiente

Ver [setup/claude-setup-manifest.md](setup/claude-setup-manifest.md) para reinstalar tudo numa
máquina nova:
- **Plugins** (17 base + 24 do arsenal) + marketplaces
- **MCPs** (21 globais: cloud, design, DB, devops, scraping, LLM)
- **Arsenal** (§8): marketplace `claude-code-workflows` (24 plugins = 79 agentes + 79 skills) +
  72 skills standalone (Vercel/Anthropics/Glaucia/etc.)
- **Gotchas** documentados (ex.: `known_marketplaces.json` vazio quebra `marketplace add`)
