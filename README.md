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
| [Claude Code](#claude-code) | The plugins in this marketplace | `/financial-portfolios:<journey>` commands |
| [claude.ai / Claude Desktop](#claudeai-and-claude-desktop) | The connector + the skills in [`dist/`](dist) | Skills in the `/` menu |
| [ChatGPT](#chatgpt) | The connector | Ask in words (skills later) |
| [Gemini CLI](#gemini-cli) | The extension | `/financial-portfolios:<journey>` commands |
| [Cursor / VS Code](#cursor-and-vs-code) | One-click MCP install | The server's MCP prompts |
| [Codex and other agents](#other-clients) | The server URL | [`AGENTS.md`](AGENTS.md) |

### Claude Code

```bash
/plugin marketplace add Financial-Portfolios-AI/financial-portfolios-ai-marketplace
/plugin install financial-portfolios
/plugin install financial-portfolios-broker   # optional: only if you want order tickets
```

| Plugin | Purpose |
|---|---|
| **Financial Portfolios** (`financial-portfolios`) | Bundles the MCP connection. Commands `start`, `report`, `portfolio`, `performance`, `breadth`, `drift`, `rebalance`, `digest`, `schedule`, `holdings-news` and `company`; the `portfolio-analysis`, `portfolio-visualization`, `market-context`, `connect-your-stack` and `automation-templates` skills; a read-only `portfolio-analyst` subagent. |
| **Financial Portfolios Broker** (`financial-portfolios-broker`) | `to-orders` command + `broker-order-prep` skill: turn a rebalance into reviewable order tickets for a brokerage MCP (IBKR, Robinhood, Alpaca, …). A separate, opt-in install because it is the only plugin that prepares orders. |

> **Renamed.** The `fpai-portfolio`, `fpai-research` and `fpai-broker` plugins are now
> `financial-portfolios` (portfolio and research merged) and `financial-portfolios-broker`. If you
> installed the old ones, `/plugin uninstall` each `fpai-*` plugin and install the new names. The
> plugin's URL override is now `FINANCIAL_PORTFOLIOS_MCP_URL` (was `FPAI_MCP_URL`), and the claude.ai
> skills are renamed too (`fpai-start` → `portfolio-start`, …): remove the old ones and upload the new
> zips.

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
are commands: `/financial-portfolios:start`, `/financial-portfolios:drift`, and so on
([`commands/financial-portfolios`](commands/financial-portfolios)).

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

Nine journeys, with the same names everywhere. **report** builds a slide deck, PDF, Word
document, spreadsheet or CSV with the assistant's own document tools where it has them:

<!-- journeys:start (generated by scripts/build.py from automations/templates.yaml) -->
| Journey | MCP prompt | Claude Code | claude.ai skill | Gemini CLI | MCP App panel |
|---|---|---|---|---|---|
| **start** | `start_here` | `/financial-portfolios:start` | `portfolio-start` | `/financial-portfolios:start` | `open_access_centre` |
| **portfolio** | `portfolio_review` | `/financial-portfolios:portfolio` | `portfolio-overview` | `/financial-portfolios:portfolio` | `open_portfolio_explorer` |
| **performance** | `portfolio_performance` | `/financial-portfolios:performance` | `portfolio-performance` | `/financial-portfolios:performance` | — |
| **holdings-news** | `market_research_digest` | `/financial-portfolios:holdings-news` | `holdings-news` | `/financial-portfolios:holdings-news` | — |
| **breadth** | `most_held_stocks` | `/financial-portfolios:breadth` | `portfolio-breadth` | `/financial-portfolios:breadth` | `open_breadth_board` |
| **drift** | `drift_check` | `/financial-portfolios:drift` | `portfolio-drift` | `/financial-portfolios:drift` | — |
| **align** | `rebalance_advisor` | `/financial-portfolios:rebalance, then /financial-portfolios-broker:to-orders` | `portfolio-align` | `/financial-portfolios:align` | `open_rebalance_studio` |
| **report** | `portfolio_report` | `/financial-portfolios:report` | `portfolio-report` | `/financial-portfolios:report` | — |
| **keep-me-posted** | `portfolio_digest` | `/financial-portfolios:schedule (or /financial-portfolios:digest once)` | `portfolio-automations` | `/financial-portfolios:keep-me-posted` | — |
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

Eight read-only recurring tasks — weekly digest, publication alert, drift watch, holdings news,
earnings week, monthly performance, research digest, monthly report — with copy-paste prompts for Claude Cowork,
ChatGPT scheduled tasks and Gemini Spark: [automations/README.md](automations/README.md).
In Claude Code: `/financial-portfolios:schedule`.

## Which deployment these point at

> **The production domain does not serve the MCP endpoint yet.** `https://financial-portfolios.ai/mcp`
> currently returns `404`, while `https://dev.financial-portfolios.ai/mcp` answers correctly. The
> Gemini extension, the `financial-portfolios` plugin and the install buttons therefore default to the
> **dev** deployment. Override with `FINANCIAL_PORTFOLIOS_MCP_URL` (plugin) or by editing
> [`gemini-extension.json`](gemini-extension.json); all of them move to production once it serves.

## Authentication

`financial-portfolios` bundles the MCP connection (`.mcp.json`); `financial-portfolios-broker` uses
it, so install `financial-portfolios` alongside it.

- **OAuth** (recommended, and the only option in claude.ai and ChatGPT) — a tokenless request answers
  `401` with the RFC 9728 challenge that starts sign-in and consent.
- `FPAI_API_TOKEN` — a personal API token (`aqat_v1_…`) from **API Access** on the portal.
- `FINANCIAL_PORTFOLIOS_MCP_URL` — override the server URL (e.g. a staging/self-hosted MCP).

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

`gemini-extension.json`, `GEMINI.md` and `plugins/financial-portfolios/.mcp.json` are generated from the
MCP server repository; change them there.

## Roadmap / ideas

See [ROADMAP.md](ROADMAP.md).

## License

MIT — see [LICENSE](LICENSE).
