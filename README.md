# AI scheduled agents for personal finance

Three prompts I run every day as scheduled tasks in Claude. They read my email, my brokerage account and public market data, and tell me only what I need to know.

I built them for myself, then shared them with friends along with the connector setup. This repo is the cleaned-up version: no personal data, every account-specific rule turned into a variable.

| Prompt | What it does | Runs |
|---|---|---|
| [01 — Family budget daily report](prompts/01-family-budget-daily-report.md) | Reconciles bank and card notification emails against a monthly budget and tells you how much you can still spend per day | Daily, late evening |
| [02 — Portfolio crash radar](prompts/02-portfolio-crash-radar.md) | A read-only risk officer that watches market stress and price signals so you are never late to a major drawdown | Every market day, after the close |
| [03 — Insider cluster-buy radar](prompts/03-insider-cluster-buy-radar.md) | Scans SEC Form 4 filings for executives buying their own stock together after a selloff, and builds a full entry and exit plan when one passes | Every market day, after the open |

## Design principles

These are what make the prompts trustworthy enough to run unattended.

1. **Read-only by default.** The brokerage connector exposes tools that can place orders. Every prompt lists them as forbidden. The agent analyzes; you decide and execute.
2. **Never invent a number.** If a data point cannot be fetched or verified, the agent says so. A missing number never changes a conclusion on its own.
3. **Quiet unless it matters.** Most runs end in one line ("no change", "no signal today"). Alerts and push notifications fire only when a written rule is crossed.
4. **Rules live outside the prompt.** Thresholds, bands and playbooks sit in a doc you edit in plain language. The prompt reads it fresh on every run.
5. **Every claim is traceable.** Sources and dates for each figure; deduplication keys and exclusion reasons for each transaction.

## How to use them

1. **Pick a runner.** They are written for [Claude](https://claude.ai) scheduled tasks and use Claude's connector and tool names (for example `ToolSearch` and the Interactive Brokers MCP tool names). They adapt to other agents that support MCP connectors and scheduling; rename the tools to match.
2. **Connect what each prompt needs.** Listed at the top of each file: Gmail, Google Drive, Interactive Brokers, web search.
3. **Fill in the variables.** Replace every `{{VARIABLE}}` with your own values. Each file has a table with examples.
4. **For the crash radar,** copy [`templates/crash-radar-parameters.md`](templates/crash-radar-parameters.md) into a Google Doc, set your own bands and thresholds, and put its file ID in the prompt.
5. **Schedule it** with the cadence suggested in each file, in your own time zone.
6. **Run it once by hand** and check every number against your bank or broker before trusting it.

## Repo structure

```
prompts/
  01-family-budget-daily-report.md
  02-portfolio-crash-radar.md
  03-insider-cluster-buy-radar.md
templates/
  crash-radar-parameters.md
```

## Disclaimer

These prompts produce analysis for personal decision-making. They are not financial, investment, tax or legal advice. Markets can and do behave outside any rule set. Verify everything and make your own decisions.

## License

[MIT](LICENSE)
