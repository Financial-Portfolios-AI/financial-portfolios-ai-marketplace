---
description: Summarize a Financial Portfolios AI model portfolio — holdings, allocation, recent changes and performance.
argument-hint: "[portfolio code, e.g. aggressive | balanced | defensive]"
---

Using the `financial-portfolios-ai` MCP tools, produce a clear briefing for the portfolio: **$ARGUMENTS** (if empty, first call `list_portfolios` and ask which one, or summarize each).

Do this:
1. `list_portfolios` to confirm the code and what the subscription includes.
2. `get_portfolio_allocation` for the current book — list the top holdings by weight, the sector mix, and the cash weight.
3. `get_portfolio_history` (last ~90 days of publications) — note what changed at the most recent rebalance (names added / removed / held) versus the prior book.
4. Summarize concisely: objective, number of holdings, largest positions and sectors, and the most recent change.

Rules:
- Use ONLY data returned by the MCP tools. Do not invent tickers, weights or prices.
- All figures are the published **model** portfolio and are informational/simulated — **not investment advice**. Say so once.
- If a tool returns an entitlement/subscription error, tell the user which subscription unlocks it rather than guessing.
