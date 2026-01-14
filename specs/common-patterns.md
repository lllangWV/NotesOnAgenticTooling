# Common Patterns Across AI Coding Assistants

Last updated: 2026-01-14 by RS Loop

Sources:
- https://redmonk.com/kholterhoff/2025/12/22/10-things-developers-want-from-their-agentic-ides-in-2025/
- https://www.thoughtworks.com/en-us/insights/blog/generative-ai/model-context-protocol-mcp-impact-2025
- https://www.technologyreview.com/2025/11/05/1127477/from-vibe-coding-to-context-engineering-2025-in-software-development/
- https://www.kore.ai/blog/choosing-the-right-orchestration-pattern-for-multi-agent-systems
- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns

## Overview

This specification documents the common architectural patterns, features, and trends observed across all major AI coding assistants in 2024-2026. The industry has evolved from simple autocomplete tools to autonomous agentic systems with standardized protocols for tool integration.

## Common Features

### Universal Capabilities

All major coding assistants (Claude Code, Cursor, GitHub Copilot, Gemini Code Assist, etc.) share these baseline features:

| Feature | Description |
|---------|-------------|
| Intelligent Autocomplete | Whole-line and multi-line completion, function/class generation |
| Chat Interfaces | Interactive, IDE-integrated conversational assistance |
| Context Awareness | Codebase understanding, project structure awareness |
| Multi-file Operations | Changes across multiple files with contextual awareness |
| Multiple Model Support | Choice between Claude, GPT, Gemini, and other LLMs |
| IDE Integration | VS Code, JetBrains, and other editor plugins |

### The Agentic Evolution

**2023:** Developers wanted better autocomplete
**2024:** Developers wanted multi-file editing
**2025:** Developers delegate entire workflows to agents

This represents a fundamental shift from passive suggestion to autonomous execution, treating AI agents as junior team members requiring oversight.

## Architectural Patterns

### 1. Subagents

**Definition:** Specialized AI assistants with dedicated expertise areas and isolated context windows.

**How They Work:**
- Each has own system prompt, tool permissions, memory space
- Automatic triggering when task matches agent description
- Can run in parallel for concurrent analysis
- Prevents "context poisoning" by isolating specialized work

**Implementation Across Tools:**
| Tool | Subagent Feature |
|------|-----------------|
| Claude Code | `.claude/agents/` with YAML frontmatter |
| Cursor | Agent Mode with specialized capabilities |
| GitHub Copilot | Coding Agent, Code Review Agent |
| Google Antigravity | Manager Surface for multi-agent orchestration |

### 2. Skills

**Definition:** Autonomous background helpers that activate automatically based on triggers.

**How They Work:**
- Trigger on events (file saves, commits, specific contexts)
- Real-time assistance without manual invocation
- Model-invoked (not user-invoked)

**Key Difference from Commands:**
- Skills: Automatic activation by AI
- Commands: Manual trigger by user

### 3. Slash Commands

**Definition:** Workflow automation tools requiring manual triggering via `/command-name`.

**Common Commands Across Tools:**
| Command Type | Examples |
|--------------|----------|
| Context Management | `/add`, `/drop`, `/clear`, `/context` |
| Model Control | `/model`, `/switch` |
| Workflow | `/commit`, `/pr`, `/test` |
| Navigation | `/help`, `/undo`, `/rewind` |

### 4. Hooks

**Definition:** Automatic event-driven actions configured in settings files.

**Lifecycle Events:**
- PreToolUse: Before tool execution
- PostToolUse: After tool completion
- Notification: When AI sends notifications
- Stop: When AI finishes responding
- SessionStart: When session begins
- UserPromptSubmit: When user sends prompt

**Execution Modes:**
- Command mode: Execute shell scripts
- Prompt mode: LLM contextual decision

### 5. Model Context Protocol (MCP)

**Definition:** Open standard for connecting AI systems to external tools and data sources.

**Timeline:**
- November 2024: Anthropic introduces MCP
- March 2025: OpenAI adopts MCP
- May 2025: Microsoft/GitHub join steering committee
- December 2025: Donated to Linux Foundation

**Adoption Metrics (2025):**
- 8 million+ MCP server downloads
- 97 million monthly SDK downloads
- 5,800+ MCP servers
- 300+ MCP clients

**Key MCP Servers:**
| Server | Purpose |
|--------|---------|
| Context7 | Version-specific documentation |
| GitHub | Code search, automation |
| GitLab | CI/CD integration |
| Semgrep | Static analysis |
| Sentry | Error tracking |
| Datadog | Observability |
| PostgreSQL | Database access |

## Multi-Agent Orchestration

**Market Interest:** Gartner reported 1,445% surge in multi-agent system inquiries (Q1 2024 to Q2 2025).

### Orchestration Patterns

| Pattern | Description | Use Case |
|---------|-------------|----------|
| Supervisor | Central orchestrator coordinates all agents | Complex task decomposition |
| Sequential | Agent output becomes next agent's input | Pipeline workflows |
| Parallel | Multiple agents work simultaneously | Independent subtasks |
| Code-Based | Deterministic task classification | Predictable performance |

### Leading Frameworks (2025)

- OpenAI Agents SDK (March 2025)
- Microsoft Agent Framework (October 2025)
- LangGraph
- CrewAI
- Google ADK

## Developer Requirements (2025)

Based on RedMonk research, developers want these 10 capabilities from agentic IDEs:

1. **Background Agents** - Tasks running autonomously overnight
2. **Persistent Memory** - Decisions remembered across sessions
3. **Predictable Pricing** - Clear costs without surprises
4. **MCP Integration** - Seamless tool connections
5. **Multi-Agent Orchestration** - Parallel agent execution
6. **Spec-Driven Development** - Requirements as contracts
7. **Reliability** - Consistent production performance
8. **Human-in-the-Loop** - Approval gates and audit trails
9. **Rollbacks** - Checkpoint systems for reversion
10. **Skills** - Reusable, shareable workflow modules

## Development Paradigms

### Vibe Coding
**Definition (Andrej Karpathy, Feb 2025):** Unstructured process of chatting with LLM, pasting code, hoping AI "gets the vibe."

**Problems:**
- 8-fold increase in code duplication (GitClear 2024)
- Model reliability issues at scale
- Maintainability concerns

### Spec-Driven Development
**Definition:** Systematic context engineering with structured specifications as contracts for agent behavior.

**Components:**
- Proper documentation
- Architectural decisions
- Version-specific references
- Systematic prompt engineering

**Consensus:** Not either/or but both—vibe coding for prototypes, spec-driven for production.

## Performance Data

### Productivity Metrics

| Study | Finding |
|-------|---------|
| GitHub Copilot | 55% faster task completion, 30% code acceptance |
| Cursor (U Chicago) | 39% increase in merged PRs, 12.5% semantic search improvement |
| METR RCT | 19% *increase* in task completion time for experienced devs |
| GitClear | 8-fold increase in code duplication (2024) |

### Tool Benchmarks (Render.com)

| Metric | Cursor | Claude Code | Gemini CLI |
|--------|--------|-------------|------------|
| Setup | 9/10 | 8/10 | 6/10 |
| Code Quality | 9/10 | 7/10 | 7/10 |
| Context Understanding | 8/10 | 5/10 | 9/10 |
| Integration | 8/10 | 9/10 | 5/10 |
| Speed | 9/10 | 7/10 | 5/10 |
| **Average** | **8.0** | **6.8** | **6.8** |

## Pricing Patterns

### Subscription Tiers (Common Structure)

| Tier | Typical Price | Features |
|------|--------------|----------|
| Free | $0 | Limited completions, basic models |
| Pro/Individual | $10-20/month | Unlimited completions, premium models |
| Team/Business | $19-40/user/month | Collaboration, admin controls |
| Enterprise | Custom | SSO, audit logs, compliance |

### Pricing Models

1. **Subscription-based:** Fixed monthly fee (Cursor, Copilot)
2. **Credit-based:** Monthly credits consumed by usage (Cursor Pro)
3. **Token-based:** Pay per API token (Claude Code API)
4. **Hybrid:** Subscription + overage charges (GitHub Copilot)

## Market Trends

### Growth Projections
- Market: $7.8B (2025) → $52B (2030)
- Gartner: 40% of enterprise apps will embed AI agents by end of 2026

### Key 2025 Entrants
- **Windsurf** (November 2024) - Cursor competitor
- **Google Antigravity** (November 2025) - Agent-first platform
- **Context7** - Documentation-as-context

### Industry Concerns
- MCP security risks
- Code quality from vibe coding
- Skepticism about fully autonomous agents
- Long-term maintainability questions

## Open Questions

- [ ] Security model for MCP server ecosystem
- [ ] Long-term code quality metrics for AI-assisted codebases
- [ ] Optimal human-in-the-loop checkpoint frequency
- [ ] Enterprise compliance frameworks for agentic tools
- [ ] Performance at scale (10M+ line codebases)
- [ ] Multi-language/polyglot project support quality
