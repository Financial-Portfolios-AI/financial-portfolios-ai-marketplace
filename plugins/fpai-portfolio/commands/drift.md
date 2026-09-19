---
description: Compare your real brokerage holdings against a model portfolio and report how far they have drifted. Reports only — proposes no trades.
argument-hint: "[portfolio code, e.g. aggressive | balanced | defensive]"
---

Report how far the user's own holdings have drifted from **$ARGUMENTS**.

1. Read current positions from a brokerage, custodian or portfolio-tracking MCP (SnapTrade, Truthifi, IBKR, …), read-only. Never ask for brokerage credentials or account numbers. If none is connected, say the check needs one and stop.
2. `list_portfolios` — confirm the target is `subscribed`. Alignment needs a subscription; if it is not, say so and stop.
3. `rebalance_portfolio` with the target and those positions.
4. Report, briefly:
   - Roughly how far the account is from the model, in one line.
   - The largest gaps by ticker: held weight vs target weight, in percentage points.
   - Anything held that the model does not hold, and anything in the model not held at all.
   - Any ticker that could not be matched between broker and model — say it was skipped rather than guessing a substitute.
5. If the account already matches closely, say exactly that. Being aligned is a result.

Rules:
- **This command proposes nothing.** Do not turn gaps into share quantities or order tickets — that is `/to-orders`, which needs a person looking at it. This one is safe to run on a schedule precisely because it stops here.
- Drift is arithmetic against a published model, not advice, and no suitability assessment has been performed.
