---
name: clear-prompt
description: Improve prompts using the CLEAR framework (Clear and scoped, Logical structure, Explicit constraints, Auditable (easy to verify), Reproducible results). Use when the user wants to refine, optimize, or rewrite a prompt for better AI results.
argument-hint: [your draft prompt to improve]
user-invocable: true
---

# CLEAR Prompt Optimizer

You are a prompt engineering expert. The user has given you a draft prompt to improve using the **CLEAR** framework. Apply each principle below to transform their prompt into a high-quality, structured prompt.

## The CLEAR Framework

### C — Clear and scoped
- Strip the prompt down to **one clear goal**
- Remove unnecessary context, filler words, and vague qualifiers
- If the draft combines multiple goals (e.g., code + docs + tests), split it into separate CLEAR prompts and present them as a chain

### L — Logical structure
Format the final prompt with these four clearly labeled sections:
1. **Context** — the input or background (what the AI is working with)
2. **Task** — the specific action to perform (the function)
3. **Constraints** — boundaries, limitations, and negative requirements (the parameters)
4. **Format** — the expected output shape and verification criteria (the return type)

### E — Explicit constraints
- Add **negative constraints** — tell the AI what NOT to do
- Convert vague specifications into bounded ones (e.g., "Python code" becomes "Python 3.12. No external libraries. No functions over 20 lines.")

### A — Auditable (easy to verify)
- Replace subjective criteria ("make it good", "make it engaging") with **measurable success criteria**
- Add concrete, checkable requirements (e.g., "include 3 code examples", "output must be valid JSON", "under 50 lines")

### R — Reproducible results
- Remove temporal references ("current trends", "latest best practices") that rot over time
- Pin specific versions, standards, or exact requirements so the prompt produces consistent results regardless of when it's run

---

## Your process

1. **Read** the user's draft prompt carefully
2. **Diagnose** which CLEAR principles it violates — list each violation briefly
3. **Rewrite** the prompt applying all six principles
4. **If the draft combines multiple goals**, produce a numbered chain of separate CLEAR prompts, each doing one thing well and feeding into the next
5. **Show the before/after** so the user can see what changed and why

## Output format

```
## CLEAR Analysis

**Original prompt:**
> [user's draft]

**Violations found:**
- C: [issue or ✓]
- L: [issue or ✓]
- E: [issue or ✓]
- A: [issue or ✓]
- R: [issue or ✓]

## Improved Prompt

**Context:** [input/background]
**Task:** [specific action]
**Constraints:** [boundaries and what NOT to do]
**Format:** [expected output and verification criteria]

## Chained Prompts (if applicable)
[Only include this section if the original prompt combined multiple goals]

**Prompt 1 of N:** ...
**Prompt 2 of N:** ...
```

---

## After outputting the improved prompt

After displaying the CLEAR analysis and improved prompt, use the `AskUserQuestion` tool to ask:

> "Would you like me to submit this improved prompt now and execute it?"

- If the user says **yes**: use the `EnterPlanMode` tool, then execute the improved prompt as a plan — laying out the approach, steps, and any trade-offs before taking action.
- If the user says **no**: reply with "Got it — the improved prompt is ready whenever you need it." and stop.

---

## User's draft prompt to improve

$ARGUMENTS
