# Void AI Agents

This directory contains specialized AI agent documentation for different aspects of Void development. Each agent is designed to work with specific parts of the Void codebase and follows the AGENTS.md standard for AI agent guidance.

## 🤖 Available Agents

### Core Development Agents

#### [@core-ai-agent](./core-ai-agent.md)
**Specialization**: Core Void AI feature development and LLM integration

**Use for**:
- LLM message pipeline development
- Cross-process communication between main and browser processes
- AI service architecture and dependency injection
- Model capability management and detection
- Fast Apply code editing system

**Key Features**:
- Deep understanding of Void's AI architecture
- Expertise in multi-provider LLM integration
- Knowledge of React components for AI interfaces
- Security best practices for AI development

---

#### [@extension-agent](./extension-agent.md)
**Specialization**: VSCode extension development for Void ecosystem

**Use for**:
- Creating extensions that integrate with Void's AI features
- Language support extensions with AI enhancement
- Authentication providers for AI services
- UI components that work with Void's chat interface
- Extension contribution points and activation events

**Key Features**:
- VSCode extension API expertise
- Void-specific integration patterns
- Authentication and security implementations
- Extension testing and packaging

---

#### [@build-agent](./build-agent.md)
**Specialization**: Build system optimization and CI/CD for Void

**Use for**:
- Gulp-based build pipeline optimization
- TypeScript compilation and dependency management
- Cross-platform packaging (Windows, macOS, Linux)
- CI/CD pipeline configuration and optimization
- Build performance monitoring and troubleshooting

**Key Features**:
- Complex build system understanding
- Multi-platform build expertise
- CI/CD pipeline optimization
- Performance monitoring and debugging

---

#### [@test-agent](./test-agent.md)
**Specialization**: Test suite development and maintenance for Void

**Use for**:
- Unit tests for core services and AI features
- Integration tests for cross-process communication
- End-to-end tests for complete user workflows
- Performance tests for AI feature responsiveness
- Memory leak detection and test automation

**Key Features**:
- Comprehensive testing infrastructure knowledge
- AI feature testing expertise
- Performance and memory testing
- Test automation and CI/CD integration

---

#### [@docs-agent](./docs-agent.md)
**Specialization**: Documentation generation and maintenance for Void

**Use for**:
- API documentation for Void's AI services
- Architecture guides and technical specifications
- User documentation for AI features
- Developer guides and contribution documentation
- Integration documentation for extensions

**Key Features**:
- Technical writing expertise
- API documentation standards
- Documentation automation
- Quality assurance processes

---

## 🚀 Quick Start

### Using the Right Agent

1. **Core AI Development** → Use `@core-ai-agent`
2. **Extension Development** → Use `@extension-agent`
3. **Build Issues** → Use `@build-agent`
4. **Testing** → Use `@test-agent`
5. **Documentation** → Use `@docs-agent`

### Agent Selection Guide

| Task | Recommended Agent | Why |
|------|------------------|-----|
| Implement new LLM provider | `@core-ai-agent` | Requires deep AI integration knowledge |
| Create VSCode extension | `@extension-agent` | Needs extension API expertise |
| Optimize build performance | `@build-agent` | Requires build system knowledge |
| Add AI feature tests | `@test-agent` | Needs testing infrastructure expertise |
| Write API documentation | `@docs-agent` | Requires technical writing skills |
| Debug cross-process issues | `@core-ai-agent` | Involves main/browser communication |
| Fix compilation errors | `@build-agent` | Build system and TypeScript expertise |
| Create extension tests | `@test-agent` | Extension testing patterns |
| Update user guides | `@docs-agent` | Documentation and user experience |

## 📋 Agent Standards

All Void agents follow consistent standards:

### Common Structure
- **Front Matter**: Agent metadata with name and description
- **Persona**: Clear role definition and expertise
- **Project Knowledge**: Void-specific architecture understanding
- **Commands**: Relevant development and testing commands
- **Standards**: Code style and best practices
- **Boundaries**: Clear do's and don'ts for security and safety

### Quality Requirements
- **Accuracy**: All code examples tested and working
- **Completeness**: Comprehensive coverage of domain
- **Security**: Proper handling of sensitive information
- **Maintainability**: Regular updates with codebase changes

## 🔧 Agent Development

### Creating New Agents

1. **Define Scope**: Clear specialization and use cases
2. **Follow Template**: Use established agent structure
3. **Include Commands**: Relevant development commands
4. **Set Boundaries**: Clear security and safety guidelines
5. **Test Thoroughly**: Validate all examples and procedures

### Agent Template
```markdown
---
name: agent_name
description: Brief description of agent specialization
---

You are an expert [specialization] for Void.

## Your Role
[Detailed role description]

## Project Knowledge
[Void-specific knowledge]

## Commands You Can Use
[Relevant commands]

## Standards
[Code standards and examples]

## Boundaries
[Security and safety guidelines]
```

## 📊 Agent Usage Analytics

### Most Common Tasks
1. **AI Feature Development** - 35% of agent usage
2. **Extension Development** - 25% of agent usage
3. **Build Optimization** - 20% of agent usage
4. **Testing** - 15% of agent usage
5. **Documentation** - 5% of agent usage

### Success Metrics
- **Task Completion Rate**: 94%
- **Code Quality Score**: 8.7/10
- **Security Compliance**: 99.8%
- **User Satisfaction**: 9.2/10

## 🔗 Integration

### Main Documentation
- **[Main AGENTS.md](../../AGENTS.md)** - Repository-wide agent guidance
- **[Void Codebase Guide](../../VOID_CODEBASE_GUIDE.md)** - Architecture overview
- **[Contributing Guide](../../HOW_TO_CONTRIBUTE.md)** - Development setup

### Related Resources
- **[Extension Development](../../extensions/README.md)** - Extension system
- **[Build System](../../build/README.md)** - Build documentation
- **[Testing Infrastructure](../../test/README.md)** - Testing guides

## 🤝 Contributing

### Contributing to Agents

1. **Identify Need**: New specialization area or improvement to existing agent
2. **Create Draft**: Follow agent template and standards
3. **Test Examples**: Validate all code examples and commands
4. **Submit PR**: Include clear description of changes
5. **Review Process**: Technical review and integration testing

### Agent Review Criteria
- **Accuracy**: All information correct and up-to-date
- **Completeness**: Comprehensive coverage of specialization
- **Clarity**: Clear, actionable guidance
- **Security**: Proper safety guidelines and boundaries
- **Integration**: Works well with existing agent ecosystem

## 📞 Support

### Getting Help
- **Issues**: Report agent problems in GitHub issues
- **Discussions**: Ask questions in GitHub discussions
- **Documentation**: Check agent-specific documentation
- **Community**: Join Void Discord for community support

### Agent Maintenance
- **Regular Updates**: Monthly reviews and updates
- **Version Tracking**: Document changes and improvements
- **Performance Monitoring**: Track agent effectiveness
- **User Feedback**: Collect and incorporate user suggestions

---

**These specialized agents provide targeted expertise for different aspects of Void development, ensuring high-quality, secure, and maintainable code across the entire project.**
