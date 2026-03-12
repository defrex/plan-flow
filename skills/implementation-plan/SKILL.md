---
name: implementation-plan
description: Read a design doc and produce a concrete, ordered implementation plan with steps, testing, and open questions.
argument-hint: [path/to/design.md | finish]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(cmux *), Bash(mkdir *)
---

Check the argument and follow the appropriate mode:

---

### Mode 1: Argument is empty

Tell the user to provide a path to a design doc: `/implementation-plan specs/[feature]/design.md` or `/implementation-plan finish`

---

### Mode 2: Argument is `finish`

Hand off the current implementation plan to a new Claude session for implementation.

#### Step 1: Determine the feature

Figure out which implementation plan to hand off:

1. Check conversation context for which `specs/*/implementation-plan.md` file was being worked on
2. If unclear, find the most recently modified `specs/*/implementation-plan.md` file
3. If still unclear, ask the user which feature to implement

#### Step 2: Commit the implementation plan

Commit `specs/[feature]/implementation-plan.md` with the message: `Add implementation plan for [feature]`

#### Step 3: Open new session in split

1. Create a horizontal split:

```bash
cmux new-pane --type terminal --direction down
```

2. Start Claude in the new pane with the implementation plan:

```bash
cmux send --surface <surface_ref> 'claude "implement the plan specs/[feature]/implementation-plan.md"'
cmux send-key --surface <surface_ref> Enter
```

Replace `[feature]` with the actual feature name.

#### Step 4: Confirm

Tell the user the implementation session has been opened and which implementation plan it's referencing.

---

### Mode 3: Argument is anything else (path to a design doc)

#### Step 1: Determine the design doc

Use the argument, conversation context, or filesystem to find the design doc:

1. **If an argument is provided**: Use it as the path to the design doc (e.g., `specs/feature/design.md`)
2. **If no argument**: Check conversation context for which design doc was being discussed
3. **If still unclear**: Find the most recently modified `specs/*/design.md` file
4. **If still unclear**: Ask the user which design doc to use

#### Step 2: Read the design doc

Read the design doc thoroughly. Understand the feature, its architecture, data flow, and any open questions.

#### Step 3: Explore the codebase

Explore the codebase to understand:

- Existing architecture and patterns relevant to the design
- Files that will need to be modified or serve as reference
- Testing patterns and conventions already in use
- Any existing code that overlaps with or relates to the planned feature

#### Step 4: Write the implementation plan

Determine the feature name from the design doc path (e.g., `specs/my-feature/design.md` → `my-feature`).

Create `specs/[feature]/implementation-plan.md` (sibling to the design doc) with the following sections:

- **Steps**: Ordered implementation steps, each with file paths and a description of what to do. For large tasks, break steps into subtasks suitable for parallel subagents, each with a clear, agent-executable verification step (e.g., "run `bun test src/foo.test.ts` and confirm it passes", not "verify it works")
- **Testing**: How to verify each step and the feature overall. Include specific commands and expected outcomes.
- **Code Review**: The final step should always be running a code review agent to do a thorough review of all changes.
- **Open Questions**: Anything unclear from the design that affects implementation. Flag decisions that need user input.

#### Step 5: Open the markdown viewer

```bash
cmux markdown open specs/[feature]/implementation-plan.md
```

This stays open and auto-refreshes — no need to re-run after updates.

#### Step 6: Iterate

Tell the user what you've planned and ask for feedback. As the user requests changes, update `specs/[feature]/implementation-plan.md` accordingly. The markdown viewer will reflect changes automatically.
