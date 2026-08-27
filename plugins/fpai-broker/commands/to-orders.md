---
description: Turn a Financial Portfolios AI rebalance into reviewable broker order tickets for a connected brokerage MCP. Proposes only — you confirm and execute.
argument-hint: "[portfolio code] [broker: ibkr | robinhood | alpaca | dry-run]"
---

Prepare broker order tickets that move the user's account toward the model portfolio **$ARGUMENTS**.
Follow the **broker-order-prep** skill. This command **proposes** orders; it never executes them.

Flow:
1. Get the target vs. current delta from the `financial-portfolios-ai` MCP (`rebalance_portfolio`, or read a `/rebalance` result already in context).
2. Read the account's **current positions and buying power** from the broker MCP (read-only calls only).
3. Build order tickets (symbol, side, quantity, order type, time-in-force) sized to the account — see the skill for sizing, rounding, and cash/PDT checks.
4. Present the tickets as a table and a total, with a clear **"review — nothing is sent"** banner.
5. STOP. Ask the user to confirm. Only if they explicitly confirm each order (or say "place all") do you call the broker MCP's order-placement tool — and if no broker is connected, or the broker is `dry-run`, just output the tickets.

Absolute rules — read the skill's safety section. Never place, modify or cancel an order without explicit per-batch user confirmation. Never guess account data. This is not investment advice.
