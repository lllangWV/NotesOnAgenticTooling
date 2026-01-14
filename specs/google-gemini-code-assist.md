# Google Gemini Code Assist Specification

Last updated: 2026-01-14 by RS Loop

Sources:
- https://developers.google.com/gemini-code-assist/docs/overview
- https://docs.cloud.google.com/gemini/docs/codeassist/overview
- https://cloud.google.com/products/gemini/pricing
- https://developers.google.com/gemini-code-assist/docs/supported-languages

## Overview

Google Gemini Code Assist is an AI-powered development tool leveraging the Gemini 2.5 model to provide assistance throughout the software development lifecycle. It offers code completion, chat assistance, and code transformation across 23+ programming languages in major IDEs, with enterprise features including private codebase customization.

## Terminology

| Term | Definition |
|------|------------|
| Code Customization | Enterprise feature providing enhanced suggestions based on private codebase |
| Next Edit Predictions | Preview feature suggesting code changes throughout file, not just at cursor |
| Code Transformation | Modifying code via commands or natural language with diff view |
| Smart Actions | Right-click menus and slash commands for common operations |
| Source Citations | References indicating which documentation informed responses |
| Gemini Cloud Assist | AI assistant for operating and optimizing Google Cloud applications |

## Behavior

### Inputs

**Supported Programming Languages (23):**
Bash, C, C++, C#, Dart, Go, GoogleSQL, Java, JavaScript, Kotlin, Lua, MATLAB, PHP, Python, R, Ruby, Rust, Scala, SQL, Swift, TypeScript, YAML

**Prompt Languages (38):**
English, Spanish, French, German, Chinese (simplified/traditional), Japanese, Korean, Arabic, Hindi, and 29 others

**IDEs:**
- Available by default: Cloud Shell, Cloud Workstations, Android Studio
- Via extension: VS Code, JetBrains IDEs (CLion, DataGrip, GoLand, IntelliJ IDEA, PhpStorm, PyCharm, Rider, RubyMine, WebStorm)

**Context Sources:**
- Opened files in IDE
- Project structure
- Publicly available code (training data)
- Google Cloud documentation
- Private repositories (Enterprise only, up to 20,000 repos)

### Outputs

**Code Assistance:**
- Real-time code completions
- Full function/block generation from comments
- Next Edit Predictions (preview)
- Conversational responses with source citations

**Privacy Guarantees (Standard/Enterprise):**
- Data used strictly for serving responses
- Not stored unless instructed
- Private code not shared for other users' benefit
- Customer code not used to train shared models

### Operations

#### Code Completion and Generation
- Real-time completions as you write
- Generate functions/blocks from comments
- Context-aware suggestions based on open files

#### Next Edit Predictions (Preview)
- Suggests changes throughout file
- Not limited to cursor position
- Predictive editing assistance

#### Conversational Chat
- Click "Gemini" in IDE to open
- Uses opened file context
- Model selection (Standard/Enterprise)

**Example Prompts:**
- "Write unit tests for my code"
- "Help me debug my code"
- "Make my code more readable"

#### Code Transformation
- Natural language commands in Quick Pick menu
- Diff view showing pending changes
- Available in VS Code, Cloud Shell, Cloud Workstations

#### Smart Actions
- Right-click context menus
- Slash commands
- Unit test generation
- Debugging support

#### Code Customization (Enterprise Only)
- Enhanced suggestions from private codebase
- Supports GitHub.com and GitLab.com repositories
- Up to 20,000 repositories in index
- Searches all indexed repositories vs current folder only
- Use @ symbol to select specific repos as context

## Constraints & Limitations

**Context Window:**
- 128,000 tokens (backed by Gemini 1.5 Pro's 1M token capability)

**Accuracy Caveat:**
- Can generate plausible but factually incorrect output
- Users must validate all output

**Platform Limitation:**
- Does not run through JetBrains Gateway

**Infrastructure as Code Support:**
- Gemini CLI
- Google Cloud CLI
- Kubernetes Resource Model (KRM)

## Pricing

| Tier | Price | Target | Key Features |
|------|-------|--------|--------------|
| For Individuals (Free) | $0 | Individual developers, students | 6,000 code requests/day, 240 chat/day, no credit card |
| Standard | $19/user/month (annual) or $22.80 (monthly) | Organizations | Code completion, chat, enterprise security, local codebase awareness |
| Enterprise | $45/user/month (annual) | Large enterprises | All Standard + private codebase customization (20K repos), Gemini Cloud Assist |

**Free Tier Limits:**
- 180,000 code completions/month
- 240 chat messages/day
- 6,000 code-related requests/day

**Comparison to GitHub Copilot Free:**
- Gemini: 180,000 completions/month vs Copilot: 2,000/month
- Gemini: 240 chat/day vs Copilot: 50 chat/month

## Examples

**Code Generation from Comments:**
```python
# Function to calculate fibonacci sequence up to n terms
# Returns a list of fibonacci numbers
```
Gemini generates complete function implementation.

**Chat-Assisted Debugging:**
1. Open file with bug
2. Click Gemini icon
3. Ask "Help me debug my code"
4. Review explanation and suggested fixes
5. Apply changes via diff view

**Code Transformation:**
1. Select code block
2. Open Quick Pick menu
3. Type natural language instruction
4. Review diff of proposed changes
5. Accept or modify

**Repository Context (Enterprise):**
1. Open chat
2. Type @ to see available repositories
3. Select specific repo for context
4. Ask question referencing that codebase

## Open Questions

- [ ] Detailed token consumption rates by operation type
- [ ] Code customization indexing time for large repository sets
- [ ] Performance comparison between Standard and Enterprise tiers
- [ ] Integration specifics with other Google Cloud services
