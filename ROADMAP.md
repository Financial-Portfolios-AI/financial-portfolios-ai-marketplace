# Roadmap / ideas

Candidate plugins and skills for the Financial Portfolios AI agentic marketplace. Each stays within the
posture: surface the model, help the user *prepare* actions, never auto-trade, never give personalized
advice.

## Analysis & insight
- **fpai-compare** — compare two portfolios (or a portfolio vs SPY/QQQ) on composition, overlap, sector
  tilt, and since-inception stats; produce a side-by-side table + chart.
- **fpai-risk** — concentration (top-N weight, single-name/sector caps), simple factor/style read
  (size, momentum, sector), and a drawdown/vol summary where price data is available.
- **fpai-explain** — "why is this name in the book?" using the leadership-signal breakdown (momentum
  legs, 52-wk-high proximity) once the portal exposes per-stock selection signals (see the portal's
  selection-explainability design). Frame as *signals behind selection*, not advice.
- **fpai-research-digest** — pull the latest commentary (`list_blog_posts`/`get_blog_post`) and produce a
  weekly digest tied to what changed in the books.

## Action preparation (still propose → confirm)
- **fpai-tax** — tax-lot–aware rebalancing: prefer long-term lots, flag wash-sale windows, optional
  loss-harvesting variant of the order tickets. Informational, US-centric caveats.
- **fpai-dca** — turn a target book into a dollar-cost-averaging schedule (e.g. N tranches over M weeks)
  and emit each tranche as reviewable tickets.
- **fpai-multi-broker** — aggregate positions across several brokerage MCPs, net the deltas once, then
  route per-broker tickets (still per-batch confirmation).
- **fpai-cash-deploy** — given new cash, propose buys that move toward the model without selling.

## Integrations
- **Market-data / news MCPs** — enrich analysis with quotes, fundamentals, and headlines (read-only).
- **Spreadsheet / export** — write holdings, changes, and order tickets to CSV / Google Sheets / Excel.
- **Notifications** — on a new publication, summarize the change and (optionally) draft the rebalance.
- **Charting artifacts** — richer visuals (allocation treemap, sector heatmap, contribution waterfall).

## Client coverage
- Ship ready-made configs/manifests for Claude (Connectors + Desktop), ChatGPT (Custom GPT Actions),
  Gemini, Cursor, and Windsurf — mirroring the portal's API Access → Connectors page.

## Platform
- **Eval suite** — golden transcripts per command/skill so changes don't regress behavior or safety.
- **Versioning & changelog** — semver per plugin; a top-level CHANGELOG.
- **CI** — lint the marketplace/plugin manifests and validate `.mcp.json` on every PR.

Contributions welcome — open an issue with the use case and the tools it needs.
