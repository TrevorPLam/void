# Void Tests

This directory contains the comprehensive test suite for Void, inherited from VSCode's testing framework and enhanced with Void-specific tests.

## 📋 Test Categories

### Core Test Suites

- **[unit/](unit/)** - Unit tests for individual components and services
- **[integration/](integration/)** - API integration tests and cross-component testing
- **[smoke/](smoke/)** - Automated UI tests and end-to-end workflows
- **[monaco/](monaco/)** - Monaco editor specific tests
- **[automation/](automation/)** - Automated testing infrastructure

### Void-Specific Tests

- **AI Integration Tests** - LLM communication and model management
- **Code Editing Tests** - Fast Apply and diff visualization
- **UI Component Tests** - Void-specific React components
- **Performance Tests** - AI feature performance benchmarks

## 🚀 Quick Start

### Running All Tests

```bash
# Run unit tests
npm run test

# Run integration tests
npm run test-integration

# Run smoke tests
npm run test-smoke

# Run specific test suite
npm run test -- --grep "Void"
```

### Development Testing

```bash
# Watch mode for unit tests
npm run test-watch

# Run tests with coverage
npm run test-coverage

# Debug tests
npm run test-debug
```

## 📁 Directory Structure

```
test/
├── unit/                    # Unit tests
│   ├── browser/            # Browser process tests
│   ├── common/             # Shared component tests
│   └── electron-main/      # Main process tests
├── integration/            # Integration tests
│   ├── browser/            # Browser integration tests
│   └── electron/           # Electron integration tests
├── smoke/                  # End-to-end UI tests
├── monaco/                 # Monaco editor tests
├── automation/             # Test automation infrastructure
├── leaks/                  # Memory leak detection
└── README.md              # This file
```

## 🔧 Test Framework

### Test Runner

Void uses **Mocha** as the primary test runner with **Chai** for assertions:

```javascript
describe('Void Feature', () => {
  it('should perform expected behavior', () => {
    expect(result).to.equal(expected);
  });
});
```

### Test Categories

#### Unit Tests
- **Individual component testing**
- **Service layer validation**
- **Utility function verification**
- **Mock dependencies for isolation**

#### Integration Tests
- **Cross-component communication**
- **API contract validation**
- **Service integration testing**
- **Process communication testing**

#### Smoke Tests
- **UI workflow validation**
- **User journey testing**
- **Performance regression detection**
- **Environment compatibility testing**

## 🧪 Void-Specific Testing

### AI Feature Testing

```typescript
describe('LLM Integration', () => {
  it('should send messages to provider', async () => {
    const response = await sendLLMMessage(testMessage);
    expect(response).to.have.property('content');
  });

  it('should handle model capabilities', () => {
    const capabilities = getModelCapabilities('gpt-4');
    expect(capabilities.supportsChat).to.be.true;
  });
});
```

### Code Editing Tests

```typescript
describe('Fast Apply', () => {
  it('should apply search/replace blocks', () => {
    const result = applyFastApply(originalCode, replaceBlock);
    expect(result).to.equal(expectedCode);
  });

  it('should handle streaming updates', async () => {
    const stream = createStreamingApply();
    // Test streaming behavior
  });
});
```

### UI Component Tests

```typescript
describe('Chat Interface', () => {
  it('should render chat messages', () => {
    const component = mount(<ChatInterface messages={testMessages} />);
    expect(component.find('.chat-message')).to.have.length(testMessages.length);
  });
});
```

## 📊 Test Coverage

### Coverage Goals

- **Unit Tests**: >90% line coverage for core services
- **Integration Tests**: >80% API coverage
- **Smoke Tests**: Critical user journey coverage

### Coverage Reports

```bash
# Generate coverage report
npm run test-coverage

# View coverage in browser
open coverage/lcov-report/index.html
```

## 🔍 Debugging Tests

### Debug Configuration

VS Code debug configuration for tests:

```json
{
  "type": "node",
  "request": "launch",
  "name": "Debug Tests",
  "program": "${workspaceFolder}/node_modules/.bin/mocha",
  "args": ["--inspect-brk", "test/unit/**/*.test.js"],
  "console": "integratedTerminal"
}
```

### Common Debugging Techniques

1. **Use `debugger` statements** in test code
2. **Run tests in isolation** to identify failing tests
3. **Use `--grep`** to run specific test patterns
4. **Check test logs** for detailed error information

## 📈 Performance Testing

### AI Feature Performance

```typescript
describe('AI Performance', () => {
  it('should respond within timeout', async () => {
    const start = Date.now();
    await sendLLMMessage(testMessage);
    const duration = Date.now() - start;
    expect(duration).to.be.below(5000); // 5 second timeout
  });
});
```

### Memory Leak Detection

The `leaks/` directory contains tools for detecting memory leaks:

```bash
# Run leak detection
npm run test-leaks

# Monitor memory usage
node --inspect test/leaks/memory-monitor.js
```

## 🛠️ Test Utilities

### Mock Services

Void provides mock implementations for testing:

```typescript
// Mock LLM provider
const mockProvider = {
  sendMessage: sinon.stub().resolves(mockResponse),
  getCapabilities: sinon.stub().returns(mockCapabilities)
};
```

### Test Helpers

Common test utilities for Void features:

```typescript
// Helper for testing code editing
function createTestEditor(content: string): TestCodeEditor {
  // Create test editor instance
}

// Helper for AI testing
function createMockLLMResponse(content: string): LLMResponse {
  // Create mock response
}
```

## 📋 CI/CD Integration

### Azure Pipelines

Tests run automatically in CI/CD pipelines:

- **Pull Request**: Unit and integration tests
- **Main Branch**: Full test suite including smoke tests
- **Release**: Performance and compatibility tests

### Test Results

Test results are published to:
- **Azure Pipelines** - Build pipeline results
- **Code Coverage** - Coverage reports and trends
- **Performance Metrics** - Benchmark results and trends

## 🔗 Related Documentation

- **[Contributing Guide](../HOW_TO_CONTRIBUTE.md)** - Development setup
- **[Void Codebase Guide](../VOID_CODEBASE_GUIDE.md)** - Architecture overview
- **[VSCode Testing Guide](https://github.com/microsoft/vscode/wiki/Testing)** - Original VSCode testing practices

---

**For detailed information about specific test suites, see the README files in each test directory.**
