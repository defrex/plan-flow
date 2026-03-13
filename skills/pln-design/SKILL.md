---
name: "pln:design"
description: Design a feature through conversation, producing a structured design doc at specs/[feature]/design.md.
argument-hint: [feature-name]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(mkdir *)
---

### Step 0: Validate argument

If no argument is provided, tell the user: `/pln:design [feature-name]`

---

### Step 1: Check for existing design doc

- **If `specs/[feature]/design.md` exists**: Read it, give a brief summary of what's in it, and ask the user what they'd like to change or discuss.
- **If it doesn't exist**: Proceed to Step 2.

### Step 2: Create directory and discuss

1. Create the `specs/[feature]/` directory
2. Ask the user to explain what they're looking for. Have a conversation to understand requirements, constraints, and goals before writing anything.

Do NOT explore the codebase or draft the design doc yet. Wait for the user to explain and for any discussion to resolve.

### Step 3: Explore and draft

Once you understand what the user wants:

1. Explore the codebase to understand the current architecture, patterns, and relevant code
2. Draft a design doc at `specs/[feature]/design.md` covering:
   - **Overview**: What the feature does and why
   - **Design**: How it works — architecture, data flow, key components
   - **Open Questions**: Anything that needs user input or further thought

Use your understanding of the codebase to make the design concrete and specific. Reference actual files, functions, and patterns from the existing code.

### Step 4: Iterate

Tell the user what you've drafted and ask for feedback. As the user requests changes, update `specs/[feature]/design.md` accordingly.

When the user is satisfied, suggest they run `/clear` and then `/pln:plan [feature]` to continue to implementation planning.
