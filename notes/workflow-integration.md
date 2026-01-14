# Workflow Integration Specification

Last updated: 2026-01-14 by RS Loop

## Overview

This specification covers best practices for integrating AI coding assistants into development workflows, including CI/CD pipelines, multi-agent coordination patterns, and compliance requirements for regulated industries.

## CI/CD Integration

### Integration Methods

#### GitHub Actions
```yaml
- name: Install GitHub Copilot CLI
  run: npm i -g @github/copilot

- name: Run Security Agent via Copilot CLI
  env:
    COPILOT_GITHUB_TOKEN: ${{ secrets.COPILOT_GITHUB_TOKEN }}
  run: |
    AGENT_PROMPT=$(cat .github/agents/security-reporter.agent.md)
    copilot --prompt "$AGENT_PROMPT" --allow-all-tools < /dev/null
```

#### Platform Requirements

| Platform | Setup Time | Key Considerations |
|----------|------------|-------------------|
| Jenkins | Varies | 4 vCPU, 8GB RAM per agent, 1,800+ plugins |
| GitHub Actions | 5-10 min | `pull-requests: write` permission required |
| GitLab CI/CD | 30-45 min | Proper runner configuration needed |
| CircleCI | 15-20 min | Monitor pipeline credits on large codebases |
| AWS Lambda | Varies | 3008 MB memory, 15-min timeout limits |

### Tool-Specific Integration

#### Claude Code CI/CD
- Execute `/install-github-app` for automatic setup
- Headless mode: `claude -p "Fix failing test" --allow-tools Edit,View,Bash`
- Issue-to-PR automation via `implement-with-claude` label
- Automatic build fix attempts from CI failure logs

#### GitHub Copilot Coding Agent
- Autonomous completion in GitHub Actions environment
- Workflow file: "Copilot Setup Steps" with `copilot-setup-steps` job
- Required permissions: `contents: read`, `issues: write`, `models: read`

#### Cursor
- Best for interactive editing and navigation
- Pair with Claude Code for automated CI/CD refactors
- VS Code extension compatibility

### Best Practices for CI/CD Integration

#### Workflow Structure
- Descriptive workflow file names (`build-and-test.yml`, `deploy-prod.yml`)
- Appropriate triggers: `push`, `pull_request`, `workflow_dispatch`, `schedule`
- `concurrency` controls to prevent simultaneous runs
- Explicit `permissions` at workflow/job levels

#### Security
- Use GitHub Secrets (`${{ secrets.MY_SECRET }}`)
- OIDC for cloud authentication (avoid long-lived credentials)
- Integrate SAST/SCA tools (CodeQL, `dependency-review-action`)
- Grant minimum necessary GITHUB_TOKEN permissions

#### Performance
- `actions/cache@v3` with `hashFiles()` for dependencies
- `strategy.matrix` for concurrent testing
- `fetch-depth: 1` for most CI builds
- `actions/upload-artifact@v3` with appropriate `retention-days`

### AI Code Review Platforms

| Platform | Key Features |
|----------|-------------|
| Qodo | 15+ agentic workflows, IDE + CI integration |
| CodeRabbit | PR analyzer, inline comments, issue detection |
| GitHub AI Code Review | GPT-4 powered feedback on PRs |
| Diffblue Cover | 250x faster test generation |
| TestSprite | MCP IDE integration, autonomous test lifecycle |

## Multi-Agent Coordination

### Core Patterns (Google ADK)

| Pattern | Description | Use Case |
|---------|-------------|----------|
| Sequential Pipeline | Linear workflow, shared `session.state` | Data processing |
| Coordinator/Dispatcher | Central agent routes to specialists | Request triage |
| Parallel Fan-Out/Gather | Concurrent execution + synthesis | Independent tasks |
| Hierarchical Decomposition | High-level breaks down subtasks | Complex goals |
| Generator and Critic | Separate creation from validation | Quality gates |
| Iterative Refinement | Generation → critique → polish cycles | Qualitative improvement |
| Human-in-the-Loop | Pause for critical authorization | High-stakes actions |
| Composite | Multiple patterns combined | Production systems |

### Microsoft Orchestration Patterns

| Pattern | Agent Limit | Example |
|---------|-------------|---------|
| Sequential | N/A | Contract generation pipeline |
| Concurrent | N/A | Stock analysis (fundamental, technical, sentiment, ESG) |
| Group Chat | ≤3 agents | Municipal park planning |
| Handoff | N/A | Customer support triage |
| Agentic (Magentic) | N/A | SRE incident response |

### Tool Implementations

#### Claude Code Subagents
- Independent context windows (~200k tokens each)
- Custom system prompts for role specialization
- Up to 10 concurrent operations
- **Performance**: 72.5% SWE-bench, 10x parallel execution
- **Real-world**: 45-minute features in under 10 minutes

```
# User-level agents: ~/.claude/agents/
# Project-level agents: .claude/agents/ (takes precedence)
```

#### Devin 2.0 (April 2025)
- Sandboxed environment (shell, editor, browser)
- Interactive planning before execution
- Fleet operations for large-scale migrations
- **Performance**: 4x faster, 67% PR merge rate (up from 34%)

### Task Decomposition Best Practices

**Methodologies**:
1. **Hierarchical Planning**: Multiple abstraction levels
2. **Functional Decomposition**: Logical components (frontend/backend/APIs)
3. **Goal-Oriented**: Focus on outcomes over procedures
4. **Prompt Engineering**: Chain-of-Thought, ReAct, Tree of Thoughts

**Performance**:
- Structured decomposition: ~58% faster task completion
- Bug-fixing improvements: ~47% better

**Best Practices**:
- Clear task definition with manageable subtasks
- Activity logs and human supervision
- Unique agent identifiers for tracking
- Focused assistance (small tasks done well)

### Orchestration Frameworks

| Framework | Type | Best For |
|-----------|------|----------|
| LangGraph | Code-first | Complex workflows, RAG, multiple tools |
| CrewAI | Low-code | Role-based teams, fast deployment |
| AutoGen | Conversational | Agent collaboration via chat |
| OpenAI Swarm | Educational | Learning multi-agent patterns |
| MetaGPT | Research | Assembly-line software development |
| n8n | Visual | 1000+ integrations |

**Performance Comparison**:
- LangGraph: Fastest, lowest latency (2.2x faster than CrewAI)
- LangChain: Highest latency and token usage
- OpenAI Swarm and CrewAI: Very similar performance

### Challenges and Solutions

| Challenge | Impact | Solution |
|-----------|--------|----------|
| Coordination Complexity | System blocks on single agent | Orchestrator-worker pattern |
| State Consistency | Transactionally inconsistent data | Avoid mutable shared state |
| Debugging | Non-deterministic failures | Full production tracing |
| Token Efficiency | 1.5x-7x token overhead | Context compaction, caching |
| Context Limits | Performance degradation | Summarize completed phases |

### Anthropic Multi-Agent Lessons

From production research system (Claude Opus 4 + Sonnet 4):
- **90.2% improvement** over single-agent approach
- **80%** of variance explained by token usage
- **40% faster** task completion with tool description rewrites
- **90% reduction** in research time with parallel tool calling

**Key Practices**:
1. Detailed delegation instructions (objectives, formats, boundaries)
2. Resource scaling guidelines in prompts
3. 3-5 subagents in parallel
4. Context summarization before 200k-token limit

## Regulated Industries

### Compliance Requirements

| Framework | Industry | Key Requirements |
|-----------|----------|-----------------|
| HIPAA | Healthcare | BAAs, PHI security, audit trails |
| SOC 2 | B2B SaaS | Security, availability, processing integrity |
| PCI DSS | Payments | Cardholder data protection |
| FINRA | Finance | Rule 3110 supervision, AI governance |
| SEC | Finance | Document AI tools, explain AI decisions |
| FDA | Medical Devices | 510(k), PCCPs, QMS (ISO 13485) |

### Auditing AI-Generated Code

**Reliability Risks**:
- GitHub Copilot: 53.7% inaccurate code
- ChatGPT: 34.8% inaccurate code

**Required Practices**:
1. Human review and sign-off for all compliance-critical outputs
2. SAST/DAST integration in CI/CD
3. License and compliance checks
4. Auto-generated audit trails
5. Model cards, versions, and evaluation metrics documentation

### Safety-Critical Systems

#### Aviation
- Standards: ARP4754B, DO-178C, DO-254
- Currently: No AI in commercial aircraft (safety concerns)
- FAA differentiates "Learned AI" vs "Learning AI"

#### Automotive
- ISO 26262 (functional safety) - Version 3 expected 2027
- ISO 21448 (SOTIF)
- ISO/PAS 8800 (AI safety for road vehicles)
- ISO 21434 (cybersecurity)

#### Medical Devices
- FDA premarket requirements (510(k), De Novo, PMA)
- Predetermined Change Control Plans (PCCPs)
- Good Machine Learning Practices (GMLP)
- 500+ AI-enabled devices FDA approved (Dec 2025)

### Governance Frameworks

| Framework | Type | Scope |
|-----------|------|-------|
| NIST AI RMF | Voluntary | Govern, Map, Measure, Manage |
| EU AI Act | Mandatory | Risk classification, fines up to 7% revenue |
| ISO/IEC 42001 | Standard | AI management system (38 controls) |

### Documentation Requirements

**Code-Level**:
- Track when, where, how AI was used
- Model name, version, purpose
- Evaluation metrics
- Decision trail documentation

**AI Bill of Materials (AI-BOM)**:
- Model name and version
- Training data sources and licensing
- Prompt content and authors
- SPDX 3.0 for standardized format

### Code Provenance Tools

| Tool | Function |
|------|----------|
| Tabnine Provenance | Flags license types in AI-generated code |
| git-ai | Fingerprints AI code, tracks through git |
| FOSSA/OpenChain | Scans for license violations |

## Security Considerations

### CI/CD-Specific Risks

| Risk | Description | Mitigation |
|------|-------------|------------|
| Behavioral Manipulation | Tricking agents into malicious code | Runtime monitoring |
| Elevated Privileges | GITHUB_TOKEN and secrets exposure | Least privilege |
| Hallucinated Packages | 5.2% Python, 21.7% JavaScript | Dependency scanning |
| Supply Chain | Malicious AI-generated dependencies | Pin versions, verify signatures |

**Statistics**:
- 25-30% of Copilot code contains CWEs
- 62% of AI-generated solutions have security flaws (CSA study)
- 67% of developers spend more time debugging AI code security issues

### Best Practices

1. **Automated Scanning**: SAST, DAST, dependency checks on every PR
2. **CI/CD Gates**: Block deployments with high-severity vulnerabilities
3. **Runtime Monitoring**: Track agent behavior, block unauthorized connections
4. **Human Oversight**: Require confirmation for destructive actions
5. **Audit Trails**: Log all AI tool usage and outputs

## Open Questions

- [ ] How to standardize AI-generated code tracking across organizations?
- [ ] What governance frameworks will emerge for multi-agent systems?
- [ ] How will compliance requirements evolve for autonomous AI agents?
- [ ] What insurance/liability frameworks will cover AI-generated code?

## Sources

### CI/CD Integration
- [Augment Code: 5 CI/CD Integrations](https://www.augmentcode.com/guides/5-ci-cd-pipeline-integrations-every-ai-coding-tool-should-support)
- [DEV Community: GitHub Copilot CLI in Actions](https://dev.to/vevarunsharma/injecting-ai-agents-into-cicd-using-github-copilot-cli-in-github-actions-for-smart-failures-58m8)
- [GitHub Copilot Coding Agent Docs](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent)
- [Developer Toolkit: Claude Code CI/CD](https://developertoolkit.ai/en/claude-code/advanced-techniques/ci-cd-integration/)

### Multi-Agent Coordination
- [Google ADK Multi-Agent Patterns](https://developers.googleblog.com/developers-guide-to-multi-agent-patterns-in-adk/)
- [Azure AI Agent Design Patterns](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns)
- [Anthropic Multi-Agent Research System](https://www.anthropic.com/engineering/multi-agent-research-system)
- [Claude Code Subagents Documentation](https://code.claude.com/docs/en/sub-agents)
- [n8n AI Agent Orchestration](https://blog.n8n.io/ai-agent-orchestration-frameworks/)

### Regulated Industries
- [FDA AI-Enabled Medical Devices](https://www.fda.gov/medical-devices/software-medical-device-samd/artificial-intelligence-enabled-medical-devices)
- [FINRA 2026 Regulatory Oversight Report](https://www.finra.org/rules-guidance/guidance/reports/2026-finra-annual-regulatory-oversight-report/gen-ai)
- [ISO/IEC 42001:2023](https://www.iso.org/standard/42001)
- [NIST AI Risk Management Framework](https://www.diligent.com/resources/blog/nist-ai-risk-management-framework)

### Security
- [StepSecurity: AI Agents in GitHub Actions](https://www.stepsecurity.io/blog/when-ai-meets-ci-cd-coding-agents-in-github-actions-pose-hidden-security-risks)
- [OpenSSF Security Guide for AI Code Assistants](https://best.openssf.org/Security-Focused-Guide-for-AI-Code-Assistant-Instructions)
- [Checkmarx 2025 CISO Guide](https://checkmarx.com/blog/ai-is-writing-your-code-whos-keeping-it-secure/)
