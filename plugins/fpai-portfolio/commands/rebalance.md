---
description: Compute buy/sell/hold orders to align your holdings with a Financial Portfolios AI model portfolio.
argument-hint: "[portfolio code] [path to your holdings CSV: ticker,quantity]"
---

Align the user's current holdings to the model portfolio **$ARGUMENTS** using the `financial-portfolios-ai` MCP.

Steps:
1. Get the holdings without making the user retype them. If a brokerage, custodian or portfolio-tracking MCP is connected (SnapTrade, Truthifi, IBKR, …), read the positions from there, read-only. Never ask for brokerage credentials or account numbers.
2. Open `open_rebalance_studio`, passing those holdings. It shows them in an editable table so the user can correct them before anything is calculated — a broker read can be stale, partial, or cover a different account than they mean. With nothing to read from, the panel is also where they paste or type them; `get_rebalance_template` gives the CSV columns (`ticker,quantity`). If the client cannot render the panel, collect the holdings in the conversation and call `rebalance_portfolio` directly.
3. Present the result as a table: ticker · action · current weight → target weight · Δ · suggested shares · est. notional. Group BUYs, SELLs, then HOLDs. Show the total turnover.
4. Call out anything notable: large single trades, names being fully exited, new positions, and the cash impact.

Rules:
- The output is a **model-alignment calculation**, informational and simulated — **not investment advice or an order**. Say so.
- Do NOT place, route or execute any trade here. To turn these into broker order tickets, hand off to the `fpai-broker` plugin's `/to-orders` command, which still requires explicit confirmation.
- Never fabricate prices or quantities — use only what `rebalance_portfolio` returns.
- For a recurring check, point the user at `/drift`, which reports how far the account has moved and proposes nothing — the part that is safe to run on a schedule.
