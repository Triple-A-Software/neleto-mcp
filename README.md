# Neleto CMS MCP server

Neleto is an all-in-one CMS with a page builder, built-in rendering and EU hosting. Every Neleto site ships with a native [Model Context Protocol](https://modelcontextprotocol.io) server, so Claude, Cursor, VS Code and other MCP clients can read and edit the site directly.

This repository documents that server. It holds no server code: the MCP server is part of every Neleto instance and runs at `/api/mcp` on your site. Nothing to install on the CMS side.

- Website: https://neleto.io
- Full docs: https://neleto.io/docs/developer/mcp
- Tools reference: [docs/tools.md](docs/tools.md) (57 tools)
- Registry name: `io.neleto/cms`

## What an agent can do with it

- Create, update and duplicate pages, including their layout and elements
- Write and publish blog posts and events
- Build reusable components and layouts (HTML templates, CSS, form fields)
- Upload files, including straight from a URL inside a page payload
- Read and change site settings, languages and meta tags
- Check templates before publishing, and open the live page afterwards to confirm it rendered

Access follows the same roles as the admin (admin, developer, editor, author). An agent never gets more rights than the account it connects with.

## Endpoint

```
https://<your-neleto-site>/api/mcp
```

Transport is Streamable HTTP. Examples: `https://mysite.free.neleto.io/api/mcp` or `https://www.example.com/api/mcp`.

## Authentication

**OAuth 2.1 (Claude.ai, Claude Desktop).** The endpoint publishes standard OAuth discovery (`/.well-known/oauth-protected-resource`, dynamic client registration, PKCE). Add the URL as a custom connector and sign in with your Neleto account. There is no token to copy.

**API token (Claude Code, Cursor, VS Code and others).** Create a token in the Neleto admin under Settings → API Tokens and send it as a header:

```
Authorization: Bearer <your-token>
```

OAuth connections can be reviewed and revoked under Profile → Security → Connected applications. Each connection inherits the permissions of the user who approved it.

## Setup

### Claude.ai and Claude Desktop

Settings → Connectors → Add custom connector → paste `https://<your-neleto-site>/api/mcp` → sign in.

### Claude Code

```bash
claude mcp add --transport http neleto https://<your-neleto-site>/api/mcp \
  --header "Authorization: Bearer <your-token>"
```

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "neleto": {
      "url": "https://<your-neleto-site>/api/mcp",
      "headers": { "Authorization": "Bearer <your-token>" }
    }
  }
}
```

### VS Code (GitHub Copilot)

`.vscode/mcp.json`:

```json
{
  "servers": {
    "neleto": {
      "type": "http",
      "url": "https://<your-neleto-site>/api/mcp",
      "headers": { "Authorization": "Bearer <your-token>" }
    }
  }
}
```

Windsurf, OpenCode and other clients: see the [setup docs](https://neleto.io/docs/developer/mcp).

## Example prompts

- "Create a landing page at /spring-offer using the default layout, with a hero, three feature cards and a contact section."
- "Take `@studio.html` and turn it into editable Neleto components. Every headline, text and image should be a field."
- "List all blog posts from 2025 that have no meta description and write one for each."
- "Add next Friday's workshop as an event and link it from the homepage."

## Don't have a Neleto site yet?

The free plan includes the MCP server: https://console.neleto.io/register

## About

Neleto is built by [Triple-A Soft](https://aaa-soft.net) in Germany. Sites run on Hetzner infrastructure with Germany as the default region.
