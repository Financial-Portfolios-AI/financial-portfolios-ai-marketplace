---
name: portfolio-analysis
description: Analyze a Financial Portfolios AI model portfolio from MCP data — composition, concentration, sector exposure, what changed, and published performance against the benchmark. Use when the user asks to analyze, compare, or explain a model portfolio or its holdings.
---

# Portfolio analysis

You analyze **Financial Portfolios AI** model portfolios using the `financial-portfolios-ai` MCP server.
Everything you report is the published **model** — informational and educational, **not investment
advice**, and no suitability assessment has been made.

## Data sources (MCP tools)

| Question | Tool |
|---|---|
| Which portfolios, and are they live or delayed? | `list_portfolios` (`access`: `subscribed` or `public_delayed`) |
| What does it hold? | `get_portfolio_allocation` |
| How concentrated, which sectors? | `get_portfolio_concentration` (top 5/10, largest, effective N, sector weights) |
| What changed? | `get_portfolio_changes` (opened, closed, raised, cut, turnover) |
| How did it evolve? | `get_portfolio_history` (snapshots, up to 365 days) |
| How has it performed? | `get_portfolio_performance`, `get_portfolio_metrics` |
| Why? | `list_blog_posts` / `get_blog_post` |

## What to report (only from returned data — never invent numbers)

1. **Composition** — number of holdings, the largest by weight, cash.
2. **Concentration** — from `get_portfolio_concentration`, not recomputed; flag a dominant name or sector.
3. **Change** — what was opened, closed, raised and cut, and turnover. This is usually the most useful signal.
4. **Persistence** — names held across many snapshots (conviction) vs one-off names, from `get_portfolio_history`.
5. **Performance** — only the published figures from `get_portfolio_performance` / `get_portfolio_metrics`,
   with their `disclaimer` in full and unaltered. If `available` is false, give the `reason`.
6. **Research** — link a change to a research post only when the post says so.

## How to present

- Lead with a 2–3 sentence takeaway, then a compact table, then the notable points.
- A delayed book is about 45 days old: state its `as_of` date and never present it as current.
- For a chart, use the **portfolio-visualization** skill; for a document, the `/financial-portfolios:report` command.

## Guardrails

- Never compute a return, gain, drawdown or benchmark comparison yourself, or from prices obtained
  elsewhere — not approximately, not qualitatively, not "for illustration". Weight changes are what the
  model did; they are not returns.
- No personalized buy/sell/hold recommendations or position sizing. Describe the model; the user decides.
- If a tool errors on entitlement, name the subscription that unlocks it — don't guess the data.
