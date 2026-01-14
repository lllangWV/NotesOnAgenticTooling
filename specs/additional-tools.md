# Additional AI Coding Tools Specification

Last updated: 2026-01-14 by RS Loop

Sources:
- https://windsurf.com/
- https://aws.amazon.com/q/developer/
- https://www.jetbrains.com/ai-ides/
- https://www.tabnine.com/
- https://sourcegraph.com/cody
- https://supermaven.com/
- https://www.qodo.ai/
- https://replit.com/

## Overview

This specification covers additional AI coding assistants beyond the major players (Claude Code, Cursor, GitHub Copilot, Gemini Code Assist). These tools represent competitive alternatives with unique differentiators in specific areas like enterprise deployment, speed, or specialized workflows.

## Tools

### Windsurf (formerly Codeium)

**What It Is:** Full AI-native IDE built to compete directly with Cursor, rebranded from Codeium in late 2024.

**Key Features:**
- **Cascade**: Flagship agentic assistant with deep contextual awareness for multi-file edits
- Multi-file refactoring across hundreds of files with single prompts
- Superior handling of large, complex codebases
- Real-time preview of AI-generated code before acceptance

**Deployment:**
- Standalone Windsurf Editor (IDE)
- Plugins for VS Code, JetBrains, Vim/Neovim, Xcode

**Pricing:**
| Plan | Price | Features |
|------|-------|----------|
| Free | $0 | 25 credits/month, unlimited Tab/Supercomplete |
| Pro | $15/month | 500 credits/month |
| Teams | $30/user/month | 500 credits/user, optional Fast Context ($10/user) |
| Enterprise | $60/user/month | 1,000 credits/user, custom pricing for 200+ |

**Credit System:** 1 credit = $0.04, premium model messages consume credits

**Compliance:** SOC 2 Type II, self-hosting options, Zero Data Retention defaults for enterprise

**Recognition:** Named Leader in 2025 Gartner Magic Quadrant for AI Code Assistants

---

### Amazon Q Developer

**What It Is:** AWS's enterprise-focused AI coding assistant with deep AWS integration.

**Key Features:**
- Agentic capabilities: autonomous feature implementation, documentation, testing, code review
- 37-50% code acceptance rates (higher than most competitors)
- Security scanning outperforms leading tools on vulnerability detection
- Code transformation: Java 8→17, .NET Framework→.NET 8 with automated testing
- Natural language AWS pricing queries and workload cost estimation

**Pricing:**
| Plan | Price | Features |
|------|-------|----------|
| Free | $0 | 50 agentic requests/month, 1,000 LOC/month transformations |
| Pro | $19/user/month | Higher limits, 4,000 LOC/month pooled |
| Overage | $0.003/LOC | For transformations beyond limits |

**IDE Support:** JetBrains, IntelliJ, Visual Studio, VS Code, Eclipse (preview)

**Impact:** AWS internal use saved 4,500 developer-years and $260M in 2024

---

### JetBrains AI Assistant

**What It Is:** Native AI integration across all JetBrains IDEs with flexible model support.

**Key Features:**
- Free tier with unlimited local completions (introduced April 2025)
- Multi-file Edit mode from AI Chat
- GPT-5 support (added August 2025)
- Local model support via OpenAI-compatible endpoints (Ollama, LM Studio)
- Deep native integration with JetBrains IDE features

**Pricing:**
| Plan | Features |
|------|----------|
| AI Free | Unlimited local completions + quota-based cloud features |
| AI Ultimate | AI Credits system (1 credit ≈ $1 USD) |
| AI Enterprise | Custom features, part of JetBrains IDE services |

**Credit System:** Valid for 12 months with monthly quota resets

---

### Tabnine

**What It Is:** Enterprise-grade AI coding platform focused on security, privacy, and flexible deployment.

**Key Features:**
- Enterprise Context Engine: learns organization's architecture and coding standards
- Image-to-Code: Figma mockups, ER diagrams → React/SQL code
- 600+ programming languages supported
- Zero code retention: never trains on proprietary code
- Private model endpoints: register Llama 3, Claude 4, Gemini 2.5, or internal models

**Pricing:**
| Plan | Price | Features |
|------|-------|----------|
| Free | $0 | Basic AI completions and chat |
| Pro | $12/user/month | Best-in-class AI models, 90-day trial |
| Enterprise | $39/user/month | Private deployment, fine-tuned models |

**Deployment Options:** SaaS, VPC, on-premises, or fully air-gapped

**Compliance:** GDPR, SOC 2, ISO 27001

**Recognition:** Named Visionary in 2025 Gartner Magic Quadrant for AI Code Assistants

---

### Sourcegraph Cody

**What It Is:** AI assistant leveraging Sourcegraph's code search intelligence for deep codebase understanding.

**Key Features:**
- Deep codebase context across entire organization (not just current file)
- Smart Apply for multi-file modifications
- Full project indexing for complex refactoring
- BYOK (Bring Your Own LLM Key) support

**Pricing (MAJOR CHANGES July 2025):**
| Plan | Status |
|------|--------|
| Cody Free | Discontinued July 23, 2025 |
| Cody Pro | Discontinued July 23, 2025 |
| Cody Enterprise | Still available, custom pricing |
| Amp | New free tool for agentic workflows (replacement) |

**Compliance:** Zero code retention, audit logs, SOC 2/GDPR/CCPA

**Deployment:** Self-hosted or single-tenant options

---

### Supermaven

**What It Is:** Speed-focused AI coding assistant with largest context window.

**Key Features:**
- 1M token context window for highest quality completions
- 3x faster code suggestions than competitors
- "Next location prediction" for intelligent completions
- Multi-model chat: GPT-4o, Claude 3.5 Sonnet, GPT-4

**Pricing:**
| Plan | Price | Features |
|------|-------|----------|
| Free | $0 | 7-day data retention |
| Pro | $10/month | 1M token window, $5 chat credits |
| Team | $10/user/month | All Pro + centralized management |

**Note:** Acquired by Anysphere (Cursor) in October 2024 - future integration expected

---

### Qodo (formerly CodiumAI)

**What It Is:** AI platform focused on code integrity and automated PR reviews.

**Key Features:**
- 15+ agentic workflows for automated reviews
- Qodo Gen: IDE-based code generation and test writing
- Qodo Merge: Open-source PR agent for every pull request
- Qodo Command: Terminal/CI agent scripting (launched June 2025)
- Deep multi-repo awareness via Qodo Aware RAG

**Pricing:**
| Plan | Price | Features |
|------|-------|----------|
| Developer (Free) | $0 | 75 PRs + 250 LLM credits/month |
| Teams | $30/user/month | 2,500 credits, PR descriptions |
| Enterprise | $45/user/month | SSO, on-prem options |

**Deployment:** SaaS, on-prem, VPC, fully air-gapped

**Recognition:** Named Visionary in 2025 Gartner Magic Quadrant

---

### Replit AI Agent

**What It Is:** Browser-based development platform with autonomous AI agents.

**Key Features:**
- Agent 3 (Sept 2025): Up to 200 minutes autonomous operation
- Autonomous testing: executes code, tests apps visually, identifies and fixes bugs
- 50+ languages with one-click deployment
- Real-time multiplayer collaboration

**Pricing:**
| Plan | Price | Features |
|------|-------|----------|
| Core | $20/month (annual) | $25 usage credits included |
| Teams | $35/user/month | $40 credits/user, 50 free viewer seats |

**Effort-based Pricing:** Tasks cost based on computational intensity (simple ~$0.25)

**Warning:** Heavy usage can quickly consume credits - some report $350/day bills

---

### Continue (Open Source)

**What It Is:** Most popular open-source AI coding assistant with 26,000+ GitHub stars.

**Key Features:**
- Model-agnostic: connect any LLM (Llama, Mistral, CodeLlama, OpenAI, Anthropic)
- TUI and headless modes for terminal-native workflows
- Chat, Plan, Agent modes
- MCP support for GitHub, Sentry, Snyk, Linear integrations

**Pricing:** Free (open source), $0.01-$0.10 per feature with cloud models (BYOK)

**Best For:** Air-gapped environments, maximum control, privacy-focused developers

---

## Comparison Matrix

| Tool | CLI | IDE | Free Tier | Pro Start | Best For |
|------|-----|-----|-----------|-----------|----------|
| Windsurf | No | Yes | Yes | $15/mo | Large codebases, multi-file refactoring |
| Amazon Q | Yes | Yes | Yes | $19/mo | AWS developers, enterprise |
| JetBrains AI | No | Yes | Yes | Credits | JetBrains users |
| Tabnine | No | Yes | Yes | $12/mo | Enterprise, air-gapped |
| Cody | No | Yes | Enterprise only | Custom | Code search intelligence |
| Supermaven | No | Yes | Yes | $10/mo | Speed-focused development |
| Qodo | Yes | Yes | Yes | $30/mo | Code quality, PR reviews |
| Replit | No | Browser | No | $20/mo | Rapid prototyping |
| Continue | Yes | Yes | Yes (OSS) | Free | Privacy, customization |

## Open Questions

- [ ] Windsurf vs Cursor detailed benchmark comparisons
- [ ] Amazon Q performance outside AWS ecosystem
- [ ] Long-term implications of Supermaven/Cursor acquisition
- [ ] Cody transition impact on existing users
- [ ] Enterprise adoption patterns for open-source alternatives
