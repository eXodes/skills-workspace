# AGENTS.md

## Project Overview

This is a **skills workspace** for building, evaluating, and packaging agent skills for GitHub Copilot CLI. A skill is a `SKILL.md` prompt module that gives an agent specialised domain knowledge for a specific class of tasks.

No build system or package manager is used. All work is file authoring and JSON-based evaluation.

---

## Repository Conventions

Each skill lives in two sibling directories at the repo root:

```
<skill-name>/               ← installable skill source
    SKILL.md
    references/
        *.md

<skill-name>-workspace/     ← development artefacts (not installed)
    <skill-name>.skill      ← packaged zip archive
    evals/
        evals.json
    trigger-evals.json
    iteration-<n>/
        benchmark.json
        benchmark.md
        eval-<n>-<name>/
            eval_metadata.json
            with_skill/
            without_skill/
    run_loop.log
```

**Naming rules:**
- Skill directory names use kebab-case: `my-skill`
- Reference files are lowercase kebab-case: `code-smells.md`
- Eval folders are numbered and named: `eval-1-code-review`
- Iteration folders are numbered sequentially: `iteration-1`, `iteration-2`

---

## Skill File Format (`SKILL.md`)

Every `SKILL.md` opens with YAML front matter followed by the agent instructions:

```markdown
---
name: skill-name
description: >
  When to trigger this skill — written for the agent's routing logic.
  Include the exact scenarios it handles and explicitly state what it does NOT handle.
---

# Skill Title

[Agent instructions: workflow, vocabulary, reference file index, output format, tone]
```

**Front matter rules:**
- `name` must match the directory name exactly
- `description` is used verbatim by the agent to decide whether to load the skill — write it to be unambiguous and precise

**Reference file table** (standard pattern in SKILL.md body):

```markdown
| File | What's in it | When to read it |
|------|-------------|----------------|
| `references/foo.md` | ... | When the user asks about X |
```

Reference files should be loaded on demand, not eagerly. The skill should specify exactly when each file is needed.

---

## Eval File Format

### `evals/evals.json`

Array of eval objects. Each eval must have:

```json
{
  "id": 1,
  "prompt": "The user message sent to the agent",
  "expected_output": "Human-readable description of what a passing response looks like",
  "files": [],
  "assertions": [
    {
      "id": "kebab-case-id",
      "description": "What this assertion checks",
      "check": "Specific, verifiable criterion"
    }
  ]
}
```

- `assertions` are graded by a separate analyser model — write `check` fields as falsifiable statements
- `files` lists any files the agent should have access to during the eval
- Use 3–6 assertions per eval; avoid redundancy

### `trigger-evals.json`

Array of `{ "query": "...", "should_trigger": true|false }` objects testing whether the skill fires correctly. Include roughly equal numbers of true/false cases. False cases should represent plausible but out-of-scope queries.

---

## Iteration and Benchmarking

Each benchmark run produces an `iteration-<n>/` folder:

- `benchmark.md` — human-readable summary table (pass rate with/without skill, delta, timing)
- `benchmark.json` — full machine-readable results with per-assertion evidence
- `eval-<n>-<name>/` — per-eval outputs split into `with_skill/` and `without_skill/`

**Target metrics:**
- Pass rate with skill: ≥ 90%
- Delta over baseline: ≥ +20 percentage points
- Trigger precision/recall (from `trigger-evals.json`): ≥ 95%

When iterating on a skill, increment the iteration folder number. Do not overwrite previous benchmark results.

---

## Adding a New Skill

1. Create `<skill-name>/SKILL.md` with front matter and agent instructions
2. Add reference files to `<skill-name>/references/` if needed
3. Create `<skill-name>-workspace/evals/evals.json` with at least 3 evals
4. Create `<skill-name>-workspace/trigger-evals.json` with ≥ 10 cases (mix of true/false)
5. Run the benchmark and save results to `<skill-name>-workspace/iteration-1/`
6. Package the skill: `cd <skill-name> && zip -r ../<skill-name>-workspace/<skill-name>.skill .`

---

## Installing a Skill Locally

```bash
# From source directory
cp -r <skill-name> ~/.agents/skills/

# From packaged archive
unzip <skill-name>-workspace/<skill-name>.skill -d ~/.agents/skills/<skill-name>/
```

---

## Key Authoring Guidelines

- **Skill descriptions** must cover casual phrasings, not just formal ones — agents match on natural language
- **Reference files** should be self-contained knowledge documents, not instructions; instructions go in `SKILL.md`
- **Assertions** in evals must be verifiable by an LLM analyser reading only the response text — avoid assertions that require running code
- **Do not load all reference files by default** — specify conditional loading logic in `SKILL.md`
- **Tone in skills** should be direct and practical; avoid filler phrases like "Great question!"
