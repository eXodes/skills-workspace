# Skills Workspace

A repository for building and evaluating **agent skills** — reusable prompt modules that give GitHub Copilot CLI specialised expertise for specific domains.

## What is a skill?

A skill is a `SKILL.md` file (with optional supporting reference files) that an agent loads to gain focused, deep knowledge about a topic. Skills tell the agent _when to activate_, _how to reason_, and _what reference material to consult_.

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

## Installing skills

Install skills from this repository using the `npx skills` CLI.

### Install skills from this repository

```bash
npx skills add eXodes/skills-workspace
```

This installs all available skills and makes them available to your AI agent.

### Install specific skills

| Skill                | Purpose                                                                                                   | Install                                                      |
| -------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| **engineering**      | Software engineering guidance: standups, code review, architecture, debugging, deployment, incidents      | `npx skills add eXodes/skills-workspace -s engineering`      |
| **refactoring-guru** | Expert advice on code quality, design patterns, and refactoring using the Refactoring Guru knowledge base | `npx skills add eXodes/skills-workspace -s refactoring-guru` |
| **refactoring-ui**   | Expert advice on UI and visual design using the Refactoring UI knowledge base                             | `npx skills add eXodes/skills-workspace -s refactoring-ui`   |

### List available skills before installing

To see what skills are available in the repository:

```bash
npx skills add eXodes/skills-workspace -l
```

### Manual installation

If you prefer to install skills manually, you can copy the skill directory:

```bash
cp -r <skill-name> ~/.agents/skills/
```

Or install from the packaged archive in the workspace directory:

```bash
unzip <skill-name>-workspace/<skill-name>.skill -d ~/.agents/skills/<skill-name>/
```
