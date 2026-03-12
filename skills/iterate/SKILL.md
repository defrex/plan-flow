---
name: iterate
description: Commit initial implementation, write implementation details, and hand off to a new session for iteration.
argument-hint: [feature-name | finish]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(cmux *), Bash(mkdir *), Bash(git *)
---

Check the argument and follow the appropriate mode:

---

### Mode 1: Argument is empty

Tell the user to provide a feature name: `/iterate [feature-name]` or `/iterate finish`

---

### Mode 2: Argument is `finish`

Hand off the implementation details to a new Claude session for bug fixing and iteration.

#### Step 1: Determine the feature

Figure out which feature to hand off:

1. Check conversation context for which `specs/*/implementation-details.md` file was being worked on
2. If unclear, find the most recently modified `specs/*/implementation-details.md` file
3. If still unclear, ask the user which feature to finish

#### Step 2: Commit the implementation details

Commit `specs/[feature]/implementation-details.md` with the message: `Add implementation details for [feature]`

#### Step 3: Open new session in split

1. Create a horizontal split:

```bash
cmux new-pane --type terminal --direction down
```

2. Start Claude in the new pane:

```bash
cmux send --surface <surface_ref> 'claude "please review specs/[feature]/design.md and specs/[feature]/implementation-details.md then ask the user how they'\''d like to proceed"'
cmux send-key --surface <surface_ref> Enter
```

Replace `[feature]` with the actual feature name.

#### Step 4: Confirm

Tell the user the iteration session has been opened and which feature it's referencing.

---

### Mode 3: Argument is anything else (feature name)

Commit the implementation and write `specs/[feature]/implementation-details.md`.

#### Step 1: Determine the feature

Use the argument as the feature name. Verify `specs/[feature]/` directory exists. If not, ask the user for the correct feature name.

#### Step 2: Read the specs

Read `specs/[feature]/design.md` and `specs/[feature]/implementation-plan.md` to understand what was intended.

#### Step 3: Explore what was implemented

Explore the codebase to understand what was actually built:

- Look at recent git changes (unstaged, staged, and recent commits since the implementation plan was committed)
- Identify new and modified files
- Understand how the implementation maps to the plan

#### Step 4: Commit the implementation

Stage all implementation files (not the specs) and commit with the message: `Implement [feature]`

Ask the user to confirm before committing.

#### Step 5: Write implementation details

Create `specs/[feature]/implementation-details.md` with the following sections:

- **Summary**: What was implemented, high-level
- **Changes**: Files added/modified with brief descriptions
- **Deviations**: How the implementation differs from the plan (if at all)
- **Known Issues**: Bugs, rough edges, incomplete areas
- **Next Steps**: Suggested improvements, things to test

Be specific and reference actual files, functions, and code patterns.

#### Step 6: Open the markdown viewer

```bash
cmux markdown open specs/[feature]/implementation-details.md
```

This stays open and auto-refreshes — no need to re-run after updates.

#### Step 7: Iterate

Tell the user what you've written and ask for feedback. As the user requests changes, update `specs/[feature]/implementation-details.md` accordingly. The markdown viewer will reflect changes automatically.
