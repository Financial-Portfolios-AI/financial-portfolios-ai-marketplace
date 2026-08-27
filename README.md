# Financial Portfolios AI — Agentic Marketplace

A **Claude Code plugin marketplace** of agentic extensions for
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
| **fpai-portfolio** | Connects the Financial Portfolios AI MCP and adds `/portfolio` + `/rebalance` commands, `portfolio-analysis` + `portfolio-visualization` skills, and a read-only `portfolio-analyst` subagent. |
| **fpai-broker** | `/to-orders` command + `broker-order-prep` skill that turn a rebalance into reviewable order tickets for a brokerage MCP (Interactive Brokers, Robinhood, Alpaca, …) — **propose → confirm → you execute**. |

## Install (Claude Code)

```bash
# add this marketplace
/plugin marketplace add Financial-Portfolios-AI/financial-portfolios-ai-marketplace
# then install a plugin
/plugin install fpai-portfolio
/plugin install fpai-broker
```

(Other MCP clients: point them at the MCP server directly — see
[financial-portfolios.ai/agentic](https://financial-portfolios.ai/agentic).)

## Authentication

The `fpai-portfolio` plugin bundles the MCP connection (`.mcp.json`). Provide your credentials via env:

- `FPAI_API_TOKEN` — a personal API token (`aqat_v1_…`) from **API Access** on the portal, **or**
- use the **OAuth** connector flow (recommended for directory clients) — the plugin points at
  `https://financial-portfolios.ai/mcp`, whose OAuth authorization server handles sign-in and consent.
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
