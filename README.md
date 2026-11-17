# Fixlight MCP server

Checks a public web page for accessibility problems and explains each one in plain English.

- **Endpoint:** `https://fixlight.fernwaylabs.com/mcp`
- **Transport:** Streamable HTTP
- **Sign-in:** none. No account and no API key.
- **Official MCP Registry name:** `io.github.fernwaylabs/fixlight`

This is a hosted server. Add the address to your AI assistant and ask it to check a page. Nothing to install.

## What it does

The server has one tool, `scan_url`, which takes the public address of one page. It loads the page in a real browser,
runs automated accessibility tests (axe-core) and returns the findings worst first, each with why it matters and how to
fix it. It also notes which findings the free [Fixlight WordPress plugin](https://wordpress.org/plugins/fixlight/)
fixes on its own.

Try asking your assistant:

> Check https://example.com/ for accessibility problems and tell me what to fix first.

## Connect it

**Claude Code**

```sh
claude mcp add --transport http fixlight https://fixlight.fernwaylabs.com/mcp
```

**Claude, ChatGPT and other chat apps:** add `https://fixlight.fernwaylabs.com/mcp` as a custom connector (or custom
MCP server) in the app's settings, where your plan allows custom connectors. No authentication.

**Cursor** (`~/.cursor/mcp.json` or `.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "fixlight": {
      "url": "https://fixlight.fernwaylabs.com/mcp"
    }
  }
}
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "servers": {
    "fixlight": {
      "type": "http",
      "url": "https://fixlight.fernwaylabs.com/mcp"
    }
  }
}
```

Any other client that supports remote MCP servers over Streamable HTTP works the same way: give it the address above.

## Limits

- It only reads pages anyone can open, and changes nothing on them. Private and local addresses are refused.
- Results for the same page are reused for a day.
- Use is limited per hour and per day.
- Automated checks find many accessibility problems, but not all of them. A page with no findings can still have
  barriers for some visitors.

## Privacy and terms

- What it sends us: https://fixlight.fernwaylabs.com/privacy/#mcp
- Terms: https://fixlight.fernwaylabs.com/terms/#mcp
- Docs: https://fixlight.fernwaylabs.com/faq/#ai-tool

`server.json` in this repository is the server's entry in the official MCP Registry. The server's source code is not
published here.

## Who makes it

Fernway Labs, a small software studio. Questions: fixlight@fernwaylabs.com
