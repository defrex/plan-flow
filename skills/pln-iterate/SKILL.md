---
name: "pln:iterate"
description: Review implementation details and discuss next steps (read-only).
argument-hint: [feature-name]
allowed-tools: Read, Glob, Grep
---

### Step 0: Validate argument

If no argument is provided, tell the user: `/pln:iterate [feature-name]`

---

### Step 1: Read all spec files

Read all three spec files:
- `specs/[feature]/design.md`
- `specs/[feature]/implementation-plan.md`
- `specs/[feature]/implementation-details.md`

If any are missing, note which ones and work with what's available.

### Step 2: Present summary

Give a concise summary of the current state:

- What was designed
- What was planned
- What was actually built
- Any deviations from the plan
- Known issues or incomplete areas

### Step 3: Discuss next steps

Ask the user how they'd like to proceed. Suggest options:

- **Fix issues**: Update the implementation plan to address known issues, then `/pln:build [feature]`
- **New iteration**: Start a new design cycle with `/pln:design [feature]`
- **Feature is done**: No further action needed

This is a read-only review skill — do not modify any files.
