# session-handoff

A Claude Code skill that reads your current session and produces a structured, paste-ready summary — so you can start a new session right where you left off.

Works in Claude Code, Codex, Gemini CLI, GitHub Copilot, OpenCode, Amp, and 12+ other agents via the [Agent Skills](https://agentskills.io) standard.

## What it does

When you invoke `/session-handoff`, the agent reads the full conversation and fills out a handoff template covering:

- What you worked on
- Decisions made (and why)
- Current state — done, in-progress, blocked
- Key files relevant to continuing
- Next steps
- Carry-forward context (env quirks, workarounds, non-obvious constraints)

The output is a fenced markdown block you can paste directly at the top of a new session.

## Installation

### Claude Code (plugin marketplace)

```
/plugin marketplace add pranav-kavle/session-handoff-skill
```

### skills CLI (all compatible agents)

```bash
npx skills add pranav-kavle/session-handoff-skill
```

### Manual

```bash
mkdir -p ~/.claude/skills/session-handoff
curl -o ~/.claude/skills/session-handoff/SKILL.md \
  https://raw.githubusercontent.com/pranav-kavle/session-handoff-skill/main/SKILL.md
```

## Usage

At any point in a session — typically when wrapping up or when context is getting full:

```
/session-handoff
```

The agent produces a filled summary block. Copy it, start a new session, paste it as your first message.

## Example output

````
## Session Handoff — 2026-07-22

### What we worked on
- Added OAuth2 refresh-token flow to the API client
- Debugged intermittent 401s in the staging environment

### Decisions made
- Use short-lived access tokens (15 min) + silent refresh — avoids storing long-lived credentials in localStorage

### Current state
- Done: token refresh logic, unit tests
- In progress: integration test against staging auth server
- Blocked / known issues: staging JWKS endpoint returns 503 under load — being tracked separately

### Key files
- `src/auth/token-client.ts` — refresh logic lives here
- `tests/auth/token-client.test.ts` — integration tests, needs one more case

### Next steps
1. Add the missing integration test for concurrent refresh calls
2. Wire token client into the existing API middleware
3. Test against staging once JWKS is stable

### Carry-forward context
Staging uses a self-signed cert — pass `NODE_TLS_REJECT_UNAUTHORIZED=0` locally or tests will silently fail with a network error rather than an auth error.
````

## When to use this

- Ending a session you plan to continue later
- Context window is filling up and you need a clean start
- Handing off work to a teammate (or future self)
- Building a lightweight audit trail of session decisions
