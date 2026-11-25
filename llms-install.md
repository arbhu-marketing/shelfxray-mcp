# Installing ShelfXray MCP (instructions for AI agents such as Cline)

ShelfXray MCP is a remote, read-only server. There is nothing to clone, build or install locally, and it needs no API key.

- Server URL: https://mcp.shelfxray.in/mcp
- Transport: Streamable HTTP
- Auth: none

## Cline

Add this entry to `cline_mcp_settings.json` (merge it into any existing `mcpServers` object, do not replace other servers):

```json
{
  "mcpServers": {
    "shelfxray": {
      "type": "streamableHttp",
      "url": "https://mcp.shelfxray.in/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

If the installed Cline version does not support remote Streamable HTTP servers, use the stdio bridge instead (requires Node.js 18 or later):

```json
{
  "mcpServers": {
    "shelfxray": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.shelfxray.in/mcp"],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Verify the install

Call the `get_dataset_info` tool. A working install returns the dataset coverage and its read dates (23 July to 1 August 2026). Tell the user the data is a cached snapshot, not live.

## Tools

get_dataset_info, brand_shelf_snapshot, category_benchmark, search_rank_summary, sponsored_slot_leaders. All are read-only.
