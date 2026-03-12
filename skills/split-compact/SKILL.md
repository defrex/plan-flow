---
name: split-compact
description: Create a compacted summary of this conversation and open it in a new Claude session in a horizontal split.
argument-hint: [file.md | focus-guidance]
allowed-tools: Read, Write, Bash(cmux *)
---

### Step 1: Determine the prompt for the new session

Check the argument:

- **If the argument is a path to a `.md` file**: Read that file. Its contents will be the initial prompt for the new session. Skip to Step 3.
- **If the argument is empty or not an `.md` file**: Proceed to Step 2 to generate a compaction summary. If the argument is non-empty, treat it as guidance for what the summary should focus on.

### Step 2: Generate a compaction summary

Write a concise summary of this conversation that will be useful as the starting prompt for a fresh Claude session. Use your best judgement, but generally include:

- **What we're working on**: the goal, task, or problem being solved
- **Key decisions made**: architectural choices, approaches chosen (and rejected), and why
- **Current state**: what's been done, what's left, any blockers
- **Important context**: file paths, commands, patterns, or constraints that came up
- **If the user provided non-empty guidance** (that wasn't an .md file path), use it to shape what the summary emphasizes

Keep it short — aim for the minimum context needed to continue the work effectively. Don't include full file contents or tool outputs, just reference paths and key findings.

End the summary with:

```
---
The above is a summary of a previous conversation that was compacted. Please ask the user what they'd like to work on next.
```

### Step 3: Open the new session

1. Write the prompt (either the .md file contents or the generated summary) to a temporary file at `/tmp/claude-compact-prompt.md`
2. Run this command to create a horizontal split with a new Claude session:

```bash
cmux new-pane --type terminal --direction down
```

3. Then open an interactive Claude session with the prompt as the first message, using the surface ref from the previous command:

```bash
cmux send --surface <surface_ref> 'claude "$(cat /tmp/claude-compact-prompt.md)"'
cmux send-key --surface <surface_ref> Enter
```

### Step 4: Confirm

Tell the user the new session has been opened with the compacted context. If you generated a summary, briefly mention the key points you included so the user can verify nothing important was missed.
