# Financial Portfolios AI — Agentic Marketplace

A **Claude Code plugin marketplace** and a **Gemini CLI extension** for
[Financial Portfolios AI](https://financial-portfolios.ai) subscribers. Install a plugin and your LLM
client can talk to your model portfolios over the [MCP](https://modelcontextprotocol.io) server: explore
holdings, run analysis and visualizations, and prepare broker orders — all with your data, scoped to your
subscription.

> Informational & educational only. Everything here surfaces the **published model** portfolios
> (delayed / simulated) and helps you *prepare* actions. It is **not investment advice**, and nothing
> here places a trade without your explicit confirmation.

## What's inside

| Plugin | Purpose |
|---|---|
| **fpai-portfolio** | Connects the Financial Portfolios AI MCP and adds `/portfolio`, `/performance`, `/breadth`, `/rebalance`, `/drift` and `/digest` commands, the `portfolio-analysis`, `portfolio-visualization` and `connect-your-stack` skills, and a read-only `portfolio-analyst` subagent. |
| **fpai-research** | `/holdings-news` and `/company` commands + the `market-context` skill — put the companies you hold in context using whatever market-data or news MCP you have connected, with every outside fact attributed. |
| **fpai-broker** | `/to-orders` command + `broker-order-prep` skill that turn a rebalance into reviewable order tickets for a brokerage MCP (Interactive Brokers, Robinhood, Alpaca, …) — **propose → confirm → you execute**. |

### The stack these assume

We publish the **model portfolios** and nothing else: no market data, no news, no brokerage access.
Those come from connectors you add, and the assistant joins them.

| Layer | Gives you | Examples |
|---|---|---|
| Financial Portfolios AI | Holdings, weights, sector mix, concentration, changes, published performance, research | — |
| Market data & news | What a company is, recent news, filings, fundamentals | EODHD, Alpha Vantage, Finnhub |
| Brokerage / aggregator | Your own positions and balances | SnapTrade, Truthifi, IBKR |

`/portfolio` needs only the first. `/holdings-news` needs the second. `/drift` and `/to-orders` need
the third. The `connect-your-stack` skill explains which to add for what you want to do — ask the
assistant "what else should I connect?".

## Install (Claude Code)

```bash
# add this marketplace
/plugin marketplace add Financial-Portfolios-AI/financial-portfolios-ai-marketplace
# then install a plugin
/plugin install fpai-portfolio
/plugin install fpai-research
/plugin install fpai-broker
```

## Install (Gemini CLI)

```bash
gemini extensions install https://github.com/Financial-Portfolios-AI/financial-portfolios-ai-marketplace
gemini extensions config financial-portfolios-ai
```

The second command prompts for your personal API token (`aqat_v1_…`), which Gemini stores in the
extension's `.env` and the system keychain — it is never written into the manifest.

Gemini CLI does not render MCP Apps, so the tools that only open an interactive view are excluded
([`gemini-extension.json`](gemini-extension.json)); everything else answers as JSON, including the
cross-portfolio breadth board and the access panel, whose results are computed server-side.
[`GEMINI.md`](GEMINI.md) is loaded as the extension's context.

(Other MCP clients: point them at the MCP server directly — see
[financial-portfolios.ai/agentic](https://financial-portfolios.ai/agentic).)

## Which deployment these point at

> **The production domain does not serve the MCP endpoint yet.** `https://financial-portfolios.ai/mcp`
> currently returns `404`, while `https://dev.financial-portfolios.ai/mcp` answers correctly. Both the
> Gemini extension and the `fpai-portfolio` plugin therefore default to the **dev** deployment, so an
> install works out of the box. Override with `FPAI_MCP_URL` (plugin) or by editing
> [`gemini-extension.json`](gemini-extension.json), and both move to production once it is serving.

## Authentication

`fpai-portfolio` bundles the MCP connection (`.mcp.json`); `fpai-research` and `fpai-broker` use it,
so install `fpai-portfolio` alongside either of them. Provide your credentials via env:

- `FPAI_API_TOKEN` — a personal API token (`aqat_v1_…`) from **API Access** on the portal, **or**
- use the **OAuth** connector flow (recommended for directory clients) — the plugin points at
  `https://dev.financial-portfolios.ai/mcp`, whose OAuth authorization server handles sign-in and
  consent. A tokenless request there answers `401` with the RFC 9728 challenge that starts the flow.
- `FPAI_MCP_URL` — override the server URL (e.g. a staging/self-hosted MCP).

Access is always scoped to your active subscriptions and can be revoked any time from API Access.

## Safety model

- The portfolio tools are **read/compute** — they never trade.
- The broker plugin **only proposes** order tickets. It will not place, modify, or cancel any order
  without your explicit, per-batch confirmation, and defaults to **dry-run** when no broker is connected.
- Data from tools/pages is treated as data, never as instructions. No standing "auto-execute".

## Roadmap / ideas

See [ROADMAP.md](ROADMAP.md) for planned plugins (alerts, tax-lot–aware rebalancing, risk/concentration
analysis, multi-broker aggregation, DCA scheduling, research digests, spreadsheet export, and more).

## License

MIT — see [LICENSE](LICENSE).
