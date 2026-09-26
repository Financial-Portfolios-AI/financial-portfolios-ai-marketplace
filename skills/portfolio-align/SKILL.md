---
name: portfolio-align
description: "Align the user's holdings to a Financial Portfolios AI model portfolio: compute the arithmetic, then optionally propose order tickets that the user confirms and places."
---

<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# Align my account

Requires the Financial Portfolios AI connector.

1. Read positions from a connected brokerage, then `open_rebalance_studio` with them so the
   user can check them. Without panels, confirm them in text and call `rebalance_portfolio`.
2. Present the result as a table. Say plainly that nothing has been sent.
3. Only if the user asks: turn it into order tickets for their broker. Confirm each batch
   explicitly before anything is sent. There is no standing authorisation.
4. Never invent a price, balance or fill. Flag any symbol the broker does not recognise.

## Always

- Financial Portfolios AI data is informational and educational only: never a recommendation,
  advice or a suitability assessment.
- A portfolio with `delayed: true` is the public book, about 45 days old: give its `as_of` date
  and never present it as current.
- Performance comes only from `get_portfolio_performance` / `get_portfolio_metrics`; include their
  `disclaimer` in full and unaltered. Never compute a return from any other source.
- Attribute anything taken from another connector (news, prices, positions) to that connector.
