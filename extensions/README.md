# Extensions

This directory contains the VSCode extensions that are bundled with Void. These extensions provide core functionality for language support, development tools, and integration services.

## 📁 Directory Overview

```
extensions/
├── [language-name]-language-features/    # Language support extensions
├── [tool-name]/                         # Tool integrations
├── authentication/                      # Authentication providers
└── ui/                                 # User interface extensions
```

## 🔧 Language Support Extensions

### Web Technologies
- **html-language-features/** - HTML IntelliSense, validation, and formatting
- **css-language-features/** - CSS completion, linting, and color pickers
- **json-language-features/** - JSON schema validation and completion
- **markdown-language-features/** - Markdown preview, editing, and linting
- **typescript-language-features/** - TypeScript and JavaScript IntelliSense

### Development Tools
- **git/** - Git source control integration
- **github/** - GitHub integration features
- **npm/** - npm script execution and package management
- **emmet/** - Emmet abbreviation expansion
- **search-result/** - Search result UI enhancements

### Authentication
- **github-authentication/** - GitHub OAuth authentication
- **microsoft-authentication/** - Microsoft account authentication

## 🚀 Extension Development

### Structure of a Language Extension

```
[language]-language-features/
├── client/                    # Browser-side extension code
├── server/                    # Language server (if applicable)
├── package.json              # Extension manifest
├── README.md                 # Extension documentation
└── test/                     # Extension tests
```

### Key Files

- **package.json** - Extension metadata, activation events, and contribution points
- **README.md** - Extension-specific documentation and setup instructions
- **client/** - Code that runs in the browser process
- **server/** - Language server implementation (if separate process needed)

## 📚 Extension Categories

### Language Features
Provide IntelliSense, validation, formatting, and other language-specific features:

- Syntax highlighting and semantic tokenization
- Code completion and parameter hints
- Error checking and linting
- Code formatting and document organization
- Refactoring and code navigation

### Tool Integrations
Integrate external development tools and services:

- Version control (Git, GitHub)
- Package managers (npm, yarn)
- Build tools and task runners
- Debugging and profiling tools

### Authentication Providers
Handle authentication with external services:

- OAuth flows for cloud services
- Token management and refresh
- Multi-provider authentication
- Secure credential storage

## 🛠️ Development Guidelines

### Adding New Extensions

1. **Create directory structure** following naming conventions
2. **Implement extension manifest** in `package.json`
3. **Add extension documentation** in `README.md`
4. **Register extension** in the build system
5. **Write tests** for core functionality

### Best Practices

- **Follow VSCode extension API** conventions
- **Implement proper error handling** and user feedback
- **Provide clear documentation** for setup and usage
- **Include comprehensive tests** for reliability
- **Handle activation events** efficiently

## 🔗 Related Documentation

- **[VSCode Extension API](https://code.visualstudio.com/api)** - Official extension development guide
- **[Extension Manifest](https://code.visualstudio.com/api/references/extension-manifest)** - package.json reference
- **[Contribution Points](https://code.visualstudio.com/api/references/contribution-points)** - Extension integration points

## 📋 Extension Status

Most extensions in this directory are inherited from the VSCode codebase and maintained to ensure compatibility with Void's architecture. Some extensions may have Void-specific modifications for AI integration or enhanced functionality.

---

**For extension-specific documentation, see the README files in each extension directory.**
