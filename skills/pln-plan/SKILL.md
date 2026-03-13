---
name: "pln:plan"
description: Read a design doc and produce a concrete, ordered implementation plan at specs/[feature]/implementation-plan.md.
argument-hint: [feature-name]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(mkdir *)
---

### Step 0: Validate argument

If no argument is provided, deduce from context or tell the user: `/pln:plan [feature-name]`

---

### Step 1: Read the design doc

Resolve the design doc at `specs/[feature]/design.md` where `[feature]` is the argument.

If the file doesn't exist, tell the user and suggest they run `/pln:design [feature]` first.

Read the design doc thoroughly. Understand the feature, its architecture, data flow, and any open questions.

### Step 2: Explore the codebase

Explore the codebase to understand:

- Existing architecture and patterns relevant to the design
- Files that will need to be modified or serve as reference
- Testing patterns and conventions already in use
- Any existing code that overlaps with or relates to the planned feature

### Step 3: Write the implementation plan

Create `specs/[feature]/implementation-plan.md` with the following sections:

- **Steps**: Ordered implementation steps, each with file paths and a description of what to do. For large tasks, break steps into subtasks suitable for parallel subagents, each with a clear, agent-executable verification step (e.g., "run `bun test src/foo.test.ts` and confirm it passes", not "verify it works")
- **Testing**: How to verify each step and the feature overall. Include specific commands and expected outcomes.
- **Code Review**: The final step should always be running a code review agent to do a thorough review of all changes.
- **Open Questions**: Anything unclear from the design that affects implementation. Flag decisions that need user input.

### Step 4: Iterate

Tell the user what you've planned and ask for feedback. As the user requests changes, update `specs/[feature]/implementation-plan.md` accordingly.

When the user is satisfied, suggest they run `/clear` and then `/pln:build [feature]` to start implementation.
