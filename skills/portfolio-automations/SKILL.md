---
name: portfolio-automations
description: "Predefined, read-only recurring tasks for Financial Portfolios AI (weekly digest, publication alert, drift watch, holdings news, earnings week, monthly performance, research digest). Use when the user wants to automate, schedule or be kept posted about their model portfolios."
---

<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# Automation templates

Offer these when the user wants something to run on a schedule. Every template is read-only:
a scheduled run never prepares, stages or places an order, whatever the user asks for.

| Template | What | Cadence | Needs |
|---|---|---|---|
| `weekly-digest` | Weekly portfolio digest | Every Monday at 08:00 | Financial Portfolios AI only |
| `rebalance-alert` | New publication alert | Every weekday at 07:00 | Financial Portfolios AI only |
| `drift-watch` | Drift watch | Every Friday at 16:30 | Financial Portfolios AI + a brokerage or aggregator connector (e.g. SnapTrade, IBKR), read-only |
| `holdings-news` | Holdings news | Every weekday at 07:30 | Financial Portfolios AI + a news or market-data connector |
| `earnings-week` | Earnings this week | Every Sunday at 18:00 | Financial Portfolios AI + a market-data connector with an earnings calendar |
| `monthly-performance` | Monthly performance note | First day of each month at 09:00 | Financial Portfolios AI only |
| `research-digest` | Research digest | Every Thursday at 12:00 | Financial Portfolios AI only |

## How to schedule

- **Claude Cowork / Claude Desktop:** create a scheduled task with the prompt and cadence below.
- **Claude Code:** `/schedule` with the prompt, or the `/financial-portfolios:schedule` command.
- **ChatGPT:** ask "run this every <cadence>" with the prompt; ChatGPT creates a scheduled task.
- **Gemini (Spark):** paste the prompt with the cadence at the start ("Every Monday at 8am, ...").

Replace [your portfolio, e.g. AQA_BALANCED] with a real code; `list_portfolios` gives them. If a template needs a
connector the user lacks, say which kind to add instead of scheduling a task that will fail.

## Prompts

### weekly-digest

Cadence: Every Monday at 08:00

```
Using Financial Portfolios AI, summarise what changed in each portfolio I subscribe to over the
last 7 days: additions, removals, the three largest weight changes and turnover. Skip any
portfolio with no changes. If nothing changed anywhere, reply with one sentence.
```

### rebalance-alert

Cadence: Every weekday at 07:00

```
Using Financial Portfolios AI, check whether any portfolio I subscribe to has published a new
allocation in the last 24 hours. If so, list what was added, removed, raised and cut. If not,
reply "No new publications."
```

### drift-watch

Cadence: Every Friday at 16:30

```
Read my positions from my brokerage connector (read-only) and compare them with the Financial
Portfolios AI model portfolio [your portfolio, e.g. AQA_BALANCED]. Report only holdings whose weight differs from the
model by more than 2 percentage points, plus names held in only one of the two. Do not prepare
or place any orders. If nothing exceeds the threshold, reply with one sentence.
```

### holdings-news

Cadence: Every weekday at 07:30

```
Take the ten largest holdings of my Financial Portfolios AI portfolio [your portfolio, e.g. AQA_BALANCED]. Using my news
connector, list any news from the last 24 hours on those companies, one line each with its
source. Skip companies with no news. Draw no buy or sell conclusions.
```

### earnings-week

Cadence: Every Sunday at 18:00

```
Using my market-data connector, list which holdings of my Financial Portfolios AI portfolios
report earnings in the coming week, with the date and the portfolios that hold each one.
```

### monthly-performance

Cadence: First day of each month at 09:00

```
Using Financial Portfolios AI, give the published performance of each portfolio I subscribe to,
with its best and worst holdings. Include the disclaimer that comes with the figures, in full.
Do not calculate any figure yourself.
```

### research-digest

Cadence: Every Thursday at 12:00

```
Using Financial Portfolios AI, summarise research posts published in the last 7 days, in two
lines each, and flag any that mention a ticker held in my portfolios. If there are none, reply
with one sentence.
```

## Always

- Financial Portfolios AI data is informational and educational only: never a recommendation,
  advice or a suitability assessment.
- A portfolio with `delayed: true` is the public book, about 45 days old: give its `as_of` date
  and never present it as current.
- Performance comes only from `get_portfolio_performance` / `get_portfolio_metrics`; include their
  `disclaimer` in full and unaltered. Never compute a return from any other source.
- Attribute anything taken from another connector (news, prices, positions) to that connector.
