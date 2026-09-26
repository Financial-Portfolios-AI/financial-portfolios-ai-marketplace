<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# Financial Portfolios AI: agent guidance

For Codex, Cursor, Copilot and other agents that read `AGENTS.md`. Connect the Financial Portfolios
AI MCP server first (see README.md); the server's own instructions carry the same rules.

## Always

- Financial Portfolios AI data is informational and educational only: never a recommendation,
  advice or a suitability assessment.
- A portfolio with `delayed: true` is the public book, about 45 days old: give its `as_of` date
  and never present it as current.
- Performance comes only from `get_portfolio_performance` / `get_portfolio_metrics`; include their
  `disclaimer` in full and unaltered. Never compute a return from any other source.
- Attribute anything taken from another connector (news, prices, positions) to that connector.
- Never place, modify or cancel an order. Order tickets are only proposed: the user confirms each
  batch and places it. There is no standing authorisation. Never invent a price, balance or fill.
- Never ask for brokerage credentials or account numbers.
- A scheduled or unattended run is text only and read-only; it never prepares orders.

## Journeys

### start: Start here

Menu of what you can do with your Financial Portfolios AI model portfolios, and which extra connectors each needs. Use when the user asks what FP.ai can do or how to get started.

Use the `start_here` prompt's approach:
1. Call `list_portfolios`; note which are subscribed and which are delayed.
2. Check which other connectors are available in this conversation: a market-data or news
   connector, and a brokerage or aggregator connector. Do not call them.
3. Offer the journeys below in one short table, marking any whose connector is missing:
   access, show a portfolio, performance, holdings news, what the portfolios share, drift,
   align my account, and scheduled digests.
4. Ask which one they want and offer to start it.

### portfolio: Show me a portfolio

Show a Financial Portfolios AI model portfolio: holdings, sector mix, concentration and what changed recently. Use when the user asks to see a portfolio or "my holdings".

1. If no portfolio is named, `list_portfolios` and use the subscribed ones.
2. Prefer `open_portfolio_explorer` so the user can browse it. If panels are not shown,
   answer in text instead.
3. In text: `get_portfolio_allocation` (top holdings and cash), `get_portfolio_concentration`
   (sector mix, effective N), `get_portfolio_changes` for the last 90 days.
4. Offer the next step: performance, holdings news, or what it shares with the other books.

### performance: How has it done

How a Financial Portfolios AI model portfolio has performed against its benchmark, with risk statistics and best and worst holdings. Hypothetical and simulated.

1. `get_portfolio_performance`, then `get_portfolio_metrics` for best and worst holdings.
2. If `available` is false, report its `reason`; it is not an error and not zero.
3. Show the figures as returned, and then the `disclaimer` in full.

### holdings-news: News on what it holds

Recent news and context for the largest holdings of a Financial Portfolios AI model portfolio, using a connected news or market-data connector.

1. `get_portfolio_allocation`; take the ten largest holdings.
2. If no news or market-data connector is available, say that one is needed and stop.
3. For each holding, resolve the ticker to a company with that connector, then fetch news
   from the last seven days. Skip holdings with nothing new.
4. One or two lines per holding, each attributed to its source. Keep the portfolio's data and
   the outside news visibly separate. Draw no buy or sell conclusion.

### breadth: What the portfolios agree on

What Financial Portfolios AI model portfolios hold in common: most widely held stocks, overlap between books, and each one's dominant sector.

Prefer `open_breadth_board`. In text, report the most widely held names, the overlap between
each pair by name and by weight, and each book's dominant sector and effective N.

### drift: How far my account has drifted

Compare the user's real brokerage holdings against a Financial Portfolios AI model portfolio and report the drift. Reports only; proposes no trades.

1. Read positions read-only from a connected brokerage or aggregator. If none is connected,
   ask the user to paste `ticker,quantity` rows instead. Never ask for credentials.
2. `get_portfolio_allocation` for the model.
3. Show a table of model weight, account weight and difference, largest first. Flag names
   held in only one of the two.
4. Stop there. Prepare no orders. If they want to act, offer the "align my account" journey.

### align: Align my account

Align the user's holdings to a Financial Portfolios AI model portfolio: compute the arithmetic, then optionally propose order tickets that the user confirms and places.

1. Read positions from a connected brokerage, then `open_rebalance_studio` with them so the
   user can check them. Without panels, confirm them in text and call `rebalance_portfolio`.
2. Present the result as a table. Say plainly that nothing has been sent.
3. Only if the user asks: turn it into order tickets for their broker. Confirm each batch
   explicitly before anything is sent. There is no standing authorisation.
4. Never invent a price, balance or fill. Flag any symbol the broker does not recognise.

### keep-me-posted: Keep me posted

Offer the FP.ai automation templates. Every one is read-only: a scheduled run never
prepares, stages or places an order.

- `weekly-digest`: Weekly portfolio digest, Every Monday at 08:00 (Financial Portfolios AI only)
- `rebalance-alert`: New publication alert, Every weekday at 07:00 (Financial Portfolios AI only)
- `drift-watch`: Drift watch, Every Friday at 16:30 (Financial Portfolios AI + a brokerage or aggregator connector (e.g. SnapTrade, IBKR), read-only)
- `holdings-news`: Holdings news, Every weekday at 07:30 (Financial Portfolios AI + a news or market-data connector)
- `earnings-week`: Earnings this week, Every Sunday at 18:00 (Financial Portfolios AI + a market-data connector with an earnings calendar)
- `monthly-performance`: Monthly performance note, First day of each month at 09:00 (Financial Portfolios AI only)
- `research-digest`: Research digest, Every Thursday at 12:00 (Financial Portfolios AI only)

1. If the user named a template, use it; otherwise list these and ask which one.
2. If it needs a portfolio, `list_portfolios` and ask which subscribed one.
3. If it needs a connector that is not available, say which kind to add and stop.
4. Run it once now so the user sees the output, then explain how to schedule it in their client.
   The prompts are in automations/README.md.
