# Flashcards MCP Server

An MCP (Model Context Protocol) server for managing flashcards with AI generation and study tracking capabilities.

## Features

- Create and manage flashcard decks
- Add, update, and delete cards within decks
- Study session management with progress tracking
- Import/export decks in JSON format
- Study metrics and analytics
- Local storage with persistence
- **NEW**: UI workflow integration for human-in-the-loop interactions
- **NEW**: Interactive study sessions with direct feedback

## Installation

1. Clone this repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Build the project:
   ```bash
   npm run build
   ```

## Usage

### Starting the Server

```bash
npm start
```

The server runs on stdio, making it compatible with Claude Desktop and other MCP clients.

### Available Commands

#### Deck Management
- `create_deck`: Create a new flashcard deck
- `list_decks`: List all available decks
- `get_deck`: Get details of a specific deck
- `delete_deck`: Delete a deck

#### Card Management
- `add_card`: Add a card to a deck
- `update_card`: Update an existing card
- `delete_card`: Delete a card from a deck

#### Study Sessions
- `start_study_session`: Begin a study session
- `complete_study_session`: Finish a session and record results
- `get_study_metrics`: Get study statistics for a deck

#### Import/Export
- `import_deck`: Import a deck from JSON format
- `export_deck`: Export a deck to JSON format

#### UI Workflow Integration (v1.1.0+)
- `startFlashcardSession`: Initialize a UI workflow session
- `showFlashcardPrompt`: Display UI elements for user interaction
- `updateFlashcardSession`: Manage workflow state and progress
- `getFlashcardSessionStatus`: Check workflow status

## UI Workflow Integration

The Flashcards MCP Server now includes UI workflow capabilities that enable human-in-the-loop interactions directly within Claude Desktop. This allows for:

- Interactive deck creation with step-by-step guidance
- Guided study sessions with immediate feedback
- Import workflows with preview and confirmation
- Progress tracking for multi-step operations

Example UI workflow usage:

```typescript
// Start a deck creation workflow
const session = await startFlashcardSession({
  type: "create_deck",
  metadata: {
    deckName: "JavaScript Basics",
    description: "Core JS concepts"
  }
});

// Show interactive UI for card creation
await showFlashcardPrompt({
  sessionId: session.id,
  promptType: "card_content",
  data: {
    currentStep: 1,
    totalSteps: 5
  }
});
```

## Configuration

### Claude Desktop Configuration

Add to your Claude Desktop config file:

```json
{
  "mcpServers": {
    "flashcards": {
      "command": "node",
      "args": ["/path/to/flashcards-mcp-server/build/src/index.js"]
    }
  }
}
```

## Data Storage

Data is stored in `~/.flashcards-mcp/` by default:
- `decks.json`: All flashcard decks
- `history.json`: Study session history

## Development

### Running in Development Mode

```bash
npm run dev
```

### Running Tests

```bash
npm test
```

### Building

```bash
npm run build
```

## Example Usage with Claude

```
Human: Create a new deck called "JavaScript Basics"
Claude: I'll create a new deck for you. 

I've created a new deck called "JavaScript Basics". 
Would you like to start adding cards to this deck now?
```

## Documentation

- [UI Workflow Documentation](docs/UI_WORKFLOW.md) - Guide to UI workflows
- [UI Tools Reference](docs/UI_TOOLS_REFERENCE.md) - Quick reference for UI tools
- [Migration Guide](docs/MIGRATION_GUIDE.md) - Upgrade guide between versions
- [Release Notes](RELEASES.md) - Version history and changelog
- [Analytics Dashboard Architecture](docs/analytics/ANALYTICS_DASHBOARD_ARCHITECTURE.md) - Analytics system design