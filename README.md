# ManyCP MCP server

**Submit your MCP server to every MCP directory, from your agent.**

ManyCP reads your GitHub repo, drafts one listing, publishes it to the official MCP Registry, opens the pull requests on the awesome lists, prepares the web forms for the rest, and keeps every listing in sync when you ship a new version. This is its remote MCP server, so you can do all of that from Claude Code, Cursor, VS Code or any MCP client:

> "Submit my weather-mcp to every directory."

- Website: https://manycp.com
- Endpoint: `https://manycp.com/mcp` (Streamable HTTP)
- Auth: `Authorization: Bearer <key>` — create a key at https://manycp.com/app/settings

## Tools

| Tool | What it does |
|---|---|
| `check_listings` | Shows which directories already list a public GitHub repo. No plan needed. |
| `list_directories` | Every directory ManyCP knows, and how each one is handled (direct publish, auto PR, auto-indexed, assisted). |
| `add_server` | Reads a GitHub repo and saves a draft listing: name, description, tools, install command, `server.json`. |
| `list_servers` | Your servers, with a status summary per directory. |
| `get_server` | One server's listing and its status in every directory, with links to PRs and listings. |
| `update_listing` | Fix the wording, tags, categories or tools of a listing. |
| `submit_server` | Files the listing everywhere it can: registry publish, pull requests from your own GitHub account, prepared forms. |
| `sync_server` | Re-reads the repo after a release and updates or flags stale listings. |

## Install

**Claude Code**

```bash
claude mcp add --transport http manycp https://manycp.com/mcp --header "Authorization: Bearer YOUR_KEY"
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "manycp": {
      "url": "https://manycp.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "inputs": [{ "type": "promptString", "id": "manycp-key", "description": "ManyCP API key", "password": true }],
  "servers": {
    "manycp": {
      "type": "http",
      "url": "https://manycp.com/mcp",
      "headers": { "Authorization": "Bearer ${input:manycp-key}" }
    }
  }
}
```

**Claude Desktop** (via `mcp-remote`)

```json
{
  "mcpServers": {
    "manycp": {
      "command": "npx",
      "args": ["mcp-remote", "https://manycp.com/mcp", "--header", "Authorization:${MANYCP_AUTH}"],
      "env": { "MANYCP_AUTH": "Bearer YOUR_KEY" }
    }
  }
}
```

## How submissions work

- **Official MCP Registry:** published directly with your GitHub identity (`io.github.<you>/*`).
- **Awesome lists and GitHub-based catalogs:** one pull request per list, opened from your own GitHub account, in each list's exact format, disclosed as sent with ManyCP.
- **Directories that crawl GitHub:** ManyCP opens one PR on your repo with the files they look for.
- **Web-form directories:** the ManyCP browser extension fills each form; you review and press Submit.

## License

MIT
