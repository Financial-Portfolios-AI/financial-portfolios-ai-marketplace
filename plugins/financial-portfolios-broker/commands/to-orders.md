---
description: Turn a Financial Portfolios AI rebalance into reviewable broker order tickets for a connected brokerage MCP. Proposes only — you confirm and execute.
argument-hint: "[portfolio code] [broker: ibkr | robinhood | alpaca | dry-run]"
---

Prepare broker order tickets that move the user's account toward the model portfolio **$ARGUMENTS**.
Follow the **broker-order-prep** skill. This command **proposes** orders; it never executes them.

Flow:
1. Read the account's **current positions and buying power** from the broker MCP (read-only calls only). Do this first: the delta is computed *from* these, and the user should never retype what the broker already knows.
2. Get the delta from the `financial-portfolios-ai` MCP. Prefer `open_rebalance_studio`, passing the positions you just read — it shows them in an editable table so the user can correct them before any arithmetic runs, which matters because a broker read can be stale, partial, or cover a different account than they mean. Fall back to `rebalance_portfolio` directly, or reuse a `/rebalance` result already in context.
3. Build order tickets (symbol, side, quantity, order type, time-in-force) sized to the account — see the skill for sizing, rounding, and cash/PDT checks.
4. Present the tickets as a table and a total, with a clear **"review — nothing is sent"** banner.
5. STOP. Ask the user to confirm. Only if they explicitly confirm each order (or say "place all") do you call the broker MCP's order-placement tool — and if no broker is connected, or the broker is `dry-run`, just output the tickets.

Know what your broker's MCP will actually do, and say so before step 5: **SnapTrade is read-only** and cannot place anything; **IBKR accepts drafts only**, which you review and submit yourself on an IBKR platform; **Robinhood** trades in a separate Agentic account and makes per-trade review *optional*; **Public.com** executes without per-trade confirmation. The confirmation gate above applies regardless of which of those you are on — a broker that permits unattended execution does not make it acceptable here.

For a recurring check, use the `drift_check` prompt instead of this command. It reports how far the account has moved from the model and proposes nothing, which is the part that is safe to run on a schedule.

Absolute rules — read the skill's safety section. Never place, modify or cancel an order without explicit per-batch user confirmation. Never guess account data. This is not investment advice.
