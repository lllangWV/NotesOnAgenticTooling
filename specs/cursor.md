# Cursor Specification

Last updated: 2026-01-14 by RS Loop

Sources:
- https://cursor.com/
- https://cursor.com/features
- https://cursor.com/pricing
- https://cursor.com/docs
- https://www.builder.io/blog/cursor-vs-github-copilot
- https://www.analyticsvidhya.com/blog/2025/07/cursor-agent-guide/

## Overview

Cursor is an AI-powered code editor built as a fork of Visual Studio Code with AI capabilities embedded directly into the editor (not as an extension). It leverages multiple frontier AI models (GPT-4, Claude, Gemini, Grok, DeepSeek) to provide intelligent code completion, generation, codebase understanding, and autonomous agent capabilities.

## Terminology

| Term | Definition |
|------|------------|
| Tab | Cursor's autocomplete feature providing multi-line edit suggestions |
| Composer | Multi-file editing feature that directly edits files based on chat instructions |
| Agent Mode | Autonomous AI agent that explores codebase, edits files, runs commands independently |
| Cursor Rules | Project-scoped guidelines that influence AI behavior to match codebase conventions |
| @ Symbols | Context referencing syntax for files, web, docs, and libraries |
| Codebase Indexing | Background analysis splitting files into chunks with numerical embeddings |

## Behavior

### Inputs

**Context Referencing with @ Symbols:**
- `@Web` - Searches the web for up-to-date information
- `@LibraryName` - References popular libraries
- `@Docs` - Adds custom documentation
- `@files` and `@folders` - Explicit project referencing
- Images can be dragged into chat for visual context

**Keyboard Shortcuts:**
- `Ctrl+K` (Cmd+K) - Generate code or describe changes to selected code
- `Tab` - Accept autocomplete suggestions

**Configuration:**
- Cursor Rules files for project-specific AI behavior
- Model selection per request

### Outputs

**Code Operations:**
- Inline code suggestions (light grey text)
- Multi-line edit suggestions
- Direct file modifications via Composer
- Terminal command generation

**Agent Mode Outputs:**
- Autonomous file exploration results
- Multi-file edit batches
- Terminal command execution
- Error fix iterations

### Operations

#### Tab (Autocomplete)
- Custom model predicts next actions
- Multi-line edit suggestions
- Cross-file intelligent completion
- Suggestions for refactors and multi-file edits

#### AI Chat Interface
- Conversational code assistance
- Context-aware responses based on open files
- Direct codebase modification capability
- Multi-model support

#### Code Generation (Ctrl+K)
- Select code and describe changes in natural language
- Generate new code without selection
- Terminal command generation from plain English

#### Composer (Multi-File Editing)
- Direct file editing based on chat instructions
- Multi-file refactoring
- Scoped changes for precise modifications
- Handles features spanning multiple files

#### Agent Mode
- Autonomous codebase exploration
- Multi-file editing without manual file selection
- Terminal command execution
- Automatic error detection and fixing
- Iteration until task completion

**Agent Mode Layers:**
1. Understanding: Analyzes project architecture
2. Execution: Breaks down requests into actionable steps
3. Integration: Manages code diffs for developer review

**Available Modes:**
- Debug Mode
- Plan Mode
- Multi-Agent Judging
- Pinned Chats
- Read-only mode

## Constraints & Limitations

**Context Windows:**
- Normal mode: 128K tokens
- Max Mode (Pro): 200K tokens

**IDE Lock-in:**
- Requires using Cursor editor (VS Code fork)
- Full VS Code extension compatibility maintained

**Model Availability:**
- OpenAI (GPT-4)
- Anthropic (Claude)
- Google (Gemini)
- xAI (Grok)
- DeepSeek

## Pricing

| Plan | Monthly Cost | Features |
|------|-------------|----------|
| Hobby (Free) | $0 | 2-week Pro trial, 50 premium requests/month, 500 free model requests/month, limited Agent |
| Pro | $20 | Extended Agent limits, unlimited Tab, background agents, max context windows, $20 monthly credits |
| Pro+ | $60 | All Pro + 3x usage multiplier on OpenAI/Claude/Gemini |
| Ultra | $200 | All Pro + 20x usage multiplier, priority feature access |
| Teams | $40/user | All Pro + shared chats/commands/rules, centralized billing, RBAC, SAML/OIDC SSO |
| Enterprise | Custom | All Teams + pooled usage, SCIM, audit logs, priority support |

**Credit Usage (Pro Plan $20 credits):**
- ~225 Claude Sonnet requests OR ~550 Gemini requests
- Claude exhausts credits 2.4x faster than Gemini

**Special Offers:**
- Verified university students: Free Pro for one year
- 20% discount for annual commitments

## Examples

**Multi-File Refactoring:**
1. Open Composer
2. Describe the refactoring needed in natural language
3. Review proposed changes across multiple files
4. Accept or modify suggestions

**Agent Mode Workflow:**
1. Activate Agent Mode
2. Describe complex task
3. Agent autonomously explores codebase
4. Agent makes changes and runs commands
5. Agent fixes errors iteratively
6. Review final results

**Context-Aware Chat:**
1. Open relevant files
2. Use @ symbols to reference additional context
3. Ask questions or request modifications
4. Chat applies changes directly to codebase

## Open Questions

- [ ] Detailed credit consumption rates per model per operation type
- [ ] Agent Mode performance benchmarks on large codebases
- [ ] Cursor Rules best practices and examples
- [ ] Background agent queue management details
