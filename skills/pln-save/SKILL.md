---
name: "pln:save"
description: Commit implementation, write implementation details doc at specs/[feature]/implementation-details.md.
argument-hint: [feature-name]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(mkdir *), Bash(git *)
---

### Step 0: Validate argument

If no argument is provided, deduce from context or tell the user: `/pln:save [feature-name]`

---

### Step 1: Validate the feature

Verify `specs/[feature]/` directory exists. If not, ask the user for the correct feature name.

### Step 2: Read the specs

Read `specs/[feature]/design.md` and `specs/[feature]/implementation-plan.md` to understand what was intended.

### Step 3: Explore what was implemented

Explore the codebase to understand what was actually built:

- Look at recent git changes (unstaged, staged, and recent commits since the implementation plan was committed)
- Identify new and modified files
- Understand how the implementation maps to the plan

### Step 4: Commit the implementation

Stage all implementation files (not the specs) and commit with the message: `Implement [feature]`

### Step 5: Write implementation details

Create `specs/[feature]/implementation-details.md` with the following sections:

- **Summary**: What was implemented, high-level
- **Changes**: Files added/modified with brief descriptions
- **Deviations**: How the implementation differs from the plan (if at all)
- **Known Issues**: Bugs, rough edges, incomplete areas
- **Next Steps**: Suggested improvements, things to test

Be specific and reference actual files, functions, and code patterns.

### Step 6: Iterate

Tell the user what you've written and ask for feedback. As the user requests changes, update `specs/[feature]/implementation-details.md` accordingly.

When the user is satisfied, suggest they run `/clear` and then `/pln:iterate [feature]` to review and plan next steps.
