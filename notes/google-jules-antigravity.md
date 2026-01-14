# Google Jules & Antigravity Specification

Last updated: 2026-01-14 by RS Loop

## Overview

**Jules** and **Antigravity** are two distinct but complementary AI coding tools from Google. Jules is a cloud-based autonomous coding agent focused on GitHub task automation. Antigravity is an AI-first IDE with multi-agent orchestration capabilities.

## Jules

### What is Jules?

Jules is an autonomous, asynchronous coding agent that helps fix bugs, add documentation, and build new features. It operates entirely in the cloud on GitHub repositories.

**Powered by**: Gemini 2.5 Pro

**Status**: Generally Available (exited beta August 2025)

### Core Workflow

1. Select a GitHub repository
2. Write detailed prompts for desired changes
3. Jules develops implementation plans
4. Review code diffs
5. Jules creates pull requests for approval

### Pricing

| Plan | Price | Daily Tasks | Concurrent Tasks |
|------|-------|-------------|------------------|
| **Free** | $0 | 15 | 3 |
| **Pro** | $19.99/month | 100 | 15 |
| **Ultra** | $124.99/month | 300 | 60 |

**Notes**:
- Access via Google AI Plans subscription
- Only available for @gmail.com accounts (18+)
- College students get Pro free for one year
- Task limits reset on rolling 24-hour window

### Unique Features

#### 1. Proactive Suggestions (2026)
- Scans connected repos for #TODO comments
- Proposes follow-on work without explicit prompting
- Enable on up to 5 repositories
- Available for Pro and Ultra subscribers

#### 2. AGENTS.md Support
- Jules reads AGENTS.md from repo root
- Describes agents/tools, conventions, input/output patterns
- Adopted by 20,000+ open-source projects
- Provides context about project goals, constraints, tools

#### 3. Scheduled Tasks
- Define recurring jobs (maintenance, dependency checks)
- Jules runs on set cadences

#### 4. Render Integration
- When PR deployment fails on Render
- Jules analyzes logs, identifies issues, writes fixes, opens PR

#### 5. Web Search
- Proactively searches for documentation, code snippets
- Results in more accurate task completion

### Architecture

- **100% Cloud-Based**: No local infrastructure required
- **Isolated VM Execution**: Tasks run in Google Cloud VMs
- **Planning System**: Generates plans requiring user review before execution
- **API (Alpha)**: REST API with Sources, Sessions, Activities resources

### GitHub Integration

1. Install Jules GitHub app
2. Connect GitHub account via OAuth
3. Grant repository access
4. Add "jules" label to issues for automatic processing
5. Jules creates PRs linked to original issues

## Antigravity

### What is Antigravity?

Antigravity is a new agentic development platform announced November 2025, designed to shift development from code-writing to task orchestration.

**Status**: Public Preview (free for individuals)

**Platform**: Mac, Windows, Linux (desktop application)

### Architecture

- **VS Code Fork**: Built with "agent-first" design philosophy
- **Models**: Gemini 3 Pro (primary), Gemini 3 Deep Think, Gemini 3 Flash, Claude Sonnet 4.5, GPT-OSS-120B
- **Benchmark**: 76.2% SWE-bench Verified score

### Core Components

#### 1. Editor View
Traditional AI-powered IDE interface with tab completions and inline commands

#### 2. Manager Surface
Dashboard for spawning and monitoring multiple agents working asynchronously across workspaces

#### 3. Agent-Controlled Browser
Autonomous web interactions for testing and verification

### Unique Features

#### 1. Artifacts System
Agents generate verification deliverables:
- Task lists and implementation plans
- Screenshots (before/after UI states)
- Browser recordings for dynamic interactions

#### 2. Interactive Artifact Feedback
Comment directly on artifacts (like Google Docs), agents incorporate feedback without stopping

#### 3. Knowledge Base
Agents save context and improve on future tasks based on learned patterns

#### 4. Google Cloud Integration
Tight Vertex AI integration for deploying to Cloud Run, Firebase, BigQuery via natural language

## Jules vs Antigravity vs Gemini Code Assist

| Feature | Jules | Antigravity | Gemini Code Assist |
|---------|-------|-------------|-------------------|
| **Type** | Cloud-based agent | Desktop IDE | IDE extension |
| **Interaction** | Delegated/async | Supervised/async | Collaborative/sync |
| **Platform** | GitHub.com | Mac/Windows/Linux | VS Code, JetBrains |
| **Best For** | GitHub task automation | Multi-agent orchestration | Real-time coding help |
| **Infrastructure** | Fully managed cloud | Local with cloud models | IDE-integrated |

## Open Questions

- [ ] Antigravity enterprise pricing and timeline to GA
- [ ] Jules support for non-Gmail accounts timeline
- [ ] Best practices for combined Jules + Antigravity workflows
- [ ] Performance benchmarks comparison

## Sources

- [Jules Official Site](https://jules.google/)
- [Jules Documentation](https://jules.google/docs/)
- [Jules API](https://developers.google.com/jules/api)
- [Jules is now out of beta](https://techcrunch.com/2025/08/06/googles-ai-coding-agent-jules-is-now-out-of-beta/)
- [Google Antigravity Announcement](https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/)
- [Jules Proactive Updates](https://blog.google/technology/developers/jules-proactive-updates/)
- [Choose the Right Google AI Developer Tool](https://cloud.google.com/blog/products/ai-machine-learning/choose-the-right-google-ai-developer-tool-for-your-workflow)
