# Source Code

This directory contains the complete source code for Void, built on top of the VSCode architecture.

## 📁 Directory Structure

```
src/
├── bootstrap/              # Application entry points and initialization
├── typings/                # TypeScript type definitions
├── vscode-dts/            # VSCode API type definitions
└── vs/                    # Core VSCode/Void application
    ├── base/              # Base utilities and common functionality
    ├── code/              # VSCode editor and Monaco integration
    ├── editor/            # Monaco editor implementation
    ├── platform/          # Platform-specific code
    └── workbench/         # Main workbench and UI components
        ├── contrib/       # VSCode extensions and contributions
        │   └── void/      # ✨ Void-specific features
        ├── browser/       # Browser process code
        ├── common/        # Shared code between processes
        ├── electron-main/ # Main process code (Node.js access)
        └── services/      # Core services and dependency injection
```

## 🚀 Quick Start

### Understanding the Architecture

Void is built on VSCode's Electron architecture with two main processes:

- **Main Process** (`electron-main/`): Has access to Node.js modules and system APIs
- **Browser Process** (`browser/`): Runs the UI and web content, limited to browser APIs

### Key Void Code Location

Most Void-specific functionality lives in:
```
src/vs/workbench/contrib/void/
├── browser/               # Browser-side Void features
├── common/                # Shared Void utilities
├── electron-main/         # Main process Void features
└── services/              # Void-specific services
```

## 🔧 Development

### Adding New Void Features

1. **Browser-side features** → `src/vs/workbench/contrib/void/browser/`
2. **Main process features** → `src/vs/workbench/contrib/void/electron-main/`
3. **Shared utilities** → `src/vs/workbench/contrib/void/common/`
4. **Services** → `src/vs/workbench/contrib/void/services/`

### Important Patterns

- **Services**: Register with `registerSingleton()` for dependency injection
- **Actions/Commands**: Register for user-invocable operations
- **Cross-process communication**: Use channels between main and browser processes

### Build Process

The source code is compiled using TypeScript and the build system in the `build/` directory. See the main [README](../README.md) for build instructions.

## 📚 Key Documentation

- **[Void Codebase Guide](../VOID_CODEBASE_GUIDE.md)** - Detailed architecture explanation
- **[Contributing Guide](../HOW_TO_CONTRIBUTE.md)** - Development setup and workflow
- **[VSCode Source Organization](https://github.com/microsoft/vscode/wiki/Source-Code-Organization)** - Understanding VSCode's structure

## 🎯 Focus Areas

### AI Integration
- LLM message pipeline and provider communication
- Code editing and application services
- Model capability management

### User Interface
- Chat and autocomplete UI components
- Settings and configuration panels
- Diff visualization and code review tools

### Core Services
- File system integration
- Model and provider management
- Authentication and security

---

**For detailed information about specific components, see the README files in each subdirectory.**
