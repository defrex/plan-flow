<div align="center">

### Plan Flow

*5-step coding agent skills: design, plan, build, save, iterate*

&nbsp;

</div>

A set of [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills that provide a structured workflow for feature design and implementation.

## Skills

### `/pln:design [feature-name]`

Iteratively design a feature through conversation, producing a structured design doc at `specs/<feature>/design.md`. Covers overview, architecture, and open questions.

### `/pln:plan [feature-name]`

Convert a design doc into a concrete, ordered implementation plan at `specs/<feature>/implementation-plan.md`. Each step includes file paths, descriptions, and testing instructions.

### `/pln:build [feature-name]`

Implement the feature step by step from the implementation plan, running verification after each step.

### `/pln:save [feature-name]`

Commit the implementation, then write `specs/<feature>/implementation-details.md` documenting what was built, deviations from the plan, and known issues.

### `/pln:iterate [feature-name]`

Read-only review of all spec files. Presents a summary of the current state and discusses next steps — fix issues, start a new iteration, or mark the feature as done.

## Workflow

```
/pln:design → /clear → /pln:plan → /clear → /pln:build → /clear → /pln:save → /clear → /pln:iterate
```

1. **Design**: Explore the codebase, draft and iterate on a design doc
2. **Plan**: Convert the design into ordered implementation steps
3. **Build**: Execute the plan step by step with verification
4. **Save**: Commit the work and document what was built
5. **Iterate**: Review the results and decide next steps

Use `/clear` between steps to start each phase with a fresh context window.

## Setup

```bash
bun install
```

Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code) and [Bun](https://bun.sh).
