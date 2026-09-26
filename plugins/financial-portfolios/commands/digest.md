---
description: A short recurring summary of what changed across your model portfolios — written to run on a schedule.
argument-hint: "[days, default 7]"
---

Produce a digest of what changed across the user's portfolios over the last **$ARGUMENTS** days (default 7).

1. `list_portfolios`.
2. For each subscribed portfolio, `get_portfolio_changes` with that number of days.
3. One short section per portfolio: whether anything changed, what was added and removed, the two or three largest weight moves in percentage points, and turnover.
4. Skip any portfolio whose `comparable` is false, with a one-line reason — usually too short a window, or a delayed book whose history ends about 45 days ago.
5. If nothing changed anywhere, say exactly that in one sentence.

Rules:
- Written for unattended use: **ask no questions**, and continue past anything unavailable rather than stopping.
- A quiet period is a result, not a failure. Report it plainly instead of padding.
- Weight changes are what the model did — they are not returns. For what performed well, use `/performance`.
- Keep it under roughly 200 words per portfolio.

To run this on a schedule, save it as a recurring Claude Cowork task or a ChatGPT task. Every tool it uses is read-only, so an unattended run proceeds without an approval prompt.
