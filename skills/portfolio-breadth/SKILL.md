---
name: portfolio-breadth
description: "What Financial Portfolios AI model portfolios hold in common: most widely held stocks, overlap between books, and each one's dominant sector."
---

<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# What the portfolios agree on

Requires the Financial Portfolios AI connector.

Prefer `open_breadth_board`. In text, report the most widely held names, the overlap between
each pair by name and by weight, and each book's dominant sector and effective N.

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
