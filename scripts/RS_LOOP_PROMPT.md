# Research Loop

The goal is to perform research on the following topic

The research topic is to investigate coding assistant tools like claude code, cursor, google antigravity, github copilot, opencode. I want to research what make these tools unique. What are their common features, for instance cli based tools have subagents, skills, slash commands, hooks, etc. What are common themes amongst the tools. What are their pricing plans. 


Do not be scared to go into research about why features are so important and explain them in detail

## Phase 1: Gather Context

1a. Study the notes directory:
    - Read `notes/README.md`
    - Scan `notes/` directory for existing spec files and use sub agents to study them
    - Identify what's already documented vs gaps

## Phase 2: 

1b. Look at `notes/OPEN_QUESTIONS.md`
   - Grab the highest priority open question. 

## Phase 2: Web Research

Launch parallel **web-search-researcher** agents to gather information about the open question

## Phase 3: Synthesize into notes

Wait for all agents to complete, then create/update spec files.

### 3a. Determine file structure
- Single topic → `notes/<topic-slug>.md`
- Complex topic → multiple files: `notes/<topic>/<subtopic>.md`

### 3b. Write spec file(s)

Use this format for each spec file:

```markdown
# <Topic> Specification

Last updated: [DATE] by RS Loop


## Overview
Brief description of the concept


{Fill in with additional information on the topic. Can you whatever layout to best explain the concept/topic.}


## Open Questions
- [ ] Items needing further research
- [ ] Unclear aspects to investigate


Sources:
- [Source 1 URL]
- [Source 2 URL]
- ...
```

### 3c. Guidelines for cleanroom notes
- **Cite sources**: Always include documentation URLs
- **Be precise**: Use exact terminology

## Phase 4: Update notes/README.md

Update (or create) `notes/README.md` as the index:

```markdown
# Project Specifications

Last updated: [DATE]

## Overview
[Concise project summary - what is being specified]

## Specifications

| Spec | Description |
|------|-------------|
| [topic-1.md](topic-1.md) | Brief description |
| [topic-2.md](topic-2.md) | Brief description |
| ... | ... |

## Changes:

### Iteration: N
- Added new spec {spec_name }: {brief reason}
- Updates spec {spec_name}: {brief reason}

{Continue the change iterations}
```

## Phase 5: Wrapping up

If you finish researching and writing notes:
1. Create notes directory if needed:
   ```bash
   mkdir -p notes
   ```
2. Run `/ralph_commit` to commit the notes
3. Output summary:
   - What spec files were created/updated
   - Key findings from research
   - Any open questions for follow-up

## Important Guidelines

1. **Cite everything**: Every claim should trace back to a source URL.

2. **Incremental refinement**: Each run should improve existing notes, not overwrite them blindly.

3. **Flag uncertainty**: Use "Open Questions" section for anything unclear.

4. ALWAYS KEEP @notes/OPEN_QUESTION.md up to do date with your learnings using a subagent. Especially after wrapping up/finishing your turn.

5. ALWAYS KEEP @notes/README.md up to do date with your learnings using a subagent. Especially after wrapping up/finishing your turn.

6. If you find inconsistentcies in the notes/* then use the oracle and then update the notes. 
