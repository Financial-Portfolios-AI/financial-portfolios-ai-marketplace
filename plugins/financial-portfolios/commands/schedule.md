---
description: Set up a recurring, read-only Financial Portfolios task from a predefined template (digest, drift watch, holdings news, ...).
argument-hint: "[weekly-digest | rebalance-alert | drift-watch | holdings-news | earnings-week | monthly-performance | research-digest | monthly-report]"
---

<!-- Generated from automations/templates.yaml by scripts/build.py. Do not edit. -->

Help the user schedule the Financial Portfolios automation template **$ARGUMENTS**.

1. Use the `automation-templates` skill. If no template was named, show its table and ask which one.
2. If the template has `{portfolio}` in it, `list_portfolios` and ask which subscribed portfolio to use.
3. If it needs a connector that is not available, say which kind to add and stop.
4. Run the prompt once now so the user sees the output.
5. Then schedule it at the template's cadence with `/schedule` (or tell them how in Cowork, ChatGPT or Gemini).

Every template is read-only. Do not schedule anything that prepares or places orders.
