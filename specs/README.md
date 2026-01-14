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
| [additional-tools.md](additional-tools.md) | Windsurf, Amazon Q, Tabnine, JetBrains AI, Cody, Supermaven, Qodo, Replit, Continue |
| [common-patterns.md](common-patterns.md) | Shared architectural patterns: subagents, skills, slash commands, hooks, MCP |

## Research Goals

- [x] Claude Code - features, pricing, unique differentiators
- [x] Cursor - features, pricing, Agent Mode, Composer
- [x] GitHub Copilot - features, pricing, coding agents, CLI (5-tier pricing update)
- [x] Google Gemini Code Assist - features, pricing, enterprise customization
- [x] Google Antigravity - agent-first platform, multi-surface autonomy
- [x] CLI-based tools - OpenCode, Aider, Cline, patterns
- [x] Common patterns - subagents, skills, slash commands, hooks, MCP
- [x] Additional tools - Windsurf, Amazon Q, Tabnine, JetBrains AI, Cody, Supermaven, Qodo
- [x] MCP ecosystem - Linux Foundation governance, security concerns, protocol versions

## Key Findings Summary

### Common Features Across All Tools
- Intelligent autocomplete (single-line to full functions)
- Chat interfaces for conversational assistance
- Context awareness of codebase and project structure
- Multi-file operations and agentic workflows
- Multiple model support (Claude, GPT, Gemini)
- IDE/editor integration
- MCP (Model Context Protocol) support becoming standard

### Unique Differentiators

| Tool | Key Differentiator |
|------|-------------------|
| Claude Code | Terminal-native, scriptable, 200K context, MCP extensibility, v2.1 hooks system |
| Cursor | VS Code fork, Composer multi-file editing, 39% more merged PRs |
| GitHub Copilot | Deep GitHub integration, coding agents from issues, 5-tier pricing |
| Gemini Code Assist | Generous free tier (180K completions/mo), 20K repo customization |
| Google Antigravity | Agent-first with browser sub-agent for UI verification |
| Windsurf | Cascade agentic assistant, superior large codebase handling |
| Amazon Q | AWS integration, 37-50% acceptance rates, code transformation |
| Tabnine | Enterprise privacy, air-gapped deployment, 600+ languages |

### Pricing Comparison (January 2026)

| Tool | Free Tier | Pro/Individual | Team/Business |
|------|-----------|----------------|---------------|
| Claude Code | No | $20/month | $30/user/month |
| Cursor | 50 requests | $20/month (Pro), $60 (Pro+), $200 (Ultra) | $40/user/month |
| GitHub Copilot | 2K completions + 50 premium | $10/month (300 premium) | $19-39/user/month |
| Gemini Code Assist | 180K completions/mo | $19/user/month | $45/user/month |
| Google Antigravity | Free preview | TBD | TBD |
| Windsurf | 25 credits/mo | $15/month | $30-60/user/month |
| Amazon Q | 50 agentic/mo | $19/user/month | $19/user/month |
| Tabnine | Basic | $12/user/month | $39/user/month |
| Supermaven | Yes | $10/month | $10/user/month |

### CLI Tool Patterns

| Pattern | Description |
|---------|-------------|
| Subagents | Specialized AI with isolated context windows |
| Skills | Auto-triggered background helpers |
| Slash Commands | User-invoked workflow automation |
| Hooks | Event-driven shell command execution |
| MCP | Universal protocol for tool integration (Linux Foundation governed) |

### MCP Ecosystem (2026)

| Metric | Value |
|--------|-------|
| Monthly SDK Downloads | 97M+ |
| Public MCP Servers | 10,000+ |
| MCP Clients | 300+ |
| Security Concern | 43% servers vulnerable to command injection |
| Governance | Linux Foundation's Agentic AI Foundation (AAIF) |

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
- [Windsurf](https://windsurf.com/)
- [Amazon Q Developer](https://aws.amazon.com/q/developer/)
- [Tabnine](https://www.tabnine.com/)
- [JetBrains AI](https://www.jetbrains.com/ai-ides/)
- [Sourcegraph Cody](https://sourcegraph.com/cody)
- [Qodo](https://www.qodo.ai/)
- [Supermaven](https://supermaven.com/)
- [Continue](https://www.continue.dev/)
- [Linux Foundation AAIF](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation)

## Open Questions

- [ ] Long-term code quality metrics for AI-assisted codebases
- [ ] MCP security audit results and CVE remediation progress
- [ ] Enterprise compliance frameworks for agentic tools
- [ ] Performance benchmarks at scale (10M+ line codebases)
- [ ] Optimal human-in-the-loop checkpoint strategies
- [ ] Impact of Supermaven/Cursor acquisition on market
- [ ] Google Antigravity GA timeline and pricing
- [ ] Sourcegraph Cody transition impact on users
- [ ] Regional adoption patterns and variations
