---
description: What a ticker in your model portfolios actually is — the company, its sector, and where it sits across the portfolios.
argument-hint: "[ticker, e.g. NVDA]"
---

Explain the holding **$ARGUMENTS**.

1. Find where it sits: `open_breadth_board`, or `get_portfolio_allocation` per portfolio — which
   portfolios hold it, at what weight, and its rank within each.
2. Resolve the ticker to a company through a connected market-data MCP. Do not guess from the symbol;
   share classes and non-US listings collide. `get_portfolio_metrics` also returns company names for
   the most-held holdings and is a good cross-check.
3. Describe the company: what it does, sector, and any recent development worth knowing.
4. Say whether the books you read are live or delayed, and their dates.

Rules:
- Attribute outside facts to their source; keep them separate from the portfolio data.
- If the ticker maps to more than one plausible security, say so and ask rather than picking one.
- If no market-data connector is available, report the portfolio position and say the company detail
  needs one.
- Being held by a model is not a recommendation to own it. Not investment advice.
