# CLEAR — A Claude Code Skill for Better Prompts

CLEAR is a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that transforms vague prompts into structured, high-quality ones using five principles:

| Letter | Principle | What it means |
|--------|-----------|---------------|
| **C** | Clear and scoped | One clear goal, no filler |
| **L** | Logical structure | Context → Task → Constraints → Format |
| **E** | Explicit constraints | Say what NOT to do |
| **A** | Auditable | Measurable success criteria, not vibes |
| **R** | Reproducible | No temporal references — works next month too |

## Installation

### Option A: Plugin install (recommended)

```bash
claude plugin install https://github.com/esison/clear-prompt-skill
```

Claude Code will download the repo and register the `/clear-prompt` slash command.

### Option B: Manual install (personal scope)

Clone the repo into your Claude Code skills directory:

```bash
git clone https://github.com/esison/clear-prompt-skill.git ~/.claude/skills/clear-prompt
```

### Option C: Project-level install

Add it to a specific project so all contributors have access:

```bash
# From your project root
mkdir -p .claude/skills
git clone https://github.com/esison/clear-prompt-skill.git .claude/skills/clear-prompt
```

## Usage

In any Claude Code session, type:

```
/clear-prompt <your draft prompt>
```

### Example

```
/clear-prompt Help me write a script to process some data files and make them more efficient
```

CLEAR will analyze the prompt against all five principles and return:

1. **Diagnosis** — which principles the draft violates
2. **Improved prompt** — rewritten with Context, Task, Constraints, and Format sections
3. **Chained prompts** (if needed) — when the original tried to do too much, CLEAR splits it into a sequence

### Before & After

**Before CLEAR:**
> Help me write a script to process some data files and make them more efficient

**After CLEAR:**

> **Context:** Multiple CSV files with identical column schemas in `./data/`
>
> **Task:** Write a Python script that merges all CSVs into a single output file
>
> **Constraints:** Use pandas only. No functions over 20 lines. No external libraries beyond pandas. Script must be under 50 lines total.
>
> **Format:** Single file `merge.py` that outputs `merged.csv`. Verify by running on `test_data/`.

## Advanced: Prompt Chaining

CLEAR's most powerful feature is **automatic chain detection**. If your draft prompt tries to do multiple things, CLEAR splits it into a sequence of focused prompts — each one feeding into the next.

```
/clear-prompt Build a REST API for user management with authentication, write tests, deploy to AWS, and update the docs
```

This produces four separate CLEAR prompts you can run in order, each with its own scope and verification criteria.

## File Structure

```
clear-prompt-skill/
├── claude-plugin.json          # Plugin manifest for `claude plugin install`
├── README.md
├── LICENSE
└── skills/
    └── clear-prompt/
        └── SKILL.md            # The skill definition
```

## Uninstall

```bash
claude plugin uninstall clear-prompt
```

Or if manually installed, remove the directory:

```bash
rm -rf ~/.claude/skills/clear-prompt
```

## License

MIT
