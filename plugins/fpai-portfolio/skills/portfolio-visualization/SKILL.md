---
name: portfolio-visualization
description: Turn Financial Portfolios AI model-portfolio data into clear visuals — allocation donut, sector bars, weight tables, holdings-change diffs, and (where price data is available) a growth curve. Use when the user asks for a chart, graph, or visual of a portfolio.
---

# Portfolio visualization

Build clean, self-contained visuals from `financial-portfolios-ai` MCP data. Only chart values the tools return.

## Chart choices
- **Allocation donut / pie** — current holding weights (group the long tail into "Other"; label cash).
- **Sector bar chart** — weight by sector.
- **Holdings table** — ticker · company · sector · weight, sorted by weight.
- **Change diff** — a two-column added / removed list plus a "held" count, from the latest vs previous book (`get_portfolio_history`).
- **Growth curve** — only if the client can access price/performance data; otherwise say so and skip.

## Output format
- In a client that renders HTML/artifacts (e.g. Claude), emit a **single self-contained HTML** snippet with inline SVG/Canvas — no external scripts or network calls. Keep it responsive and theme-neutral.
- In a text-only client, emit a compact Markdown table and, if helpful, an ASCII bar chart.
- Always include a short caption + the disclaimer: *model portfolio, delayed/simulated, informational only — not investment advice.*

## Rules
- Never fabricate data points to "complete" a chart — show only what the MCP returned; label gaps.
- Keep colors sector-consistent when you draw both a donut and a sector bar.
