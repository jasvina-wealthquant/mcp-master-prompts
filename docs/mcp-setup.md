# MCP setup notes

You only need the servers a prompt lists under **MCPs**. Each section below covers one tool type.

## Adding a server

**Claude Code**

```bash
# Remote (HTTP) server
claude mcp add --transport http <name> <url>

# Local (stdio) server
claude mcp add <name> -- npx -y <package>

# Check what is connected
claude mcp list
```

**Claude Desktop, Cursor, Windsurf and others** use a JSON config with the same idea:

```json
{
  "mcpServers": {
    "firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": { "FIRECRAWL_API_KEY": "your-key" }
    }
  }
}
```

Never commit API keys. Keep them in environment variables or your client's secret store.

## By tool type

| Tool type | What the prompts expect it to do | Example servers |
| --- | --- | --- |
| Web search and scrape | Search the web, fetch a page as clean text, optionally crawl a site | Firecrawl, Brave Search, Exa, Fetch |
| Broker and market data | Quotes, OHLC history, holdings, positions, instrument search | Zerodha Kite, Alpaca, Polygon |
| Code and repos | Read files, list issues and PRs, read diffs, post comments | GitHub, Git, Filesystem |
| Creative generation | Generate images, video, music, voice; check credit cost first | Artlist, Higgsfield, Replicate |
| Documents and data | Read PDFs, spreadsheets and notes; run SQL | Filesystem, Google Drive, Notion, SQLite, Postgres |
| Browser automation | Click, log in, paginate, screenshot | Playwright, Puppeteer |

## Safety defaults worth setting

- **Broker servers:** use read only scopes where possible. The prompts here never place orders, and you should keep it that way unless you mean it.
- **Paid generation servers:** check your balance before a batch. The [cost guard](../prompts/00-meta/cost-guard.md) prompt automates this.
- **Write capable servers (GitHub, Notion, social):** keep your client's tool permission prompts on.
