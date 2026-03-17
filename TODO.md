# Void TODO

Based on codebase analysis and 2026 tooling research, this document tracks implementation priorities to elevate Void from a paused open-source AI IDE to a competitive, modern development environment.

---

## [ ] VOID-001: Modernize Build System

### Definition of Done
- [ ] Build time reduced from ~15s to < 5 seconds
- [ ] Hot Module Replacement (HMR) working with < 50ms latency
- [ ] No manual style refresh hacks in build pipeline
- [ ] All React components building with SWC instead of TSC
- [ ] Package manager migrated from npm to pnpm
- [ ] CI/CD pipelines updated with pnpm caching

### Out of Scope
- Full VSCode extension system migration
- Electron version upgrades (major version changes)
- Complete UI framework replacement
- Mobile app development
- Cloud infrastructure setup

### Strict Rules to Follow
- MUST maintain VSCode extension API compatibility
- MUST keep `strict: true` TypeScript configuration
- MUST preserve all 15+ AI provider integrations
- MUST maintain Electron main/browser process separation
- MUST keep MCP protocol compatibility

### Existing Code Patterns
```typescript
// Current build process (build.js)
// scope-tailwind → src2/ → tsup → out/
// Two-pass build with manual file watching
execSync('npx scope-tailwind ./src -o src2/ -s void-scope -c styles.css -p "void-"');
execSync('npx tsup');

// Current tsconfig (good foundation)
{
  "compilerOptions": {
    "strict": true,
    "jsx": "react-jsx",
    "moduleResolution": "NodeNext"
  }
}
```

### Advanced Code Patterns
```typescript
// Target: Vite + SWC configuration
// vite.config.ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react-swc'

export default defineConfig({
  plugins: [react()], // SWC-powered React
  root: './src',
  build: {
    outDir: './out',
    lib: {
      entry: [
        'sidebar-tsx/index.tsx',
        'void-settings-tsx/index.tsx',
        'void-editor-widgets-tsx/index.tsx',
        'void-onboarding/index.tsx',
        'quick-edit-tsx/index.tsx',
        'diff/index.tsx'
      ],
      formats: ['es']
    },
    rollupOptions: {
      external: [/^\.\.\/.\.\./] // Keep VSCode externals external
    }
  },
  css: {
    postcss: {
      plugins: [scopedTailwindPlugin] // Integrated CSS scoping
    }
  }
})
```

### Anti-Patterns
- ❌ Manual file watching with setTimeout hacks
- ❌ Two-pass build process (CSS → JS)
- ❌ npm install in CI without caching
- ❌ Running tsc for type checking during build
- ❌ Modifying node_modules for quick fixes

---

## Subtasks

#### [ ] VOID-001-1: Set up Vite configuration
**Target Files**: `src/vs/workbench/contrib/void/browser/react/vite.config.ts`
**Related Files**: `src/vs/workbench/contrib/void/browser/react/package.json`, `src/vs/workbench/contrib/void/browser/react/tsconfig.json`

#### [ ] VOID-001-2: Integrate scope-tailwind as PostCSS plugin
**Target Files**: `src/vs/workbench/contrib/void/browser/react/postcss.config.js`
**Related Files**: `src/vs/workbench/contrib/void/browser/react/tailwind.config.js`, `src/vs/workbench/contrib/void/browser/react/src/styles.css`

#### [ ] VOID-001-3: Migrate to pnpm
**Target Files**: `package.json` (root), `.npmrc`, `package-lock.json` → `pnpm-lock.yaml`
**Related Files**: `.github/workflows/*.yml` (CI/CD updates)

#### [ ] VOID-001-4: Update build scripts
**Target Files**: `src/vs/workbench/contrib/void/browser/react/build.js` → `scripts/build-react.mjs`
**Related Files**: `package.json` scripts section

#### [ ] VOID-001-5: Verify HMR in development
**Target Files**: `src/vs/workbench/contrib/void/browser/react/src/util/services.tsx`
**Related Files**: All React component files

#### [ ] VOID-001-6: Update CI/CD for pnpm caching
**Target Files**: `.github/workflows/*.yml`
**Related Files**: `.npmrc` (pnpm configuration)

---

## [ ] VOID-002: Refactor AI Provider Architecture

### Definition of Done
- [ ] New provider added in < 50 lines (vs current ~100)
- [ ] All 15+ providers using unified adapter interface
- [ ] Unit testable with mock adapters
- [ ] Provider-specific logic isolated in adapters
- [ ] No breaking changes to existing provider configurations
- [ ] Error handling consistent across all providers

### Out of Scope
- Adding new AI providers (keep current 15+)
- Removing existing provider support
- Changing provider API keys or authentication
- LLM model training or fine-tuning
- Custom model hosting infrastructure

### Strict Rules to Follow
- MUST maintain backward compatibility with existing configs
- MUST preserve all current provider capabilities (FIM, tools, reasoning)
- MUST keep streaming response support for all providers
- MUST preserve retry logic and error handling patterns
- MUST NOT break user settings during migration

### Existing Code Patterns
```typescript
// Current implementation (sendLLMMessage.impl.ts: ~968 lines)
const _sendOpenAICompatibleChat = async ({ messages, onText, onFinalMessage, ... }) => {
  const openai = await newOpenAICompatibleSDK({ providerName, settingsOfProvider });
  const options: OpenAI.Chat.Completions.ChatCompletionCreateParamsStreaming = {
    model: modelName,
    messages: messages as any,
    stream: true,
    ...nativeToolsObj
  };
  // 100+ lines of provider-specific streaming logic
};

// Provider dispatch (940+ lines of provider definitions)
export const sendLLMMessageToProviderImplementation = {
  anthropic: { sendChat: sendAnthropicChat, sendFIM: null, list: null },
  openAI: { sendChat: (params) => _sendOpenAICompatibleChat(params), ... },
  // ... 13 more providers
};
```

### Advanced Code Patterns
```typescript
// Target: Clean adapter pattern
// adapters/base.ts
interface LLMAdapter {
  sendChat(params: ChatParams): Promise<ChatResponse>;
  sendFIM?(params: FIMParams): Promise<FIMResponse>;
  listModels?(): Promise<Model[]>;
  supports: AdapterCapabilities;
}

// adapters/openai.ts
class OpenAIAdapter implements LLMAdapter {
  constructor(private config: ProviderConfig) {}

  async sendChat(params: ChatParams): Promise<ChatResponse> {
    const client = new OpenAI({ apiKey: this.config.apiKey });
    return this.streamResponse(client.chat.completions.create({...}));
  }

  private streamResponse(promise) {
    // Unified streaming logic ~30 lines
  }
}

// adapters/registry.ts
const adapterRegistry: Record<ProviderName, AdapterConstructor> = {
  anthropic: AnthropicAdapter,
  openAI: OpenAIAdapter,
  // ... etc
};

// Usage: ~5 lines per provider
export function getAdapter(provider: ProviderName): LLMAdapter {
  const Constructor = adapterRegistry[provider];
  return new Constructor(getProviderConfig(provider));
}
```

### Anti-Patterns
- ❌ 900+ line files with mixed provider logic
- ❌ Copy-paste code between similar providers
- ❌ Provider-specific streaming logic scattered
- ❌ Hardcoded provider capabilities in multiple places
- ❌ No separation between transport and business logic

---

## Subtasks

#### [ ] VOID-002-1: Create base adapter interface
**Target Files**: `src/vs/workbench/contrib/void/common/adapters/llmAdapter.ts`
**Related Files**: `src/vs/workbench/contrib/void/common/sendLLMMessageTypes.ts`

#### [ ] VOID-002-2: Implement OpenAI-compatible base adapter
**Target Files**: `src/vs/workbench/contrib/void/electron-main/adapters/openaiBaseAdapter.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/llmMessage/sendLLMMessage.impl.ts`

#### [ ] VOID-002-3: Implement Anthropic adapter
**Target Files**: `src/vs/workbench/contrib/void/electron-main/adapters/anthropicAdapter.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/llmMessage/sendLLMMessage.impl.ts`

#### [ ] VOID-002-4: Implement Gemini adapter
**Target Files**: `src/vs/workbench/contrib/void/electron-main/adapters/geminiAdapter.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/llmMessage/sendLLMMessage.impl.ts`

#### [ ] VOID-002-5: Implement Ollama adapter
**Target Files**: `src/vs/workbench/contrib/void/electron-main/adapters/ollamaAdapter.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/llmMessage/sendLLMMessage.impl.ts`

#### [ ] VOID-002-6: Create adapter factory/registry
**Target Files**: `src/vs/workbench/contrib/void/electron-main/adapters/adapterFactory.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/sendLLMMessageChannel.ts`

#### [ ] VOID-002-7: Migrate all providers to new system
**Target Files**: `src/vs/workbench/contrib/void/electron-main/llmMessage/sendLLMMessage.impl.ts`
**Related Files**: All adapter files in `src/vs/workbench/contrib/void/electron-main/adapters/`

---

## [ ] VOID-003: State Management Modernization

### Definition of Done
- [ ] Zustand stores implemented for settings, threads, MCP
- [ ] React DevTools integration for state debugging
- [ ] Persistent state working for user settings
- [ ] No memory leaks from event listeners
- [ ] Time-travel debugging functional
- [ ] Gradual migration: old and new systems coexist
- [ ] All React components using new state hooks

### Out of Scope
- Rewriting service layer architecture
- Changing IPC communication patterns
- Database backend for state persistence
- Real-time collaboration state sync
- Undo/redo system for code edits

### Strict Rules to Follow
- MUST maintain current state shape for compatibility
- MUST dispose of old listeners properly
- MUST work with existing service injection
- MUST preserve event-driven updates for VSCode integration
- MUST NOT break existing settings storage

### Existing Code Patterns
```typescript
// Current pattern (services.tsx)
let settingsState: VoidSettingsState
const settingsStateListeners: Set<(s: VoidSettingsState) => void> = new Set()

export const _registerServices = (accessor: ServicesAccessor) => {
  const settingsStateService = accessor.get(IVoidSettingsService)
  settingsState = settingsStateService.state
  settingsStateService.onDidChangeState(() => {
    settingsState = settingsStateService.state
    settingsStateListeners.forEach(listener => listener(settingsState))
  })
}

export const useSettingsState = () => {
  const [state, setState] = useState(settingsState)
  useEffect(() => {
    settingsStateListeners.add(setState)
    return () => settingsStateListeners.delete(setState)
  }, [])
  return state
}
```

### Advanced Code Patterns
```typescript
// Target: Zustand stores
// stores/settingsStore.ts
import { create } from 'zustand'
import { persist } from 'zustand/middleware'

interface SettingsState {
  settingsOfProvider: SettingsOfProvider
  modelSelectionOfFeature: ModelSelectionOfFeature
  setSettingOfProvider: (provider, setting, value) => Promise<void>
  setModelSelectionOfFeature: (feature, value) => Promise<void>
}

export const useSettingsStore = create<SettingsState>()(
  persist(
    (set, get) => ({
      settingsOfProvider: defaultSettings,
      modelSelectionOfFeature: defaultSelections,
      setSettingOfProvider: async (provider, setting, value) => {
        // Call existing service, update state
        await settingsService.setSettingOfProvider(provider, setting, value)
        set({ settingsOfProvider: settingsService.state.settingsOfProvider })
      },
      // ... other actions
    }),
    {
      name: 'void-settings-storage',
      partialize: (state) => ({
        settingsOfProvider: state.settingsOfProvider
      })
    }
  )
)

// Usage in components
function ModelSelector() {
  const { modelSelectionOfFeature, setModelSelectionOfFeature } = useSettingsStore()
  // Automatic re-renders, devtools support, persistence
}
```

### Anti-Patterns
- ❌ Global variables outside React lifecycle
- ❌ Manual listener management
- ❌ No cleanup of event listeners
- ❌ Direct state mutation
- ❌ Mixing React and non-React state

---

## Subtasks

#### [ ] VOID-003-1: Add Zustand dependency
**Target Files**: `src/vs/workbench/contrib/void/browser/react/package.json`
**Related Files**: `src/vs/workbench/contrib/void/browser/react/vite.config.ts` (external deps config)

#### [ ] VOID-003-2: Create settings store
**Target Files**: `src/vs/workbench/contrib/void/browser/react/src/stores/settingsStore.ts`
**Related Files**: `src/vs/workbench/contrib/void/common/voidSettingsService.ts`

#### [ ] VOID-003-3: Create chat threads store
**Target Files**: `src/vs/workbench/contrib/void/browser/react/src/stores/threadsStore.ts`
**Related Files**: `src/vs/workbench/contrib/void/browser/chatThreadService.ts`

#### [ ] VOID-003-4: Create MCP store
**Target Files**: `src/vs/workbench/contrib/void/browser/react/src/stores/mcpStore.ts`
**Related Files**: `src/vs/workbench/contrib/void/common/mcpService.ts`

#### [ ] VOID-003-5: Migrate components to new stores
**Target Files**: `src/vs/workbench/contrib/void/browser/react/src/sidebar-tsx/SidebarChat.tsx`
**Related Files**: All components using `useSettingsState`, `useChatThreadsState`, etc.

---

## [ ] VOID-004: MCP Ecosystem Expansion

### Definition of Done
- [ ] HTTP Streamable transport implemented
- [ ] MCP server registry browser integrated
- [ ] 5+ built-in servers included (filesystem, git, fetch, etc.)
- [ ] Server templates for community contributions
- [ ] Automatic server discovery from mcp.json
- [ ] Server health monitoring and restart
- [ ] Tool result caching for performance

### Out of Scope
- MCP protocol server implementation (we're a client)
- Custom MCP transport protocols
- Paid MCP server marketplace
- MCP server hosting infrastructure
- Remote MCP server management UI

### Strict Rules to Follow
- MUST maintain compatibility with official MCP SDK
- MUST support all official transport types (stdio, SSE, HTTP)
- MUST preserve existing mcp.json configuration format
- MUST handle server crashes gracefully
- MUST keep tool execution sandboxed

### Existing Code Patterns
```typescript
// Current MCP implementation (mcpChannel.ts: ~396 lines)
export class MCPChannel implements IServerChannel {
  private readonly infoOfClientId: InfoOfClientId = {}
  private readonly _refreshingServerNames: Set<string> = new Set()

  private readonly mcpEmitters = {
    serverEvent: {
      onAdd: new Emitter<MCPServerEventResponse>(),
      onUpdate: new Emitter<MCPServerEventResponse>(),
      onDelete: new Emitter<MCPServerEventResponse>(),
    }
  }

  // Supports stdio and SSE transports currently
  // HTTP Streamable transport missing
}
```

### Advanced Code Patterns
```typescript
// Target: Full transport support + built-in servers
// transports/httpStreamable.ts
import { StreamableHTTPClientTransport } from '@modelcontextprotocol/sdk/client/streamableHttp'

export class HTTPStreamableTransport implements MCPTransport {
  private transport: StreamableHTTPClientTransport

  async connect(config: ServerConfig): Promise<void> {
    this.transport = new StreamableHTTPClientTransport(
      new URL(config.endpoint)
    )
    await this.transport.start()
  }

  async callTool(name: string, params: any): Promise<ToolResult> {
    return this.transport.send({ method: 'tools/call', params })
  }
}

// servers/builtinRegistry.ts
export const builtinServers: Record<string, ServerDefinition> = {
  'filesystem': {
    name: 'filesystem',
    description: 'Local file system access',
    transport: 'stdio',
    command: 'npx',
    args: ['-y', '@modelcontextprotocol/server-filesystem', '~'],
    builtin: true
  },
  'git': {
    name: 'git',
    description: 'Git repository operations',
    transport: 'stdio',
    command: 'npx',
    args: ['-y', '@modelcontextprotocol/server-git'],
    builtin: true
  },
  'fetch': {
    name: 'fetch',
    description: 'Web content fetching',
    transport: 'stdio',
    command: 'npx',
    args: ['-y', '@modelcontextprotocol/server-fetch'],
    builtin: true
  },
  'github': {
    name: 'github',
    description: 'GitHub API integration',
    transport: 'stdio',
    command: 'npx',
    args: ['-y', '@modelcontextprotocol/server-github'],
    builtin: true,
    requiresConfig: ['githubPersonalAccessToken']
  }
  // ... etc
}

// UI Integration
// mcpBrowser.tsx - Server marketplace UI
export function MCPServerMarketplace() {
  const availableServers = useAvailableMCPServers()
  const installedServers = useInstalledMCPServers()

  return (
    <div className="mcp-marketplace">
      <h2>MCP Server Registry</h2>
      {Object.values(builtinServers).map(server => (
        <ServerCard
          key={server.name}
          server={server}
          installed={!!installedServers[server.name]}
          onInstall={() => installServer(server)}
        />
      ))}
    </div>
  )
}
```

### Anti-Patterns
- ❌ Only supporting stdio transport
- ❌ Hardcoded server configurations
- ❌ No server health monitoring
- ❌ Synchronous tool calls blocking UI
- ❌ No tool result caching

---

## Subtasks

#### [ ] VOID-004-1: Implement HTTP Streamable transport
**Target Files**: `src/vs/workbench/contrib/void/electron-main/mcp/transports/httpStreamable.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/mcpChannel.ts`

#### [ ] VOID-004-2: Add transport abstraction layer
**Target Files**: `src/vs/workbench/contrib/void/electron-main/mcp/transports/base.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/mcpChannel.ts`

#### [ ] VOID-004-3: Create built-in server registry
**Target Files**: `src/vs/workbench/contrib/void/common/mcp/builtinServers.ts`
**Related Files**: `src/vs/workbench/contrib/void/common/mcpService.ts`

#### [ ] VOID-004-4: Add server marketplace UI
**Target Files**: `src/vs/workbench/contrib/void/browser/react/src/void-settings-tsx/MCPServers.tsx`
**Related Files**: `src/vs/workbench/contrib/void/browser/react/src/void-settings-tsx/Settings.tsx`

#### [ ] VOID-004-5: Implement server health monitoring
**Target Files**: `src/vs/workbench/contrib/void/electron-main/mcp/serverHealth.ts`
**Related Files**: `src/vs/workbench/contrib/void/electron-main/mcpChannel.ts`

#### [ ] VOID-004-6: Add tool result caching
**Target Files**: `src/vs/workbench/contrib/void/common/mcp/toolCache.ts`
**Related Files**: `src/vs/workbench/contrib/void/common/mcpService.ts`

---

## [ ] VOID-005: Agentic AI Features

### Definition of Done
- [ ] Planning agent: break down user requests into tasks
- [ ] Code review agent: automated PR reviews
- [ ] Documentation agent: auto-generate from code
- [ ] Testing agent: generate and run tests
- [ ] Multi-step task execution with checkpoints
- [ ] User approval flow for destructive actions
- [ ] Task history and replay capability

### Out of Scope
- Fully autonomous code changes without approval
- Multi-user collaborative agents (complex sync)
- Natural language to full application generation
- AI model training or fine-tuning
- Automatic deployment to production

### Strict Rules to Follow
- MUST require user approval for file modifications
- MUST maintain all existing safety checks
- MUST preserve checkpoint/rollback functionality
- MUST integrate with existing tool system
- MUST show reasoning/planning to user

### Existing Code Patterns
```typescript
// Current tool system (toolsService.ts: ~594 lines)
type CallBuiltinTool = {
  [T in BuiltinToolName]: (p: BuiltinToolCallParams[T]) =>
    Promise<{ result: BuiltinToolResultType[T], interruptTool?: () => void }>
}

// Chat thread with tool calls (chatThreadService.ts: ~1885 lines)
type ToolMessage = {
  role: 'tool'
  name: string
  params: any
  result: string
  approvalType?: ToolApprovalType
}
```

### Advanced Code Patterns
```typescript
// Target: Agent system built on existing tools
// agents/base.ts
interface Agent {
  name: string
  description: string
  plan: (request: string, context: AgentContext) => Promise<TaskPlan>
  execute: (plan: TaskPlan, onStep: StepCallback) => Promise<AgentResult>
}

// agents/planningAgent.ts
class PlanningAgent implements Agent {
  async plan(request: string, context: AgentContext): Promise<TaskPlan> {
    const llm = await this.getLLM()
    const response = await llm.chat({
      system: planningSystemPrompt,
      messages: [
        { role: 'user', content: `Break down this request into steps: ${request}` }
      ]
    })

    return this.parsePlan(response.text)
  }

  async execute(plan: TaskPlan, onStep): Promise<AgentResult> {
    const checkpoint = await this.createCheckpoint()

    for (const step of plan.steps) {
      try {
        const result = await this.executeStep(step)
        onStep({ step, status: 'completed', result })
      } catch (error) {
        onStep({ step, status: 'failed', error })
        await this.rollback(checkpoint)
        return { success: false, error }
      }
    }

    return { success: true }
  }
}

// agents/codeReviewAgent.ts
class CodeReviewAgent implements Agent {
  async plan(request: string): Promise<TaskPlan> {
    return {
      steps: [
        { tool: 'read_file', params: { uri: request.fileUri } },
        { tool: 'search_for_files', params: { query: 'related code patterns' } },
        { tool: 'read_lint_errors', params: { uri: request.fileUri } },
        { llm: 'analyze and generate review comments' }
      ]
    }
  }
}

// UI Integration
// AgentPanel.tsx
export function AgentPanel() {
  const [activeAgent, setActiveAgent] = useState<Agent | null>(null)
  const [plan, setPlan] = useState<TaskPlan | null>(null)
  const [executionState, setExecutionState] = useState<ExecutionState>('idle')

  return (
    <div className="agent-panel">
      <AgentSelector onSelect={setActiveAgent} />
      {plan && <TaskPlanViewer plan={plan} onApprove={() => executePlan(plan)} />}
      {executionState === 'running' && <ExecutionProgress />}
    </div>
  )
}
```

### Anti-Patterns
- ❌ Fully autonomous changes without approval
- ❌ No checkpoint/rollback mechanism
- ❌ Hidden planning/decision making
- ❌ Agents bypassing existing tool safety
- ❌ No progress visibility to user

---

## Subtasks

#### [ ] VOID-005-1: Create agent base interface
**Target Files**: `src/vs/workbench/contrib/void/common/agents/agent.ts`
**Related Files**: `src/vs/workbench/contrib/void/common/toolsServiceTypes.ts`

#### [ ] VOID-005-2: Implement planning agent
**Target Files**: `src/vs/workbench/contrib/void/browser/agents/planningAgent.ts`
**Related Files**: `src/vs/workbench/contrib/void/browser/toolsService.ts`

#### [ ] VOID-005-3: Implement code review agent
**Target Files**: `src/vs/workbench/contrib/void/browser/agents/codeReviewAgent.ts`
**Related Files**: `src/vs/workbench/contrib/void/browser/voidSCMService.ts`

#### [ ] VOID-005-4: Implement documentation agent
**Target Files**: `src/vs/workbench/contrib/void/browser/agents/documentationAgent.ts`
**Related Files**: `src/vs/workbench/contrib/void/common/directoryStrService.ts`

#### [ ] VOID-005-5: Implement testing agent
**Target Files**: `src/vs/workbench/contrib/void/browser/agents/testingAgent.ts`
**Related Files**: `src/vs/workbench/contrib/void/browser/terminalToolService.ts`

#### [ ] VOID-005-6: Add agent UI panel
**Target Files**: `src/vs/workbench/contrib/void/browser/react/src/sidebar-tsx/AgentPanel.tsx`
**Related Files**: `src/vs/workbench/contrib/void/browser/react/src/sidebar-tsx/SidebarChat.tsx`

#### [ ] VOID-005-7: Implement task checkpoint system
**Target Files**: `src/vs/workbench/contrib/void/common/agents/checkpointService.ts`
**Related Files**: `src/vs/workbench/contrib/void/browser/editCodeService.ts`

---

## Implementation Priority

1. **VOID-001**: Modernize Build System (Foundation for all other work, immediate performance gains)
2. **VOID-003**: State Management Modernization (Stability, debugging, developer experience)
3. **VOID-002**: AI Provider Architecture (Maintainability, easier to add providers)
4. **VOID-004**: MCP Ecosystem Expansion (Competitive differentiation, extensibility)
5. **VOID-005**: Agentic AI Features (Long-term competitive advantage)

## Notes

- All changes must maintain backward compatibility with existing user settings
- Follow VSCode extension patterns for service registration and lifecycle
- Keep AI provider integrations tested - these are core value proposition
- MCP ecosystem is rapidly evolving - design for extensibility
- Consider Cloud Development Environment (CDE) support for future roadmap
- Mobile companion app is out of scope but architecture should allow for it
- Security: Maintain local-first, privacy-focused approach as key differentiator
- Performance: Build time and HMR are critical for developer adoption
- Documentation: Update VOID_CODEBASE_GUIDE.md as architecture evolves
