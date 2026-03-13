---
name: "pln:build"
description: Implement a feature step by step from its implementation plan.
argument-hint: [feature-name]
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(mkdir *), Bash(bun *)
---

### Step 0: Validate argument

If no argument is provided, deduce from context or tell the user: `/pln:build [feature-name]`

---

### Step 1: Read the specs

Verify `specs/[feature]/implementation-plan.md` exists. If not, tell the user and suggest they run `/pln:plan [feature]` first.

Read both:
- `specs/[feature]/design.md`
- `specs/[feature]/implementation-plan.md`

Understand the full context of what needs to be built.

### Step 2: Implement step by step

Work through each step in the implementation plan in order:

1. Read and understand the step
2. Implement the changes described
3. Run the verification command specified in the step (tests, type checks, etc.)
4. If verification fails, fix the issue before moving to the next step
5. Briefly report progress after each step

### Step 3: Code review

After all steps are complete, run a code review as described in the plan. Fix any issues found.

### Step 4: Wrap up

Tell the user implementation is complete and summarize what was built.

Suggest they run `/pln:save` to commit and document the implementation and then `/clear` and `/pln:iterate [feature]` to make further changes.
