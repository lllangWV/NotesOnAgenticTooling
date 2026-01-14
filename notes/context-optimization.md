# Context Window Optimization Specification

Last updated: 2026-01-14 by RS Loop (Iteration 6)

## Overview

This specification covers context window optimization strategies for AI coding assistants, including indexing vs on-demand context approaches, CLAUDE.md and similar context files best practices, and token optimization techniques for large codebases (>100k LOC). Effective context management is critical for AI coding tools to provide accurate, relevant assistance while minimizing costs.

## Key Findings

**Context quality matters more than context size.** Research consistently shows that smaller, well-curated context windows outperform larger, unfocused ones. Models' performance can degrade by 24.2% when poorly configured with irrelevant tokens.

**The industry is converging on hybrid approaches** that combine:
1. AST-based structural indexing for precise code relationships
2. Embedding-based semantic search for conceptual matching
3. Keyword/BM25 search for exact term matching
4. Two-stage retrieval with reranking for accuracy
5. Incremental indexing for freshness without full rebuilds

---

## 1. Indexing vs On-Demand Context Approaches

### 1.1 Pre-Indexing Approaches

Pre-indexing builds embeddings and indexes before queries, enabling fast semantic retrieval.

#### Cursor - Embedding-Based Indexing

**Architecture:**
- **AST-based chunking**: Uses tree-sitter to parse code into Abstract Syntax Trees, breaking code into semantic units (functions, classes, logical blocks)
- **Chunk size**: "A few hundred tokens each" with semantic boundaries preserved
- **Embedding model**: OpenAI embedding API or custom models; at indexing time uses dedicated encoder emphasizing comments and docstrings
- **Storage**: Turbopuffer vector database with AWS S3 for primary storage
- **Incremental updates**: Merkle tree structure checks for hash mismatches every 10 minutes, uploading only modified files
- **Two-stage retrieval**: Vector search for candidates, then AI model re-ranking for relevance

**Performance:**
- Fast retrieval once indexed (up to 272k token context)
- Semantic search available at 80% indexing completion
- Initial indexing: ~60 seconds for large repos
- Privacy: Filenames obfuscated, code chunks encrypted, source code not stored permanently (only in memory during indexing)
- Indexes deleted after 6 weeks of inactivity

#### GitHub Copilot - Hybrid Remote/Local Indexing

**Three indexing tiers:**
1. **Remote Index**: Built from default branch, handles large codebases (GitHub.com, GitHub Enterprise Cloud, Azure DevOps)
2. **Local Index**: Advanced semantic index stored locally, limited to 2,500 indexable files
3. **Basic Index**: Fallback for projects >2,500 files without remote index

**New Embedding Model (2025):**
- Custom-trained model specifically for code and documentation
- **37.6% lift** in retrieval quality (scores from 0.362 to 0.498)
- ~2x faster throughput
- **8x smaller index size**
- Training methodology: Contrastive learning with InfoNCE loss and Matryoshka Representation Learning
- Training data: Python (36.7%), Java (19%), C++ (13.8%), JS/TS (8.9%), C# (4.6%), Other (17%)
- Uses "hard negatives" (code that looks correct but isn't) to improve discrimination

**Technical Details:**
- Updates: Index refreshed "within seconds" when starting new conversations
- Initial indexing: Up to 60 seconds for large repos
- Shared indexes across organization users
- Scales to billions of vectors with low latency
- Automatic history compression at 95% token limit

#### Windsurf (Cascade) - RAG with Deep Context

- **Cascade Technology**: Proprietary engine that indexes codebase into a relational graph, tracking dependencies and logic flows across files
- **M-Query Techniques**: Uses LLMs with retrieval-augmented generation for on-the-fly context retrieval
- **Indexing Engine**: Pre-scans entire repository to create semantic index, enabling retrieval from anywhere in codebase
- **Local & Remote**: Supports both local indexing (immediate upon opening) and remote indexing (on Codeium servers for teams)
- ~200,000 token context window through RAG-based selection
- **Fast Context Subagent**: Operates "up to 20x faster" using specialized SWE-grep models
- Automatic context discovery without manual file tagging (unlike tools limited to recently-viewed files)

#### Continue.dev - Transitioning to Hybrid

**Default Configuration:**
- **Embedding Model**: all-MiniLM-L6-v2 (384 dimensions, 22M parameters, 5x faster than larger models)
- **Storage**: Local in `~/.continue/index` with SQLite metadata database
- **Chunking**: Tree-sitter AST parsing to understand class/function structure

**Retrieval Pipeline:**
- nRetrieve=25 initial results, nFinal=5 after reranking (default)
- LLM-powered reranking enabled by default (useReranking=true)

**Recent Evolution (2024-2025):**
- @Codebase provider deprecated in favor of Agent mode with built-in file exploration tools and MCP servers
- Now combines embeddings-based retrieval with keyword search and ripgrep for fast text search

#### Refact.ai - Dual Indexing System

**Architecture:**
- **AST Index**: Uses tree-sitter to parse source files, creates in-memory mapping for fast definition lookup and reference finding
- **Vector Database**: Converts text segments (up to 1024 tokens) into 768-dimensional vectors using AI models
- **Implementation**: Written in Rust within refact-lsp

**Chunking Strategy:**
- Text files: Uses empty lines as boundary hints
- Structured code: "Skeletonization" - shortens function bodies while preserving class structure

**Integration:**
- Aggregates results from both AST and VecDB sources
- Tracks "usefulness" scores per line
- Respects token budgets
- Best results: Enable both AST and VecDB together

### 1.2 On-Demand Approaches

On-demand retrieval fetches context dynamically at query time without pre-indexing.

#### Claude Code - Grep/Glob-Based Just-in-Time Retrieval

**Philosophy:** "Just in time" approach maintains lightweight identifiers (file paths, queries) and retrieves dynamically at runtime.

**Implementation:**
- Uses standard grep/glob tools for pattern matching
- No pre-indexing or embeddings required
- CLAUDE.md files loaded upfront; grep/glob tools enable runtime exploration

**Performance:**
- **5.5x fewer tokens** than Cursor for same tasks
- No stale indexing problems
- Predictable, exact matches

**Trade-offs:**
- Can be slower due to sequential searches
- May retrieve irrelevant context without semantic understanding
- Best practice: "Grep for symbol usage, list candidates, open only 3-5 most relevant files"

#### Aider - Graph-Based Repository Map

**Architecture:**
- Concise map of entire git repository with important classes/functions and signatures
- Uses tree-sitter for AST extraction
- PageRank-based ranking identifies high-relevance files

**Token Efficiency:**
- **4.3-6.5% token utilization** while preserving architectural context
- Default 1k tokens for repo-map (configurable via `--map-tokens`)
- Lowest token consumption among tested agents

### 1.3 Hybrid Approaches

#### Sourcegraph Cody - Multi-Strategy Context Engine

**Multi-Stage Retrieval:**
1. **Retrieval stage**: Cast wide net across multiple sources
   - Keyword search (Zoekt) - fast, exact matches
   - Embedding-based - semantic similarity
   - Graph-based - dependency relationships
   - Local context - editor state, recent history
2. **Ranking stage**: Transformer models filter to fit token budget

**Scale:** Handles 300,000+ repositories and monorepos exceeding 90GB.

### 1.4 Comparison Matrix

| Approach | Tools | Token Efficiency | Setup Cost | Accuracy |
|----------|-------|------------------|------------|----------|
| Pre-Indexing | Cursor, Copilot, Windsurf | Medium | High | High (semantic) |
| On-Demand | Claude Code | High (5.5x better) | Low | Medium (exact match) |
| Graph-Based | Aider | Highest (4.3-6.5%) | Low | High (structural) |
| Hybrid | Sourcegraph Cody | Medium-High | High | Highest |

### 1.5 RAG (Retrieval Augmented Generation) for Code

**Key Distinction from Text RAG:**
- Code has inherent structure (AST) that text lacks
- Semantic boundaries (functions, classes) must be preserved
- Solution: Generate natural language descriptions for code chunks

**Embedding Models Performance (2025-2026):**

| Model | Dimensions | Parameters | Context | Type | Notes |
|-------|-----------|------------|---------|------|-------|
| Voyage Code-3 | 1536 | N/A | 16K tokens | Commercial | Leading code-specific, +14.52% vs OpenAI ada |
| Qwen3 Embedding | N/A | N/A | N/A | Open | MTEB leaderboard #1 (70.58 score, June 2025) |
| GitHub Copilot 2025 | N/A | N/A | N/A | Proprietary | +37.6% retrieval quality, 8x smaller index |
| OpenAI text-embedding-3-small | 1536 | N/A | 8K | Commercial | Excellent despite being general-purpose |
| all-MiniLM-L6-v2 | 384 | 22M | 256 tokens | Open | Fast, 84-85% STS-B, 5x faster than larger |
| Refact.ai | 768 | N/A | 1024 tokens | Open | Code-specific |
| GraphCodeBERT | 768 | 125M | 512 tokens | Open | Better than CodeBERT for code tasks |

**Chunking Best Practices:**
- **AST-Based Chunking (cAST)**: Parses code into AST, applies recursive split-then-merge on syntax trees
  - Carnegie Mellon Research (2025): +4.3 points Recall@5, +3.3 points Precision on RepoEval
  - SWE-bench: +2.67 points Pass@1 with Claude-3.7-Sonnet
- **Chunk Size Metric**: Use non-whitespace character count (not lines) for consistent density across languages
- **Optimal Size**: 256-512 tokens (roughly 100-200 words) with 20-30% overlap between chunks
- Preserve function/class boundaries - structure-aware chunking reduces noise
- Tree-sitter: Language-agnostic AST parsing eliminating language-specific heuristics (36x faster than traditional parsers)
- Precision improvements correlate most strongly with generation quality

**Retrieval Algorithms:**

| Algorithm | Type | Best For | Performance |
|-----------|------|----------|-------------|
| Cosine Similarity | Dense | Semantic matching | Pre-computed embeddings |
| BM25 | Sparse | Exact matches, rare terms | Better for specific queries |
| Hybrid (BM25 + Embeddings) | Combined | General code search | Best overall results |
| Cross-encoder Reranking | Two-stage | High precision | +28% NDCG@10, +1.5s latency |

**Two-Stage Retrieval Pipeline:**
1. Pre-ranking: BM25/TF-IDF for broad candidate retrieval (~50 documents)
2. Re-ranking: Cross-encoder or LLM for precision (~10 final results)
- Cross-encoders provide +28% NDCG@10 improvement
- 0.6B reranker can match 8B models with lower latency

---

## 2. CLAUDE.md and Context File Best Practices

### 2.1 CLAUDE.md for Claude Code

**Official Structure:**
- No required format - use standard Markdown
- Automatically read when Claude Code starts in a directory
- Supports hierarchical structure (parent directories, subdirectories)

**File Placement Options:**
- `CLAUDE.md` - Check into git for team sharing
- `CLAUDE.local.md` - Add to .gitignore for personal preferences
- `~/.claude/CLAUDE.md` - Global settings for all projects

**What to Include:**
- Common bash commands with descriptions
- Core files and utility functions
- Code style guidelines specific to project
- Testing instructions
- Repository etiquette (branch naming, commit formats)
- Developer environment setup

**Key Best Practices:**
- **Length**: Keep under 300 lines (ideally under 60 lines - HumanLayer's root file is under 60 lines)
- **Instruction Limit**: Frontier LLMs can follow ~150-200 instructions reliably; Claude Code's system prompt already contains ~50 instructions
- **WHY, WHAT, HOW structure**:
  - WHAT: Tech stack, project architecture, codebase organization
  - WHY: Project purpose, functional goals of components
  - HOW: Development workflows, testing, build commands
- **Progressive disclosure**: Store task-specific instructions in separate markdown files within `agent_docs/` directory, reference from CLAUDE.md
- **Iterate based on performance**: Treat CLAUDE.md like a frequently-used prompt that needs refinement
- **Use `#` key during sessions**: Auto-incorporate updates into relevant CLAUDE.md files
- **Never auto-generate**: Manually craft carefully - highest-leverage configuration point

**Performance Impact:**
- System prompt optimization yielded **5%+ performance gains** on SWE Bench
- Repository-specific CLAUDE.md files produced **+10.87% accuracy improvements** when specialized for specific codebases

**Anti-Patterns to Avoid:**
1. **Including Code Snippets**: They become outdated quickly - use file:line references instead
2. **Stuffing Everything Into One File**: Break out specific processes into referenced files
3. **Context Overload**: Dumping large llms.txt files crowds context window, leads to poor performance
4. **Complex Slash Commands**: Long list of complex custom slash commands creates anti-pattern
5. **No Iteration**: Adding content without testing effectiveness
6. **Using LLMs as Linters**: Don't include code style guidelines - use deterministic tools (Biome) and hooks

**Hierarchical Loading:**
Claude Code recurses up from the current working directory, reading any CLAUDE.md or CLAUDE.local.md files it finds. This is useful for monorepos where you might have `foo/CLAUDE.md` and `foo/bar/CLAUDE.md`.

### 2.2 Cursor's .cursorrules

**Current State:**
- `.cursorrules` file is **legacy** but still supported
- **New system**: Project Rules stored in `.cursor/rules` directory

**Project Rule Structure:**
```markdown
---
description: "Rule purpose"
alwaysApply: false
globs: ["**/*.ts", "**/*.tsx"]
---
Content here
```

**Rule Application Types:**
- **Always Apply**: Every chat session
- **Apply Intelligently**: When Agent determines relevance
- **Apply to Specific Files**: Pattern matching via globs
- **Apply Manually**: Via @-mention in chat

**Best Practices:**
- Keep rules under 500 lines
- Focus on specific, actionable guidance
- Include concrete examples and file references
- Divide large rules into composable components

### 2.3 GitHub Copilot Custom Instructions

**File Types:**
1. `.github/copilot-instructions.md` - Repository-wide instructions
2. `.github/instructions/NAME.instructions.md` - Path-specific instructions
3. `AGENTS.md` - Emerging standard, nearest file takes precedence

**Best Practices:**
- Keep it brief: No longer than 2 pages
- Include: High-level repository summary, languages, frameworks, build instructions
- Verification: Check References list in Copilot Chat responses

### 2.4 Aider Configuration

**Configuration System:**
- `.aider.conf.yml` - YAML configuration file
- `.aiderignore` - Uses `.gitignore` syntax to exclude files
- `.env` - Environment variables for API keys

**Context Management:**
- `--subtree-only` flag to limit scope to current subdirectory
- Repository map automatically generated
- Strategic file addition: Be thoughtful about which files to add

### 2.5 AGENTS.md - The Emerging Standard

An emerging cross-tool standard for providing context to AI coding assistants.

**Hierarchical Levels:**
1. **User-level**: `~/.gitlab/duo/AGENTS.md` (all projects)
2. **Workspace-level**: Project root (single project)
3. **Subdirectory-level**: Monorepo folders (specific components)

**Example:** OpenAI repository uses 88 nested AGENTS.md files.

### 2.6 Tool Comparison Matrix

| Feature | Claude Code | Cursor | GitHub Copilot | Aider |
|---------|-------------|--------|----------------|-------|
| Main File | CLAUDE.md | .cursorrules (legacy) | copilot-instructions.md | .aider.conf.yml |
| Local Override | CLAUDE.local.md | User Rules | Personal settings | Home dir config |
| Subdirectory Support | Yes (hierarchical) | Yes (via globs) | Yes (via globs) | Yes (subtree-only) |
| AGENTS.md Support | No | Yes | Yes | No |
| Recommended Size | <300 lines | <500 lines | <2 pages | N/A |

### 2.7 Common Mistakes to Avoid

1. **Context Bloat**: Embedding entire files via @ mentions wastes tokens
2. **Negative-Only Constraints**: "Never use X" without alternatives gets agents stuck
3. **Generic Style Guides**: Use linters/formatters instead
4. **No Iteration**: Add incrementally, measure impact, refine
5. **MCP Overload**: Enabling 20+ MCP servers (>20k tokens overhead)

---

## 3. Token Optimization for Large Codebases

### 3.1 Token Consumption Patterns

**Context Window Sizes (2025-2026):**

| Model/Tool | Context Window | Capacity |
|------------|----------------|----------|
| Claude Sonnet 4 / 4.5 | 1M tokens | 500+ files |
| Claude 3.5/3.7 Sonnet, Haiku 3.5 | 200K tokens | 120-150 files |
| GPT-4.1 | 1M tokens | 500+ files |
| GPT-4o / GPT-4o mini | 128K tokens | 80-100 files |
| GPT-5 | 400K input / 128K output | 200+ files |
| Gemini 2.5 Pro / Flash | 1M tokens | 500+ files |
| Gemini 3 Pro | 2M tokens | 1,000+ files |
| Meta Llama 4 Maverick | 1M tokens | 500+ files |
| Codex | 192K tokens | 120+ files |

**Note**: Claude Sonnet 4.5 and Haiku 4.5 include "Context Awareness" feature - they track remaining token budget throughout conversations.

**Token-to-Content Conversions:**
- English text: ~1 token per 4 characters
- Source code: ~1 token per 4-5 characters
- Typical code line: 10-15 tokens
- Average function: 50-200 tokens
- Average file: 500-2,000 tokens

**Common Inefficiencies:**
- File reading operations: Agents can spend 60,000 tokens reading files
- Context pollution: Irrelevant open files consume context
- Redundant searches: Searching from scratch in every conversation

### 3.2 Context Window Management Strategies

#### Automatic Summarization

**Claude Code Compaction:**
- Triggers at ~95% context capacity
- Summarizes conversation to reduce context window size
- Sessions stopping at 75% produce higher-quality code

**Structured Summarization (Factory.ai):**
- Explicit sections for: session intent, file modifications, decisions, next steps
- 98.6% compression ratio while maintaining context quality
- Scored highest in quality benchmarks (3.70/5.0)

#### Context Pruning Strategies

1. **Pruning + Summarization**: Compress to semantically-rich summaries before dropping
2. **Structured Note-Taking**: Write notes to external memory, retrieve as needed
3. **Just-in-Time Retrieval**: Maintain lightweight identifiers, load dynamically

### 3.3 Large Codebase Strategies (>100k LOC)

**Architectural Intelligence Over Context Expansion:**

1. **Context Engines**: Analyze dependency relationships, understand service boundaries
2. **Intelligent Context Scoping**: Scope to relevant subsystems
3. **Repository Overviews + Semantic Search**: Targeted file operations based on relevance

**Token Efficiency Metrics:**

| Approach | Token Usage | Key Advantage |
|----------|-------------|---------------|
| Aider repo-map | 8.5-13k tokens | 4.3-6.5% context utilization |
| Vector embeddings | 22.8k avg | 54% reduction vs grep |
| Full-text search | 47k+ tokens | Exhaustive but expensive |

#### Monorepo-Specific Strategies

1. **MCP Servers**: Nx builds a "map" of codebase via MCP servers
2. **Nested Configuration Files**: OpenAI uses 88 nested AGENTS.md files
3. **Scaffolding and Pattern Replication**: Provide comprehensive examples

**Key Finding:** "Monorepos consolidate all code in one place, fundamentally improving contextual access for LLMs."

### 3.4 Tool-Specific Optimization

#### Claude Code

**Optimization Strategies:**
1. Explicit file control via CLAUDE.md (specify readable files, forbidden directories)
2. Disable unused MCP servers (can save 5-15k tokens)
3. Batch related changes together
4. Use subagents for research tasks (preserves main context)

**Subagent Benefits:**
- Operate in their own context window
- Report back condensed findings
- Can save 10-50k tokens per research task

#### Cursor

**@codebase Limitations:**
"Using @codebase does not ensure that Cursor will include all relevant code in the context"

**Better Approach:**
- Use `@filename` for specific files when you know what you need
- Keep files under 500 lines
- Document in first 100 lines
- Restart conversations frequently (save 75% of tokens)

#### Aider

**--map-tokens Configuration:**
- Default: 1,000 tokens
- Configurable: `aider --map-tokens 2048`
- Dynamic adjustment when no files added to chat

### 3.5 Cost Optimization Strategies

#### Prompt Caching (Most Effective)

**Impact:** Up to 90% discount on cached tokens (50-90% savings overall)

**How It Works:**
- Model providers (OpenAI, Anthropic, Google) store input prefixes and reuse across requests
- Cached tokens cost 90% less than fresh tokens
- Reduces time-to-first-token by 50-80%
- Particularly valuable for agents and multi-step workflows reusing context across thousands of requests

**Best Practices:**
- Use standardized templates across similar tasks
- Batch similar requests consecutively
- Set appropriate TTLs (24-48 hours for stable content)
- System message caching for repeated contexts

**Semantic Caching:**
- Goes beyond exact prefix matches
- Identifies conceptually similar queries and serves cached responses
- Reduces API calls by 30-70% for certain workloads

**Real-World Results:**
- $0.15 → $0.02 per query (87% reduction)
- One YC startup reduced monthly AI coding bill from $12,000 to under $3,000

#### Model Routing

**Strategy:** Route queries to appropriate model tiers

| Task Type | Recommended Model | Cost (per 1M tokens) |
|-----------|------------------|---------------------|
| Autocompletion | GPT-3.5 / Haiku | $1-2 |
| Quick fixes | Sonnet 4 | $3-18 |
| Complex refactoring | Opus 4 / o1 | $15-90 |

#### Combined Strategies

**Maximum Impact:** 50-80% cost reduction

1. Prompt caching for static content
2. Batch processing for background tasks (50% discount)
3. Semantic caching for similar queries (30-70% reduction)
4. Model routing based on complexity (40% reduction)

### 3.6 File Organization Best Practices

**Configuration Files:**
```
/repo-root/
├── AGENTS.md (project-wide standards)
├── frontend/
│   └── AGENTS.md (React/TypeScript specific)
├── backend/
│   └── AGENTS.md (Python/FastAPI specific)
```

**File Size Guidelines:**
- Files: 200-500 lines maximum
- Functions: 20-50 lines typical
- Document in first 100 lines for AI indexing

**Gitignore Patterns for AI Tools:**
```gitignore
# Performance optimization
node_modules/
vendor/
dist/
build/

# Security
.env*
secrets/
*.key

# Large files
*.csv
*.db
logs/
```

---

## 4. Performance Benchmarks

### 4.1 Retrieval Accuracy

**Key Findings:**
- BM25 often outperforms complex embeddings for code generation
- Agentic search consistently outperforms RAG approaches
- Similar code retrieval can introduce noise, degrading results by up to 15%

### 4.2 Token Efficiency Comparison

| Tool | Tokens for Same Task | Efficiency |
|------|---------------------|------------|
| Aider | Baseline | Most efficient (4.3-6.5%) |
| Claude Code | 5.5x fewer than Cursor | High |
| Cursor | Baseline | Medium |
| Vector RAG | 40% fewer than grep-only | Medium-High |

### 4.3 Real-World Benchmark Results (2026)

- GitHub Copilot: 55% faster task completion
- Cursor: 39% increase in merged PRs
- Claude Code: 5.5x token efficiency advantage

**Quality Concerns:**
- METR trial: AI tools increased task completion time by 19% among experienced developers
- GitClear analysis: 8-fold increase in code duplication during 2024

---

## 5. Recommendations by Use Case

### For Production at Scale
- **Sourcegraph Cody** or **GitHub Copilot Enterprise**
- Multi-strategy retrieval with proven scale

### For Cost-Sensitive Deployments
- **Cursor** with Turbopuffer backend
- **Aider** with repository map

### For Development & Prototyping
- **Claude Code** for simplicity
- No infrastructure overhead

### For Monorepos & Complex Projects
- **Windsurf/Cascade** with 200k token context
- **Cursor Composer** for multi-file edits

### For Token-Efficient Operations
- **Aider** (4.3-6.5% utilization)
- **Claude Code** (5.5x fewer tokens)

---

## Open Questions

- [ ] Optimal balance between pre-indexing and on-demand retrieval by project type
- [ ] Best embedding models for specific programming languages
- [ ] Standardized metrics for measuring context retrieval quality
- [ ] Long-term impact of aggressive context compression on code quality
- [ ] Privacy implications of different indexing approaches in enterprise settings

---

## Sources

### Indexing & Retrieval
- [How Cursor Indexes Codebases Fast - Engineer's Codex](https://read.engineerscodex.com/p/how-cursor-indexes-codebases-fast)
- [Cursor – Codebase Indexing](https://docs.cursor.com/context/codebase-indexing)
- [GitHub Copilot gets smarter at finding your code: Inside our new embedding model](https://github.blog/news-insights/product-news/copilot-new-embedding-model-vs-code/)
- [Indexing repositories for GitHub Copilot Chat](https://docs.github.com/copilot/concepts/indexing-repositories-for-copilot-chat)
- [Repository map - Aider](https://aider.chat/docs/repomap.html)
- [How Cody provides remote repository awareness - Sourcegraph](https://sourcegraph.com/blog/how-cody-provides-remote-repository-context)
- [Context Awareness Overview - Windsurf Docs](https://docs.windsurf.com/context-awareness/overview)
- [Codebase Retrieval - Continue.dev](https://docs.continue.dev/features/codebase-embeddings)
- [What are the accuracy limits of codebase retrieval? - Continue Blog](https://blog.continue.dev/accuracy-limits-of-codebase-retrieval/)
- [RAG in Refact.ai: Technical Details](https://refact.ai/blog/2024/rag-in-refact-ai-technical-details/)
- [Building RAG on codebases - LanceDB](https://lancedb.com/blog/building-rag-on-codebases-part-1/)
- [Introducing Contextual Retrieval - Anthropic](https://www.anthropic.com/news/contextual-retrieval)

### Context Files
- [Claude Code: Best practices for agentic coding - Anthropic](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Writing a good CLAUDE.md - HumanLayer Blog](https://www.humanlayer.dev/blog/writing-a-good-claude-md)
- [CLAUDE.md: Best Practices Learned from Optimizing Claude Code - Arize](https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/)
- [How the Creator of Claude Code Uses Claude Code](https://blog.sivaramp.com/blog/how-creator-of-claude-code-uses-claude-code/)
- [Rules - Cursor Docs](https://cursor.com/docs/context/rules)
- [Cursor AI Complete Guide 2025](https://medium.com/@hilalkara.dev/cursor-ai-complete-guide-2025-real-experiences-pro-tips-mcps-rules-context-engineering-6de1a776a8af)
- [awesome-cursorrules - GitHub](https://github.com/PatrickJS/awesome-cursorrules)
- [Adding custom instructions for GitHub Copilot](https://docs.github.com/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)
- [5 tips for writing better custom instructions for Copilot - GitHub Blog](https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/)
- [AGENTS.md customization files - GitLab Docs](https://docs.gitlab.com/user/gitlab_duo/customize_duo/agents_md/)
- [Instruction Files for AI Coding Assistants - Overview](https://aruniyer.github.io/blog/agents-md-instruction-files.html)
- [YAML config file - Aider](https://aider.chat/docs/config/aider_conf.html)
- [Specifying coding conventions - Aider](https://aider.chat/docs/usage/conventions.html)

### Token Optimization
- [Effective context engineering for AI agents - Anthropic](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Evaluating Context Compression for AI Agents - Factory.ai](https://factory.ai/news/evaluating-compression)
- [The Context Window Problem: Scaling Agents Beyond Token Limits - Factory.ai](https://factory.ai/news/context-window-problem)
- [AI Coding Assistants for Large Codebases - Augment Code](https://www.augmentcode.com/tools/ai-coding-assistants-for-large-codebases-a-complete-guide)
- [How to Reduce GPT API Cost: 8 Proven Strategies](https://www.cursor-ide.com/blog/reduce-gpt-5-2-api-cost)
- [Prompt Caching Guide 2025 - PromptBuilder](https://promptbuilder.cc/blog/prompt-caching-token-economics-2025)
- [LLM Cost Optimization: Complete Guide - Koombea](https://ai.koombea.com/blog/llm-cost-optimization)
- [Context Rot: How Increasing Input Tokens Impacts LLM Performance - Chroma Research](https://research.trychroma.com/context-rot)

### Research Papers
- [An Empirical Study of Retrieval-Augmented Code Generation - ACM](https://dl.acm.org/doi/10.1145/3717061)
- [cAST: Enhancing Code Retrieval-Augmented Generation with Structural Chunking via AST - arXiv](https://arxiv.org/html/2506.15655v1)
- [Meta-RAG on Large Codebases Using Code Summarization](https://arxiv.org/html/2508.02611v1)
- [An Exploratory Study of Code Retrieval Techniques](https://www.preprints.org/manuscript/202510.0924)
- [CoIR: A Comprehensive Benchmark for Code Information Retrieval Models](https://arxiv.org/html/2407.02883v1)
- [An Empirical Study of Developer-Provided Context](https://arxiv.org/html/2512.18925v1)

### Embedding Models
- [voyage-code-2: Elevate Your Code Retrieval - Voyage AI](https://blog.voyageai.com/2024/01/23/voyage-code-2-elevate-your-code-retrieval/)
- [voyage-code-3: more accurate code retrieval - Voyage AI](https://blog.voyageai.com/2024/12/04/voyage-code-3/)
- [Qwen3 Embedding: Advancing Text Embedding and Reranking](https://qwenlm.github.io/blog/qwen3-embedding/)
- [all-MiniLM-L6-v2 - Hugging Face](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)

### Monorepo & Enterprise
- [Monorepos & AI - Monorepo Tools](https://monorepo.tools/ai)
- [Nx and AI - Why They Work so Well Together](https://nx.dev/blog/nx-and-ai-why-they-work-together)
- [Integrate Nx with your Coding Assistant](https://nx.dev/docs/getting-started/ai-setup)

### Tools & Resources
- [awesome-claude-md - GitHub](https://github.com/josix/awesome-claude-md)
- [awesome-claude-code - GitHub](https://github.com/hesreallyhim/awesome-claude-code)
- [claude-code-showcase - GitHub](https://github.com/ChrisWiles/claude-code-showcase)
- [LSP-AI GitHub Repository](https://github.com/SilasMarvin/lsp-ai)
- [Code Pathfinder MCP Server](https://codepathfinder.dev/mcp)
- [Claude Context MCP - GitHub](https://github.com/zilliztech/claude-context)
