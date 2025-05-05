# UI Tools Quick Reference

## startFlashcardSession

Initialize a new UI workflow session.

```typescript
startFlashcardSession({
  type: "create_deck" | "study" | "import",
  metadata: {
    // Type-specific metadata
    deckName?: string,
    deckId?: string,
    sourceFile?: string,
    // ... other fields
  }
})
```

**Returns**: Session object with `id`, `type`, `status`, `metadata`

**Example**:
```typescript
const session = await startFlashcardSession({
  type: "create_deck",
  metadata: {
    deckName: "React Hooks",
    targetCards: 10
  }
});
```

## showFlashcardPrompt

Display a UI element for user interaction.

```typescript
showFlashcardPrompt({
  sessionId: string,
  promptType: "card_content" | "card_feedback" | "import_preview" | ...,
  data: {
    // Prompt-specific data
    currentStep?: number,
    totalSteps?: number,
    question?: string,
    // ... other fields
  }
})
```

**Returns**: User's response or input

**Example**:
```typescript
const userInput = await showFlashcardPrompt({
  sessionId: session.id,
  promptType: "card_content",
  data: {
    currentStep: 1,
    totalSteps: 5,
    deckName: "React Hooks"
  }
});
```

## updateFlashcardSession

Update session state and metadata.

```typescript
updateFlashcardSession({
  sessionId: string,
  updates: {
    status?: "active" | "completed" | "cancelled",
    step?: number,
    cardsAdded?: number,
    // ... other updates
  }
})
```

**Returns**: Updated session object

**Example**:
```typescript
await updateFlashcardSession({
  sessionId: session.id,
  updates: {
    step: 2,
    cardsAdded: 1
  }
});
```

## getFlashcardSessionStatus

Check the current status of a workflow session.

```typescript
getFlashcardSessionStatus({
  sessionId: string
})
```

**Returns**: Session status object

**Example**:
```typescript
const status = await getFlashcardSessionStatus({
  sessionId: session.id
});

if (status.state === 'completed') {
  console.log('Workflow finished!');
}
```

## UI Component Types

### Text Area

For multi-line text input:
```typescript
{
  type: "ui_textarea",
  label: "Question",
  placeholder: "Enter your question...",
  required: true
}
```

### Select

For choice selection:
```typescript
{
  type: "ui_select",
  label: "Correct?",
  options: [
    { value: "yes", label: "Yes ✓" },
    { value: "no", label: "No ✗" }
  ]
}
```

## Workflow States

- `active`: Session is in progress
- `completed`: Session finished successfully
- `cancelled`: Session was cancelled
- `error`: Session encountered an error

## Common Patterns

### Multi-step Workflow

```typescript
// 1. Start session
const session = await startFlashcardSession({ type: "create_deck" });

// 2. Loop through steps
for (let i = 1; i <= totalSteps; i++) {
  // Show prompt
  const input = await showFlashcardPrompt({
    sessionId: session.id,
    promptType: "card_content",
    data: { currentStep: i, totalSteps }
  });
  
  // Update progress
  await updateFlashcardSession({
    sessionId: session.id,
    updates: { step: i + 1 }
  });
}

// 3. Complete session
await updateFlashcardSession({
  sessionId: session.id,
  updates: { status: "completed" }
});
```

### Error Handling

```typescript
try {
  const session = await startFlashcardSession({
    type: "study"
  });
  
  // ... workflow logic
  
} catch (error) {
  if (error.code === 'SESSION_TIMEOUT') {
    console.log('Session timed out');
  } else if (error.code === 'USER_CANCELLED') {
    console.log('User cancelled workflow');
  }
}
```

### Session Cleanup

```typescript
async function cleanupSession(sessionId: string) {
  try {
    await updateFlashcardSession({
      sessionId,
      updates: { status: "cancelled" }
    });
  } catch (error) {
    console.error('Cleanup failed:', error);
  }
}
```

## Tips

1. Always handle session cancellation
2. Provide clear progress indicators
3. Validate user input before processing
4. Keep session metadata minimal but useful
5. Implement timeouts for user responses