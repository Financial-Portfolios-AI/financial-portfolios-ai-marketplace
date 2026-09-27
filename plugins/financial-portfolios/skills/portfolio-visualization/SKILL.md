---
name: portfolio-visualization
description: Turn Financial Portfolios AI model-portfolio data into clear visuals — allocation donut, sector bars, concentration, change diffs and the published performance series. Use when the user asks for a chart, graph, or visual of a portfolio.
---

# Portfolio visualization

Chart only values the `financial-portfolios-ai` MCP tools return.

## Panels first

Where the client renders MCP Apps (claude.ai, Claude Desktop, ChatGPT, VS Code), the interactive panels
are the best visual: `open_portfolio_explorer` for one book, `open_breadth_board` across books,
`open_rebalance_studio` for alignment. Build charts yourself only when panels are not shown or the user
wants a specific chart or a file.

## Chart catalogue

| Chart | Data | Notes |
|---|---|---|
| Allocation donut | `get_portfolio_allocation` | Group the long tail into "Other"; label cash. |
| Sector bars | `get_portfolio_concentration` | Sector weights as returned. |
| Concentration | `get_portfolio_concentration` | Top 5 / top 10 / largest, effective N; a treemap works for weights. |
| Change diff | `get_portfolio_changes` | Opened / closed / raised / cut, with turnover. |
| Holdings over time | `get_portfolio_history` | Weight of the top names across snapshots. |
| Published performance | `get_portfolio_performance` | The portfolio and benchmark series and statistics exactly as returned, with the `disclaimer` beneath. If `available` is false, show the `reason` instead of a chart. |
| Best / worst holdings | `get_portfolio_metrics` | As returned. |

Never draw a growth or return curve from prices fetched elsewhere, or reconstruct one from weights.

## Output format

- In a client that renders HTML/artifacts, emit a **single self-contained HTML** snippet with inline
  SVG/Canvas — no external scripts or network calls. Keep it responsive and theme-neutral.
- In a text-only client, emit a compact Markdown table and, if helpful, an ASCII bar chart.
- Use one colour per sector, the same in every chart, so the donut, bars and reports agree.
- Caption every chart with the portfolio, its `as_of` date (and "delayed" if it is the public book),
  and: *model portfolio, informational only — not investment advice.* Performance charts also carry the
  `disclaimer` in full.

## Rules

- Never fabricate data points to "complete" a chart — show only what the MCP returned; label gaps.
