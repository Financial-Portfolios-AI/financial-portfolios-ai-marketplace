---
description: What your model portfolios hold in common — most widely held stocks, overlap between books, and each one's dominant sector.
---

Show what the user's portfolios have in common.

1. `open_breadth_board` — it reads every portfolio and returns the cross-portfolio view in one call.
2. Report the most widely held names: how many portfolios hold each, the average weight where held, and the largest single weight.
3. Report the overlap between each pair, **distinguishing shared names from shared weight**. Two books can hold most of the same names and put very different money behind them.
4. Note anything listed in `unavailable` — the counts cover the rest only, so do not present a partial picture as the whole one.
5. Flag any book that is delayed or on a different date, since overlap partly reflects timing.

Rules:
- Breadth is not conviction. A name held everywhere at a token weight is not the same as one held twice at a large weight, and neither is a reason to own it.
- Use only what the tool returned. Not investment advice.
