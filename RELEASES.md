# Releases

## Version 1.1.0 - UI Workflow Integration
*Released: 2025-05-04*

This release introduces UI workflow capabilities for human-in-the-loop interactions within Claude Desktop.

### 🎯 Key Features

#### UI Workflow Integration
- **Human-in-the-Loop Prompts**: Interactive UI elements for deck creation, study sessions, and imports
- **Workflow Session Management**: Track and manage multi-step operations with state persistence
- **Progress Tracking**: Visual progress indicators for multi-step workflows

#### New Tools
- `startFlashcardSession`: Initialize UI workflow sessions
- `showFlashcardPrompt`: Display UI elements for user interaction
- `updateFlashcardSession`: Manage workflow state and progress
- `getFlashcardSessionStatus`: Check current workflow status

### 🚀 Improvements

- Enhanced deck creation process with step-by-step UI guidance
- Interactive study mode with immediate feedback collection
- Import workflows with preview and confirmation steps
- Error handling for UI operations and session management

### 📚 Documentation

- Comprehensive UI workflow documentation in `docs/UI_WORKFLOW.md`
- Updated README with UI workflow examples
- Migration guide for v1.0.0 to v1.1.0 users

### 🔧 Technical Changes

- Implemented WorkflowManager class for session handling
- Added TypeScript interfaces for workflow types
- Introduced session metadata tracking
- Added cleanup handlers for cancelled sessions

### 📦 Installation

```bash
npm install @no-smoke/mcp-flashcards@1.1.0
```

### 🔄 Upgrade Instructions

1. Update your MCP configuration to the latest version
2. Ensure Claude Desktop supports UI elements
3. No breaking changes - existing integrations continue to work
4. UI workflows are opt-in features

---

## Version 1.0.0 - Initial Release
*Released: 2025-05-04*

### 🎉 Features

- Basic flashcard deck management
- Create, read, update, and delete operations for decks and cards
- Study mode with spaced repetition algorithm
- Import/Export functionality
- Statistics tracking
- Full MCP integration

### 📚 Core Functionality

- Deck management (create, list, get, delete)
- Card operations (add, update, delete)
- Study sessions with card tracking
- JSON-based data persistence

### 🔧 Technical Details

- TypeScript implementation
- Jest testing framework
- ESLint and Prettier configuration
- GitHub Actions CI/CD pipeline

### 📦 Installation

```bash
npm install @no-smoke/mcp-flashcards@1.0.0
```

---

## Version 0.1.0 - Project Setup
*Released: 2025-05-04*

### 🏗️ Initial Setup

- Project scaffolding
- Basic MCP server structure
- Repository configuration
- Development environment setup

### 🔧 Infrastructure

- TypeScript configuration
- Build system setup
- Testing framework integration
- CI/CD pipeline basics

---

## Roadmap

### Version 1.2.0 (Planned)
- Rich text support for card content
- Advanced study algorithms
- Collaborative study sessions
- Analytics dashboard

### Version 1.3.0 (Planned)
- Mobile app integration
- Cloud synchronization
- Custom UI themes
- Plugin system for extensions

### Version 2.0.0 (Planned)
- Complete UI overhaul
- Real-time collaboration
- AI-powered card generation
- Advanced analytics and insights

---

For detailed changelog, see [CHANGELOG.md](CHANGELOG.md)