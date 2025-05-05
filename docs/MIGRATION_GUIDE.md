# Migration Guide: v1.0.0 to v1.1.0

## Overview

Version 1.1.0 introduces UI workflow capabilities while maintaining full backward compatibility with v1.0.0. This guide helps you upgrade smoothly and take advantage of new features.

## No Breaking Changes

The good news: **there are no breaking changes**. All existing code and integrations will continue to work exactly as before.

## New Features Available

### UI Workflow Tools

Four new tools are available for interactive workflows:

1. **startFlashcardSession**: Initialize UI workflow sessions
2. **showFlashcardPrompt**: Display UI elements for user interaction
3. **updateFlashcardSession**: Manage workflow state
4. **getFlashcardSessionStatus**: Check workflow status

### Using UI Workflows (Optional)

To use the new UI capabilities:

```typescript
// Before (v1.0.0) - Still works!
await createDeck({
  name: "JavaScript Basics",
  description: "Core JS concepts"
});

// After (v1.1.0) - With UI workflow
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

## Prerequisites

### Claude Desktop Requirements

To use UI features, ensure:
1. Claude Desktop is updated to the latest version
2. MCP UI components are supported (check Claude Desktop release notes)

### Configuration Updates

No changes required to your existing MCP configuration. To verify UI support:

```json
{
  "mcpServers": {
    "flashcards": {
      "command": "npx",
      "args": ["@no-smoke/mcp-flashcards"],
      "env": {
        "FLASHCARDS_DATA_DIR": "./flashcards-data"
      }
    }
  }
}
```

## Migration Steps

### 1. Update Package

```bash
npm update @no-smoke/mcp-flashcards@1.1.0
```

### 2. Verify Installation

```bash
npm list @no-smoke/mcp-flashcards
```

### 3. Test Existing Code

Run your existing integrations to ensure they work as expected.

### 4. Explore UI Features (Optional)

Start experimenting with UI workflows:

```typescript
// Example: Interactive deck creation
async function createDeckInteractive() {
  const session = await startFlashcardSession({
    type: "create_deck",
    metadata: {
      deckName: "My New Deck"
    }
  });
  
  // Your UI workflow logic here
}
```

## Common Migration Scenarios

### Scenario 1: Keep Everything As-Is

No action needed! Your existing code continues to work without modification.

### Scenario 2: Add UI to Existing Features

Gradually introduce UI workflows alongside existing code:

```typescript
// Existing function
async function studyDeck(deckId: string) {
  const card = await getNextCard({ deckId });
  // ... existing logic
}

// New UI-enhanced version
async function studyDeckWithUI(deckId: string) {
  const session = await startFlashcardSession({
    type: "study",
    metadata: { deckId }
  });
  
  // UI-driven study session
}
```

### Scenario 3: Full UI Migration

Replace programmatic workflows with interactive UI:

```typescript
// Before
async function importDeck(filePath: string) {
  const data = await readFile(filePath);
  await importDeck({ data });
}

// After
async function importDeckWithUI(filePath: string) {
  const session = await startFlashcardSession({
    type: "import",
    metadata: {
      sourceFile: filePath
    }
  });
  
  // Show preview and get user confirmation
  await showFlashcardPrompt({
    sessionId: session.id,
    promptType: "import_preview",
    data: { /* preview data */ }
  });
}
```

## Best Practices

1. **Test Incrementally**: Add UI features one at a time
2. **Maintain Fallbacks**: Keep programmatic options available
3. **Handle Errors**: Add error handling for UI operations
4. **Monitor Sessions**: Clean up abandoned sessions

## Troubleshooting

### UI Not Appearing

1. Check Claude Desktop version
2. Verify MCP server is running
3. Confirm UI tools are available in tool list

### Session Errors

```typescript
try {
  const session = await startFlashcardSession(/* ... */);
} catch (error) {
  if (error.code === 'SESSION_NOT_FOUND') {
    // Handle missing session
  }
}
```

### Performance Issues

- Limit active sessions
- Implement session timeouts
- Clean up completed sessions

## Getting Help

- Check [UI Workflow Documentation](UI_WORKFLOW.md)
- Review [example implementations](../examples)
- Open an issue on [GitHub](https://github.com/No-Smoke/flashcards-mcp-server/issues)

## Next Steps

1. Update to v1.1.0
2. Test existing integrations
3. Explore UI features at your own pace
4. Provide feedback for future improvements