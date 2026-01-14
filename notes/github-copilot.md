# GitHub Copilot Specification

Last updated: 2026-01-14 by RS Loop

## Overview

GitHub Copilot has evolved from a code completion tool into a comprehensive AI-powered development platform with autonomous agents, multi-model support, and extensive IDE integration. It offers five pricing tiers and fully supports Model Context Protocol (MCP).

## Pricing

### Individual Plans

| Plan | Price | Key Features |
|------|-------|--------------|
| **Free** | $0/month | 2,000 completions/month, 50 agent/chat requests/month |
| **Pro** | $10/month ($100/year) | Unlimited completions, 300 premium requests/month, coding agent |
| **Pro+** | $39/month ($390/year) | 1,500 premium requests/month (5x Pro), Claude Opus 4.1 |

### Organization Plans

| Plan | Price | Key Features |
|------|-------|--------------|
| **Business** | $19/user/month | 300 premium requests/user, IP indemnity, SAML SSO |
| **Enterprise** | $39/user/month | 1,000 premium requests/user, custom model fine-tuning, codebase indexing |

**Premium Request Overages**: $0.04 per request across all paid tiers

**Free for**: Students, teachers, and open source maintainers (Pro tier)

## Core Features

### Code Completion
- Autocomplete-style inline "ghost text" suggestions
- **Next Edit Suggestions** (preview): Predicts next edit location
- Exceptional for: Python, JavaScript, TypeScript, Ruby, Go, C#, C++

### Copilot Chat
Available on: GitHub.com, GitHub Mobile, VS Code, Visual Studio, JetBrains, Eclipse, Xcode, Windows Terminal

**Modes**:
- **Agent Mode**: Complex coding tasks with autonomous execution
- **Ask Mode**: Answering questions about codebase
- **Edit Mode**: Granular code modification control
- **Plan Mode**: Generating implementation strategies

**Context Enhancement** via #-mentions:
- `#file` - Specific files
- `#codebase` - Entire repository
- `#terminalSelection` - Terminal output

### Agent Mode (IDE-based)

Autonomous, real-time AI coding assistant that performs multi-step tasks.

**Capabilities**:
- Analyze entire codebase for context
- Make autonomous edits in local environment
- Execute terminal commands
- Run tests and builds
- Self-healing with automatic error detection

**Available in**: VS Code, Visual Studio, JetBrains IDEs

### Copilot Coding Agent (GitHub-hosted)

Autonomous AI developer working independently in background.

**How It Works**:
1. Assign GitHub issues to @copilot
2. Works in isolated GitHub Actions environment
3. Creates pull requests with complete implementations
4. Continues working when IDE is closed

**Key Difference from Agent Mode**: Operates asynchronously on GitHub infrastructure, not local environment.

### Copilot CLI (January 2026)

Terminal-based interface with enhanced agents:
- **Explore**: Fast codebase analysis
- **Task**: Runs commands like tests/builds
- **Plan**: Generates implementation strategies
- **Code-review**: Identifies issues in code changes

Features:
- Auto-compression at 95% token capacity
- Web fetching capability
- Integration with GitHub.com operations

## IDE Integrations

| IDE | Features |
|-----|----------|
| **VS Code** | Full feature set including MCP servers |
| **Visual Studio** | Code completion, Chat, Agent mode, MCP |
| **JetBrains IDEs** | Full suite support, MCP management |
| **Xcode** | Completion, Chat, Next edit suggestions, MCP |
| **Eclipse** | Completion, Chat, Next edit suggestions, MCP |
| **Vim/Neovim** | Code completion |
| **Windows Terminal** | Chat interface |

## MCP Support

**Status**: Fully supported and GA (VS Code 1.102+)

### GitHub MCP Server

Enables:
- Automating code-related workflows
- Third-party tool integration (Cursor, Windsurf)
- Cloud-based development without local setup
- GitHub operations from third-party IDEs

### Supported Environments

**Local MCP Servers**: VS Code, JetBrains, Xcode, Eclipse
**Remote MCP Servers**: VS Code, Visual Studio, JetBrains, Xcode, Eclipse, Cursor, Windsurf

### Enterprise Policy Controls
- MCP policy disabled by default for Business/Enterprise
- Administrators must explicitly enable
- Audit logging available

## Copilot Workspace (Discontinued)

**Important**: Technical preview ended May 30, 2025.

Capabilities now available through:
- Agent mode in IDEs
- Copilot coding agent on GitHub
- Copilot Spaces (GA September 2025)
- Copilot Edits

## Extensions

GitHub provides comprehensive Copilot Extensibility Platform.

### Extension Types

**Skillsets**: Lightweight, minimal setup, automatic handling
**Agents**: Complex integrations with full control, custom logic

### Development Approaches
- **Server-side**: Execute on your backend, available in all clients
- **Client-side**: Installed locally, IDEs only, faster response

## Recent Updates (January 2026)

- **GPT-5.2-Codex** now GA across all interfaces
- **Claude Opus 4.5** moved to GA with 50% reduced token usage
- **Gemini 3 Flash** available in Visual Studio, JetBrains, Xcode, Eclipse
- C++ code editing tools with reference viewing

## Open Questions

- [ ] Migration path from Copilot Workspace
- [ ] Fine-tuning process details for Enterprise
- [ ] Content exclusion policy documentation

## Sources

- [GitHub Copilot Features](https://docs.github.com/en/copilot/get-started/features)
- [Plans for GitHub Copilot](https://docs.github.com/en/copilot/get-started/plans)
- [About Coding Agent](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent)
- [About MCP](https://docs.github.com/en/copilot/concepts/context/mcp)
- [Agent Mode 101](https://github.blog/ai-and-ml/github-copilot/agent-mode-101-all-about-github-copilots-powerful-mode/)
- [GitHub Copilot CLI Enhanced Agents](https://github.blog/changelog/2026-01-14-github-copilot-cli-enhanced-agents-context-management-and-new-ways-to-install/)
- [GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/overview)
- [Building Copilot Extensions](https://docs.github.com/en/copilot/building-copilot-extensions/about-building-copilot-extensions)
