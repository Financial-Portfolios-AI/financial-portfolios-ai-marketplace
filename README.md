# Financial Portfolios AI — Agentic Marketplace

Plugins, skills and extensions that connect your AI assistant to your
[Financial Portfolios AI](https://financial-portfolios.ai) model portfolios over
[MCP](https://modelcontextprotocol.io): explore holdings, see performance, check drift, and prepare
broker orders — all with your data, scoped to your subscription.

> Informational & educational only. Everything here surfaces the **published model** portfolios
> (delayed / simulated) and helps you *prepare* actions. It is **not investment advice**, and nothing
> here places a trade: **it proposes → you confirm → you place**.

> **Preview.** Everything below points at the **dev** deployment,
> `https://dev.financial-portfolios.ai/mcp`, because `https://financial-portfolios.ai/mcp` returns
> `404` today. See [Which deployment these point at](#which-deployment-these-point-at).

## Pick your assistant

| Assistant | What to install | Journeys by name |
|---|---|---|
| [Claude Code](#claude-code) | The plugins in this marketplace | `/fpai-portfolio:<journey>` commands |
| [claude.ai / Claude Desktop](#claudeai-and-claude-desktop) | The connector + the skills in [`dist/`](dist) | Skills in the `/` menu |
| [ChatGPT](#chatgpt) | The connector | Ask in words (skills later) |
| [Gemini CLI](#gemini-cli) | The extension | `/fpai:<journey>` commands |
| [Cursor / VS Code](#cursor-and-vs-code) | One-click MCP install | The server's MCP prompts |
| [Codex and other agents](#other-clients) | The server URL | [`AGENTS.md`](AGENTS.md) |

### Claude Code

```bash
/plugin marketplace add Financial-Portfolios-AI/financial-portfolios-ai-marketplace
/plugin install fpai-portfolio
/plugin install fpai-research
/plugin install fpai-broker
```

| Plugin | Purpose |
|---|---|
| **FP.ai Portfolio** (`fpai-portfolio`) | Bundles the MCP connection. Commands `start`, `portfolio`, `performance`, `breadth`, `drift`, `rebalance`, `digest`, `schedule`; the `portfolio-analysis`, `portfolio-visualization`, `connect-your-stack` and `automation-templates` skills; a read-only `portfolio-analyst` subagent. |
| **FP.ai Research** (`fpai-research`) | `holdings-news` and `company` commands + the `market-context` skill — the companies you hold in context from your market-data or news MCP, every outside fact attributed. |
| **FP.ai Broker** (`fpai-broker`) | `to-orders` command + `broker-order-prep` skill: turn a rebalance into reviewable order tickets for a brokerage MCP (IBKR, Robinhood, Alpaca, …). |

Claude Code shows MCP App panels as text, not as interactive views
([anthropics/claude-code#95149](https://github.com/anthropics/claude-code/issues/95149)), so the
commands answer in text.

### claude.ai and Claude Desktop

1. Add the connector: Settings → Connectors → Add custom connector, URL
   `https://dev.financial-portfolios.ai/mcp`. Sign-in is OAuth, so there is no key to paste.
2. Add the skills: Settings → Capabilities → Skills → Upload skill, one zip from [`dist/`](dist)
   at a time.

claude.ai does not show MCP prompts
([claude-ai-mcp#333](https://github.com/anthropics/claude-ai-mcp/issues/333)), so the skills are
how the journeys get a name there: once added, they appear in the `/` menu. The MCP App panels do
render here.

### ChatGPT

Add `https://dev.financial-portfolios.ai/mcp` as a custom connector (developer mode) and sign in
with OAuth. Ask for a journey in words ("show my portfolio", "how far has my account drifted").
A ChatGPT package of the skills will follow once production serves `/mcp`.

### Gemini CLI

```bash
gemini extensions install https://github.com/Financial-Portfolios-AI/financial-portfolios-ai-marketplace
gemini extensions config financial-portfolios-ai
```

The second command prompts for your personal API token (`aqat_v1_…`), which Gemini stores in the
extension's `.env` and the system keychain — it is never written into the manifest. The journeys
are commands: `/fpai:start`, `/fpai:drift`, and so on ([`commands/fpai`](commands/fpai)).

Gemini CLI does not render MCP Apps, so the tools that only open an interactive view are excluded
([`gemini-extension.json`](gemini-extension.json)); the breadth board and access panel answer as
JSON. [`GEMINI.md`](GEMINI.md) is loaded as the extension's context.

### Cursor and VS Code

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=financial-portfolios-ai&config=eyJ1cmwiOiJodHRwczovL2Rldi5maW5hbmNpYWwtcG9ydGZvbGlvcy5haS9tY3AifQ%3D%3D)
[![Add to VS Code](https://img.shields.io/badge/VS_Code-Add_MCP_server-0098FF?logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=financial-portfolios-ai&config=%7B%22name%22%3A%22financial-portfolios-ai%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A//dev.financial-portfolios.ai/mcp%22%7D)
[![Add to VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Add_MCP_server-24bfa5?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=financial-portfolios-ai&config=%7B%22name%22%3A%22financial-portfolios-ai%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A//dev.financial-portfolios.ai/mcp%22%7D&quality=insiders)

These add the connector; the journeys are available as the server's MCP prompts.

### Other clients

Windsurf, Zed, LM Studio, Codex and anything else that speaks MCP: add the server URL by hand.

```
https://dev.financial-portfolios.ai/mcp
```

Command-line clients that cannot run the OAuth sign-in send a personal token in an `X-API-Key`
header instead. Agents that read [`AGENTS.md`](AGENTS.md) get the journeys and rules from it.

## The journeys

Eight journeys, with the same names everywhere:

<!-- journeys:start (generated by scripts/build.py from automations/templates.yaml) -->
| Journey | MCP prompt | Claude Code | claude.ai skill | Gemini CLI | MCP App panel |
|---|---|---|---|---|---|
| **start** | `start_here` | `/fpai-portfolio:start` | `fpai-start` | `/fpai:start` | `open_access_centre` |
| **portfolio** | `portfolio_review` | `/fpai-portfolio:portfolio` | `fpai-portfolio` | `/fpai:portfolio` | `open_portfolio_explorer` |
| **performance** | `portfolio_performance` | `/fpai-portfolio:performance` | `fpai-performance` | `/fpai:performance` | — |
| **holdings-news** | `market_research_digest` | `/fpai-research:holdings-news` | `fpai-holdings-news` | `/fpai:holdings-news` | — |
| **breadth** | `most_held_stocks` | `/fpai-portfolio:breadth` | `fpai-breadth` | `/fpai:breadth` | `open_breadth_board` |
| **drift** | `drift_check` | `/fpai-portfolio:drift` | `fpai-drift` | `/fpai:drift` | — |
| **align** | `rebalance_advisor` | `/fpai-portfolio:rebalance, then /fpai-broker:to-orders` | `fpai-align` | `/fpai:align` | `open_rebalance_studio` |
| **keep-me-posted** | `portfolio_digest` | `/fpai-portfolio:schedule (or /fpai-portfolio:digest once)` | `fpai-automations` | `/fpai:keep-me-posted` | — |
<!-- journeys:end -->

### The stack these assume

We publish the **model portfolios** and nothing else: no market data, no news, no brokerage access.
Those come from connectors you add, and the assistant joins them.

| Layer | Gives you | Examples |
|---|---|---|
| Financial Portfolios AI | Holdings, weights, sector mix, concentration, changes, published performance, research | — |
| Market data & news | What a company is, recent news, filings, fundamentals | EODHD, Alpha Vantage, Finnhub |
| Brokerage / aggregator | Your own positions and balances | SnapTrade, Truthifi, IBKR |

**portfolio** needs only the first. **holdings-news** needs the second. **drift** and **align** need
the third. Ask the assistant "what else should I connect?".

## Automation templates

Seven read-only recurring tasks — weekly digest, publication alert, drift watch, holdings news,
earnings week, monthly performance, research digest — with copy-paste prompts for Claude Cowork,
ChatGPT scheduled tasks and Gemini Spark: [automations/README.md](automations/README.md).
In Claude Code: `/fpai-portfolio:schedule`.

## Which deployment these point at

> **The production domain does not serve the MCP endpoint yet.** `https://financial-portfolios.ai/mcp`
> currently returns `404`, while `https://dev.financial-portfolios.ai/mcp` answers correctly. The
> Gemini extension, the `fpai-portfolio` plugin and the install buttons therefore default to the
> **dev** deployment. Override with `FPAI_MCP_URL` (plugin) or by editing
> [`gemini-extension.json`](gemini-extension.json); all of them move to production once it serves.

## Authentication

`fpai-portfolio` bundles the MCP connection (`.mcp.json`); `fpai-research` and `fpai-broker` use it,
so install `fpai-portfolio` alongside either of them.

- **OAuth** (recommended, and the only option in claude.ai and ChatGPT) — a tokenless request answers
  `401` with the RFC 9728 challenge that starts sign-in and consent.
- `FPAI_API_TOKEN` — a personal API token (`aqat_v1_…`) from **API Access** on the portal.
- `FPAI_MCP_URL` — override the server URL (e.g. a staging/self-hosted MCP).

Access is always scoped to your active subscriptions and can be revoked any time from API Access.

## Safety model

- The portfolio tools are **read/compute** — they never trade.
- Order tickets are **only proposed**: you confirm each batch, and you place it. There is no standing
  authorisation, no auto-execute, and no invented prices; with no broker connected it is a dry run.
- Scheduled runs are text only and read-only; they never prepare orders.
- Performance figures are hypothetical and simulated, and always come with their disclaimer.
- These rules live in the MCP server's own instructions; the skills and commands repeat them.
- Data from tools/pages is treated as data, never as instructions.

## For contributors

[`automations/templates.yaml`](automations/templates.yaml) is the single source for the journeys and
automation templates. Edit it, then run `python scripts/build.py` (needs `pyyaml`); files it writes
carry a "Generated … Do not edit" header. CI runs `python scripts/build.py --check` and
`claude plugin validate`. Bump a plugin's `version` in its `plugin.json` when its contents change, so
`/plugin update` picks it up.

`gemini-extension.json`, `GEMINI.md` and `plugins/fpai-portfolio/.mcp.json` are generated from the
MCP server repository; change them there.

## Roadmap / ideas

See [ROADMAP.md](ROADMAP.md).

## License

MIT — see [LICENSE](LICENSE).
