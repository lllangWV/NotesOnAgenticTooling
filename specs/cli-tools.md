# CLI-Based AI Coding Tools Specification

Last updated: 2026-01-14 by RS Loop

Sources:
- https://opencode.ai/
- https://github.com/opencode-ai/opencode
- https://aider.chat/
- https://github.com/Aider-AI/aider
- https://cline.bot/
- https://www.kdnuggets.com/top-5-agentic-coding-cli-tools
- https://thenewstack.io/ai-coding-tools-in-2025-welcome-to-the-agentic-cli-era/

## Overview

CLI-based AI coding assistants operate in the terminal, providing developers with low-level control, scriptability, and integration with CI/CD systems. The 2025-2026 period marked the "Agentic CLI Era" with tools like OpenCode, Aider, Claude Code, Gemini CLI, and Cline offering autonomous, multi-step coding workflows through terminal interfaces.

## Terminology

| Term | Definition |
|------|------------|
| Agentic CLI | Terminal-based AI tool capable of autonomous multi-step task execution |
| TUI | Terminal User Interface - graphical interface within terminal |
| Plan Mode | Preview changes without modifications |
| Build Mode | Execute actual modifications |
| Human-in-the-Loop | Workflow requiring human approval for actions |
| Headless Operation | Running without graphical interface for automation |

## Tools Comparison

### OpenCode

**Source:** https://opencode.ai/

**What It Is:**
- Open-source AI coding agent
- Terminal, desktop app, or IDE extension
- Built in Go with TUI interface

**Key Features:**
- Multi-platform: Terminal, desktop, IDE extension
- Model flexibility: Free models or connect Claude, GPT, Gemini
- Language Server Protocol integration
- Privacy-focused: No code/context storage
- Dual modes: Plan (preview) and Build (execute)
- Built-in "Build" and "Plan" agents
- Custom agent creation support

**Pricing:**
- Core: Free with own API keys or Claude Pro/ChatGPT Plus subscription
- Zen: Pay-as-you-go starting at $20 credit
- Black (unannounced): $20/month base tier

**Installation:**
- npm, Homebrew, Arch Linux repositories, Docker

---

### Aider

**Source:** https://aider.chat/

**What It Is:**
- One of the first open-source AI coding assistants
- 38.8k GitHub stars
- Tight git integration

**Key Features:**
- Supports 15+ providers: GPT-4, Claude, Gemini, GROQ, DeepSeek, Ollama
- 67% success rate in benchmark testing (highest tested)
- Automatic commits with descriptive messages
- Voice-to-code capability
- Image/web page input
- Prompt caching
- File watching
- Optional web UI and VS Code extensions

**Slash Commands:**
- `/add` - Add files to conversation
- `/model` - Change AI model
- `/drop` - Remove files from context
- `/editor` - Open external editor

**Pricing:**
- Free (pay only for AI model API usage)

---

### Cline (formerly Claude Dev)

**Source:** https://cline.bot/

**What It Is:**
- Autonomous coding agent for VS Code/JetBrains with CLI support
- 54.1k GitHub stars
- ~2 million downloads in 6 months

**Key Features:**
- 63% success rate in benchmark testing
- Open-source with flexible LLM backend
- Dual "Plan" and "Act" modes
- Human-in-the-loop GUI for permissions
- Headless browser for runtime error fixing
- Model Context Protocol (MCP) support

**Unique Capabilities:**
- Can launch headless browser
- Fix runtime errors and visual bugs
- Requires permission for file changes and terminal commands

**Pricing:**
- Free (pay only for AI model API usage)

---

### Gemini CLI

**Source:** Google (open-source)

**What It Is:**
- Open-source AI agent from Google (2025)
- Free access to Gemini 2.5 Flash
- 1 million token context window

**Key Features:**
- Lightweight terminal access to AI
- Free tier: 60 requests/minute, 1,000 requests/day

**Challenges:**
- Setup complexity
- Free plan quota consumed quickly with advanced models

---

### Other Notable Tools

| Tool | Stars | Notes |
|------|-------|-------|
| Continue | 30,795 | IDE-agnostic, CLI for headless operations |
| Goose | - | Reference MCP implementation, early MCP client |
| Droid (Factory) | - | Local problem-solving, Docker log reading |
| OpenAI Codex CLI | - | Terminal assistant from OpenAI |

## Common CLI Patterns

### Subagents
- Specialized AI assistants with dedicated expertise
- Isolated context windows per agent
- Prevents "context poisoning"
- Automatic triggering based on task matching
- Can run in parallel

### Skills
- Autonomous background helpers
- Trigger on events (file saves, commits, contexts)
- Real-time assistance without manual invocation
- New `context_fork` parameter for independent windows

### Slash Commands
- Manual workflow automation triggers
- Type `/command-name` to execute
- Orchestrate multiple actions
- Invoke agents for complex tasks

### Hooks
- Automatic event-driven actions
- Configure in settings files
- Lifecycle events: PostToolUse, UserPromptSubmit, SessionStart
- Two modes: Command (shell scripts) or Prompt (LLM decision)

### Model Context Protocol (MCP)
- Open standard for AI system integrations
- Introduced by Anthropic (November 2024)
- Adopted by OpenAI (March 2025)
- Donated to Linux Foundation (December 2025)
- Universal adapter for AI-to-tool connections

**Top MCP Servers:**
- Context7: Documentation-as-context pipeline
- GitHub MCP: Code search, testing, commits
- GitLab MCP: CI/CD pipeline integration
- Semgrep MCP: Static analysis
- Sentry MCP: Error tracking
- Datadog MCP: Metrics, logs, traces
- PostgreSQL MCP: Database bridge

## CLI vs IDE Trade-offs

### CLI Advantages
- Complex task orchestration
- System-level CI/CD integration
- Headless operation capability
- Greater autonomy and customization
- Project-wide operations
- Privacy and data sovereignty
- Model flexibility
- Cost control via open-source

### IDE Advantages
- Routine coding tasks
- Quick inline suggestions
- Graphical interfaces
- Fast setup time
- Focused single-file context

### When to Use CLI
- Orchestrating multi-file refactoring
- Privacy/data sovereignty requirements
- Terminal workflow preference
- CI/CD pipeline integration
- Cost management priority

### When to Use IDE
- Routine coding tasks
- Quick inline suggestions preferred
- Team prefers graphical interfaces
- Fast setup needed
- Single-file focused work

**Best Practice:** Many developers use both—IDE for routine coding, CLI for complex orchestration.

## Benchmark Results

| Tool | Success Rate | Notes |
|------|-------------|-------|
| Aider | 67% | Highest among tested |
| Cline | 63% | Strong autonomous capability |
| Claude Code | 56% | Good session summaries |
| Various others | Varies | Task-dependent performance |

## Pricing Summary

| Tool | License | Cost Model |
|------|---------|-----------|
| Aider | Open-source | Free + API costs |
| OpenCode | Open-source | Free + API costs (or Zen $20 credit) |
| Cline | Open-source | Free + API costs |
| Continue | Open-source | Free + API costs |
| Gemini CLI | Open-source | Free tier with limits |
| Claude Code | Commercial | $20/month (Pro) bundled |

## Open Questions

- [ ] Long-term maintainability of codebases built with CLI agents
- [ ] Security implications of MCP server ecosystem
- [ ] Performance of local models vs cloud APIs
- [ ] Enterprise management features for open-source tools
- [ ] True autonomous error-fixing reliability metrics
