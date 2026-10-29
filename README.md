# Moved

This repository has moved to **[www-joyautomart-com/mcp-server](https://github.com/www-joyautomart-com/mcp-server)**, the official JOY Automart MCP server.

Official MCP Registry name: `com.joyautomart/mcp`. Remote endpoint: https://www.joyautomart.com/mcp

---

# JOY Automart MCP Server

[![npm](https://img.shields.io/npm/v/@joyautomart/mcp-server)](https://www.npmjs.com/package/@joyautomart/mcp-server) ![License: MIT](https://img.shields.io/badge/license-MIT-green)

The official Model Context Protocol (MCP) server for **JOY Automart**, Bangladesh's automotive parts and vehicle marketplace. It lets AI assistants search the parts catalogue (in English, Bangla or Banglish), check BDT prices, stock and chassis fitment, browse and compare JOY Auto Exchange vehicle listings, watch auctions, and prepare buyer handoff links.

- **Remote endpoint:** `https://www.joyautomart.com/mcp` (Streamable HTTP, protocol 2025-03-26)
- **No account needed** for the public, read-only tools
- **Developer guide:** [developers.html](developers.html) (to be served at https://www.joyautomart.com/developers)

## Connect (remote, recommended)

```json
{
  "mcpServers": {
    "joy-automart": { "type": "http", "url": "https://www.joyautomart.com/mcp" }
  }
}
```
Claude Code: `claude mcp add --transport http joy-automart https://www.joyautomart.com/mcp`

## Connect (stdio, via npm)

For clients that only support local stdio servers:
```json
{
  "mcpServers": {
    "joy-automart": {
      "command": "npx",
      "args": ["-y", "@joyautomart/mcp-server"],
      "env": { "JOY_AGENT_TOKEN": "joyagt_optional" }
    }
  }
}
```
Options: `--url <endpoint>` (defaults to the endpoint above). `JOY_AGENT_TOKEN` is optional.

## Tools

| Tool | Purpose |
|---|---|
| `search_parts` | Search the parts catalogue by query, make, chassis, category, stock and maximum BDT price |
| `get_part` | Full detail for one part: price, stock, minimum order, offers, bulk price breaks |
| `search_vehicles` | Search vehicle listings by make, fuel, year and BDT price |
| `get_vehicle` | Full detail for one listing, including the QC summary where available |
| `get_auction_status` | Current bid, bid count and end time for a JOY auction |
| `compare_vehicles` | Side-by-side comparison of 2 to 4 listings |
| `get_buying_guide` | Payment methods, delivery zones and buying process |
| `prepare_buyer_handoff` | Product link plus a pre-filled WhatsApp message to JOY sales |

## Buyer token (optional)
Create one at https://www.joyautomart.com/cars/account?section=ai-agents&portal=retail and send it as `Authorization: Bearer joyagt_...`, or set it as `JOY_AGENT_TOKEN` for the npm proxy. Keep tokens secret.

## Fitment caveat
Fitment results are guidance only. Before you buy, confirm the chassis code or OEM number with JOY's sales team.

## Files
- `bin/joyautomart-mcp.js`: stdio to Streamable HTTP proxy (`@modelcontextprotocol/sdk`)
- `server.json`: official MCP Registry entry (`com.joyautomart/mcp`)
- `smithery.yaml`, `glama.json`: directory configs

## Licence
MIT © Ahmed Arafat Joyadh / JOY Automart
