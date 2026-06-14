# Claude Code — Manifesto de Setup Portável

Tudo que está instalado no meu ambiente Claude Code (plugins, MCPs, agentes, skills) +
comandos para reinstalar em outra máquina.

> Levantado em 2026-06-13 a partir de `~/.claude/settings.json`,
> `~/.claude/plugins/installed_plugins.json` e dos `.mcp.json` dos plugins.

---

## 1. Marketplaces de plugins

```bash
# O oficial (claude-plugins-official) já vem por padrão. Os extras:
claude plugin marketplace add thedotmack/claude-mem
claude plugin marketplace add jarrodwatts/claude-hud
```

---

## 2. Plugins (17 — todos a nível de usuário)

```bash
# Marketplace oficial (claude-plugins-official)
claude plugin install frontend-design@claude-plugins-official
claude plugin install superpowers@claude-plugins-official
claude plugin install context7@claude-plugins-official
claude plugin install github@claude-plugins-official
claude plugin install skill-creator@claude-plugins-official
claude plugin install chrome-devtools-mcp@claude-plugins-official
claude plugin install searchfit-seo@claude-plugins-official
claude plugin install typescript-lsp@claude-plugins-official
claude plugin install security-guidance@claude-plugins-official
claude plugin install code-review@claude-plugins-official
claude plugin install pr-review-toolkit@claude-plugins-official
claude plugin install commit-commands@claude-plugins-official
claude plugin install claude-md-management@claude-plugins-official
claude plugin install claude-code-setup@claude-plugins-official
claude plugin install playwright@claude-plugins-official

# Marketplaces de terceiros
claude plugin install claude-mem@thedotmack          # v10.6.3
claude plugin install claude-hud@claude-hud          # v0.0.11 (statusline)
```

| Plugin | Marketplace | Versão |
|--------|-------------|--------|
| frontend-design | claude-plugins-official | unknown |
| superpowers | claude-plugins-official | 5.0.7 |
| context7 | claude-plugins-official | unknown |
| github | claude-plugins-official | unknown |
| skill-creator | claude-plugins-official | unknown |
| chrome-devtools-mcp | claude-plugins-official | latest |
| searchfit-seo | claude-plugins-official | 1.0.0 |
| typescript-lsp | claude-plugins-official | 1.0.0 |
| security-guidance | claude-plugins-official | unknown |
| code-review | claude-plugins-official | unknown |
| pr-review-toolkit | claude-plugins-official | unknown |
| commit-commands | claude-plugins-official | unknown |
| claude-md-management | claude-plugins-official | 1.0.0 |
| claude-code-setup | claude-plugins-official | 1.0.0 |
| playwright | claude-plugins-official | unknown |
| claude-mem | thedotmack | 10.6.3 |
| claude-hud | claude-hud | 0.0.11 |

---

## 3. MCPs

### 3a. MCPs trazidos por plugins (globais — disponíveis em qualquer pasta)
Instalam-se automaticamente junto com os plugins; **não** precisa de `claude mcp add`:

| MCP | Plugin que o fornece |
|-----|----------------------|
| chrome-devtools | chrome-devtools-mcp |
| context7 | context7 |
| playwright | playwright |
| mcp-search | claude-mem |

Config extra do chrome-devtools (em `~/.claude/settings.json` → `pluginConfigs`):
```json
"chrome-devtools-mcp@claude-plugins-official": {
  "mcpServers": {
    "chrome-devtools": {
      "executablePath": "/home/dellareti/.local/share/flatpak/app/com.google.Chrome/current/active/files/extra/chrome"
    }
  }
}
```
> Ajuste o caminho do Chrome na máquina nova.

### 3b. MCPs por projeto (ficam no `.mcp.json` de cada repositório)
Exemplo do projeto ps1-recomp:
```json
{
  "mcpServers": {
    "ps1-recomp": { "type": "stdio", "command": ".venv/bin/python", "args": ["tools/ps1_mcp_server.py"] },
    "ghidra":     { "type": "sse", "url": "http://localhost:8080/sse" },
    "pcsx-redux": { "type": "sse", "url": "http://localhost:8078/sse" }
  }
}
```
- `ps1-recomp`: venv Python + `tools/ps1_mcp_server.py` (versionado no repo)
- `ghidra`: GhidraMCP plugin rodando na porta 8080
- `pcsx-redux`: `tools/pcsx_redux_mcp/server.py` + `startup.lua` no console Lua

### 3c. MCPs da conta claude.ai (OAuth — migram com o login)
Gmail, Google Calendar, Google Drive. Não dependem da máquina.

### 3d. MCPs globais adicionados manualmente (`claude mcp add --scope user`)
Instalados em 2026-06-13 para o perfil full-stack (frontend/backend, cloud, DevOps, design, QA).
Vão para `~/.claude.json`. Reinstalar com:

```bash
# --- Remotos / sem credencial ---
claude mcp add --transport sse  cloudflare-docs           https://docs.mcp.cloudflare.com/sse           --scope user
claude mcp add --transport sse  cloudflare-bindings       https://bindings.mcp.cloudflare.com/sse       --scope user   # OAuth Cloudflare
claude mcp add --transport sse  cloudflare-observability  https://observability.mcp.cloudflare.com/sse  --scope user   # OAuth Cloudflare
claude mcp add --transport http sentry                    https://mcp.sentry.dev/mcp                    --scope user   # OAuth Sentry
claude mcp add --transport http canva                     https://mcp.canva.com/mcp                     --scope user   # OAuth Canva
claude mcp add --transport http figma-dev-mode            http://127.0.0.1:3845/mcp                     --scope user   # precisa do app Figma Desktop aberto

# --- Locais sem credencial ---
claude mcp add kubernetes --scope user -- npx -y mcp-server-kubernetes                          # usa o kubeconfig ambiente
claude mcp add terraform  --scope user -- docker run -i --rm hashicorp/terraform-mcp-server
claude mcp add shadcn     --scope user -- npx -y shadcn@latest mcp

# --- Locais COM credencial (trocar REPLACE_ME / connstring) ---
claude mcp add framelink-figma --scope user -e FIGMA_API_KEY=REPLACE_ME          -- npx -y figma-developer-mcp --stdio
claude mcp add supabase        --scope user -e SUPABASE_ACCESS_TOKEN=REPLACE_ME  -- npx -y @supabase/mcp-server-supabase@latest
claude mcp add digitalocean    --scope user -e DIGITALOCEAN_API_TOKEN=REPLACE_ME -- npx -y @digitalocean/mcp
claude mcp add postgres        --scope user -- npx -y @modelcontextprotocol/server-postgres "postgresql://USER:PASS@HOST:5432/DBNAME"

# --- Dev / frameworks / automação (lote 2) ---
claude mcp add docker     --scope user -- npx -y docker-mcp                 # alternativa Linux (Docker Engine puro), substitui o gateway
claude mcp add n8n        --scope user -- npx -y n8n-mcp                     # docs/nodes/workflows n8n (1º npx baixa ~grande)
claude mcp add svelte     --scope user -- npx -y @sveltejs/mcp              # MCP oficial de docs da Svelte
claude mcp add firecrawl  --scope user -e FIRECRAWL_API_KEY=REPLACE_ME -- npx -y firecrawl-mcp
claude mcp add gemini     --scope user -- npx -y gemini-mcp-tool            # wrapper do Gemini CLI (precisa Gemini CLI autenticado)
claude mcp add --transport http vercel https://mcp.vercel.com --scope user # OAuth Vercel; cobre deploy e Next.js

# --- Pendentes / requerem ajuste no host ---
# aws-core : claude mcp add aws-core --scope user -- uvx awslabs.core-mcp-server@latest   (precisa creds AWS + AWS_REGION; falhou no 1º health check)
# ssh      : configurar por host com a chave SSH (ex.: npx -y ssh-mcp ...) — não instalado por ser específico da máquina
```

### Lote 2 — frameworks/dev (2026-06-13)
| MCP | Papel | Estado | Credencial |
|-----|-------|--------|------------|
| docker | DevOps/containers (Linux) | ✔ conectado | — (acesso ao Docker socket) |
| n8n | Automação/workflows | ✔ conectado | opcional (API do seu n8n) |
| svelte | Frontend (docs Svelte) | ✔ conectado | — |
| firecrawl | Scraping/crawl | ✔ conecta | FIRECRAWL_API_KEY |
| gemini | LLM auxiliar (Gemini CLI) | ✔ conecta | Gemini CLI autenticado |
| vercel | Deploy + Next.js | ! OAuth | login Vercel |

> **Frameworks/linguagens sem MCP dedicado** (React, Next-código, Django, Go, Rust, Node, Nest):
> usar **context7** (já instalado) — serve docs atualizadas via "use context7" no prompt.
> Next.js também é coberto pelo **vercel** (build/deploy/erros).

| MCP | Papel | Estado pós-install | Credencial |
|-----|-------|--------------------|------------|
| cloudflare-docs | Cloud (docs CF) | ✔ conectado | — |
| cloudflare-bindings | Cloud (Workers/bindings) | ! OAuth | login Cloudflare |
| cloudflare-observability | Cloud (logs/obs) | ! OAuth | login Cloudflare |
| sentry | Observabilidade/erros | ! OAuth | login Sentry |
| canva | Design | ! OAuth | login Canva |
| figma-dev-mode | Design pixel-perfect | ✘ precisa app Figma aberto | — (app desktop) |
| framelink-figma | Design via API | ✔ conecta | FIGMA_API_KEY |
| shadcn | Frontend/components | ✔ conectado | — |
| kubernetes | DevOps | ✔ conectado | kubeconfig |
| terraform | DevOps/IaC | ✔ conectado | — |
| supabase | Backend/DB | ✔ conecta | SUPABASE_ACCESS_TOKEN |
| postgres | Backend/DB | ✔ conecta | connstring |
| digitalocean | VPS | ✔ conecta | DIGITALOCEAN_API_TOKEN |
| aws-core | Cloud AWS | ✘ pendente | creds AWS + região |
| docker | DevOps/containers | ✘ requer Docker Toolkit | — |

> Já cobertos por plugins (não readicionar): chrome-devtools (Google DevTools), playwright (QA), github (PR review), context7 (docs de libs / system design).

---

## 4. Agentes

Sem agentes customizados instalados (`~/.claude/agents/` e `.claude/agents/` vazios).
Built-in disponíveis: `claude`, `claude-code-guide`, `Explore`, `general-purpose`, `Plan`,
`statusline-setup`. (Plugins como `pr-review-toolkit` podem registrar agentes próprios.)

> Agentes customizados que eu criar ficam em `../agents/`.

---

## 5. Skills

Skills vêm habilitadas via plugins (ex.: `code-review`, `skill-creator`, `superpowers`,
`commit-commands`, `claude-md-management`). Skills customizadas que eu criar ficam em `../skills/`.

---

## 6. Settings de usuário relevantes (`~/.claude/settings.json`)

```json
{
  "model": "opus",
  "statusLine": { "type": "command", "command": "<launcher do plugin claude-hud>" },
  "enabledPlugins": { "...os 17 plugins acima...": true },
  "extraKnownMarketplaces": {
    "thedotmack": { "source": { "source": "github", "repo": "thedotmack/claude-mem" } },
    "claude-hud": { "source": { "source": "github", "repo": "jarrodwatts/claude-hud" } }
  }
}
```

---

## 7. Ordem de reinstalação numa máquina nova

1. `claude plugin marketplace add thedotmack/claude-mem`
2. `claude plugin marketplace add jarrodwatts/claude-hud`
3. Rodar o bloco de `claude plugin install` da seção 2
4. Ajustar `executablePath` do chrome-devtools no settings
5. Em cada repo, garantir o `.mcp.json` correspondente
6. `model: opus` e a statusline aplicam ao habilitar claude-hud + settings

---

## 8. Arsenal de agentes & skills (2026-06-13)

Fontes analisadas para montar o arsenal full-stack/arquiteto/devops/segurança.

### ⚠️ Gotcha obrigatório antes de qualquer `marketplace add`
Se `~/.claude/plugins/known_marketplaces.json` estiver **vazio (0 bytes)**, todo
`claude plugin marketplace add` falha com `JSON Parse error: Unexpected EOF`. Corrigir:
```bash
[ -s ~/.claude/plugins/known_marketplaces.json ] || printf '{}' > ~/.claude/plugins/known_marketplaces.json
```

### 8a. wshobson/agents → marketplace `claude-code-workflows` (84 plugins; instalei 24)
Trouxe **79 agentes + 79 skills**. Core curado cobrindo todos os domínios:
```bash
claude plugin marketplace add wshobson/agents
M=claude-code-workflows
for p in \
  c4-architecture full-stack-orchestration \
  backend-development api-scaffolding database-design database-migrations \
  frontend-mobile-development ui-design \
  python-development javascript-typescript systems-programming jvm-languages \
  cloud-infrastructure kubernetes-operations cicd-automation observability-monitoring incident-response \
  security-scanning backend-api-security reverse-engineering \
  comprehensive-review tdd-workflows debugging-toolkit git-pr-workflows ; do
  claude plugin install "$p@$M"
done
```
Plugins do marketplace **não instalados** (disponíveis sob demanda): blockchain-web3, game-development,
quantitative-trading, machine-learning-ops, llm-application-dev, data-engineering, payment-processing,
seo-*, content-marketing, hr-legal-compliance, startup-business-analyst, etc. — adicionar só quando precisar
(evita inflar o contexto de toda sessão).

### 8b. Skills standalone → `~/.claude/skills/`
`npx skills add` às vezes cai em modo interativo; o método **determinístico** é clonar a fonte e copiar
a pasta da skill. Receita:
```bash
DST=~/.claude/skills; mkdir -p "$DST"
SRC=/tmp/skill-src; mkdir -p "$SRC"; cd "$SRC"
git clone --depth 1 https://github.com/anthropics/skills anthropics-skills
git clone --depth 1 https://github.com/vercel-labs/agent-skills vercel-agent-skills
git clone --depth 1 https://github.com/glaucia86/skills glaucia-skills

# Vercel (frontend/react/design)
for s in react-best-practices composition-patterns web-design-guidelines vercel-optimize deploy-to-vercel; do
  cp -r "$SRC/vercel-agent-skills/skills/$s" "$DST/$s"; done
# Anthropics (testing/mcp/design/documentos)
for s in webapp-testing mcp-builder canvas-design web-artifacts-builder pdf docx xlsx pptx; do
  cp -r "$SRC/anthropics-skills/skills/$s" "$DST/$s"; done
# Glaucia (planejamento/workflow)
for s in implementation-readiness-gate task-clarification-harness review-to-release-workflow implementation-contract-review-harness; do
  cp -r "$SRC/glaucia-skills/$s" "$DST/$s"; done

# Extras via npx skills (CLI da skills.sh)
npx -y skills@latest add https://github.com/vercel-labs/skills        --skill find-skills   --global -y
npx -y skills@latest add https://github.com/vercel-labs/agent-browser --skill agent-browser --global -y
```

| Skill | Fonte | Uso |
|-------|-------|-----|
| react-best-practices, composition-patterns | vercel-agent-skills | React/Next performance e composição |
| web-design-guidelines, vercel-optimize, deploy-to-vercel | vercel-agent-skills | UI review, custo Vercel, deploy |
| webapp-testing | anthropics/skills | Testar webapp com Playwright |
| mcp-builder | anthropics/skills | Criar MCP servers |
| canvas-design, web-artifacts-builder | anthropics/skills | Arte/PNG/PDF, artifacts HTML complexos |
| pdf, docx, xlsx, pptx | anthropics/skills | Gerar/editar documentos Office/PDF |
| implementation-readiness-gate, task-clarification-harness, review-to-release-workflow, implementation-contract-review-harness | glaucia86/skills | **Planejamento**: clarificação, gates go/no-go, workflow de release |
| find-skills | vercel-labs/skills | Descobrir/instalar novas skills |
| agent-browser | vercel-labs/agent-browser | Automação de browser p/ agentes |

> **Pulados de propósito:** `obra/superpowers` = idêntico ao plugin superpowers já instalado;
> `frontend-design` já vem do plugin frontend-design.
> Clones-fonte ficam em `/home/dellareti/arsenal-sources` (caminho **sem espaços** — o CLI quebra
> com espaços no path) e em `_arsenal_sources/` (não committar; é working dir).

### 8c. Lote grande de skills via `npx skills add` (49 skills, multi-fonte)
Instaladas em `~/.claude/skills/` (total subiu para **72**). Método (não-interativo):
```bash
npx -y skills@latest add https://github.com/<owner>/<repo> --skill <skill> --global -y < /dev/null
```
Notas operacionais:
- O CLI mostra `■ Failed to install 1` por repo — é uma skill **secundária** do repo, não o alvo;
  o alvo entra normalmente. Validar sempre por `ls ~/.claude/skills`, não pela mensagem.
- **Colisão:** `react-best-practices` (0xbigboss/claude-code) sobrescreveu a homônima da Vercel.
  A versão Vercel continua disponível como `vercel-react-best-practices`.

Lista por domínio (repo → skill):
- **Arquitetura/refactor:** mattpocock/skills→improve-codebase-architecture, handoff
- **Svelte/SvelteKit:** sveltejs/ai-tools→svelte-code-writer, svelte-core-bestpractices;
  ejirocodes/agent-skills→svelte5-best-practices; spences10/svelte-skills-kit→sveltekit-structure;
  vercel-labs/json-render→svelte, shadcn-svelte
- **React/Next:** vercel-labs/json-render→react; google-labs-code/stitch-skills→react:components;
  vercel-labs/next-skills→next-best-practices, next-cache-components, next-upgrade;
  vercel-labs/next-browser→next-browser; 0xbigboss/claude-code→react-best-practices;
  vercel-labs/agent-skills→vercel-react-native-skills, vercel-react-view-transitions, vercel-react-best-practices
- **UI/UX & design:** nextlevelbuilder/ui-ux-pro-max-skill→ui-ux-pro-max; shadcn/ui→shadcn;
  vercel-labs/agent-skills→web-design-guidelines; anthropics/skills→skill-creator
- **JS/TS:** github/awesome-copilot→javascript-typescript-jest; sickn33/antigravity-awesome-skills→
  javascript-mastery, typescript-expert, nodejs-best-practices; wshobson/agents→typescript-advanced-types,
  nodejs-backend-patterns; dotneet/claude-code-marketplace→typescript-react-reviewer;
  jeffallan/claude-skills→typescript-pro
- **Python:** wshobson/agents→python-performance-optimization, python-testing-patterns;
  jeffallan/claude-skills→fastapi-expert; vintasoftware/django-ai-plugins→django-expert;
  affaan-m/everything-claude-code→django-security
- **Go:** jeffallan/claude-skills→golang-pro; affaan-m/everything-claude-code→golang-patterns,
  golang-testing; samber/cc-skills-golang→golang-code-style
- **Rust:** apollographql/skills→rust-best-practices; github/awesome-copilot→rust-mcp-server-generator;
  claude-dev-suite/claude-dev-suite→actix-web
- **Node frameworks:** mcollina/skills→fastify-best-practices; jeffallan/claude-skills→rails-expert
- **Segurança/infra:** openai/skills→security-best-practices; rysweet/amplihack→cybersecurity-analyst;
  aradotso/security-skills→anthropic-cybersecurity-skills (754 skills MITRE/NIST);
  xixu-me/skills→github-actions-docs, secure-linux-web-hosting; aj-geddes/useful-ai-prompts→code-review-analysis

> ⚠️ **Peso de contexto:** 72 skills standalone + skills dos plugins é muito. Se a seleção de skills
> do Claude começar a degradar, podar com `npx skills remove <skill>` (ou `ls ~/.claude/skills` e apagar
> dirs). Manter as de uso real, arquivar o resto.
