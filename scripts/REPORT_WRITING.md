# Report Writing

The goal is to write a report to convince a company to adopt claude code and cursor as tool. This should be a comprehensive report about coding assistant tools as a whole and give recommendations for payign for these tool. My thesis is we want a ide-base coding assistant tool and most importantly claude-code either the teams version or 3 acounts that we account share. This is scoped for a team of 10 developers 

## Phase 1: Grabing the todo task


1a. Study the reports directory:
    - Read `reports/README.md`
    - Scan `reports/` directory for exisiting sections and use sub agents to study them

1b. Study the notes directory:
    - Read `notes/README.md`
    - Scan `notes/` directory for existing spec files and use sub agents to study them


## Phase 2: Grabing the todo task

1b. Look at `reports/TODO.md`
   - Grab the highest priority todo and implement it


## Phase 4: Update reports/README.md

Update (or create) `reports/README.md` as the index:

```markdown
# Report

Last updated: [DATE]

## Overview
[Concise Report summary]

## Specifications

| Spec | Description |
|------|-------------|
| [section-1.md](section-1.md) | Brief description |
| [section-2.md](section-2.md) | Brief description |
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

2. **Incremental refinement**: Each run should improve existing sections, not overwrite them blindly.

4. ALWAYS KEEP @reports/TODO.md up to do date with your learnings using a subagent. Especially after wrapping up/finishing your turn.

6. If you find inconsistentcies in the reports/* then use the oracle and then update the notes. 

99999999999999999999999. DO NOT SEARCH IN THE `data` directory. THIS IS OFF LIMITS.

9999999999999999999999999. OCCASIONALLY move completed open questions TODO.md to a file called FINISHED_TODO.md to make room for new question.