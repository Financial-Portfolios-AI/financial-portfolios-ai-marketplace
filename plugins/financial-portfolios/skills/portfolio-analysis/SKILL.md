---
name: portfolio-analysis
description: Analyze a Financial Portfolios AI model portfolio from MCP data — allocation drift, concentration, sector exposure, rebalance changes, and performance vs benchmark. Use when the user asks to analyze, compare, or explain a model portfolio or its holdings.
---

# Portfolio analysis

You analyze **Financial Portfolios AI** model portfolios using the `financial-portfolios-ai` MCP server.
Everything you report is the published, delayed/simulated **model** — informational, **not investment advice**.

## Data sources (MCP tools)
- `list_portfolios` — the portfolios the subscription includes.
- `get_portfolio_allocation` — current target book (ticker, weight, sector).
- `get_portfolio_history` — past published books (to measure change over time).
- `list_blog_posts` / `get_blog_post` — the research/commentary behind the model.

## What to compute (only from returned data — never invent numbers)
1. **Composition** — number of holdings, top-N by weight, sector distribution, cash weight. Note if the book is roughly equal-weight (it usually is by design).
2. **Concentration** — largest position and top-5 / top-10 weight share; flag single-name or single-sector concentration.
3. **Change over time** — diff the latest book vs the previous publication: names **added / removed / held**, and how sector weights shifted. This is the most useful signal.
4. **Persistence** — names held across many consecutive publications (conviction) vs one-off names.
5. **Performance context** — if the client also has price/history access, describe the trajectory qualitatively; do not overstate precision.

## How to present
- Lead with a 2–3 sentence takeaway, then a compact table, then the notable points.
- Prefer tables for holdings/changes; keep prose tight.
- Always attach the one-line disclaimer: *model portfolio, delayed/simulated, informational only — not investment advice.*
- If the user wants a chart, hand off to the **portfolio-visualization** skill.

## Guardrails
- Do not give personalized buy/sell/hold recommendations or position sizing advice. Describe the model; the user decides.
- If a tool errors on entitlement, name the subscription that unlocks it — don't guess the data.
