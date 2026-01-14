# GitHub Copilot Specification

Last updated: 2026-01-14 by RS Loop

Sources:
- https://docs.github.com/en/copilot
- https://github.com/features/copilot
- https://code.visualstudio.com/docs/copilot/overview
- https://docs.github.com/en/copilot/get-started/plans
- https://github.com/github/copilot-cli

## Overview

GitHub Copilot is an AI-powered coding assistant providing contextualized support throughout the software development lifecycle. It offers code completions, conversational chat assistance, autonomous agents, and deep integration with the GitHub ecosystem. Available across multiple IDEs and platforms, Copilot uses advanced language models (GPT, Claude, Gemini) to enhance developer productivity.

## Terminology

| Term | Definition |
|------|------------|
| Coding Agent | Autonomous agent that works on GitHub issues and creates pull requests |
| Background Coding Agent | Agent running in GitHub Actions environment to complete tasks asynchronously |
| Code Review Agent | Agent that analyzes pull requests for bugs, improvements, and security issues |
| Copilot Spaces | Organized project context (code, documentation, notes) for tailored assistance |
| Next Edit Suggestions | Proactive suggestions for complementary changes when you modify code |
| Premium Requests | Requests using advanced models, subject to monthly allowances |
| MCP | Model Context Protocol for extending Copilot capabilities |

## Behavior

### Inputs

**IDE Integration:**
- Visual Studio Code (automatic extension installation)
- Visual Studio
- JetBrains IDEs
- Azure Data Studio
- Xcode
- Vim/Neovim
- Eclipse
- Windows Terminal

**Context Sources:**
- Open files in IDE
- Imported libraries and dependencies
- Existing code patterns
- Natural language prompts and comments
- Project structure
- GitHub repository data

**Model Selection:**
- GPT-4o
- Claude 3.5/Claude Opus 4.1
- Gemini 2.0 Flash
- Additional models per tier

### Outputs

**Code Completions:**
- Single line completions
- Multi-line completions
- Entire function implementations
- Context-aware suggestions

**Agent Outputs:**
- Pull requests from issue assignments
- Code review comments
- Suggested fixes for CodeQL alerts
- Terminal command suggestions

### Operations

#### Code Completion
- Real-time inline suggestions
- Range from single line to entire functions
- Uses context of open files, imports, and patterns
- Multi-language support

#### Copilot Chat
- Available on GitHub.com, GitHub Mobile, supported IDEs, Windows Terminal
- Generate test cases
- Explain code functionality
- Request refactoring suggestions
- Multi-model support

#### Copilot CLI
- Terminal-native interface
- Answers questions from command line
- Makes changes to local files
- Interacts with GitHub.com (list PRs, create issues)
- Same agentic harness as coding agent

#### Agent Mode (IDE-based)
- Determines which files need changes
- Offers code changes and terminal commands
- Handles compile and lint errors automatically
- Monitors terminal and test output
- Iterates until task completion

#### Background Coding Agent
- Assign GitHub issues to Copilot
- Works in GitHub Actions environment
- Creates pull requests with results
- Available via github.com, GitHub Mobile, GitHub CLI

#### Code Review Agent
- Analyzes pull requests for bugs
- Identifies improvement opportunities
- Detects security issues
- Runs before human review

#### Extensions & MCP
- Model Context Protocol for external tool integration
- Custom agents for specific workflows
- Copilot Spaces for context organization

#### Next Edit Suggestions
- Proactive complementary change suggestions
- Cross-file reference updates
- Test file updates when code changes

## Constraints & Limitations

**IP Protection:**
- Duplicate detection and code reference features
- IP indemnity for unmodified suggestions (when filtering enabled)
- License identification for open-source matches

**Model Limitations:**
- May generate incorrect or inefficient code
- Context awareness can slow with very large projects
- May not generate adequate test cases in all scenarios
- Requires human oversight

**Platform Requirements:**
- GitHub account required
- Enterprise tier requires GitHub Enterprise Cloud

## Pricing

### Individual Plans

| Plan | Cost | Features |
|------|------|----------|
| Free | $0 | 50 chat messages/month, 2,000 code completions/month, basic models |
| Pro | $10/month or $100/year | Unlimited completions, premium models, 300 premium requests/month, coding agent |
| Pro+ | $39/month or $390/year | All Pro + 1,500 premium requests/month (5x), all chat models, GitHub Spark |

### Organization Plans

| Plan | Cost | Features |
|------|------|----------|
| Business | $19/user/month | IDE + CLI + Mobile, coding agent, 300 premium requests/user, centralized management, content exclusion |
| Enterprise | $39/user/month | All Business + 1,000 premium requests/user, GitHub.com chat, codebase indexing, tailored suggestions |

**Free Access:**
- Verified students and teachers
- Maintainers of popular open-source projects

## Examples

**Code Completion Workflow:**
1. Start typing code or write a comment describing intent
2. Copilot suggests completion inline
3. Press Tab to accept or continue typing to refine
4. Suggestions update based on context

**Issue-to-PR Workflow:**
1. Create or select GitHub issue
2. Assign issue to Copilot
3. Copilot works in background via GitHub Actions
4. Review generated pull request
5. Merge or request changes

**Chat-Assisted Development:**
1. Open Copilot Chat in IDE
2. Ask question about code or request changes
3. Review explanation or suggested code
4. Apply changes or continue conversation

**CLI Usage:**
```bash
# Get help with commands
gh copilot suggest "find all large files in repo"

# Explain a command
gh copilot explain "git rebase -i HEAD~3"
```

## Open Questions

- [ ] Detailed premium request consumption by model and operation
- [ ] Codebase indexing performance and limitations for Enterprise
- [ ] MCP server ecosystem and recommended integrations
- [ ] Agent mode reliability metrics for complex multi-file tasks
