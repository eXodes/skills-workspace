# Skills Workspace

A repository for building and evaluating **agent skills** — reusable prompt modules that give GitHub Copilot CLI specialised expertise for specific domains.

## What is a skill?

A skill is a `SKILL.md` file (with optional supporting reference files) that an agent loads to gain focused, deep knowledge about a topic. Skills tell the agent *when to activate*, *how to reason*, and *what reference material to consult*.

Skills are installed at `~/.agents/skills/<skill-name>/` and packaged as `.skill` zip archives for distribution.

## Repository structure

Each skill lives in two sibling directories:

```
skills-workspace/
├── <skill-name>/               # Skill source files (installable)
│   ├── SKILL.md                # Skill definition: metadata, workflow, instructions
│   └── references/             # Supporting knowledge files loaded on demand
│
└── <skill-name>-workspace/     # Development workspace (not installed)
    ├── <skill-name>.skill      # Packaged skill (zip archive)
    ├── evals/
    │   └── evals.json          # Evaluation prompts and assertions
    ├── trigger-evals.json      # Trigger detection test cases
    ├── iteration-*/            # Benchmark results per iteration
    │   ├── benchmark.md        # Pass rate summary
    │   └── eval-*/             # Per-eval run outputs
    └── run_loop.log            # Skill creator session log
```

## Skill file format

Each `SKILL.md` starts with a YAML front matter block:

```yaml
---
name: skill-name
description: >
  One-paragraph description used by the agent to decide when to trigger this skill.
  Should cover the exact scenarios this skill handles and explicitly exclude what it doesn't.
---
```

The body contains the agent instructions: workflow steps, vocabulary, reference file index, output format, and tone guidelines.

## Developing a skill

1. **Create source files** — `<skill-name>/SKILL.md` plus any `references/*.md` knowledge files
2. **Write evals** — `evals/evals.json` with prompts, expected outputs, and assertions; `trigger-evals.json` for trigger detection
3. **Benchmark** — run evals with and without the skill to measure the improvement delta
4. **Iterate** — refine the skill instructions based on benchmark failures
5. **Package** — zip the skill directory into a `.skill` archive for distribution

## Installing a skill

Install any skill from this repository using the `skills` CLI:

```bash
npx skills add eXodes/skills-workspace
```

This installs all skills from this repo and makes them available to your AI agent.

To install a specific skill by name, you can also copy the skill directory manually:

```bash
cp -r <skill-name> ~/.agents/skills/
```

Or install from the packaged archive:

```bash
unzip <skill-name>.skill -d ~/.agents/skills/<skill-name>/
```
