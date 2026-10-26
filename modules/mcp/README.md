# Model Context Protocol (MCP) Module

This module documents how to expose security tools directly as native tool calls to AI agents using Model Context Protocol (MCP).

---

## Example MCP Client Configuration

Add this block to your agent's MCP settings (e.g. `claude_desktop_config.json` or Antigravity MCP settings):

```json
{
  "mcpServers": {
    "pd-tools": {
      "command": "npx",
      "args": ["-y", "pd-tools-mcp"],
      "env": {
        "PATH": "/usr/local/bin:/usr/bin:/bin"
      }
    }
  }
}
```

When enabled, the AI agent can execute tools like `subfinder`, `httpx`, and `nuclei` directly as native function calls without interacting with bash text streams.
