# AGENTS.md

## Project Overview

Skills workspace for building, evaluating, and packaging agent skills. Skill = `SKILL.md` prompt module giving agents specialised domain knowledge.

No build system or package manager. All work is file authoring and JSON-based evaluation.

---

## Skills in this repo

| Skill              | Benchmark           |
| ------------------ | ------------------- |
| `engineering`      | 94% vs 61% (+33pp)  |
| `pdf-viewer`       | 100% vs 11% (+89pp) |
| `refactoring-guru` | 100% vs 61% (+39pp) |
| `refactoring-ui`   | 100% vs 75% (+25pp) |
| `strudel`          | 100% vs 91% (+9pp)  |

---

## Repository Structure

Each skill = two sibling dirs at repo root:

```
<skill-name>/               ← installable skill source
    SKILL.md
    references/
        *.md

<skill-name>-workspace/     ← development artefacts (not installed)
    <skill-name>.skill      ← packaged zip archive
    README.md               ← file index + benchmark summary
    evals/
        evals.json
    trigger-evals.json      ← not all workspaces have this yet
    iteration-<n>/
        benchmark.json
        benchmark.md
        eval-<n>-<name>/
            eval_metadata.json
            grading.json
            with_skill/
            without_skill/
    run_loop.log            ← description optimiser session log (optional)
```

**Naming rules:**

- Skill dirs: kebab-case (`my-skill`)
- Reference files: lowercase kebab-case (`code-smells.md`)
- Eval folders: `eval-<n>-<name>` (e.g. `eval-1-code-review`)
- Iteration folders: `iteration-1`, `iteration-2` — never overwrite, always increment

---

## Skill File Format (`SKILL.md`)

```markdown
---
name: skill-name          ← must match directory name exactly
description: >
  When to trigger — written for agent routing logic.
  Cover exact scenarios handled. Explicitly state what it does NOT handle.
---

# Skill Title

[Agent instructions: workflow, vocabulary, reference file index, output format, tone]
```

**Reference file table** (standard pattern in SKILL.md body):

```markdown
| File                | What's in it | When to read it            |
| ------------------- | ------------ | -------------------------- |
| `references/foo.md` | ...          | When the user asks about X |
```

Reference files: load on demand, not eagerly. Specify conditional loading logic.

---

## Eval File Format

### `evals/evals.json`

```json
{
  "id": 1,
  "prompt": "User message sent to the agent",
  "expected_output": "Human-readable description of passing response",
  "files": [],
  "assertions": [
    {
      "id": "kebab-case-id",
      "description": "What this assertion checks",
      "check": "Specific, falsifiable criterion"
    }
  ]
}
```

- `assertions` graded by separate analyser model — `check` must be falsifiable from response text alone
- `files`: any files agent needs during eval
- Use 3–6 assertions per eval; avoid redundancy

### `trigger-evals.json`

```json
{ "query": "...", "should_trigger": true|false }
```

≥ 10 cases, roughly equal true/false split. False cases = plausible but out-of-scope queries.

---

## Iteration and Benchmarking

**Target metrics:**

- Pass rate with skill: ≥ 90%
- Delta over baseline: ≥ +20pp
- Trigger precision/recall: ≥ 95%

`benchmark.md` has human-readable summary table. `benchmark.json` has per-assertion evidence. `grading.json` per eval has raw grading output.

---

## Key Commands

### Package a skill

```bash
cd <skill-name> && zip -r ../<skill-name>-workspace/<skill-name>.skill .
```

### Install (preferred — npx CLI)

```bash
# All skills
npx skills add eXodes/skills-workspace

# Single skill
npx skills add eXodes/skills-workspace -s <skill-name>

# List available
npx skills add eXodes/skills-workspace -l
```

### Install (manual)

```bash
# From source
cp -r <skill-name> ~/.agents/skills/

# From packaged archive
unzip <skill-name>-workspace/<skill-name>.skill -d ~/.agents/skills/<skill-name>/
```

---

## Adding a New Skill

1. Create `<skill-name>/SKILL.md` with front matter + agent instructions
2. Add reference files to `<skill-name>/references/` if needed
3. Create `<skill-name>-workspace/evals/evals.json` (≥ 3 evals)
4. Create `<skill-name>-workspace/trigger-evals.json` (≥ 10 cases)
5. Run benchmark → save to `<skill-name>-workspace/iteration-1/`
6. Package: `cd <skill-name> && zip -r ../<skill-name>-workspace/<skill-name>.skill .`

Use the `skill-creator` skill for creating, modifying, and benchmarking skills.

---

## Key Authoring Guidelines

- **Skill descriptions**: cover casual phrasings — agents match on natural language
- **Reference files**: self-contained knowledge docs, not instructions; instructions go in `SKILL.md`
- **Assertions**: must be verifiable by LLM analyser reading only response text — no assertions requiring code execution
- **Reference loading**: specify conditional logic in `SKILL.md`; never load all eagerly
- **Tone**: direct and practical; no filler like "Great question!"
- **Out-of-scope handling**: when skill routing fails, still help with general knowledge — don't abandon user with only a meta-explanation
