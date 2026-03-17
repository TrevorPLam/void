# Void CLI

The Void Command Line Interface provides command-line access to Void's features and development tools.

## 🚀 Quick Start

### Installation

The CLI is built as part of the main Void build process. After building Void:

```bash
# From the void repository root
./scripts/code.sh --help
```

### Basic Usage

```bash
# Start Void with specific configuration
./scripts/code.sh --user-data-dir ./my-data

# Open Void with specific workspace
./scripts/code.sh ./my-project

# Enable developer mode
./scripts/code.sh --dev

# List all available options
./scripts/code.sh --help
```

## 📁 Directory Structure

```
cli/
├── src/
│   ├── bin/                  # Entry points and executables
│   ├── commands/             # CLI command implementations
│   ├── desktop/              # Desktop integration
│   └── *.rs                  # Rust source files
├── Cargo.toml                # Rust package configuration
├── Cargo.lock                # Dependency lock file
└── README.md                 # This file
```

## 🔧 Available Commands

### Development Commands

- **`code`** - Start Void IDE
- **`code --dev`** - Enable development mode
- **`code --help`** - Show all available options
- **`code --version`** - Display version information

### Configuration Options

- **`--user-data-dir <path>`** - Set user data directory
- **`--extensions-dir <path>`** - Set extensions directory
- **`--profile <name>`** - Use specific profile
- **`--locale <locale>`** - Set interface language

### Workspace Management

- **`code <workspace-path>`** - Open specific workspace
- **`code --new-window`** - Open in new window
- **`code --reuse-window`** - Reuse existing window

## 🛠️ Development

### Building the CLI

The CLI is written in Rust and built as part of the main Void build:

```bash
# From repository root
npm run build-cli

# Or build everything including CLI
npm run watch
```

### Adding New Commands

1. **Create command module** in `src/commands/`
2. **Implement command logic** following existing patterns
3. **Register command** in the CLI entry point
4. **Add documentation** and help text
5. **Write tests** for the new functionality

### Code Structure

- **Entry Points** (`src/bin/`) - Main executable files
- **Commands** (`src/commands/`) - Individual command implementations
- **Desktop Integration** (`src/desktop/`) - OS-specific integrations
- **Utilities** - Shared CLI utilities and helpers

## 🔗 Integration

### With Void IDE

The CLI integrates tightly with the Void IDE:

- **Configuration sharing** - Uses same settings and preferences
- **Extension management** - Can manage extensions from command line
- **Workspace handling** - Seamlessly opens workspaces in IDE
- **Profile support** - Supports multiple user profiles

### With Development Tools

- **Build system integration** - Works with npm build scripts
- **Testing support** - Can run test suites from command line
- **Debugging** - Provides debugging interfaces
- **Extension development** - Supports extension development workflows

## 📚 Configuration

### Settings Files

The CLI respects Void's configuration system:

- **Settings** - Shared with IDE configuration
- **Keybindings** - Command line keybinding support
- **Extensions** - Extension state and management
- **Profiles** - Multiple configuration profiles

### Environment Variables

- **`VOID_USER_DATA_DIR`** - Override user data directory
- **`VOID_EXTENSIONS_DIR`** - Override extensions directory
- **`VOID_LOG_LEVEL`** - Set logging verbosity
- **`NODE_ENV`** - Node environment setting

## 🔍 Troubleshooting

### Common Issues

1. **Build failures** - Ensure Rust and Node.js are properly installed
2. **Permission errors** - Check file permissions on target directories
3. **Path issues** - Use absolute paths for workspace directories
4. **Configuration conflicts** - Check for conflicting settings

### Debug Mode

Enable debug logging for troubleshooting:

```bash
./scripts/code.sh --log-level debug
```

## 📋 Dependencies

- **Rust** - Core CLI implementation language
- **Node.js** - Integration with Void's Node.js components
- **Electron** - Desktop application framework
- **VSCode APIs** - Integration with VSCode extension system

---

**For more detailed information about Void development, see the main [README](../README.md) and [Contributing Guide](../HOW_TO_CONTRIBUTE.md).**
