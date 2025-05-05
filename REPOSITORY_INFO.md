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

## Local Development Setup

For local development:

1. Clone this repository:
   ```bash
   git clone https://github.com/No-Smoke/flashcards-mcp-server.git
   cd flashcards-mcp-server
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Build the project:
   ```bash
   npm run build
   ```

4. Run in development mode:
   ```bash
   npm run dev
   ```

## Claude Desktop Configuration

Configure this repository in Claude Desktop as:

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

## Deprecated Repositories

The following repositories have been deprecated in favor of this consolidated repository:

- `mcp-flashcards` - Archived
- `flashcards-mcp` - Deprecated
- `flashcard-mcp` - Deprecated

Last updated: May 5, 2025