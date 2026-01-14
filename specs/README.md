# AI Coding Assistants Specifications

Last updated: 2026-01-14

## Overview

This directory contains cleanroom black-box specifications for major AI coding assistants, documenting their external behavior, features, pricing, and common patterns. These specs are derived from official documentation and trusted sources, focusing on observable behavior rather than internal implementation.

## Specifications

| Spec | Description |
|------|-------------|
| [claude-code.md](claude-code.md) | Anthropic's terminal-native agentic coding tool with MCP support |
| [cursor.md](cursor.md) | VS Code fork with embedded AI, Composer multi-file editing, and Agent Mode |
| [github-copilot.md](github-copilot.md) | GitHub's AI assistant with deep ecosystem integration and coding agents |
| [google-gemini-code-assist.md](google-gemini-code-assist.md) | Google's Gemini-powered assistant with enterprise codebase customization |
| [google-antigravity.md](google-antigravity.md) | Google's agent-first development platform with autonomous multi-surface agents |
| [cli-tools.md](cli-tools.md) | CLI-based tools: OpenCode, Aider, Cline, Gemini CLI, and others |
| [common-patterns.md](common-patterns.md) | Shared architectural patterns: subagents, skills, slash commands, hooks, MCP |

## Research Goals

- [x] Claude Code - features, pricing, unique differentiators
- [x] Cursor - features, pricing, Agent Mode, Composer
- [x] GitHub Copilot - features, pricing, coding agents, CLI
- [x] Google Gemini Code Assist - features, pricing, enterprise customization
- [x] Google Antigravity - agent-first platform, multi-surface autonomy
- [x] CLI-based tools - OpenCode, Aider, Cline, patterns
- [x] Common patterns - subagents, skills, slash commands, hooks, MCP

## Key Findings Summary

### Common Features Across All Tools
- Intelligent autocomplete (single-line to full functions)
- Chat interfaces for conversational assistance
- Context awareness of codebase and project structure
- Multi-file operations
- Multiple model support (Claude, GPT, Gemini)
- IDE/editor integration

### Unique Differentiators

| Tool | Key Differentiator |
|------|-------------------|
| Claude Code | Terminal-native, scriptable, 200K context, MCP extensibility |
| Cursor | VS Code fork, Composer multi-file editing, 39% more merged PRs |
| GitHub Copilot | Deep GitHub integration, coding agents from issues |
| Gemini Code Assist | Generous free tier (180K completions/mo), 20K repo customization |
| Google Antigravity | Agent-first with browser sub-agent for UI verification |

### Pricing Comparison

| Tool | Free Tier | Pro/Individual | Team/Business |
|------|-----------|----------------|---------------|
| Claude Code | No | $20/month | $30/user/month |
| Cursor | Limited (50 requests) | $20/month | $40/user/month |
| GitHub Copilot | 2K completions/mo | $10/month | $19/user/month |
| Gemini Code Assist | 180K completions/mo | $19/user/month | $45/user/month |
| Google Antigravity | Free preview | TBD | TBD |

### CLI Tool Patterns

| Pattern | Description |
|---------|-------------|
| Subagents | Specialized AI with isolated context windows |
| Skills | Auto-triggered background helpers |
| Slash Commands | User-invoked workflow automation |
| Hooks | Event-driven shell command execution |
| MCP | Universal protocol for tool integration |

## Sources

Primary documentation sources used:
- [Claude Code Documentation](https://code.claude.com/docs/)
- [Cursor Documentation](https://cursor.com/docs)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Google Gemini Code Assist](https://developers.google.com/gemini-code-assist/docs/)
- [Google Antigravity Blog](https://developers.googleblog.com/)
- [Aider Documentation](https://aider.chat/docs/)
- [OpenCode](https://opencode.ai/)
- [Model Context Protocol](https://modelcontextprotocol.io/)

## Open Questions

- [ ] Long-term code quality metrics for AI-assisted codebases
- [ ] Security implications of MCP server ecosystem
- [ ] Enterprise compliance frameworks for agentic tools
- [ ] Performance benchmarks at scale (10M+ line codebases)
- [ ] Optimal human-in-the-loop checkpoint strategies
