---
name: implementation-plan
description: Read a design doc and produce a concrete, ordered implementation plan with steps, testing, and open questions.
argument-hint: [path/to/design.md]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(cmux *), Bash(mkdir *)
---

### Step 1: Determine the design doc

Use the argument, conversation context, or filesystem to find the design doc:

1. **If an argument is provided**: Use it as the path to the design doc (e.g., `specs/feature/design.md`)
2. **If no argument**: Check conversation context for which design doc was being discussed
3. **If still unclear**: Find the most recently modified `specs/*/design.md` file
4. **If still unclear**: Ask the user which design doc to use

### Step 2: Read the design doc

Read the design doc thoroughly. Understand the feature, its architecture, data flow, and any open questions.

### Step 3: Explore the codebase

Explore the codebase to understand:

- Existing architecture and patterns relevant to the design
- Files that will need to be modified or serve as reference
- Testing patterns and conventions already in use
- Any existing code that overlaps with or relates to the planned feature

### Step 4: Write the implementation plan

Determine the feature name from the design doc path (e.g., `specs/my-feature/design.md` → `my-feature`).

Create `specs/[feature]/implementation-plan.md` (sibling to the design doc) with the following sections:

#### Steps

Ordered implementation steps. Each step should include:

- **File paths**: Which files to create or modify
- **Description**: What to do in clear, actionable terms

For large tasks, break steps into subtasks suitable for parallel subagents. Each subtask must have a clear, agent-executable verification step — something concrete like "run `bun test src/foo.test.ts` and confirm it passes", not vague like "verify it works".

#### Testing

How to verify each step and the feature overall. Include specific commands to run and expected outcomes.

#### Code Review

The final step should always be: run a code review agent to do a thorough review of all changes made during implementation.

#### Open Questions

Anything unclear from the design that affects implementation. Flag decisions that need user input before proceeding.

### Step 5: Open the markdown viewer

```bash
cmux markdown open specs/[feature]/implementation-plan.md
```

This stays open and auto-refreshes — no need to re-run after updates.

### Step 6: Iterate

Tell the user what you've planned and ask for feedback. As the user requests changes, update `specs/[feature]/implementation-plan.md` accordingly. The markdown viewer will reflect changes automatically.
