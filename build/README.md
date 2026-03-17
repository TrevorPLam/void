# Build System

This directory contains the complete build system for Void, including compilation scripts, packaging configurations, and CI/CD pipeline definitions.

## 🚀 Quick Start

### Building Void

```bash
# Install dependencies
npm install

# Development build (watch mode)
npm run watch

# Production build
npm run compile

# Package for distribution
npm run gulp vscode-darwin-x64    # macOS Intel
npm run gulp vscode-darwin-arm64  # macOS Apple Silicon
npm run gulp vscode-win32-x64    # Windows
npm run gulp vscode-linux-x64    # Linux
```

### Development Mode

For active development, use the built-in watch mode:

```bash
# Start development build
npm run watch

# Or use VSCode task: Ctrl+Shift+B → Run Build Task
```

## 📁 Directory Structure

```
build/
├── azure-pipelines/           # Azure DevOps CI/CD pipelines
├── builtin/                   # Built-in extensions and resources
├── checksums/                # Build integrity checksums
├── darwin/                   # macOS-specific build scripts
├── linux/                    # Linux-specific build scripts
├── win32/                    # Windows-specific build scripts
├── .cachesalt                # Build cache configuration
├── .gitattributes            # Git attributes for build
├── .gitignore               # Build-specific git ignores
├── .moduleignore             # Module ignore patterns
├── gulpfile.js              # Main build script (Gulp)
└── various build scripts     # Platform-specific utilities
```

## 🔧 Build Process

### 1. Dependencies Installation

```bash
npm install
```

Installs:
- Node.js dependencies
- TypeScript compiler
- Build tools (Gulp, ESLint, etc.)
- Development dependencies

### 2. Compilation

The build process compiles TypeScript to JavaScript and bundles the application:

```bash
# Full compilation
npm run compile

# Watch mode for development
npm run watch
```

### 3. Packaging

Creates platform-specific distributables:

```bash
# macOS packages
npm run gulp vscode-darwin-x64
npm run gulp vscode-darwin-arm64

# Windows packages
npm run gulp vscode-win32-x64
npm run gulp vscode-win32-arm64

# Linux packages
npm run gulp vscode-linux-x64
npm run gulp vscode-linux-arm64
```

## 🛠️ Build Components

### Gulp Tasks

The build system uses Gulp for task automation:

- **`compile`** - TypeScript compilation
- **`watch`** - Development build with file watching
- **`vscode-*`** - Platform-specific packaging
- **`eslint`** - Code linting
- **`clean`** - Clean build artifacts

### TypeScript Configuration

- **`tsconfig.json`** - TypeScript compiler options
- **`src/tsconfig.base.json`** - Base TypeScript configuration
- **Multiple tsconfig files** - Different configurations for different parts

### Platform-Specific Builds

Each platform has specific requirements:

#### Windows
- Visual Studio build tools required
- Windows-specific packaging and signing
- Installer creation

#### macOS
- Xcode command line tools required
- Code signing and notarization
- DMG creation

#### Linux
- Various Linux distribution support
- Package creation (deb, rpm, AppImage)
- Dependency management

## 📦 Build Artifacts

### Development Build

Located in `.build/` directory:
```
.build/
├── electron/               # Electron application
├── client/                 # Browser client code
├── server/                 # Server-side code
└── extensions/            # Built-in extensions
```

### Production Packages

Platform-specific distributables:
- **Windows**: `.exe` installer and portable versions
- **macOS**: `.dmg` disk images and unsigned builds
- **Linux**: `.deb`, `.rpm`, `.AppImage` packages

## 🔍 CI/CD Integration

### Azure Pipelines

The `azure-pipelines/` directory contains:

- **`product-build.yml`** - Main build pipeline
- **`product-build-pr.yml`** - Pull request builds
- **`distro-build.yml`** - Distribution builds

### Build Pipeline Stages

1. **Setup** - Install dependencies and tools
2. **Compile** - Build TypeScript and bundle code
3. **Test** - Run unit and integration tests
4. **Package** - Create platform-specific packages
5. **Sign** - Code signing (where applicable)
6. **Publish** - Upload to distribution channels

## ⚙️ Configuration

### Build Configuration Files

- **`product.json`** - Product metadata and configuration
- **`cgmanifest.json`** - Component governance manifest
- **`package.json`** - Node.js dependencies and scripts

### Environment Variables

- **`NODE_ENV`** - Environment (development/production)
- **`BUILD_ARCH`** - Target architecture
- **`BUILD_PLATFORM`** - Target platform

## 🔧 Customization

### Adding New Build Tasks

1. **Create task in Gulpfile** - Add new Gulp task
2. **Update package.json** - Add npm script if needed
3. **Test locally** - Verify task works correctly
4. **Update CI** - Add to Azure Pipelines if needed

### Platform Support

To add support for a new platform:

1. **Create platform directory** - Add build scripts
2. **Update Gulp tasks** - Add packaging logic
3. **Configure CI** - Update Azure Pipelines
4. **Test thoroughly** - Verify build and functionality

## 📋 Dependencies

### Required Tools

- **Node.js** >= 20.18.2
- **npm** or **yarn** package manager
- **Python** (for some native modules)
- **Platform-specific build tools**:
  - Windows: Visual Studio 2022
  - macOS: Xcode Command Line Tools
  - Linux: GCC/Clang and development libraries

### Development Dependencies

- **TypeScript** - Language compilation
- **Gulp** - Build task runner
- **ESLint** - Code linting
- **Electron** - Application framework

## 🔗 Related Documentation

- **[Contributing Guide](../HOW_TO_CONTRIBUTE.md)** - Development setup
- **[Void Codebase Guide](../VOID_CODEBASE_GUIDE.md)** - Architecture overview
- **[void-builder](https://github.com/voideditor/void-builder)** - Distribution system

---

**For detailed build instructions, see the [Contributing Guide](../HOW_TO_CONTRIBUTE.md).**
