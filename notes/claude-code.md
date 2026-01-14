# Claude Code Specification

Last updated: 2026-01-14 by RS Loop

## Overview

Claude Code is Anthropic's terminal-based agentic AI coding assistant that operates autonomously in your terminal. Unlike IDE extensions that provide suggestions, Claude Code is an autonomous agent that can directly read files, execute commands, modify code, run tests, and manage git workflows through natural language commands.

## Architecture

- **CLI-Based Runtime**: Written in Shell (48.2%), Python (32.7%), TypeScript (12.5%)
- **Requires**: Node.js 18+
- **No Remote Indexing**: Uses on-demand search rather than pre-built code index
- **Built on Claude Agent SDK**: Provides agentic tool loop, context management, session persistence

### Installation

```bash
# macOS/Linux/WSL
curl -fsSL https://claude.ai/install.sh | bash

# Homebrew
brew install --cask claude-code

# Windows (WinGet)
winget install Anthropic.ClaudeCode
```

## Pricing

| Plan | Price | Key Features |
|------|-------|--------------|
| **Free** | $0 | Very limited usage (trial tier) |
| **Pro** | $20/month ($17/month annual) | Claude Sonnet 4.5, 5x usage limits, ~45 messages/5 hours |
| **Max** | $100/month | 5x Pro limits, generous Opus 4.5 access |
| **Max Ultimate** | $200/month | 20x Pro limits, effectively unlimited |
| **Team** | $30/month ($25/month annual) | Min 5 members, team collaboration |

### API Pricing (per million tokens)

| Model | Input | Output |
|-------|-------|--------|
| Haiku 4.5 | $1 | $5 |
| Sonnet 4.5 | $3 | $15 |
| Opus 4.5 | $5 | $25 |

**Cost Saving**: Prompt caching (0.1x cost for cache reads), Batch API (50% discount)

## Unique Features

### 1. Terminal-First Autonomous Architecture
- Lives in your terminal, not a separate IDE
- Composable and scriptable following Unix philosophy
- Supports piping: `tail -f app.log | claude -p "Slack me if you see anomalies"`
- Headless mode for CI/CD integration

### 2. Extended Thinking Mode
- Press **Tab** to toggle on/off
- Uses "serial test-time compute" for complex reasoning
- Accuracy improves logarithmically with thinking tokens

### 3. Session Management & Teleporting
- Persistent sessions stored in `~/.claude/projects/`
- Session teleporting between web and CLI
- 5-hour session limit
- Can fork sessions to explore different approaches

### 4. MCP Integration
- Connects to external tools via Model Context Protocol
- Official integrations: GitHub, Figma, Slack, Google Drive, Jira, Sentry

## Subagents

Subagents are specialized AI assistants that handle specific types of tasks in isolated context windows.

### Configuration

Location: `.claude/agents/` (project) or `~/.claude/agents/` (user)

```yaml
---
name: code-reviewer
description: Expert code reviewer for quality and security reviews
tools: [Read, Glob, Grep]
model: claude-sonnet-4.5
---
Analyze code quality, identify security issues, and suggest improvements...
```

### Key Characteristics
- **Isolated Context Windows**: Only send relevant information back
- **Execution Modes**: Foreground (blocking) or Background (concurrent)
- **Tool Restrictions**: Limit which tools a subagent can use
- **Cost Control**: Route tasks to faster, cheaper models

## Skills and Slash Commands

### Skills
- Modular capabilities that extend Claude's functionality
- Located in `.claude/skills/SKILL.md` or `~/.claude/skills/`
- Claude autonomously chooses when to use them
- Pre-built: PowerPoint, Excel, Word, PDF

### Slash Commands
- Saved prompts invoked by typing `/command-name`
- Located in `.claude/commands/` or `~/.claude/commands/`
- Support variables and parameters

| Aspect | Skills | Slash Commands |
|--------|--------|----------------|
| Invocation | Auto-invoked by Claude | Manually typed |
| Purpose | Building blocks for complex tasks | Quick repetitive actions |
| Scope | Multi-step operations | Single-purpose actions |

## Hooks

Hooks are custom triggers that run shell commands at specific points during Claude Code's operation.

### Available Hook Events

| Event | Timing | Use Case |
|-------|--------|----------|
| **PreToolUse** | Before tool call | Validation, adding context, blocking |
| **PostToolUse** | After tool completion | Logging, auditing, downstream actions |
| **PermissionRequest** | On permission dialog | Custom approval logic |
| **UserPromptSubmit** | Before Claude processes prompt | Adding context, validation |

### Configuration

In `.claude/settings.json`:
- Exit 0: Success, operation continues
- Exit 2: Blocking error, stderr fed back to Claude
- 60-second execution limit (configurable)

## Built-in Tools

| Category | Tools |
|----------|-------|
| **File Operations** | Read, Write, Edit, MultiEdit, NotebookRead, NotebookEdit |
| **Code Navigation** | Glob, Grep, LS |
| **Command Execution** | Bash (persistent session) |
| **Web Access** | WebSearch, WebFetch |
| **Planning** | TodoRead, TodoWrite, Task |

## Context Management

### CLAUDE.md File
- Most important file for Claude Code effectiveness
- Becomes part of system prompt
- Should document: bash commands, code style, testing instructions, conventions

```bash
claude /init  # Auto-generates CLAUDE.md from codebase analysis
```

### Best Practices
- Use subagents to "farm out" exploration work
- Keep main context clean
- Refine CLAUDE.md like any frequently used prompt

## Open Questions

- [ ] Detailed comparison of context management vs. indexed approaches
- [ ] Performance benchmarks for large codebases (>100k LOC)
- [ ] Best practices for multi-Claude workflows in teams

## Sources

- [Claude Code Overview](https://code.claude.com/docs/en/overview)
- [GitHub - anthropics/claude-code](https://github.com/anthropics/claude-code)
- [Claude Code Product Page](https://www.claude.com/product/claude-code)
- [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Claude Code Pricing](https://claudelog.com/claude-code-pricing/)
- [Create Custom Subagents](https://code.claude.com/docs/en/sub-agents)
- [Slash Commands](https://code.claude.com/docs/en/slash-commands)
- [Hooks Reference](https://code.claude.com/docs/en/hooks)
