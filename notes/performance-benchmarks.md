# AI Coding Assistant Performance & Benchmarks

Last updated: 2026-01-14 by RS Loop

## Overview

This document provides comprehensive analysis of AI coding assistant performance across multiple dimensions: benchmark results (SWE-bench, HumanEval), token consumption patterns, response times/latency, and multi-file refactoring capabilities. The landscape has seen dramatic improvement, with top models progressing from ~4% in 2023 to over 80% on SWE-bench Verified in 2025-2026.

---

## SWE-bench Benchmark Results

SWE-bench evaluates AI coding agents on real GitHub issues, measuring their ability to resolve software engineering problems autonomously.

### SWE-bench Verified Results (2025-2026)

The most widely cited benchmark for real-world coding capabilities (500 human-validated problems).

| Model | Score | Date |
|-------|-------|------|
| **Claude Opus 4.5** | **80.9%** | Dec 2025 |
| Gemini 3 Flash | 78.0% | Nov 2025 |
| Claude Sonnet 4.5 | 77.2% | Sep 2025 |
| GPT-5.2 | 75.4% | Nov 2025 |
| Claude Sonnet 4 | 72.7% | Sep 2025 |
| OpenAI o3 | 71.7% | Dec 2025 |
| Claude 3.7 Sonnet | 62.3-70.3% | 2024 |
| GitHub Copilot (Claude 3.7) | 56.5% | 2025 |
| Cursor | 51.7% | 2025 |
| Gemini 2.0 Flash | 51.8% | 2024 |
| OpenAI o1 | 48.9% | 2024 |

**Key Insight**: Claude Opus 4.5 was the first model to exceed 80% on SWE-bench Verified.

### SWE-bench Pro Results (Enterprise-Level)

More challenging benchmark with 1,865 tasks across 41 professional repositories.

| Model | Score | Notes |
|-------|-------|-------|
| Claude Opus 4.5 | 45.89% | Dec 2025 |
| Claude Sonnet 4.5 | 43.60% | Sep 2025 |
| Gemini 3 Pro Preview | 43.30% | Nov 2025 |
| Claude Sonnet 4 | 42.70% | Sep 2025 |
| GPT-5 (High) | 41.78% | Nov 2025 |

**Critical Finding**: Significant performance drop on Pro vs Verified (80% → 45%) highlights difficulty of enterprise-complexity tasks.

### Tool-Specific Comparisons

**Cursor vs GitHub Copilot** (500 SWE-bench Verified tasks):
- **Copilot**: 283 tasks solved (56.5% resolution rate)
- **Cursor**: 258 tasks solved (51.7% resolution rate)
- **Speed**: Cursor 30% faster (62.95s vs 89.91s average)

**Aider Performance**:
- SWE-bench Lite: 26.3% (state-of-the-art in May 2024)
- Polyglot Benchmark: GPT-5 (high) achieves 88.0% at $29.08 cost

### Historical Evolution

| Year | Best Performance | Key Milestone |
|------|-----------------|---------------|
| 2023 | 4.4% | AI first applied to SWE-bench |
| 2024 | ~50% → 71.7% | Rapid improvement, Verified released |
| 2025 | 80.9% | Claude Opus 4.5 breaks 80% barrier |

**18x improvement** from 2023 to 2025.

---

## HumanEval & MBPP Benchmarks

Function-level code generation benchmarks.

### HumanEval Results (2025)

| Model | Pass@1 |
|-------|--------|
| o1-mini | 96.2% |
| Claude 3.5 Sonnet | 92.0% |
| GPT-4o | 90.2% |
| Codestral 25.01 | 86.6% |
| Claude 2 (2023) | 71.2% |
| GPT-4 (2023) | ~67% |

**HumanEval Pro** (enhanced version with self-invoking tasks):
- o1-mini: 96.2% → 76.2% (20 percentage point drop)

### Other Benchmarks

- **LiveCodeBench**: Contamination-free evaluation with 1,055 problems (continuously updated)
- **BigCodeBench**: LLMs score up to 60% vs human 97% - significant gap remains
- **RepoQA**: Long-context code understanding (500 tests across 50 repositories)

---

## Token Consumption & Costs

### Token Usage by Workflow Type

| Workflow | Token Estimate |
|----------|---------------|
| Average Pull Request | ~2,300 tokens |
| Feature Development | 50K+ tokens (with iterations) |
| Bug Fixes | Lower (narrower scope) |
| Large Refactors | Highest consumption |
| Code Conversion | ~100 lines = 1,000 tokens |

### Tool-Specific Token Management

**Claude Code**:
- 5-hour rolling windows:
  - Pro: ~44,000 tokens/window
  - Max5: ~88,000 tokens/window
  - Max20: ~220,000 tokens/window
- Daily spending: Average $6/developer (90% below $12)
- Extended context (>200K tokens): $6 input / $22.50 output per million

**Cursor**:
- Pro Plan ($20/month): 500 fast requests ≈ 5M tokens/month
- Effective rate: ~$0.30-$0.60 per million tokens
- 10-person team easily burns thousands of requests monthly

**GitHub Copilot**:
- Premium requests (June 2025): 300 for Pro, 1,500 for Pro+
- Users report $41.87+ in overages beyond $10/month subscription
- Agent mode and o1 model are "particularly token-intensive"

**Aider (BYOK)**:
- Typical feature: $0.01-0.10 with GPT-4o
- File processing: $0.007 per file
- 50-developer team: $100-300/month total API costs

### Cost Comparison by Use Case

| Use Case | Monthly Cost |
|----------|-------------|
| **Prototyping** | $0-5 (Gemini free, Aider + DeepSeek) |
| **Professional** | $10-30 (Copilot Pro, Cursor Pro, Claude Pro) |
| **Heavy-Duty** | $100-300+ (Claude Max, API-direct users) |
| **Power Users** | $5K+/month (reported extreme usage) |

### Token Optimization Techniques

1. **Prompt Caching**: 10x cheaper, up to 85% latency reduction
2. **Batch Processing**: 50% cost reduction for non-urgent tasks
3. **Model Selection**: Haiku $1/M vs Opus $5/M (5x difference)
4. **Context Pruning**: Remove irrelevant files with `/drop`
5. **Efficient Serialization**: Poor formatting wastes 40-70% of tokens

---

## Response Times & Latency

### Time to First Token (TTFT) by Model

| Model | TTFT | Tokens/sec |
|-------|------|------------|
| Mistral Large 2512 | 0.30s | 40 |
| Claude 3.5 Haiku | 0.36s | 133 |
| GPT-5.2 | 0.50s | 67 |
| Claude 3 Haiku | 0.55s | 133 |
| Claude 3.5 Sonnet | 0.64s | 78 |
| Claude 4.5 Sonnet | ~2.0s | - |
| DeepSeek V3.2 | 19s | 33 |

### Tool-Specific Response Times

**GitHub Copilot**:
- Inline completion: 110-140ms (optimized from 180-220ms)
- Chat: 2.9s (improved from 3.8s)
- Serves 400M completion requests/day

**Cursor**:
- Composer 2.0: 250 tokens/second
- Task completion: Under 30 seconds (4x faster than competitors)
- User reports: 20-60 second delays in some cases

**Claude Code**:
- Writes ~1,200 lines in 5 minutes vs Codex ~200 lines in 10 minutes
- Haiku 4.5: Sub-200ms for small prompts
- Performance degradation reported for heavily-used projects

**Aider**:
- GPT-4-1106: 2-2.5x faster than June GPT-4
- Diff format significantly reduces latency vs whole-file format

### Factors Affecting Latency

1. **Context Length**: Self-attention scales quadratically (2x tokens = 4x compute)
2. **Model Size**: Haiku 300-550ms vs Sonnet 2-19s TTFT
3. **API vs Local**: Local <100ms, Cloud 5-10s for complex tasks
4. **Streaming**: Reduces perceived latency to <1s

### Optimization Techniques

- **Prompt Caching**: Up to 85% latency reduction for long prompts
- **Streaming**: Single most effective approach for interactive coding
- **Connection Reuse**: Eliminates TCP handshake overhead
- **Request Parallelization**: Reduced candidates from 2-3 to 1 for single-line

---

## Multi-File Refactoring Capabilities

### Tool Capabilities Comparison

| Tool | Approach | Best For |
|------|----------|----------|
| **Claude Code** | Autonomous multi-step execution | Large-scale refactoring, entire features |
| **Cursor** | Preview-first with granular acceptance | Controlled repo-wide refactors |
| **Aider** | Git-integrated CLI workflow | Structured refactors with version control |
| **GitHub Copilot** | Agent mode with iterative correction | Smaller repos, VS Code users |

### Refactoring Benchmark Results

**Aider Refactoring Benchmark** (89 large Python methods):

| Model | Success Rate |
|-------|-------------|
| Claude 3.5 Sonnet (Oct 2024) | **92.1%** |
| O1-Preview | 75.3% |
| Claude 3 Opus | 72.3% |
| Claude 3.5 Sonnet (June 2024) | 64.0% |
| GPT-4o | 62.9% |
| DeepSeek V3 | 55.1% |

### Case Studies

**Atlassian Nav4 Cleanup** (1,400+ files):
- Transformed weeks of manual work into automation pipeline
- AI reasoning outperformed pure script generation
- Key: Small batched changes with tight feedback loops

**Rakuten** (Claude Code):
- 7 hours sustained autonomous coding
- 79% improvement in time-to-market (24 days → 5 days)

### Limitations and Failure Modes

**What AI Handles Well**:
- Low-level consistency edits (rename, type changes)
- Maintainability improvements (52.5% of agent refactoring)
- Readability enhancements (28.1%)

**What AI Struggles With**:
- Code duplication removal (1.1% vs 13.7% for humans)
- Modularity and reuse (4.6% vs 12.9% for humans)
- Architectural changes requiring deep system understanding
- Context management in large codebases (>2,500 files)

**Empirical Finding**: Agents excel at consistency-oriented, lower-level edits but show less capability for transformative architectural improvements.

### Best Practices

1. **Incremental Implementation**: Start with small, non-critical functions
2. **Comprehensive Testing**: Establish E2E tests before refactoring
3. **Human Review**: Never accept changes blindly
4. **Task Decomposition**: Break complex refactoring into smaller commands
5. **Git Integration**: Use tools with automatic commits for easy reversal
6. **Context Management**: Use tools with 200K+ token context windows

---

## Benchmark Limitations & Critiques

### SWE-bench Issues

1. **Solution Leakage** (32.67%): Solutions in issue reports inflate scores
2. **Weak Test Cases** (31.08%): Incomplete tests miss flawed fixes
3. **Data Contamination**: Models pre-trained on public GitHub repos
4. **Task Clarity**: Ambiguous problem statements cause misinterpretation
5. **Environment Inconsistencies**: Patches fail due to dependency differences

**TestEnhancer Study**: Resolution rates dropped 27-36 percentage points with enhanced tests.

### HumanEval Limitations

- Only 164 problems, focus on algorithms/simple math
- Average 7.7 tests per problem (EvalPlus adds 80x more)
- Performance drop on HumanEval Pro shows brittleness

### Real-World vs Benchmark Gap

- BigCodeBench: LLMs 60% vs Human 97%
- Different scaffolding changes GPT-4 from 2.7% to 28.3% on same benchmark
- Benchmarks measure entire agent system, not just model

---

## Key Takeaways

1. **Dramatic Progress**: 18x improvement on SWE-bench from 2023-2025 (4.4% → 80.9%)

2. **Claude Leads Accuracy**: Opus 4.5 at 80.9% SWE-bench Verified, Sonnet 4.5 at 92.1% refactoring

3. **Enterprise Gap**: 70-80% Verified → 23-46% Pro shows real-world complexity challenges

4. **Cost Variance**: $0.01/task (Aider) to $25/hour (Roocode) - tool selection matters

5. **Optimization Critical**: Prompt caching provides 10x cost reduction on cached tokens

6. **Refactoring Reality**: AI excels at consistency edits, struggles with architectural changes

7. **Speed vs Quality**: Cursor 30% faster but Copilot 5% higher success rate

8. **Benchmark Caveats**: 32-63% of benchmark results may be inflated by leakage/weak tests

---

## Open Questions

- [ ] How do benchmarks translate to actual developer productivity gains?
- [ ] What is the long-term reliability of AI-assisted refactoring at enterprise scale?
- [ ] How do different models perform across non-Python languages?
- [ ] What is the optimal human-AI collaboration pattern for complex refactoring?

---

## Sources

### SWE-bench & Benchmarks
- [SWE-bench Official Leaderboards](https://www.swebench.com/)
- [Scale AI SWE-Bench Pro](https://scale.com/leaderboard/swe_bench_pro_public)
- [LLM Stats SWE-Bench Verified](https://llm-stats.com/benchmarks/swe-bench-verified)
- [EvalPlus HumanEval+ Leaderboard](https://evalplus.github.io/leaderboard.html)
- [Aider LLM Leaderboards](https://aider.chat/docs/leaderboards/)
- [LiveCodeBench](https://livecodebench.github.io/)
- [BigCodeBench](https://bigcode-bench.github.io/)

### Token & Cost Analysis
- [Claude Code Docs - Manage Costs](https://code.claude.com/docs/en/costs)
- [Faros AI - Claude Code Token Limits](https://www.faros.ai/blog/claude-code-token-limits)
- [Vantage - Cursor Pricing Explained](https://www.vantage.sh/blog/cursor-pricing-explained)
- [DEV Community - AI Coding Tools Cost Comparison](https://dev.to/stevengonsalvez/2025s-best-ai-coding-tools-real-cost-geeky-value-honest-comparison-4d63)
- [ngrok - Prompt Caching](https://ngrok.com/blog/prompt-caching/)

### Response Times & Latency
- [AIMultiple LLM Latency Benchmark](https://research.aimultiple.com/llm-latency-benchmark/)
- [GitHub Blog - Faster GitHub Copilot](https://github.blog/ai-and-ml/github-copilot/the-road-to-better-completions-building-a-faster-smarter-github-copilot-with-a-new-custom-model/)
- [Sourcegraph - Lifecycle of Code AI Completion](https://sourcegraph.com/blog/the-lifecycle-of-a-code-ai-completion)
- [Anthropic - Prompt Caching](https://www.anthropic.com/news/prompt-caching)

### Refactoring Capabilities
- [Aider Refactoring Leaderboard](https://aider.chat/docs/leaderboards/refactor.html)
- [Atlassian - Large-Scale Refactoring with AI](https://www.atlassian.com/blog/developer/how-to-effectively-utilise-ai-to-enhance-large-scale-refactoring)
- [Anthropic - Enabling Claude Code Autonomy](https://www.anthropic.com/news/enabling-claude-code-to-work-more-autonomously)
- [VS Code - GitHub Copilot Agent Mode](https://code.visualstudio.com/blogs/2025/02/24/introducing-copilot-agent-mode)
- [Agentic Refactoring Study (arXiv)](https://arxiv.org/abs/2511.04824)

### Benchmark Critiques
- [Runloop - SWE-bench Limitations](https://runloop.ai/blog/swe-bench-deep-dive-unmasking-the-limitations-of-a-popular-benchmark)
- [Toloka - Fixing SWE-bench](https://toloka.ai/blog/fixing-swe-bench-a-smarter-way-to-evaluate-coding-ai/)
