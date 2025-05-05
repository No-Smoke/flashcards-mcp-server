# UI Workflow Documentation

## Overview

The MCP Flashcards server (v1.1.0+) includes UI workflow capabilities that enable human-in-the-loop interactions directly within Claude Desktop. This allows for interactive deck creation, guided study sessions, and user-driven import workflows.

## Architecture

The UI workflow system consists of three main components:

1. **Workflow Manager**: Handles session state and workflow orchestration
2. **UI Components**: MCP-compatible UI elements for user interaction
3. **Session Management**: Tracks workflow progress and metadata

## Workflow Types

### 1. Create Deck Workflow

Interactive deck creation with user input for cards.

```typescript
// Start a deck creation workflow
await startFlashcardSession({
  type: "create_deck",
  metadata: {
    deckName: "JavaScript Advanced Concepts",
    description: "Advanced JavaScript patterns and techniques"
  }
});
```

Steps:
1. Initialize session with deck metadata
2. Present UI prompt for card content
3. User provides question and answer
4. Update session state with new card
5. Repeat steps 2-4 or finish workflow

### 2. Study Workflow

Guided study session with user feedback.

```typescript
// Start a study session
await startFlashcardSession({
  type: "study",
  metadata: {
    deckId: "deck-123",
    cardCount: 10
  }
});
```

Steps:
1. Initialize session with deck selection
2. Present card question via UI
3. User reviews answer
4. Collect user feedback (correct/incorrect)
5. Update statistics and proceed to next card

### 3. Import Workflow

File import with user confirmation.

```typescript
// Start an import workflow
await startFlashcardSession({
  type: "import",
  metadata: {
    sourceFile: "cards.json",
    format: "json"
  }
});
```

Steps:
1. Initialize session with file metadata
2. Present preview of import data
3. User confirms or cancels import
4. Process import if confirmed
5. Show import results

## UI Components

The workflow system uses MCP's UI elements:

### Text Area Component

For multi-line text input (card content, descriptions):

```typescript
{
  type: "ui_textarea",
  label: "Enter card question",
  placeholder: "What is...?",
  required: true
}
```

### Select Component

For choices (study feedback, workflow options):

```typescript
{
  type: "ui_select",
  label: "Did you get it right?",
  options: [
    { value: "correct", label: "Correct ✓" },
    { value: "incorrect", label: "Incorrect ✗" }
  ]
}
```

## Session Management

### Session Lifecycle

1. **Creation**: `startFlashcardSession` initializes a new session
2. **Active**: Session is in progress with user interaction
3. **Update**: `updateFlashcardSession` modifies session state
4. **Completion**: Session ends successfully
5. **Cancellation**: User cancels workflow or timeout occurs

### Session State

Each session maintains:
- `id`: Unique session identifier
- `type`: Workflow type (create_deck, study, import)
- `status`: Current status (active, completed, cancelled)
- `metadata`: Type-specific data
- `createdAt` / `updatedAt`: Timestamps

## Implementation Examples

### Complete Deck Creation Workflow

```typescript
// 1. Start deck creation
const session = await startFlashcardSession({
  type: "create_deck",
  metadata: {
    deckName: "React Hooks",
    targetCards: 5
  }
});

// 2. Show UI prompt for first card
await showFlashcardPrompt({
  sessionId: session.id,
  promptType: "card_content",
  data: {
    currentStep: 1,
    totalSteps: 5,
    deckName: "React Hooks"
  }
});

// 3. Process user input and update session
await updateFlashcardSession({
  sessionId: session.id,
  updates: {
    step: 2,
    cardsAdded: 1
  }
});

// 4. Continue with remaining cards...

// 5. Complete session
await updateFlashcardSession({
  sessionId: session.id,
  updates: {
    status: "completed",
    totalCards: 5
  }
});
```

### Study Session with Feedback

```typescript
// 1. Start study session
const session = await startFlashcardSession({
  type: "study",
  metadata: {
    deckId: "deck-456",
    algorithm: "spaced_repetition"
  }
});

// 2. Present card
await showFlashcardPrompt({
  sessionId: session.id,
  promptType: "study_card",
  data: {
    question: "What is the useState hook?",
    cardId: "card-789"
  }
});

// 3. Get user feedback
await showFlashcardPrompt({
  sessionId: session.id,
  promptType: "card_feedback",
  data: {
    cardId: "card-789"
  }
});

// 4. Update statistics
await markCard({
  cardId: "card-789",
  correct: true
});

// 5. Continue or complete session
```

## Best Practices

1. **Session Cleanup**: Always handle session cancellation/completion
2. **Error Handling**: Implement proper error handling for UI interactions
3. **User Experience**: Provide clear progress indicators
4. **State Management**: Keep session state consistent with user actions
5. **Timeouts**: Implement reasonable timeouts for user responses

## Migration Guide

For users upgrading from v1.0.0 to v1.1.0:

1. The basic programmatic API remains unchanged
2. UI workflows are opt-in - existing integrations continue to work
3. To use UI workflows, implement the new session-based tools
4. Update Claude Desktop configuration for UI support

## Troubleshooting

Common issues and solutions:

1. **Session Not Found**: Ensure session ID is valid and active
2. **UI Not Displaying**: Verify Claude Desktop version supports UI elements
3. **Workflow Timeout**: Check session status before operations
4. **State Inconsistency**: Use updateFlashcardSession to maintain state

## Future Enhancements

Planned improvements:
- Rich text support for card content
- File upload UI components
- Multi-user session support
- Advanced study algorithms integration
- Custom UI themes