# ShelfXray MCP

[![ShelfXray MCP connector on Glama](https://glama.ai/mcp/connectors/in.shelfxray/shelf-data/badges/score.svg)](https://glama.ai/mcp/connectors/in.shelfxray/shelf-data)

A free, no-login [Model Context Protocol](https://modelcontextprotocol.io) server for public quick-commerce shelf data. It answers, from a cached snapshot, how brands appeared on Blinkit, Zepto and Swiggy Instamart in Bengaluru and Delhi NCR: search rank, store coverage, and who owned the sponsored slots.

There is no account and no API key. The transport is Streamable HTTP. The polite limit is 60 requests a minute per IP.

**Server URL:** `https://mcp.shelfxray.in/mcp`

Install page: [shelfxray.in/mcp](https://shelfxray.in/mcp)

Agent install file: [llms-install.md](llms-install.md)

Official MCP Registry: [`in.shelfxray/shelf-data`](https://registry.modelcontextprotocol.io/v0.1/servers?search=in.shelfxray)

Glama connector: [in.shelfxray/shelf-data](https://glama.ai/mcp/connectors/in.shelfxray/shelf-data)

This repository is documentation only. It holds install snippets, `server.json`, `.mcp.json`, the logo and the licence for these docs. It does not contain server source code or any client data.

## Read this first: the data is a cached snapshot, not live

Shelf reads were taken between **23 July and 1 August 2026**. Each row carries its own read date. Coverage is three categories (coffee, protein and energy bars, baby care), two cities, and only the top 8 brands per search. Sponsored slots are placements owned, never rupees spent. Every tool answer states its as-of date.

## Install

### Claude Code

```bash
claude mcp add --transport http shelfxray https://mcp.shelfxray.in/mcp
```

### Claude (claude.ai and Claude Desktop)

Open Settings, then Connectors, then **Add custom connector**. Name it `ShelfXray` and paste `https://mcp.shelfxray.in/mcp`. Leave authentication empty.

### Cursor

Use the [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=shelfxray&config=eyJ1cmwiOiJodHRwczovL21jcC5zaGVsZnhyYXkuaW4vbWNwIn0=) button, or add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "shelfxray": { "url": "https://mcp.shelfxray.in/mcp" }
  }
}
```

### VS Code

Use the [Add to VS Code](vscode:mcp/install?%7B%22name%22%3A%22shelfxray%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A//mcp.shelfxray.in/mcp%22%7D) button, or add this to `.vscode/mcp.json`:

```json
{
  "servers": {
    "shelfxray": { "type": "http", "url": "https://mcp.shelfxray.in/mcp" }
  }
}
```

### Any client that only speaks stdio

```json
{
  "mcpServers": {
    "shelfxray": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.shelfxray.in/mcp"]
    }
  }
}
```

## Tools

| Tool | What it does |
| --- | --- |
| `get_dataset_info` | Coverage, read dates, method, limitations and how to cite. Call this first. |
| `brand_shelf_snapshot` | One brand's rank, store coverage and sponsored slots, by platform and city. |
| `category_benchmark` | Ad pressure, results depth and price range for a category. |
| `search_rank_summary` | Who led a search keyword, per platform and city. |
| `sponsored_slot_leaders` | Brands ranked by sponsored placements owned. |

All five tools are read-only. Try: "What does the ShelfXray dataset cover, and how fresh is it?"

## Data, licence and citation

The answers are built on the public [Dark Store Index open dataset](https://darkstoreindex.com/data) (CSV and JSON), licensed **CC BY 4.0**.

Please cite: *Source: The Dark Store Index, 23 July 2026 to 1 August 2026. https://darkstoreindex.com/data*

Only public, shopper-facing shelf reads are served. No brand login, seller account or client data is involved, and nothing is modelled. Method: [darkstoreindex.com/about](https://darkstoreindex.com/about).

The files in this repository (docs, `server.json`, logo) are licensed under the MIT License. That licence does not replace the CC BY 4.0 terms that apply to the dataset.

## Privacy

The server needs no account. To count use, it keeps anonymous daily counters of distinct clients, successful and failed calls, and calls per tool. A client is counted by a one-way hash of its IP address and user agent, mixed with a random secret that changes every 7 days and is deleted after 15 days, so the hash cannot be turned back into an IP or linked across weeks. Raw IP addresses, user agents and the questions you send (tool arguments) are not stored. Counters are kept for up to 400 days. Rate limiting uses the IP in memory for one minute and never writes it down.

The full policy is at [shelfxray.in/privacy](https://shelfxray.in/privacy).

## Links

- Docs: https://shelfxray.in/mcp
- Privacy: https://shelfxray.in/privacy
- Official registry: https://registry.modelcontextprotocol.io/v0.1/servers?search=in.shelfxray
- Contact: hello@shelfxray.in
