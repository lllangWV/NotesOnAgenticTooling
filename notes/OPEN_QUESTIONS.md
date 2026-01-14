# Open Questions - AI Coding Assistant Tools Research

Last updated: 2026-01-14

## Completed Questions (Iteration 6)

### Context Window Optimization
- [x] Detailed comparison of indexing vs on-demand context approaches
- [x] Best practices for CLAUDE.md and similar context files
- [x] How to optimize token usage for large codebases (>100k LOC)?

See [context-optimization.md](context-optimization.md) for comprehensive findings including:
- Cursor, Copilot, Sourcegraph Cody, Windsurf, Continue.dev, Refact.ai indexing approaches
- Claude Code and Aider on-demand approaches
- Embedding models comparison with dimensions and context limits
- CLAUDE.md anti-patterns and +10.87% accuracy improvements
- Token optimization with 50-90% cost savings via prompt caching

## Completed Questions (Iteration 4)

### Enterprise Adoption
- [x] What compliance certifications do tools have (SOC 2, HIPAA)?
- [x] How do enterprise deployment models differ?
- [x] What are best practices for team-wide adoption?
- [x] How do organizations handle API key management at scale?

See [enterprise-adoption.md](enterprise-adoption.md) for comprehensive findings.

## Completed Questions (Iteration 3)

### Performance & Benchmarks
- [x] How do tools compare on SWE-bench and similar benchmarks?
- [x] What is the actual token consumption for typical workflows?
- [x] How do response times compare across tools?
- [x] What is the success rate for complex multi-file refactors?

See [performance-benchmarks.md](performance-benchmarks.md) for comprehensive findings.

## Completed Questions (Iteration 2)

### Claude Code
- [x] What are Claude Code's unique features vs competitors?
- [x] What is the pricing model?
- [x] How do subagents work in Claude Code?
- [x] What are skills and slash commands?
- [x] How do hooks work?

### Cursor
- [x] What makes Cursor unique as an AI-first IDE?
- [x] What is the pricing model?
- [x] How does Cursor's agent mode work?
- [x] What context features does Cursor provide?

### GitHub Copilot
- [x] What are Copilot's current features (2025)?
- [x] What is the pricing model?
- [x] How does Copilot agent mode work?
- [x] What IDE integrations exist?

### Google Antigravity / Jules
- [x] What is Google Antigravity/Jules?
- [x] How does it differ from Gemini Code Assist?
- [x] What is the pricing model?
- [x] What unique features does it offer?

### OpenCode & Other CLI Tools
- [x] What is OpenCode and how does it work?
- [x] What other CLI-based coding assistants exist?
- [x] How do they compare to Claude Code?

### Cross-Cutting Themes
- [x] What common architectural patterns exist across tools?
- [x] What is MCP (Model Context Protocol) and who supports it?
- [x] How do different tools handle context management?
- [x] What are common agentic features (subagents, tool use, etc.)?
- [x] How do pricing models compare across tools?

### Advanced Topics
- [x] How do tools handle security and sandboxing?
- [x] What customization/extensibility options exist?
- [x] How do tools integrate with development workflows (git, CI/CD)?

## Priority 1: Integration Questions

### MCP Ecosystem
- [ ] What are the most valuable MCP servers for coding workflows?
- [ ] How to build custom MCP servers for proprietary systems?
- [ ] What security considerations exist for MCP server deployment?
- [ ] How does MCP interact with other protocols (A2A, ACP)?

### Workflow Integration
- [ ] Best practices for CI/CD integration with AI agents
- [ ] How to integrate AI coding assistants with code review workflows?
- [ ] What are effective multi-agent coordination patterns?
- [ ] How to handle AI-generated code in regulated industries?

## Priority 2: Future Trends

### Emerging Capabilities
- [ ] What's the roadmap for multi-modal context (images, diagrams)?
- [ ] How will tools evolve to support larger context windows?
- [ ] What new agent communication protocols are emerging?
- [ ] How will local/on-device models affect the landscape?

### Market Evolution
- [ ] Which tools are gaining/losing market share?
- [ ] What consolidation is happening in the market?
- [ ] How are pricing models evolving?
- [ ] What features are becoming commoditized vs differentiated?

## Research Gaps Identified

1. **Long-term reliability data**: Limited information on uptime and reliability across tools
2. **Real-world cost analysis**: Need more case studies on actual monthly costs
3. **Enterprise case studies**: Detailed implementation stories from large organizations
4. **Offline capabilities**: Varying documentation on fully offline operation
5. **Windows-specific support**: Limited documentation for Windows users
6. **Multi-language support**: How tools perform across different programming languages

## Notes for Future Research

- Consider setting up benchmarking environment to test tools directly
- Reach out to enterprise users for case study interviews
- Monitor MCP specification updates for breaking changes
- Track new tool releases and major version updates
