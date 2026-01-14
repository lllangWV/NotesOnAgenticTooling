# AI Coding Assistant Tools - Research Notes

Last updated: 2026-01-14

## Overview

This directory contains comprehensive research notes on AI-powered coding assistant tools, covering CLI-based tools (Claude Code, OpenCode, Aider), IDE-integrated tools (Cursor, GitHub Copilot), and cloud-based solutions (Google Jules/Antigravity). The research focuses on unique features, common patterns, pricing models, and the emerging Model Context Protocol (MCP) ecosystem.

## Specifications

| Spec | Description |
|------|-------------|
| [claude-code.md](claude-code.md) | Anthropic's terminal-based agentic coding assistant |
| [cursor.md](cursor.md) | AI-first IDE built on VS Code with agent mode and background agents |
| [github-copilot.md](github-copilot.md) | GitHub's AI coding assistant with agent mode and MCP support |
| [google-jules-antigravity.md](google-jules-antigravity.md) | Google's cloud-based agent (Jules) and agentic IDE (Antigravity) |
| [cli-tools.md](cli-tools.md) | Open-source CLI tools: OpenCode, Aider, Cline, Goose, Continue, OpenHands |
| [mcp-protocol.md](mcp-protocol.md) | Model Context Protocol specification and adoption |
| [cross-cutting-themes.md](cross-cutting-themes.md) | Common patterns, security, extensibility across all tools |
| [OPEN_QUESTIONS.md](OPEN_QUESTIONS.md) | Tracked open questions for future research |

## Key Findings

### Tool Categories

1. **CLI-First Tools**: Claude Code, OpenCode, Aider - terminal-based, composable, scriptable
2. **AI-First IDEs**: Cursor, Google Antigravity - rebuilt around AI workflows
3. **IDE Extensions**: GitHub Copilot - extends existing IDEs with AI
4. **Cloud Agents**: Google Jules - fully cloud-based autonomous agents

### Common Features Across Tools

- **MCP Support**: Industry-wide adoption of Model Context Protocol
- **Agent Mode**: Autonomous multi-step task execution
- **Subagents/Background Agents**: Parallel task handling
- **Hooks/Rules**: Customizable automation triggers
- **Skills/Commands**: Reusable prompts and workflows

### Pricing Summary

| Tool | Free Tier | Paid Plans |
|------|-----------|------------|
| Claude Code | Limited trial | $20-200/month |
| Cursor | Hobby (limited) | $20-200/month |
| GitHub Copilot | 2,000 completions/month | $10-39/month |
| Google Jules | 15 tasks/day | $20-125/month |
| OpenCode/Aider | Full (open source) | API costs only |

### MCP Adoption

Model Context Protocol has become the industry standard for AI tool integration:
- **97M** monthly SDK downloads
- **10,000+** active servers
- Supported by: Claude, ChatGPT, Cursor, Copilot, Gemini

## Changes

### Iteration 2 (2026-01-14)
- Added [claude-code.md](claude-code.md): Comprehensive Claude Code specification
- Added [cursor.md](cursor.md): Cursor AI IDE features and pricing
- Added [github-copilot.md](github-copilot.md): GitHub Copilot current state
- Added [google-jules-antigravity.md](google-jules-antigravity.md): Google's AI coding tools
- Added [cli-tools.md](cli-tools.md): Open-source CLI alternatives comparison
- Added [mcp-protocol.md](mcp-protocol.md): MCP protocol deep dive
- Added [cross-cutting-themes.md](cross-cutting-themes.md): Common patterns analysis
- Updated [OPEN_QUESTIONS.md](OPEN_QUESTIONS.md): Marked completed questions, added new ones

### Iteration 1 (2026-01-14)
- Created initial notes structure
- Added OPEN_QUESTIONS.md with priority research questions
