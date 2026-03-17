# Void Core Features

This directory contains the core Void-specific functionality that differentiates Void from VSCode. These are the AI-powered features and enhancements that make Void a next-generation development environment.

## 🚀 Overview

Void's core features are organized into three main areas:

- **AI Integration** - LLM communication and model management
- **Code Editing** - Advanced code manipulation and application
- **User Interface** - Enhanced UI components for AI interactions

## 📁 Directory Structure

```
src/vs/workbench/contrib/void/
├── browser/                   # Browser-side UI and interactions
│   ├── react/                # React components for Void UI
│   ├── media/                # UI assets and icons
│   └── *.ts                  # Browser process code
├── common/                   # Shared utilities and types
│   ├── *.ts                  # Common interfaces and helpers
│   └── protocols/            # Communication protocols
├── electron-main/            # Main process AI features
│   ├── *.ts                  # Main process code
│   └── services/             # AI service implementations
└── services/                 # Void-specific services
    ├── *.ts                  # Service implementations
    └── registration/         # Service registration
```

## 🧠 AI Integration

### LLM Message Pipeline

The core AI communication flow:

```
User Input → Browser Process → Main Process → AI Provider → Response → Browser Process → UI Update
```

#### Key Components

- **`sendLLMMessage`** - Main process LLM communication
- **`modelCapabilities`** - Model feature detection and management
- **Provider Management** - Support for multiple AI providers (OpenAI, Ollama, etc.)

### Model Management

- **Dynamic Model Discovery** - Automatically detect available models
- **Capability Detection** - Understand model features and limitations
- **Provider Abstraction** - Unified interface for different AI providers
- **Configuration Management** - Model settings and preferences

## ✏️ Code Editing Features

### Fast Apply System

Void's patented Fast Apply system enables quick code changes:

```
<<<<<<< ORIGINAL
// original code
=======
// modified code
>>>>>>> UPDATED
```

#### Components

- **`editCodeService`** - Main code editing service
- **DiffZone Management** - Visual change tracking
- **Streaming Updates** - Real-time code application
- **Conflict Resolution** - Handle edit conflicts gracefully

### Code Application Methods

1. **Fast Apply** - Search/replace blocks for quick changes
2. **Slow Apply** - Full file rewrite for complex changes
3. **Streaming Apply** - Real-time code generation and application

## 🎨 User Interface

### Chat Interface

- **Multi-turn Conversations** - Context-aware chat sessions
- **Agent Mode** - Advanced AI agent interactions
- **Gather Mode** - Code context collection
- **File Attachments** - Include files in conversations

### Autocomplete Integration

- **Inline Suggestions** - Real-time code completion
- **Context Awareness** - Understand project context
- **Multi-provider Support** - Use different models for different tasks

### Diff Visualization

- **Real-time Diffs** - See changes as they happen
- **Interactive Review** - Accept/reject individual changes
- **Historical Tracking** - Maintain change history

## 🔧 Service Architecture

### Core Services

- **`voidSettingsService`** - Configuration and settings management
- **`voidModelService`** - Model and provider management
- **`editCodeService`** - Code editing and application
- **`voidChatService`** - Chat and conversation management

### Service Registration

Services are registered using VSCode's dependency injection:

```typescript
registerSingleton(voidSettingsService, VoidSettingsService);
registerSingleton(voidModelService, VoidModelService);
registerSingleton(editCodeService, EditCodeService);
```

## 🛠️ Development

### Adding New Features

1. **Determine Process Location**:
   - Browser process → `browser/` directory
   - Main process → `electron-main/` directory
   - Shared → `common/` directory

2. **Create Service** (if needed):
   - Implement service class
   - Register in service registry
   - Add to dependency injection

3. **Add UI Components** (if needed):
   - Create React components in `browser/react/`
   - Register with VSCode contribution points
   - Add styling and assets

4. **Update Configuration**:
   - Add settings to `voidSettingsService`
   - Update model capabilities if needed
   - Add to user interface

### Communication Between Processes

Void uses a channel-based communication system:

```typescript
// Main process to browser
mainProcessChannel.send('void-event', data);

// Browser to main process
mainProcessChannel.call('void-command', params);
```

## 📋 Configuration

### Settings Structure

Void settings are organized by feature:

```typescript
interface VoidSettings {
  // Provider configuration
  providers: ProviderConfiguration[];
  
  // Model settings
  models: ModelSettings;
  
  // Feature toggles
  features: {
    autocomplete: boolean;
    chat: boolean;
    apply: boolean;
  };
  
  // UI preferences
  ui: UISettings;
}
```

### Model Capabilities

The `modelCapabilities` file defines what each model can do:

```typescript
interface ModelCapability {
  name: string;
  provider: string;
  supportsChat: boolean;
  supportsCompletion: boolean;
  maxTokens: number;
  // ... other capabilities
}
```

## 🔍 Testing

### Unit Tests

- Service layer testing
- UI component testing
- Communication protocol testing

### Integration Tests

- End-to-end AI workflows
- Multi-process communication
- Model provider integration

### Manual Testing

- AI provider connectivity
- Code application accuracy
- UI responsiveness and usability

## 📚 Key Files

### Core Services

- **`services/voidSettingsService.ts`** - Settings management
- **`services/editCodeService.ts`** - Code editing
- **`electron-main/sendLLMMessage.ts`** - AI communication

### UI Components

- **`browser/react/chat.tsx`** - Chat interface
- **`browser/react/autocomplete.tsx`** - Autocomplete UI
- **`browser/media/`** - Icons and assets

### Configuration

- **`common/protocols/`** - Communication protocols
- **`common/types/`** - Shared type definitions
- **`modelCapabilities`** - Model feature definitions

## 🔗 Related Documentation

- **[Void Codebase Guide](../../../VOID_CODEBASE_GUIDE.md)** - Architecture overview
- **[Contributing Guide](../../../HOW_TO_CONTRIBUTE.md)** - Development setup
- **[Main README](../../../README.md)** - Project overview

---

**This is the heart of Void's AI-powered development experience. All major Void features are implemented here.**
