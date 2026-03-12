<div align="center">

### Plan Flow

*3-phase coding agent skills: design, implement, refine*

&nbsp;

</div>

A set of [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills that provide a structured workflow for feature design and implementation planning.

## Skills

### `/design [feature-name]`

Iteratively design a feature through conversation, producing a structured design doc at `specs/<feature>/design.md`. Covers overview, architecture, and open questions. Use `/design finish` to commit the doc and hand off to an implementation planning session.

### `/implementation-plan [path/to/design.md]`

Convert a design doc into a concrete, ordered implementation plan at `specs/<feature>/implementation-plan.md`. Each step includes file paths, descriptions, and testing instructions. Use `/implementation-plan finish` to commit the plan and hand off to an implementation session.

### `/split-compact [file.md | focus-guidance]`

Create a compacted summary of the current conversation and open it in a new Claude session in a split pane. Useful for preserving context across long workflows.

## Workflow

```
/design feature-name  -->  /design finish  -->  /implementation-plan  -->  /implementation-plan finish  -->  implement
```

1. **Design**: Explore the codebase, draft and iterate on a design doc
2. **Plan**: Convert the design into ordered implementation steps
3. **Implement**: Execute the plan in a fresh session with full context

Each transition commits work and opens a new Claude session with the relevant context.

## Setup

```bash
bun install
```

Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code) and [Bun](https://bun.sh).
