<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

# Financial Portfolios automation templates

Recurring, read-only tasks. Paste one into your assistant's scheduler:

| Assistant | Where |
|---|---|
| Claude Cowork / Desktop | Scheduled tasks → New task, paste the prompt, pick the cadence |
| Claude Code | `/financial-portfolios:schedule <template>` |
| ChatGPT | Paste the prompt and add "every <cadence>"; ChatGPT creates the task |
| Gemini (Spark) | Paste the prompt, starting with the cadence |

Every template only reads. None of them prepares or places an order.

## Weekly portfolio digest

**Cadence:** Every Monday at 08:00 · **Needs:** Financial Portfolios AI only

```
Using Financial Portfolios AI, summarise what changed in each portfolio I subscribe to over the
last 7 days: additions, removals, the three largest weight changes and turnover. Skip any
portfolio with no changes. If nothing changed anywhere, reply with one sentence.
```

Gemini Spark / Muse: start the prompt with "Every Monday at 08:00, ".

## New publication alert

**Cadence:** Every weekday at 07:00 · **Needs:** Financial Portfolios AI only

```
Using Financial Portfolios AI, check whether any portfolio I subscribe to has published a new
allocation in the last 24 hours. If so, list what was added, removed, raised and cut. If not,
reply "No new publications."
```

Gemini Spark / Muse: start the prompt with "Every weekday at 07:00, ".

## Drift watch

**Cadence:** Every Friday at 16:30 · **Needs:** Financial Portfolios AI + a brokerage or aggregator connector (e.g. SnapTrade, IBKR), read-only

```
Read my positions from my brokerage connector (read-only) and compare them with the Financial
Portfolios AI model portfolio [your portfolio, e.g. AQA_BALANCED]. Report only holdings whose weight differs from the
model by more than 2 percentage points, plus names held in only one of the two. Do not prepare
or place any orders. If nothing exceeds the threshold, reply with one sentence.
```

Gemini Spark / Muse: start the prompt with "Every Friday at 16:30, ".

## Holdings news

**Cadence:** Every weekday at 07:30 · **Needs:** Financial Portfolios AI + a news or market-data connector

```
Take the ten largest holdings of my Financial Portfolios AI portfolio [your portfolio, e.g. AQA_BALANCED]. Using my news
connector, list any news from the last 24 hours on those companies, one line each with its
source. Skip companies with no news. Draw no buy or sell conclusions.
```

Gemini Spark / Muse: start the prompt with "Every weekday at 07:30, ".

## Earnings this week

**Cadence:** Every Sunday at 18:00 · **Needs:** Financial Portfolios AI + a market-data connector with an earnings calendar

```
Using my market-data connector, list which holdings of my Financial Portfolios AI portfolios
report earnings in the coming week, with the date and the portfolios that hold each one.
```

Gemini Spark / Muse: start the prompt with "Every Sunday at 18:00, ".

## Monthly performance note

**Cadence:** First day of each month at 09:00 · **Needs:** Financial Portfolios AI only

```
Using Financial Portfolios AI, give the published performance of each portfolio I subscribe to,
with its best and worst holdings. Include the disclaimer that comes with the figures, in full.
Do not calculate any figure yourself.
```

Gemini Spark / Muse: start the prompt with "First day of each month at 09:00, ".

## Research digest

**Cadence:** Every Thursday at 12:00 · **Needs:** Financial Portfolios AI only

```
Using Financial Portfolios AI, summarise research posts published in the last 7 days, in two
lines each, and flag any that mention a ticker held in my portfolios. If there are none, reply
with one sentence.
```

Gemini Spark / Muse: start the prompt with "Every Thursday at 12:00, ".

## Monthly portfolio report

**Cadence:** First business day of each month at 09:00 · **Needs:** Financial Portfolios AI only

```
Using Financial Portfolios AI, write a report on my portfolio [your portfolio, e.g. AQA_BALANCED] as text: the as-of
date, top holdings, sector mix and concentration, what changed in the last month, and the
published performance with its disclaimer in full. Calculate no figure yourself, create no
files and end with "Not investment advice."
```

Gemini Spark / Muse: start the prompt with "First business day of each month at 09:00, ".
