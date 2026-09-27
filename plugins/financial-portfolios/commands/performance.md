---
description: How a Financial Portfolios AI model portfolio has performed — against its benchmark, its risk statistics, and which holdings helped and hurt. Hypothetical and simulated.
argument-hint: "[portfolio code, e.g. aggressive | balanced | defensive]"
---

Report the published performance of **$ARGUMENTS** (if empty, call `list_portfolios` and ask which one).

1. `get_portfolio_performance`. If `available` is false, say why using the `reason` it returns — the price history is still being built — and stop. That is an answer, not an error.
2. Give the headline figures against the benchmark's: total and annualized return, volatility, Sharpe, Sortino, maximum drawdown, and the period they cover.
3. Give the relative figures — beta, alpha, information ratio, tracking error, correlation — each with one plain sentence saying what it describes.
4. `get_portfolio_metrics` for the best and worst performers and the win rate by name and by invested capital.
5. Say whether these are live or delayed figures, from `access` and `delayed`.

Rules:
- **Show the `disclaimer` field from the response with the figures, in full and unaltered.** These are hypothetical, simulated results computed from published model holdings and total-return prices — not the results of any account. Do not paraphrase that notice or move it somewhere it can be dropped.
- Never compute a return, gain, drawdown or benchmark comparison yourself, and never from prices obtained elsewhere. A figure derived that way is nobody's published number and will not match the website.
- Past figures say nothing about what comes next. This is not investment advice.
