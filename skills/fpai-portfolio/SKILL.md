---
name: fpai-portfolio
description: "Show a Financial Portfolios AI model portfolio: holdings, sector mix, concentration and what changed recently. Use when the user asks to see a portfolio or \"my holdings\"."
---

<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# Show me a portfolio

Requires the Financial Portfolios AI connector.

1. If no portfolio is named, `list_portfolios` and use the subscribed ones.
2. Prefer `open_portfolio_explorer` so the user can browse it. If panels are not shown,
   answer in text instead.
3. In text: `get_portfolio_allocation` (top holdings and cash), `get_portfolio_concentration`
   (sector mix, effective N), `get_portfolio_changes` for the last 90 days.
4. Offer the next step: performance, holdings news, or what it shares with the other books.

## Always

- Financial Portfolios AI data is informational and educational only: never a recommendation,
  advice or a suitability assessment.
- A portfolio with `delayed: true` is the public book, about 45 days old: give its `as_of` date
  and never present it as current.
- Performance comes only from `get_portfolio_performance` / `get_portfolio_metrics`; include their
  `disclaimer` in full and unaltered. Never compute a return from any other source.
- Attribute anything taken from another connector (news, prices, positions) to that connector.
