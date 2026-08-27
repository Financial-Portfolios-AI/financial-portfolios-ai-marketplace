---
description: Compute buy/sell/hold orders to align your holdings with a Financial Portfolios AI model portfolio.
argument-hint: "[portfolio code] [path to your holdings CSV: ticker,quantity]"
---

Align the user's current holdings to the model portfolio **$ARGUMENTS** using the `financial-portfolios-ai` MCP.

Steps:
1. If the user has not provided a holdings file, call `get_rebalance_template` and show the expected CSV columns (`ticker,quantity`), then ask them to paste or point to their holdings.
2. Call `rebalance_portfolio` with the target portfolio code and the user's holdings. This returns the model-aligned buy / sell / hold actions with target weights.
3. Present the result as a table: ticker · action · current weight → target weight · Δ · suggested shares · est. notional. Group BUYs, SELLs, then HOLDs. Show the total turnover.
4. Call out anything notable: large single trades, names being fully exited, new positions, and the cash impact.

Rules:
- The output is a **model-alignment calculation**, informational and simulated — **not investment advice or an order**. Say so.
- Do NOT place, route or execute any trade here. To turn these into broker order tickets, hand off to the `fpai-broker` plugin's `/to-orders` command, which still requires explicit confirmation.
- Never fabricate prices or quantities — use only what `rebalance_portfolio` returns.
