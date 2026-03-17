# <div align="center">
  <img src="./src/vs/workbench/browser/parts/editor/media/slice_of_void.png" alt="Void Welcome" width="100" height="100"/>
  <h1>Void</h1>
  <p><strong>The open-source Cursor alternative</strong></p>
</div>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D20.18.2-brightgreen)](https://nodejs.org/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)](https://github.com/voideditor/void)
[![Discord](https://img.shields.io/discord/1102584477606404118?color=blue&label=discord)](https://discord.gg/RSNjgaugJs)
[![Project Status](https://img.shields.io/badge/status-paused-orange)](https://github.com/voideditor/void#note)

> Use AI agents on your codebase, checkpoint and visualize changes, and bring any model or host locally. Void sends messages directly to providers without retaining your data.

## 🚀 Quick Start

Get Void running in **5 minutes**:

### Prerequisites
- **Node.js** >= 20.18.2 (use `nvm install && nvm use` for automatic setup)
- **Build Tools**:
  - **Windows**: Visual Studio 2022 with "Desktop development with C++" and "Node.js build tools"
  - **macOS**: Xcode and Python (usually pre-installed)
  - **Linux**: `sudo apt-get install build-essential g++ libx11-dev libxkbfile-dev` (Ubuntu/Debian)

### Installation

```bash
# Clone the repository
git clone https://github.com/voideditor/void.git
cd void

# Install dependencies
npm install

# Build in development mode
npm run watch  # or press Ctrl+Shift+B in VSCode
```

### Launch Void

```bash
# Start the development version
./scripts/code.sh     # macOS/Linux
./scripts/code.bat    # Windows
```

**🎉 Done!** Open the Void window and start coding with AI assistance.

---

## 📖 Overview

This repository contains the full source code for Void, an open-source IDE that brings AI-powered development tools directly to your workflow. Built as a fork of VSCode, Void maintains familiar functionality while adding powerful AI capabilities.

### ✨ Key Features
- **AI Agent Integration** - Connect multiple AI models and providers
- **Code Checkpointing** - Visualize and track changes over time
- **Local Model Support** - Run models locally for privacy and speed
- **Direct Provider Communication** - No data retention, maximum privacy
- **Familiar VSCode Experience** - All your favorite extensions and shortcuts

### 🎯 Target Users
- **Developers** wanting AI assistance without vendor lock-in
- **Teams** requiring on-premise AI solutions
- **Privacy-conscious** coders who need local model support
- **Open-source contributors** building the future of development tools

---

## 🛠️ Development

### For Contributors
We welcome contributions! See our [Contributing Guide](HOW_TO_CONTRIBUTE.md) for detailed setup instructions.

### Project Structure
```
void/
├── src/vs/workbench/contrib/void/    # Core Void functionality
├── extensions/                        # VSCode extensions
├── cli/                              # Command-line interface
├── build/                            # Build system and pipelines
├── resources/                        # Icons and assets
└── scripts/                          # Development and build scripts
```

### Key Documentation
- **[Void Codebase Guide](VOID_CODEBASE_GUIDE.md)** - Understanding the architecture
- **[Contributing Guide](HOW_TO_CONTRIBUTE.md)** - Development setup and workflow
- **[void-builder](https://github.com/voideditor/void-builder)** - Build and distribution

---

## 🤝 Community & Support

- **� [Website](https://voideditor.com)** - Official project site
- **💬 [Discord](https://discord.gg/RSNjgaugJs)** - Chat with the community
- **📋 [Project Board](https://github.com/orgs/voideditor/projects/2)** - Roadmap and issues
- **📧 [Email](mailto:hello@voideditor.com)** - Direct contact

---

## ⚠️ Important Note

**We've paused work on the Void IDE** (this repository) to explore novel coding ideas. We're focusing on innovation over feature-parity.

**What this means:**
- ✅ Void continues running and remains functional
- ⚠️ Some existing features may stop working over time
- 🔄 Active maintenance and issue reviews are paused
- 📧 We'll respond to all email inquiries about building your own version

**Interested in maintaining Void?** Contact us - we'd love to help you get started with your own fork!

---

## 📄 License & Credits

Void is licensed under the [MIT License](LICENSE.txt).

**Base Project**: Fork of [Microsoft VSCode](https://github.com/microsoft/vscode)
**Original Code**: Inherits VSCode's licensing and credits
**Void Modifications**: Our additions are open source under MIT

See [ThirdPartyNotices.txt](ThirdPartyNotices.txt) for complete attribution.

---

## 🔗 Related Projects

- **[void-builder](https://github.com/voideditor/void-builder)** - Build and distribution system
- **[awesome-readme](https://github.com/matiassingers/awesome-readme)** - README inspiration
- **[vscode](https://github.com/microsoft/vscode)** - Original VSCode repository

---

<div align="center">

**[⬆ Back to top](#-void)**

Made with ❤️ by the Void community

</div>
