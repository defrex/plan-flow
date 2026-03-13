---
name: design
description: Design a feature through conversation, producing a structured design doc, then hand off to a fresh Claude session for implementation.
argument-hint: [feature-name | finish]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(cmux *), Bash(mkdir *)
---

Check the argument and follow the appropriate mode:

---

### Mode 1: Argument is empty

Tell the user to provide a feature name: `/design [feature-name]` or `/design finish`

---

### Mode 2: Argument is `finish`

Hand off the current design to a new Claude session for implementation.

#### Step 1: Determine the feature

Figure out which feature design to hand off:

1. Check conversation context for which `specs/*/design.md` file was being worked on
2. If unclear, find the most recently modified `specs/*/design.md` file
3. If still unclear, ask the user which feature to finish

#### Step 2: Commit the design doc

Commit `specs/[feature]/design.md` with the message: `Add design doc for [feature]`

#### Step 3: Open new session in split

1. Create a horizontal split:

```bash
cmux new-pane --type terminal --direction down
```

2. Start Claude in the new pane with the `/implementation-plan` skill:

```bash
cmux send --surface <surface_ref> 'claude "/implementation-plan specs/[feature]/design.md"'
cmux send-key --surface <surface_ref> Enter
```

Replace `[feature]` with the actual feature name.

#### Step 4: Confirm

Tell the user the implementation planning session has been opened and which design doc it's referencing.

---

### Mode 3: Argument is anything else (feature name)

Design a feature iteratively, producing `specs/[feature]/design.md`.

#### Step 1: Check for existing design doc

- **If `specs/[feature]/design.md` exists**: Read it, give a brief summary of what's in it, and ask the user what they'd like to change or discuss.
- **If it doesn't exist**: Proceed to Step 2.

#### Step 2: Create directory and discuss

1. Create the `specs/[feature]/` directory
2. Ask the user to explain what they're looking for. Have a conversation to understand requirements, constraints, and goals before writing anything.

Do NOT explore the codebase or draft the design doc yet. Wait for the user to explain and for any discussion to resolve.

#### Step 3: Explore and draft

Once you understand what the user wants:

1. Explore the codebase to understand the current architecture, patterns, and relevant code
2. Draft a design doc at `specs/[feature]/design.md` covering:
   - **Overview**: What the feature does and why
   - **Design**: How it works — architecture, data flow, key components
   - **Open Questions**: Anything that needs user input or further thought

Use your understanding of the codebase to make the design concrete and specific. Reference actual files, functions, and patterns from the existing code.

#### Step 4: Open the markdown viewer

Run this command so the user can see the design doc rendered:

```bash
cmux markdown open specs/[feature]/design.md
```

This stays open and auto-refreshes — no need to re-run after updates.

#### Step 5: Iterate

The design doc is now open. Tell the user what you've drafted and ask for feedback. As the user requests changes, update `specs/[feature]/design.md` accordingly. The markdown viewer will reflect changes automatically.
