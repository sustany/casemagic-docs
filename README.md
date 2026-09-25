# CaseMagic MCP server

[![CaseMagic MCP connector](https://glama.ai/mcp/connectors/io.github.sustany/casemagic/badges/score.svg)](https://glama.ai/mcp/connectors/io.github.sustany/casemagic)

**Watch US federal court cases for new filings and keep a Case Passport any AI assistant can load.**

CaseMagic is a hosted [Model Context Protocol](https://modelcontextprotocol.io) server. It re-reads a federal court docket on a schedule, tells you when anything new is filed, and keeps a persistent record of the case, called the Case Passport. That record is the same in ChatGPT, Claude, Gemini, Grok, Perplexity or any other MCP client.

This repository holds documentation only. The server is hosted; there is nothing to install or run.

| | |
|---|---|
| Endpoint | `https://casemagic.ai/mcp` |
| Transport | Streamable HTTP (JSON-RPC over POST), stateless |
| Protocol versions | 2025-06-18, 2025-03-26 |
| Auth | OAuth 2.1, authorization code + PKCE (S256), dynamic client registration. Six read-only tools need no auth. |
| Server card | https://casemagic.ai/.well-known/mcp/server-card.json |
| Registry name | `io.github.sustany/casemagic` |
| Full tool reference | https://casemagic.ai/llms-full.txt |
| Website | https://casemagic.ai |

## Add it to your client

**ChatGPT, Claude, Gemini, Grok, Perplexity:** add a custom connector with the address `https://casemagic.ai/mcp`. There is a step-by-step page for each at https://casemagic.ai/integrations.

**Cursor:** [![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=casemagic&config=eyJ1cmwiOiJodHRwczovL2Nhc2VtYWdpYy5haS9tY3AifQ%3D%3D)

**VS Code:** [Install in VS Code](https://insiders.vscode.dev/redirect/mcp/install?name=casemagic&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fcasemagic.ai%2Fmcp%22%7D)

**Cline:** see [llms-install.md](llms-install.md).

**Any other client:**

```json
{
  "mcpServers": {
    "casemagic": { "type": "http", "url": "https://casemagic.ai/mcp" }
  }
}
```

## Tools

Watching and the Case Passport (need a CaseMagic account; 7-day free trial):

| Tool | What it does |
|---|---|
| `watch_case` | Begin monitoring a saved case for new filings. |
| `create_case_passport` | Save a case to the account, creating its Case Passport. |
| `get_case_passport` | Load the persistent record of a saved case. |
| `get_case_updates` | What has changed since a given time, for one case or every case the account follows. |
| `get_case_mail` | Read the correspondence sent to the case address. |
| `send_case_mail` | Draft a message for the person to review and send. It never sends one itself. |
| `stop_watch` | Stop monitoring a saved case. |

Reading a federal docket (free, no account, no token):

| Tool | What it does |
|---|---|
| `find_federal_case` | Find a federal case by number or name; court, judge, status and latest activity. |
| `get_case_status` | Judge, filing date, open or closed, nature of suit. |
| `get_recent_case_activity` | The most recent docket entries, with the text the court published. |
| `explain_docket_entry` | One docket entry in full, with the entries around it. |
| `get_case_documents` | Entries that have a document available, with a link where one is free. |
| `get_case_deadlines` | Dates the docket states, plus post-judgment and appeal deadlines from the federal rules. |

Try it without signing in: *"Check federal case 1:23-cv-11195 in the Southern District of New York."*

## Scope and limits

- US federal district courts only. No state, county or traffic courts.
- Every answer says where it came from and when the docket was read. It is not real time.
- CaseMagic reports what a court source says. It is not a law firm and does not give legal advice.

## Links

[Pricing](https://casemagic.ai/pricing) · [Privacy](https://casemagic.ai/privacy) · [Terms](https://casemagic.ai/terms) · [Security](https://casemagic.ai/security) · Support: support@casemagic.ai
