# CLI-Based AI Coding Assistants Specification

Last updated: 2026-01-14 by RS Loop

## Overview

CLI-based AI coding assistants represent a growing category of terminal-first tools that integrate AI capabilities directly into developer workflows. These tools follow Unix philosophy principles: composable, scriptable, and pipeable.

## OpenCode

### What is OpenCode?

OpenCode is an open-source, terminal-based AI coding agent written in Go. With 69,000+ GitHub stars, it's positioned as a model-agnostic alternative to Claude Code.

**Repository**: https://github.com/opencode-ai/opencode
**License**: MIT

### Key Features

- **Multi-Provider Support**: OpenAI, Anthropic, Google, Groq, AWS Bedrock, Azure OpenAI, OpenRouter, local models via Ollama
- **Bring Your Own Keys**: Use existing Claude Pro or ChatGPT Plus subscriptions
- **Unified Interface**: Same terminal experience regardless of backend
- **MCP Integration**: Full Model Context Protocol support
- **Language Server Protocol**: Native LSP support for intelligent code analysis

### Architecture

- Written primarily in Go
- TUI (Terminal User Interface) with Bubble Tea framework
- SQLite for local session management
- Hot-reloadable MCP server connections

### Configuration

```bash
# Install
go install github.com/opencode-ai/opencode@latest

# Or via Homebrew
brew install opencode
```

### Comparison to Claude Code

| Aspect | OpenCode | Claude Code |
|--------|----------|-------------|
| License | MIT (open source) | Proprietary |
| Models | Any provider | Claude only |
| Pricing | Free + API costs | Subscription |
| MCP | Supported | Supported |
| Context | Dynamic discovery | On-demand search |

## Aider

### What is Aider?

Aider is an open-source AI pair programming tool that works directly in your terminal with local git repos. It has 39,800+ GitHub stars.

**Repository**: https://github.com/Aider-AI/aider
**License**: Apache 2.0

### Key Features

- **Git-Native Workflow**: Auto-commits with sensible messages
- **Multi-File Editing**: Coherent changes across multiple files
- **Voice & Image Input**: Support for images, web pages, voice-to-code
- **Model Flexibility**: Works with GPT-4o, Claude 3.5, Gemini 1.5, local models via Ollama
- **Quality Assurance**: Auto-runs linting and tests after modifications

### Pricing

- **Tool Cost**: $0 (open source)
- **API Costs**: ~$0.007 per file, $3-5/hour for complex projects
- **Free Option**: Use with Ollama for $0 total cost

### Architecture

- Primarily Python (80% of codebase)
- Terminal-centric workflow
- Git integration is fundamental to design

## Cline

### What is Cline?

Cline is an open-source autonomous AI coding agent with a unique plan-and-act workflow. Available as VS Code extension and Cline CLI.

**Repository**: https://github.com/cline/cline

### Key Features

- **Plan & Act Modes**: Separates strategic thinking (read-only) from implementation
- **Human-in-the-Loop**: Approval required for every file change and terminal command
- **Browser Automation**: Uses Claude's Computer Use capability
- **MCP Integration**: Create and install custom tools on-the-fly
- **Cline Core**: Standalone service with gRPC API for automation

### Architecture

- Protocol Buffers for type-safe communication
- Service-oriented design
- Three-tier state management (session, project, global)
- Controller and Task classes for agentic execution loop

## Goose

### What is Goose?

Goose is an open-source AI agent framework from Block (Square, Cash App). Now part of Linux Foundation's Agentic AI Foundation (AAIF).

**Repository**: https://github.com/block/goose
**License**: Apache 2.0

### Key Features

- **Multi-Model Configuration**: Optimize cost/performance by task
- **MCP Integration**: Seamless Model Context Protocol support
- **Dual Interface**: Desktop app and CLI
- **Autonomous Operation**: Builds projects from scratch, writes code, debugs

### Architecture

- Written in Rust
- Electron desktop interface + CLI
- Fully local operation possible

## Continue

### What is Continue?

Continue is an open-source IDE-first platform with 20,000+ GitHub stars that also supports CLI operations.

**Repository**: https://github.com/continuedev/continue
**License**: Apache 2.0

### Key Features

- **Enterprise Control**: Centralized configuration management
- **Custom AI Assistants**: Create and share in IDE
- **Multi-Purpose**: Chat, autocomplete, embeddings
- **IDE + CLI**: Extensions for VS Code/JetBrains plus standalone CLI

### Pricing

| Tier | Price | Features |
|------|-------|----------|
| **Solo (Free)** | $0 | Use with your own API keys |
| **Teams** | $10/dev/month | Centralized config, shared agents |
| **Enterprise** | Custom | Advanced governance, self-hosting |

## OpenHands (formerly OpenDevin)

### What is OpenHands?

OpenHands is an open-source platform for creating AI agents that emulate human software developers.

**Repository**: https://github.com/OpenHands/OpenHands
**License**: MIT

### Key Features

- **Comprehensive Capabilities**: Modify code, execute commands, browse web, interact with APIs
- **Event-Stream Architecture**: Defines agent-environment interface
- **Hierarchical Agents**: Agents can delegate to other agents
- **Docker-Based Security**: Isolated environments torn down post-session
- **Evaluation Harness**: Support for 15+ benchmarks (SWE-bench, etc.)

### Architecture

- Python-based SDK
- CLI for easy startup
- Local GUI with REST API and React SPA
- SSH-mediated interface for security

## Other Notable Tools

### GPT Engineer
- **Repository**: https://github.com/AntonOsika/gpt-engineer
- **Stars**: 50,000+
- **Focus**: Rapid prototyping, code generation experiments
- **Status**: Development shifted to Lovable (commercial), open source remains

### Gemini CLI (Google)
- Free and open source
- 60 requests/min, 1,000 requests/day free tier
- Brings Gemini models to terminal

### Cursor CLI
- Part of Cursor IDE ecosystem (January 2026 release)
- Model management, rules, MCP control
- Cross-IDE support (Neovim, JetBrains access)

## Common Architecture Patterns

### 1. MCP Integration
- Dynamic tool discovery (pull only when needed)
- Token efficiency
- Standardized integration across tools

### 2. Human-in-the-Loop
- Agent proposes actions
- Developer reviews and approves
- Full transparency and audit trail

### 3. Service-Oriented Design
- Controller as central orchestrator
- Task manager for execution
- State manager with three-tier precedence

### 4. Sandbox Execution
- Docker-based isolation
- Post-session teardown
- SSH-mediated interface

### 5. Multi-Model Architecture
- Different models for different tasks
- Optimize performance vs. cost
- Fallback chains for reliability

## Pricing Comparison

| Tool | Base Cost | API Costs | Monthly Estimate |
|------|-----------|-----------|------------------|
| **Aider** | $0 | Variable | $0-150 |
| **OpenCode** | $0 | Variable | $0-150 |
| **Claude Code** | $20-200 | Included | $100-200 |
| **Cline** | $0 | Variable | $0-150 |
| **Goose** | $0 | Variable | $0-150 |
| **Continue** | $0-10+ | Variable | $0-160+ |

## Open Questions

- [ ] Long-term maintenance of archived OpenCode repository
- [ ] Detailed benchmarks across all tools on standardized tasks
- [ ] Offline capabilities comparison
- [ ] Enterprise security certifications

## Sources

- [OpenCode Official](https://opencode.ai/)
- [Aider Official](https://aider.chat/)
- [Cline Official](https://cline.bot/)
- [Goose GitHub](https://github.com/block/goose)
- [OpenHands GitHub](https://github.com/OpenHands/OpenHands)
- [Continue Hub](https://hub.continue.dev/)
- [Top 10 Open-Source CLI Coding Agents](https://dev.to/forgecode/top-10-open-source-cli-coding-agents-you-should-be-using-in-2025-with-links-244m)
- [Top 7 Open-Source AI Coding Assistants 2026](https://www.secondtalent.com/resources/open-source-ai-coding-assistants/)
