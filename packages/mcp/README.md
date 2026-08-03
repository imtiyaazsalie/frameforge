# frameforge-mcp

> The MCP server half of [Frameforge](https://github.com/imtiyaazsalie/frameforge), a two-way Figma agent for Claude Code, Cursor, Codex, and other MCP clients.

The server runs locally, relays to the Frameforge Figma plugin over a WebSocket on `127.0.0.1`, and exposes **112 MCP tools** for reading designs with grounded design context, writing back to the canvas, and pulling in context from your codebase. No paid Figma tier is required.

## Install

Add it to your MCP client config (e.g. Claude Code's `.mcp.json`):

```json
{
  "mcpServers": {
    "frameforge": {
      "command": "npx",
      "args": ["-y", "frameforge-mcp@latest"]
    }
  }
}
```

Requires Node.js 20.19+ or 22.12+. `npx` runs the server as its own process, so it doesn't share your project's Node version.

## Connecting to Figma

The server expects the Frameforge plugin to be running in your Figma app. The [main repository](https://github.com/imtiyaazsalie/frameforge) covers installing the plugin, connecting, and the available skills.

## Links

- Repository & docs: https://github.com/imtiyaazsalie/frameforge
- Issues: https://github.com/imtiyaazsalie/frameforge/issues

## License

[MIT](https://github.com/imtiyaazsalie/frameforge/blob/main/LICENSE)
