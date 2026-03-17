# Development Scripts

This directory contains utility scripts for building, testing, and developing Void. These scripts automate common development tasks and provide convenient shortcuts for working with the Void codebase.

## 🚀 Quick Start

### Common Development Tasks

```bash
# Start Void in development mode
./scripts/code.sh

# Build Void for production
./scripts/build.sh

# Run all tests
./scripts/test.sh

# Clean build artifacts
./scripts/clean.sh
```

## 📁 Directory Structure

```
scripts/
├── code.sh                   # Main Void launcher
├── code.bat                  # Windows Void launcher
├── build.sh                  # Build script (Unix-like systems)
├── test.sh                   # Test runner script
├── clean.sh                  # Build cleanup script
├── release.sh                # Release preparation script
├── appimage/                 # AppImage creation scripts
└── *.ps1                     # PowerShell scripts (Windows)
```

## 🔧 Available Scripts

### Development Scripts

#### `code.sh` / `code.bat`
Main Void launcher script.

```bash
# Basic usage
./scripts/code.sh

# With custom user data directory
./scripts/code.sh --user-data-dir ./my-data

# Development mode
./scripts/code.sh --dev

# Specific workspace
./scripts/code.sh ./my-project
```

**Features:**
- Automatic dependency checking
- Environment validation
- Development mode activation
- Custom configuration support

#### `build.sh`
Build Void for production or development.

```bash
# Full build
./scripts/build.sh

# Development build
./scripts/build.sh --dev

# Specific platform
./scripts/build.sh --platform linux-x64
```

#### `test.sh`
Run the Void test suite.

```bash
# All tests
./scripts/test.sh

# Unit tests only
./scripts/test.sh --unit

# Integration tests only
./scripts/test.sh --integration

# With coverage
./scripts/test.sh --coverage
```

### Utility Scripts

#### `clean.sh`
Clean build artifacts and temporary files.

```bash
# Clean all build artifacts
./scripts/clean.sh

# Clean specific directories
./scripts/clean.sh --build-only

# Clean dependencies
./scripts/clean.sh --deps
```

#### `release.sh`
Prepare Void for release.

```bash
# Prepare release
./scripts/release.sh --version 1.0.0

# Create packages
./scripts/release.sh --package

# Update version numbers
./scripts/release.sh --bump patch
```

## 🖥️ Platform-Specific Scripts

### Windows Scripts

#### `code.bat`
Windows launcher script with PowerShell integration.

```batch
REM Basic usage
scripts\code.bat

REM With administrator privileges
scripts\code.bat --admin

REM Debug mode
scripts\code.bat --debug
```

#### PowerShell Scripts (`.ps1`)
Advanced Windows automation scripts.

```powershell
# Build with PowerShell
.\scripts\build.ps1

# Test with PowerShell
.\scripts\test.ps1

# Release with PowerShell
.\scripts\release.ps1
```

### Linux Scripts

#### `code.sh`
Linux/Unix launcher script.

```bash
# Standard usage
./scripts/code.sh

# With specific display
./scripts/code.sh --display :1

# With custom environment
./scripts/code.sh --env production
```

### macOS Scripts

#### `code.sh`
macOS launcher with system integration.

```bash
# Standard usage
./scripts/code.sh

# With specific architecture
./scripts/code.sh --arch arm64

# With system integration
./scripts/code.sh --system-integration
```

## 📦 Package Creation Scripts

### AppImage Scripts (`appimage/`)

Create Linux AppImage packages:

```bash
# Create AppImage
./scripts/appimage/create-appimage.sh

# With custom icon
./scripts/appimage/create-appimage.sh --icon custom.png

# Portable version
./scripts/appimage/create-appimage.sh --portable
```

### Distribution Packages

Scripts for creating platform-specific packages:

```bash
# Debian package
./scripts/create-deb.sh

# RPM package
./scripts/create-rpm.sh

# Windows installer
./scripts/create-installer.bat
```

## 🔍 Script Configuration

### Environment Variables

Scripts respect these environment variables:

```bash
# Node.js version
export NODE_VERSION=20.18.2

# Build configuration
export BUILD_TYPE=production

# Test configuration
export TEST_ENV=ci

# Release configuration
export RELEASE_CHANNEL=stable
```

### Configuration Files

- **`.env`** - Local environment configuration
- **`scripts/config.sh`** - Global script configuration
- **`scripts/platform-config.sh`** - Platform-specific settings

## 🛠️ Script Development

### Adding New Scripts

1. **Create script file** with appropriate extension:
   - `.sh` for Unix-like systems
   - `.bat` for Windows
   - `.ps1` for PowerShell

2. **Add script header** with standard information:
   ```bash
   #!/bin/bash
   # Void Development Script
   # Description: Brief description of script purpose
   # Usage: ./scripts/script-name.sh [options]
   ```

3. **Implement error handling**:
   ```bash
   set -e  # Exit on error
   set -u  # Exit on undefined variables
   ```

4. **Add help documentation**:
   ```bash
   function show_help() {
     echo "Usage: $0 [options]"
     echo "Options:"
     echo "  --help     Show this help message"
     echo "  --version  Show version information"
   }
   ```

5. **Test script** before committing:
   ```bash
   # Test in development environment
   ./scripts/test-script.sh --dry-run
   ```

### Script Standards

#### Error Handling
- Use `set -e` for bash scripts
- Implement proper error messages
- Provide exit codes for different scenarios

#### Logging
- Use consistent logging format
- Include timestamps for long-running operations
- Provide verbose and quiet modes

#### Compatibility
- Test on target platforms
- Handle platform differences gracefully
- Provide fallbacks for missing dependencies

## 🔧 Advanced Usage

### Script Chaining

Combine scripts for complex workflows:

```bash
# Build and test
./scripts/build.sh && ./scripts/test.sh

# Clean, build, and package
./scripts/clean.sh && ./scripts/build.sh && ./scripts/release.sh --package
```

### Parallel Execution

Run scripts in parallel for faster builds:

```bash
# Parallel build and test
./scripts/build.sh & ./scripts/test.sh & wait
```

### CI/CD Integration

Scripts are designed for CI/CD pipelines:

```yaml
# Azure Pipelines example
- script: ./scripts/build.sh --ci
  displayName: 'Build Void'

- script: ./scripts/test.sh --coverage
  displayName: 'Run Tests'
```

## 📋 Troubleshooting

### Common Issues

1. **Permission errors** - Make scripts executable:
   ```bash
   chmod +x scripts/*.sh
   ```

2. **Environment issues** - Check required tools:
   ```bash
   ./scripts/check-environment.sh
   ```

3. **Build failures** - Clean and rebuild:
   ```bash
   ./scripts/clean.sh && ./scripts/build.sh
   ```

### Debug Mode

Enable debug logging for troubleshooting:

```bash
# Enable debug mode
DEBUG=1 ./scripts/code.sh

# Verbose output
./scripts/build.sh --verbose

# Dry run (no changes)
./scripts/release.sh --dry-run
```

## 🔗 Related Documentation

- **[Build System](../build/README.md)** - Build system documentation
- **[Contributing Guide](../HOW_TO_CONTRIBUTE.md)** - Development setup
- **[Main README](../README.md)** - Project overview

---

**These scripts are designed to make Void development easier and more consistent across different platforms.**
