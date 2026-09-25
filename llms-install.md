# Installing the CaseMagic MCP server

CaseMagic is a hosted server. There is nothing to clone, build or run, and no API key to set. Installing it means adding one entry to the client's MCP settings.

## Cline

Add this to `cline_mcp_settings.json` (Cline: MCP Servers, Installed, Configure MCP Servers):

```json
{
  "mcpServers": {
    "casemagic": {
      "type": "streamableHttp",
      "url": "https://casemagic.ai/mcp",
      "disabled": false
    }
  }
}
```

If the file already has an `mcpServers` object, add only the `casemagic` entry to it.

## Check that it works

Six tools work with no sign-in. Call `find_federal_case` with:

```json
{ "case_number": "1:23-cv-11195", "court": "nysd" }
```

It should return the court, the judge, the case status and the latest docket activity for that case in the Southern District of New York.

## Signing in (only for watching a case)

`watch_case`, `create_case_passport`, `get_case_passport`, `get_case_updates`, `get_case_mail`, `send_case_mail` and `stop_watch` need a CaseMagic account. The server answers those calls with an OAuth 2.1 sign-in challenge; the client opens a browser window and registers itself automatically (dynamic client registration). Do not ask the user for a token or put one in the settings file.

## Other clients

Any client that speaks Streamable HTTP can use the same address, `https://casemagic.ai/mcp`. Clients that use the common format:

```json
{
  "mcpServers": {
    "casemagic": { "type": "http", "url": "https://casemagic.ai/mcp" }
  }
}
```
