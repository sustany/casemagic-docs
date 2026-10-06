# CaseMagic for Claude

Check, understand and watch United States federal court cases from Claude.

CaseMagic reads federal district court dockets and keeps watching the ones you care about. This plugin connects Claude to CaseMagic's hosted MCP server and adds five skills that know how to use it well.

## What you can ask

- "Check federal case 1:23-cv-11195 in the Southern District of New York."
- "Explain the most recent order in my case in plain English."
- "What dates are set in my case? Put them on my calendar."
- "Watch this case and tell me when anything new is filed."
- "What changed across all my cases this week?"

## Skills

| Skill | What it does |
| --- | --- |
| `check-case` | Finds a federal case by number or name and reports the judge, status and latest filings, citing how fresh the reading is. |
| `explain-filing` | Explains a docket entry or filing in plain English from the court's own text. |
| `case-deadlines` | Lists every date the docket states and can write them to an `.ics` calendar file. |
| `watch-case` | Saves a case to your CaseMagic account and turns on monitoring for new filings. |
| `case-briefing` | Summarizes what changed across your saved cases since a given day, optionally as a Markdown file. |

## Connection

The plugin adds one remote MCP server:

```json
{ "mcpServers": { "casemagic": { "type": "http", "url": "https://casemagic.ai/mcp" } } }
```

Nothing to install and no API key. Looking up, reading and explaining a public docket is free and needs no account. Saving a case, watching it and reading your saved cases' documents use OAuth: the first time, Claude opens CaseMagic's own sign-in page and you approve access.

## Pricing

Checking and explaining cases is free. Watching a case is a paid subscription (Individual, Professional and Practice plans, with a free trial); Claude shows the current prices and a checkout link when you first ask to watch a case. Nothing is charged until you complete checkout yourself.

## Coverage and limits

- United States federal district courts only. State, county, family and traffic courts are not covered.
- CaseMagic reports what the court record says. It is not a law firm and does not give legal advice.
- Deadlines are only those the docket states, plus a small set computed from nationwide federal rules. Deadlines that depend on local rules or standing orders are not computed.

## Privacy and support

- Privacy policy: https://casemagic.ai/privacy
- Terms: https://casemagic.ai/terms
- Support: support@casemagic.ai
- Website: https://casemagic.ai

CaseMagic is operated by Decentralized Publishing LLC, Irvine, California.
