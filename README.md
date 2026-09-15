# Kubera for Cursor

Ask about your real net worth, portfolio and holdings directly in Cursor.

This plugin connects Cursor to [Kubera](https://www.kubera.com)'s hosted MCP
server. Install it, sign in once with OAuth, and ask questions like:

- "What's my net worth?"
- "How am I allocated across stocks, cash, crypto and real estate?"
- "What were my biggest movers this month?"
- "What's my CAGR since 2020?"

## What's inside

| Path | Purpose |
| --- | --- |
| `.cursor-plugin/plugin.json` | Plugin manifest (name, logo, metadata) |
| `mcp.json` | Points Cursor at Kubera's remote MCP server |
| `skills/kubera-portfolio/SKILL.md` | Tells the model when to call Kubera, and to confirm before any write |
| `assets/logo.svg` | Marketplace logo |

## Install

**From the Marketplace** — search for *Kubera* and click **Add**. Cursor opens
Kubera's OAuth consent screen; approve it and the tools are live.

**Locally, for development:**

```bash
git clone https://github.com/kubera/kubera-grok-plugin ~/.cursor/plugins/local/kubera
```

Then reload Cursor (`Cmd+Shift+P` → *Developer: Reload Window*), open the MCP
settings, connect **kubera** via OAuth, and ask "What's my net worth?".

## Authentication

The server is a remote MCP endpoint at `https://api.kubera.com/api/v1/mcp` and
authenticates with OAuth 2.1 — Cursor runs the flow on first use. You need an
active Kubera account.

**There are no secrets in this repository, and none are needed.** Nothing here
should ever contain a client secret, API key or token. See
[Kubera's AI assistants guide](https://help.kubera.com/article/173-ai-assistants-part-2)
for the connector setup this plugin automates.

## Tools

Read-only: net worth and portfolio snapshots, holdings and sections, net worth
history, CAGR, top movers, per-item history, cash flow, tickers, profile.

Write (always confirmed with you first): create/update/archive portfolios,
sheets, sections and items; cash flow; default portfolio.

## Support

- Docs: https://help.kubera.com
- Issues: https://github.com/kubera/kubera-grok-plugin/issues

## License

MIT — see [LICENSE](LICENSE).
