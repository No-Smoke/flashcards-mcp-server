# Repository Information

## Verified Repository Locations

- **Local repository**: `/home/vanya/work/claude-projects/flashcards-mcp-server`
- **Remote repository**: `https://github.com/No-Smoke/flashcards-mcp-server`

## Consolidation Status

The Flashcards MCP server project has been consolidated into this repository. All documentation and code from previously separate repositories (such as mcp-flashcards) has been migrated here to provide a single source of truth.

## Repository Structure

- `/src` - Source code for the MCP server
- `/docs` - Documentation including UI workflows, migration guides, and references
- `/build` - Compiled JavaScript output
- `/tests` - Test suite

## Configuration

For Claude Desktop, configure this repository as:

```json
{
  "mcpServers": {
    "flashcards": {
      "command": "node",
      "args": ["/home/vanya/work/claude-projects/flashcards-mcp-server/build/src/index.js"]
    }
  }
}
```

Last updated: May 5, 2025