# Flashcards MCP Server

A Model Context Protocol (MCP) server for creating, managing, and studying flashcard decks, with integrated AI-powered flashcard generation from documents.

## Features

### Core Functionality
- **Flashcard Management**: Create, read, update, and delete flashcard decks
- **Study Sessions**: Practice flashcards with progress tracking
- **Spaced Repetition**: Intelligent scheduling based on learning science
- **Multi-format Support**: Import/export JSON, CSV, and PDF formats

### AI-Powered Features
- **Automatic Generation**: Create flashcards from PDFs and documents using Claude AI
- **Google Drive Integration**: Import and process files directly from Google Drive
- **Smart Text Analysis**: Extract key information and generate questions

### Frontend Interface
- **React UI Components**: Modern, responsive flashcard study interface
- **Progress Dashboard**: Track learning with visual charts and statistics
- **Deck Management**: Easy deck organization with drag-and-drop support
- **Study Animations**: Smooth card flipping and transitions

### Analytics Dashboard
- **Study Metrics**: Comprehensive tracking of learning patterns and retention
- **Performance Insights**: Analysis of card difficulty and learning efficiency
- **Interactive Visualizations**: Data-driven charts for progress monitoring
- **Personalized Recommendations**: AI-powered suggestions for study optimization

## Architecture

```
flashcards-mcp-server/
├── src/
│   ├── server.ts           # Main MCP server entry point
│   ├── services/           # Business logic services
│   ├── models/             # Data models and interfaces
│   ├── utils/              # Utility functions
│   ├── monitoring/         # Performance monitoring 
│   ├── analytics/          # Analytics dashboard components
│   └── tests/              # Unit and integration tests
├── frontend/               # React UI components
├── docs/                   # Documentation
└── scripts/                # Installation and utility scripts
```

## Quick Start

### Prerequisites
- Node.js 16+ and npm
- Claude API key (for AI generation)
- Google Cloud credentials (optional, for Drive integration)

### Installation

```bash
# Install dependencies
npm install

# Configure API keys
cp config.example.json config.json
# Edit config.json with your API keys

# Build the server
npm run build

# Start the server
npm start
```

For detailed installation instructions, see [Installation Guide](docs/installation.md).

## Usage with Claude Desktop

Add to your Claude Desktop configuration:

```json
{
  "mcpServers": {
    "flashcards": {
      "command": "node",
      "args": ["path/to/flashcards-mcp-server/dist/server.js"],
      "env": {
        "CLAUDE_API_KEY": "your-api-key"
      }
    }
  }
}
```

## Available MCP Tools

### Deck Management
- `createDeck`: Create a new flashcard deck
- `getDeck`: Retrieve deck details
- `updateDeck`: Update deck metadata
- `deleteDeck`: Remove a deck
- `listDecks`: List all available decks

### Card Operations
- `addCard`: Add a flashcard to a deck
- `updateCard`: Modify an existing card
- `deleteCard`: Remove a card from a deck
- `listCards`: List all cards in a deck

### Study Features
- `studyDeck`: Start a study session
- `answerCard`: Submit an answer for a card
- `getStudyStats`: Get study performance statistics

### AI Generation
- `generateFlashcards`: Create flashcards from document content
- `importGoogleDriveFile`: Import and process file from Google Drive
- `processAndGenerateCards`: Upload file content and generate cards

### Analytics Tools
- `getDashboardData`: Get comprehensive analytics dashboard data
- `getStudyMetrics`: Retrieve detailed study performance metrics
- `exportAnalytics`: Export analytics data in various formats
- `getRetentionStats`: Get spaced repetition effectiveness statistics

## Examples

### Create a Deck
```typescript
await mcpClient.call('createDeck', {
  name: 'Medical Terminology',
  description: 'Common medical terms and definitions'
});
```

### Generate Cards from PDF
```typescript
await mcpClient.call('processAndGenerateCards', {
  filePath: '/path/to/document.pdf',
  deckId: 'medical-terms-deck',
  options: { model: 'claude-3-7-sonnet-20250219' }
});
```

### Study Session
```typescript
const session = await mcpClient.call('studyDeck', {
  deckId: 'medical-terms-deck'
});

const result = await mcpClient.call('answerCard', {
  sessionId: session.sessionId,
  cardId: session.currentCard.id,
  rating: 4
});
```

## Documentation

- [Installation Guide](docs/installation.md)
- [API Reference](docs/api-reference.md)
- [React Components](docs/react-components.md)
- [Analytics Dashboard](docs/analytics/ANALYTICS_DASHBOARD_ARCHITECTURE.md)

## Testing

The project includes comprehensive test coverage:

```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Watch mode for development
npm run test:watch
```

## Development

```bash
# Start in development mode
npm run dev

# Watch for changes
npm run watch

# Type checking
npm run build
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Model Context Protocol](https://github.com/modelcontextprotocol) by Anthropic
- [Claude AI](https://anthropic.com) for flashcard generation
- React and TypeScript communities

## Support

For support, please:
1. Check the [documentation](docs/)
2. Review [existing issues](https://github.com/No-Smoke/flashcards-mcp-server/issues)
3. Open a new issue with detailed information

---

Built with ❤️ by the Flashcards MCP team