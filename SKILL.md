---
name: session-handoff
description: Use when ending a Claude Code session and wanting to continue in a new one — reads the conversation and produces a structured, paste-ready summary capturing what was done, decisions made, current state, and next steps.
---

# Session Handoff

## Overview

Reads the current session and produces a paste-ready summary block. Start your next session by pasting it — the new agent picks up with full context.

## When to Use

- You're ending a session and plan to continue later
- Your context window is getting full and you need a fresh start
- You want a written record of a session's decisions and outcomes

## Recipe

When invoked, read the full conversation and fill in the template below. Be terse — the output is scaffolding for a future agent, not a narrative for a human reader.

```
## Session Handoff — [YYYY-MM-DD]

### What we worked on
- [task or feature, one line each]

### Decisions made
- [decision] — [one-line rationale]

### Current state
- Done: [completed items]
- In progress: [started but unfinished]
- Blocked / known issues: [anything broken or stuck]

### Key files
- [path] — [why it matters for continuing]

### Next steps
1. [first thing to do next session]
2. [second, etc.]

### Carry-forward context
[Non-obvious constraints, workarounds, env quirks, or anything that burned time this session that the next agent must know.]
```

## Rules

- **Fill every section.** Write "none" rather than omitting a section — a blank section is ambiguous.
- **Key files:** only files directly relevant to continuing the work. Skip files you only read for reference.
- **Decisions:** only non-obvious choices. Skip anything self-evident from the code.
- **Carry-forward context:** this is the most important section. Capture the stuff that isn't in the code — environment assumptions, workarounds, stakeholder constraints, gotchas that burned time.

## Output

Print the filled template as a fenced markdown block so it's easy to copy. Nothing else — no preamble, no commentary.
