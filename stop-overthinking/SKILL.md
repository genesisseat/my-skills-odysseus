# stop-overthinking

<!--
description: Breaks the agent out of reasoning loops by forcing a single concrete command instead of continued planning. Use when thinking exceeds 10 lines with no tool call, or when "perhaps/maybe/could be" appears repeatedly without action.
category: agent-behavior
tags: [agent, reasoning, loops, thinking, behavior, productivity]
-->

## When to Use

When the agent is stuck in a thinking/reasoning loop — re-explaining the same situation, listing the same options repeatedly, or writing long analysis paragraphs without calling any tool. Signs include:

- Thinking block longer than ~10 lines without a tool call following it
- The words "perhaps", "maybe", "could be", "let's consider" appearing more than 3 times in one thinking block
- Restating what already failed instead of trying something new
- Writing "let's do X" but then not doing X

---

## Core Rule

**If you know the next command, run it. Do not explain it first.**

Thinking is for deciding. Once decided, act immediately.

---

## Procedure

### When you catch yourself looping:

1. **Stop writing.** Cut the thinking block immediately.
2. **Identify the single next action** — one command, not a plan.
3. **Run it.**
4. **Read the output.**
5. Only then decide the next single action.

---

## The One-Step Rule

At any point, you only need to answer one question:

> "What is the ONE command I should run right now?"

Run that command. Read the result. Then ask the question again.

Never plan more than one step ahead while waiting for output.

---

## Decision Tree for Common Stuck States

```
Don't know where I am?
  → run: pwd && whoami && ls /

Don't know if a tool exists?
  → run: which <toolname>

Don't know what's mounted?
  → run: cat /proc/mounts

Don't know where a directory is?
  → run: find / -type d -name "<name>" 2>/dev/null

Don't know what's in /mnt/?
  → run: ls -la /mnt/

Don't know what environment this is?
  → run: uname -a && cat /etc/os-release
```

Pick the matching command. Run it. Stop explaining.

---

## Anti-Patterns

❌ "We need to figure out X. Perhaps Y. Or maybe Z. Given the constraints..."
❌ Writing the same hypothesis 3 times with slightly different wording
❌ "Let's try X" followed by more paragraphs instead of actually trying X
❌ Summarizing previous failures before attempting the next step
❌ Asking "what should I do?" when a diagnostic command from the decision tree applies

---

## Companion Skills

- `wsl-path-fix` — converts Windows paths to Linux format
- `diagnose-and-recover` — what to do when commands fail

**Order of operations:**
```
Path given → [wsl-path-fix] → convert syntax
Command fails → [diagnose-and-recover] → run diagnostics  
Agent loops → [stop-overthinking] → cut thinking, run next command
```
