# Claude Code Specification

Last updated: 2026-01-14 by RS Loop

Sources:
- https://code.claude.com/docs/en/overview
- https://www.anthropic.com/engineering/claude-code-best-practices
- https://code.claude.com/docs/en/sub-agents
- https://code.claude.com/docs/en/mcp
- https://claude.com/pricing
- https://claudecode.io/comparison

## Overview

Claude Code is Anthropic's agentic coding tool that operates directly in the terminal. Unlike traditional coding assistants that offer suggestions, Claude Code takes direct action on codebases—editing files, running commands, creating commits, and integrating with external tools through the Model Context Protocol (MCP).

## Terminology

| Term | Definition |
|------|------------|
| Agentic Coding | AI that autonomously executes multi-step coding tasks rather than just suggesting code |
| MCP | Model Context Protocol - open standard for connecting AI to external data sources and tools |
| Subagent | Specialized AI assistant with dedicated expertise, isolated context window, and custom tool permissions |
| Skill | Model-invoked capability that Claude autonomously uses based on context |
| Slash Command | User-invoked workflow automation triggered by typing `/command-name` |
| Hook | Shell command that executes at lifecycle points (PreToolUse, PostToolUse, etc.) |
| CLAUDE.md | Project-specific instruction file read automatically by Claude Code |

## Behavior

### Inputs

**Installation Methods:**
- macOS/Linux/WSL: `curl -fsSL https://claude.ai/install.sh | bash`
- Windows PowerShell: `irm https://claude.ai/install.ps1 | iex`
- Homebrew: `brew install --cask claude-code`

**Configuration Files:**
- `CLAUDE.md` - Project instructions at repository root or any directory level
- `.claude/agents/` - Project-level subagent definitions (YAML frontmatter in Markdown)
- `~/.claude/agents/` - User-level subagent definitions
- `.claude/skills/` - Project-level skills
- `~/.claude/skills/` - User-level skills
- `.claude/commands/` - Project slash commands
- `~/.claude/commands/` - Personal slash commands
- `.claude/settings.json` - Hook configurations

**Command Line Interface:**
- Interactive mode: `claude`
- Headless mode: `claude -p "your prompt"`
- Piped input: `tail -f app.log | claude -p "Slack me if you see any anomalies"`

### Outputs

**Direct Actions:**
- File edits and creation
- Command execution in terminal
- Git commits with descriptive messages
- Pull request creation and updates
- External tool interactions via MCP

**Session Information:**
- Session summaries with costs and processing time
- Context usage metrics

### Operations

#### Subagents
- Specialized AI assistants handling specific task types
- Each runs in isolated context window with custom system prompt
- Independent tool access and permissions
- Can run in parallel for concurrent analysis

**Tool Permissions by Role:**
- Read-only agents: Read, Grep, Glob
- Research agents: Read, Grep, Glob, WebFetch, WebSearch
- Code writers: Read, Write, Edit, Bash, Glob, Grep

#### Skills
- Model-invoked (not user-invoked) capabilities
- Claude autonomously uses them based on context
- Can include multiple files and scripts
- Located in `.claude/skills/` or `~/.claude/skills/`

#### Slash Commands
- User-invoked via `/command-name`
- Autocomplete works anywhere in input
- Built-in: `/help`, `/compact`, `/init`, `/context`, `/clear`, `/catchup`, `/rewind`, `/hooks`, `/pr`

#### Hooks
- Execute at lifecycle points: PreToolUse, PostToolUse, Notification, Stop
- Receive JSON data via stdin with session information
- Configured via `/hooks` command or settings file

#### MCP Integration
- Resources: Expose data referenced via @ mentions
- Dynamic updates via `list_changed` notifications
- Pre-built servers: Google Drive, Slack, GitHub, Git, Postgres, Puppeteer

## Constraints & Limitations

**Context Window:**
- Up to 200,000 tokens context length

**Platform Availability:**
- CLI (primary interface)
- Web version
- Desktop app
- VS Code extension
- JetBrains plugin
- GitHub Actions
- GitLab CI/CD
- Slack integration
- Chrome Extension (beta)

**Enterprise Requirements:**
- Claude API, AWS Bedrock, Google Vertex AI, Microsoft Foundry support
- SOC 2 Type II, ISO/IEC 27001:2022, ISO 42001:2023 certified
- FedRAMP High authorization available

## Pricing

| Plan | Monthly Cost | Claude Code Access | Usage Limits |
|------|-------------|-------------------|--------------|
| Free | $0 | No | Limited daily messages |
| Pro | $20 | Yes | ~45 messages/5 hours, Claude Sonnet 4.5 |
| Max (5x) | $100 | Yes | 5x Pro usage |
| Max (20x) | $200 | Yes | 20x Pro usage, generous Opus 4.5 access |
| Team | $30/user | Yes | Min 5 members |

**API Token Pricing:**
| Model | Input (per 1M tokens) | Output (per 1M tokens) |
|-------|----------------------|------------------------|
| Haiku | $1 | $5 |
| Sonnet 4.5 | $3 | $15 |
| Opus 4.5 | $5 | $25 |

## Examples

**Research-Plan-Implement Workflow:**
1. Ask Claude to explore relevant files (no coding)
2. Create plan using extended thinking ("think hard," "ultrathink")
3. Gain approval
4. Implement

**Test-Driven Development:**
1. Write tests first
2. Confirm failures
3. Commit tests
4. Iteratively develop until tests pass

**Context Optimization:**
- Use `/clear` between tasks to prevent context pollution
- Maintain checklists as working scratchpads
- Use `#` key to incorporate instructions into documentation

## Open Questions

- [ ] Specific token consumption rates for different operation types
- [ ] Detailed hook configuration examples for complex workflows
- [ ] Performance benchmarks across different codebase sizes
