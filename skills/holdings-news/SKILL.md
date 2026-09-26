---
name: holdings-news
description: "Recent news and context for the largest holdings of a Financial Portfolios AI model portfolio, using a connected news or market-data connector."
---

<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# News on what it holds

Requires the Financial Portfolios AI connector.

1. `get_portfolio_allocation`; take the ten largest holdings.
2. If no news or market-data connector is available, say that one is needed and stop.
3. For each holding, resolve the ticker to a company with that connector, then fetch news
   from the last seven days. Skip holdings with nothing new.
4. One or two lines per holding, each attributed to its source. Keep the portfolio's data and
   the outside news visibly separate. Draw no buy or sell conclusion.

## Always

- Financial Portfolios AI data is informational and educational only: never a recommendation,
  advice or a suitability assessment.
- A portfolio with `delayed: true` is the public book, about 45 days old: give its `as_of` date
  and never present it as current.
- Performance comes only from `get_portfolio_performance` / `get_portfolio_metrics`; include their
  `disclaimer` in full and unaltered. Never compute a return from any other source.
- Attribute anything taken from another connector (news, prices, positions) to that connector.
