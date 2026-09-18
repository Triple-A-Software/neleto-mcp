# Installing the Neleto MCP server (instructions for AI agents)

The Neleto MCP server is remote. It runs inside the user's Neleto site, so there is no package to install or build.

## 1. Ask the user for two things

1. **The URL of their Neleto site**, for example `https://mysite.free.neleto.io` or `https://www.example.com`. The MCP endpoint is that URL plus `/api/mcp`.
2. **An API token**, unless their client supports OAuth (Claude.ai and Claude Desktop custom connectors do; they need no token). Tokens are created in the Neleto admin under Settings → API Tokens.

If the user has no Neleto site yet, point them to https://console.neleto.io/register (the free plan includes the MCP server).

## 2. Add the server to the client config

Use transport `streamable-http` (called `http` in some clients) with this URL and header:

```json
{
  "mcpServers": {
    "neleto": {
      "type": "streamable-http",
      "url": "https://<site>/api/mcp",
      "headers": { "Authorization": "Bearer <token>" }
    }
  }
}
```

Adjust the key names to the client's format (for example `servers` instead of `mcpServers` in VS Code).

## 3. Verify

Call the `settings_get` tool. A working connection returns the site's settings, including `publicBaseUrl`. A `401` means the token is missing, wrong or revoked.

## Notes for working with the tools

- `page_update`, `layout_update` and `component_update` replace every field you leave out. Load the object with the matching `_get` tool first and send it back complete.
- Page, layout, component, post and event IDs are integers. File IDs are UUID strings.
- Images can be ingested inline: put `{ "sourceUrl": "https://…" }` where a file ID is expected in element data.
- Before publishing template changes, run `lsp_check_page`, `lsp_check_layout` or `lsp_check_component` and fix any errors.

Full reference: https://neleto.io/docs/developer/mcp/tools
