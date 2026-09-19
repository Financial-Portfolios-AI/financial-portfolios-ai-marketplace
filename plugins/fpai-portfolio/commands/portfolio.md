---
description: Summarize a Financial Portfolios AI model portfolio — holdings, allocation, recent changes and performance.
argument-hint: "[portfolio code, e.g. aggressive | balanced | defensive]"
---

Using the `financial-portfolios-ai` MCP tools, produce a clear briefing for the portfolio: **$ARGUMENTS** (if empty, first call `list_portfolios` and ask which one, or summarize each).

Do this:
1. `list_portfolios` to confirm the code and what the subscription includes.
2. `get_portfolio_allocation` for the current book — list the top holdings by weight and the cash weight.
3. `get_portfolio_concentration` for the sector mix, the dominant sector and the concentration figures. Use it rather than working them out by hand: it derives effective N from the weights, so those figures appear for a delayed book too, where the portal returns them as null.
4. `get_portfolio_changes` (last ~90 days) — what was added, removed, raised and cut, and how much of the book moved.
5. Summarize concisely: objective, number of holdings, largest positions and sectors, concentration, and the most recent change.
6. Offer the next step rather than doing it unprompted: `/performance` for how it has done, `/breadth` for what it shares with the other portfolios, or `open_portfolio_explorer` to browse it interactively.

Rules:
- Use ONLY data returned by the MCP tools. Do not invent tickers, weights or prices.
- All figures are the published **model** portfolio and are informational/simulated — **not investment advice**. Say so once.
- Weight changes are what the model did; they are not returns. If the user asks how it performed, that is `/performance`, which carries its own required disclosure.
- If a tool returns an entitlement/subscription error, tell the user which subscription unlocks it rather than guessing.
