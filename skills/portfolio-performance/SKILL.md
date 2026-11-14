---
name: portfolio-performance
description: "How a Financial Portfolios AI model portfolio has performed against its benchmark, with risk statistics and best and worst holdings. Hypothetical and simulated."
---

<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# How has it done

Requires the Financial Portfolios AI connector.

1. `get_portfolio_performance`, then `get_portfolio_metrics` for best and worst holdings.
2. If `available` is false, report its `reason`; it is not an error and not zero.
3. Show the figures as returned, and then the `disclaimer` in full.

## Always

- Financial Portfolios AI data is informational and educational only: never a recommendation,
  advice or a suitability assessment.
- A portfolio with `delayed: true` is the public book, about 45 days old: give its `as_of` date
  and never present it as current.
- Performance comes from `get_portfolio_performance` / `get_portfolio_metrics`; include their
  `disclaimer` in full and unaltered. If the user supplies their own prices and asks for a
  recalculation, you may work it out from the `get_portfolio_history` weights, held forward between
  snapshots, but label it as the user's own hypothetical calculation from their data - never the
  publisher's figure - and say it may differ from the website.
- Attribute anything taken from another connector (news, prices, positions) to that connector.
