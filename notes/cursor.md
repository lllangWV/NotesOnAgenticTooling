# Cursor Specification

Last updated: 2026-01-14 by RS Loop

## Overview

Cursor is an AI-first code editor built as a fork of Visual Studio Code, designed from the ground up for AI-assisted development. It achieved $100M ARR in 12 months and secured a $2.3B Series D at $29.3B valuation. Over 50% of Fortune 500 companies adopted Cursor by mid-2025.

## Architecture

- **VS Code Fork**: Built on VS Code's Electron-based architecture
- **Multi-Model Support**: OpenAI, Anthropic, Google, xAI models
- **Proprietary Models**: Composer (4x faster coding model), Tab (custom autocomplete)
- **Codebase Indexing**: Semantic search via Turbopuffer vector database

## Pricing

### Individual Plans

| Tier | Cost | Key Features |
|------|------|--------------|
| **Hobby** | Free | Limited Agent requests, limited Tab completions |
| **Pro** | $20/month ($16/month annual) | Unlimited Tab completions, Background Agents |
| **Pro+** | $60/month | 3x usage multiplier on models |
| **Ultra** | $200/month | 20x usage multiplier, priority access |

### Business Plans

| Tier | Cost | Key Features |
|------|------|--------------|
| **Teams** | $40/user/month | Shared chats/commands/rules, SAML/OIDC SSO |
| **Enterprise** | Custom | Pooled usage, SCIM, audit logs |

**Note**: Since June 2025, Cursor uses usage-based credit pool system instead of request counts.

## Unique Features

### 1. Agent-Centric Architecture (Cursor 2.0)
- Redesigned interface prioritizing agent workflows
- Delegate entire coding tasks with checkpoints
- "Agent workbench that happens to be an editor"

### 2. Shadow Workspace
- Hidden window for AI agents to interact with language servers/linters
- Doesn't affect developer's active workspace
- Enables concurrent AI work across all languages

### 3. Background Agents
- Spawn asynchronous agents in isolated Ubuntu VMs
- Work on separate branches, can open PRs
- Run multiple background agents in parallel
- Internet access, can install packages

### 4. Composer
- Multi-file editing assistant (access via Cmd+I)
- Proprietary frontier model, 4x faster than similar models
- ~30 second completion time for most tasks
- Context pills show active context

## Agent Mode

Access via **Cmd+I** for autonomous coding assistance.

### Three Foundational Elements
1. **Instructions**: System prompts and behavioral rules
2. **Tools**: 8 primary capabilities (semantic search, file nav, web search, rules, file reading, file editing, shell commands, browser control)
3. **User Messages**: Task descriptions

### Workflow Features
- **Automatic Context Summarization**: As conversations lengthen
- **Checkpoints**: Automatic snapshots before changes (stored locally)
- **Message Queuing**: Queue tasks with Ctrl+Enter while agent works
- **Parallel Execution**: Multiple agents via git worktrees

## Context Features

### Codebase Indexing Process

1. File synchronization to Cursor servers
2. Intelligent chunking (functions, classes, logical units)
3. Vector conversion (semantic embeddings)
4. Storage in Turbopuffer vector database
5. Query processing and vector conversion
6. Similarity matching
7. Ranked results

**Privacy**: Code content never stored in plaintext on servers - only embeddings

### @Symbols for Context

| Symbol | Function |
|--------|----------|
| `@Files` | Reference specific files |
| `@Code` / `@Symbols` | Reference functions, classes, variables |
| `@Codebase` | Scan entire codebase for relevant snippets |
| `@Web` | Search the web |
| `@LibraryName` | Reference library documentation |
| `@Docs` | Add custom documentation |

## Tab Completion

Cursor's specialized autocompletion system goes beyond traditional autocomplete:

- **Multi-line Editing**: Modify multiple existing lines simultaneously
- **Predictive Navigation**: Press Tab again to jump to predicted next edit
- **Cross-File Awareness**: Portal window for cross-file suggestions
- **Automatic Imports**: Adds missing imports for TypeScript/Python

## MCP Support

Cursor supports Model Context Protocol for extending Agent capabilities.

### Supported MCP Features
- Tools (fully supported)
- Prompts
- Resources
- Roots
- Elicitation

### Configuration

Place `mcp.json` at:
- `.cursor/mcp.json` (project-specific)
- `~/.cursor/mcp.json` (global)

### Limitations
- Currently sends only first 40 tools to Agent
- May not work properly over SSH/remote development
- Resources not yet supported (planned)

## Cursor CLI (January 2026)

### Features
- **Model Management**: `/models` to list and switch models
- **Rules Management**: `/rules` to create/edit rules
- **MCP Control**: `/mcp enable` and `/mcp disable`
- **Hooks**: Now 10-20x faster
- **Headless Mode**: Support for non-interactive scripts
- **Cross-IDE Support**: Access Cursor Agent from Neovim/JetBrains

## Open Questions

- [ ] Detailed comparison with Claude Code for different use cases
- [ ] Best practices for Background Agents workflow
- [ ] Enterprise deployment patterns

## Sources

- [Cursor Features](https://cursor.com/features)
- [Cursor Pricing](https://cursor.com/pricing)
- [Agent Overview](https://cursor.com/docs/agent/overview)
- [Codebase Indexing](https://cursor.com/docs/context/codebase-indexing)
- [Model Context Protocol](https://cursor.com/docs/context/mcp)
- [Tab Overview](https://cursor.com/docs/tab/overview)
- [Cursor 2.0 and Composer](https://cursor.com/blog/2-0)
- [Shadow Workspace](https://cursor.com/blog/shadow-workspace)
- [Cursor CLI](https://cursor.com/cli)
