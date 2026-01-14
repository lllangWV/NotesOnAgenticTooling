# Google Antigravity Specification

Last updated: 2026-01-14 by RS Loop

Sources:
- https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/
- https://dev.to/googleai/where-were-going-we-dont-need-chatbots-introducing-the-antigravity-ide-2c3k
- https://www.index.dev/blog/google-antigravity-agentic-ide
- https://antigravityai.org/

## Overview

Google Antigravity is a revolutionary "agent-first" development platform announced November 2025 alongside Gemini 3. Instead of suggesting code, it deploys autonomous AI agents that independently plan, execute, and verify complex development tasks across editor, terminal, and browser environments. Currently in free public preview.

## Terminology

| Term | Definition |
|------|------------|
| Agent-First | Paradigm where autonomous agents are central to development, not sidebar chatbots |
| Manager Surface | Dedicated interface for spawning and observing multiple agents |
| Editor View | Traditional AI-powered IDE for synchronous, hands-on coding |
| Multi-Surface Autonomy | Agents working across editor, terminal, and browser simultaneously |
| Browser Sub-Agent | Agent component that controls Chromium for UI verification |
| Walkthrough Artifacts | Human-readable documentation with screenshots and verification results |
| Deep Think Mode | Extended reasoning for complex architectural decisions |

## Behavior

### Inputs

**Platforms:**
- macOS
- Windows
- Linux

**AI Models:**
- Gemini 3 Pro (default)
- Claude Sonnet 4.5 (switchable)
- Claude Opus 4.5 (switchable)
- GPT-OSS-120B (switchable)

**Context:**
- 1 million token context window
- Full codebase comprehension

**Development Modes:**
1. Agent-Driven (full autonomy)
2. Agent-Assisted (verification checkpoints) - recommended
3. Review-Driven (human approval each step)
4. Custom (task-specific configuration)

### Outputs

**Agent Artifacts:**
- Human-readable implementation plans
- Embedded evidence (not raw tool calls)
- Walkthrough artifacts with screenshots
- Verification results

**Code Operations:**
- Multi-file modifications
- Terminal command execution
- Browser-based UI testing and fixes

### Operations

#### Dual Interface Architecture

**Editor View:**
- Traditional AI-powered IDE
- Tab completions
- Inline commands
- Synchronous, hands-on coding

**Manager Surface:**
- Dedicated agent orchestration interface
- Spawn multiple agents
- Observe agents across workspaces
- Long-running maintenance tasks
- Asynchronous bug fixes

#### Three Command Surfaces

**Editor Surface:**
- Code modification
- Inline suggestions
- File operations

**Terminal Surface:**
- Command execution
- Build operations
- Test running

**Browser Surface:**
- UI verification
- Visual testing
- Runtime error detection

#### Browser Sub-Agent
- Launches/controls headless or visible Chromium
- Uses Gemini 3's multimodal vision
- "Sees" web applications like a user
- Generates Walkthrough Artifacts
- Screenshots and verification results

#### Asynchronous Execution
- Agents work in background
- Developers focus on primary tasks
- Results available when complete
- Queue management for multiple tasks

#### Deep Think Mode
- Extended reasoning capability
- Complex architectural decisions
- Thorough analysis before action

## Constraints & Limitations

**Privacy Consideration:**
- All code processing on Google's servers
- Concern for regulated industries
- IP-sensitive work considerations

**Current Status:**
- Public preview (free for individuals)
- Not yet generally available

**Platform Requirements:**
- Desktop application required
- No web-only option mentioned

## Pricing

| Tier | Price | Status |
|------|-------|--------|
| Public Preview | Free | Current |

Enterprise and paid tiers not yet announced.

## Performance Benchmarks

| Benchmark | Score | Comparison |
|-----------|-------|------------|
| SWE-bench Verified | 76.2% | 1% behind Claude Sonnet 4.5 |
| Terminal-Bench 2.0 | 54.2% | Multi-step workflow completion |
| Feature Development | 40% faster | vs Cursor for Next.js + Supabase |
| Refactoring Accuracy | 94% | vs Cursor's 78% |

## Examples

**Agent-Driven Development:**
1. Describe feature in natural language
2. Agent analyzes codebase (1M token context)
3. Agent creates implementation plan
4. Agent executes across editor, terminal, browser
5. Agent verifies via browser sub-agent
6. Review Walkthrough Artifacts with screenshots
7. Approve or request changes

**Multi-Agent Workflow:**
1. Open Manager Surface
2. Spawn Agent A for backend API changes
3. Spawn Agent B for frontend updates
4. Spawn Agent C for test writing
5. Monitor all agents in dashboard
6. Review consolidated results

**Browser Verification:**
1. Agent makes UI changes
2. Browser sub-agent launches Chromium
3. Navigates to relevant pages
4. Takes screenshots
5. Verifies visual appearance
6. Documents in Walkthrough Artifact
7. Fixes runtime errors if detected

**Agent-Assisted Mode (Recommended):**
1. Describe task
2. Agent creates plan
3. Review plan at checkpoint
4. Approve to continue
5. Agent executes first phase
6. Review at next checkpoint
7. Iterate until complete

## Open Questions

- [ ] Enterprise pricing and availability timeline
- [ ] Data retention and privacy policies for enterprise
- [ ] Integration with existing CI/CD pipelines
- [ ] Team collaboration features
- [ ] Custom model fine-tuning capabilities
- [ ] Offline/on-premises deployment options
