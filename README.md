# Skills Workspace

A repository for building and evaluating **agent skills** — reusable prompt modules that give agents specialised expertise for specific domains.

## What is a skill?

A skill is a `SKILL.md` file (with optional supporting reference files) that an agent loads to gain focused, deep knowledge about a topic. Skills tell the agent _when to activate_, _how to reason_, and _what reference material to consult_.

Skills are installed at `~/.agents/skills/<skill-name>/` and packaged as `.skill` zip archives for distribution.

## Skills

| Skill                                     | Purpose                                                                                              | Benchmark           |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------- | ------------------- |
| [**engineering**](#engineering)           | Software engineering guidance: standups, code review, architecture, debugging, deployment, incidents | 94% vs 61% (+33pp)  |
| [**pdf-viewer**](#pdf-viewer)             | Interactive PDF viewer: annotate, fill forms, sign, stamp — with live visual feedback                | 100% vs 11% (+89pp) |
| [**refactoring-guru**](#refactoring-guru) | Code quality, design patterns, and refactoring using the Refactoring Guru knowledge base             | 100% vs 61% (+39pp) |
| [**refactoring-ui**](#refactoring-ui)     | UI and visual design using the Refactoring UI knowledge base                                         | 100% vs 75% (+25pp) |
| [**strudel**](#strudel)                   | JavaScript live coding music in Strudel (Tidal Cycles port)                                          | 100% vs 91% (+9pp)  |

---

### engineering

Software engineering guidance and best practices. Routes to specialised references depending on task type.

**References**: standup, code-review, architecture, system-design, debug, deploy-checklist, incident-response, tech-debt, testing-strategy, documentation  
**Packaged**: `engineering-workspace/engineering.skill` (15.2KB)  
**Benchmark** (iteration 1): 94% with skill vs. 61% without (+33pp) across 6 evals. Strongest on deploy, tech debt, and incident response routing.

---

### pdf-viewer

Interactive PDF viewer skill. Opens documents in a live viewer and supports annotation, form-filling, and signature placement with real-time visual feedback. Does **not** trigger for pure text extraction or summarisation — routes those to the native Read tool.

**MCP server**: [`@modelcontextprotocol/server-pdf`](https://github.com/modelcontextprotocol/ext-apps/tree/main/examples/pdf-server) — the MCP Apps PDF server this skill is built for. Add to your MCP client config:

```json
{
  "mcpServers": {
    "pdf": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-pdf",
        "--stdio"
      ]
    }
  }
}
```

**Tools exposed**: `list_pdfs`, `display_pdf`, `interact` (navigate, annotate, search, extract, fill forms, save)  
**References**: view-pdf (core API), open, annotate, fill-form, sign  
**Packaged**: `pdf-viewer-workspace/pdf-viewer.skill` (8KB)  
**Benchmark** (iteration 1): 100% with skill vs. 11% without (+89pp) across 5 evals covering contract annotation, W-9 form filling, NDA signing, summarisation routing, and arXiv paper annotation.

---

### refactoring-guru

Code quality and design patterns advisor using the Refactoring Guru knowledge base. Identifies named code smells, recommends canonical refactoring techniques, and selects design patterns with reasoning.

**References**: code-smells, design-patterns, refactoring-techniques, pattern-selection-guide  
**Packaged**: `refactoring-guru-workspace/refactoring-guru.skill` (22KB)  
**Benchmark** (iteration 1): 100% with skill vs. 61% without (+39pp) across 3 evals covering code review, pattern selection, and smell+refactoring scenarios.

---

### refactoring-ui

UI and visual design advisor using the Refactoring UI knowledge base. Addresses visual hierarchy, colour palettes, typography, spacing, shadows, and empty states. Does **not** handle frontend framework implementation, CSS debugging, or animations.

**Packaged**: `refactoring-ui-workspace/refactoring-ui.skill`  
**Benchmark** (iteration 3): 100% with skill vs. 75% without (+25pp) across 7 evals.

---

### strudel

JavaScript live coding music expert for Strudel (Tidal Cycles port). Covers mini-notation, patterns, samples, synths, effects, and euclidean rhythms. Does **not** handle general JavaScript, DAWs, or music theory outside Strudel code.

**Packaged**: `strudel-workspace/strudel.skill`  
**Benchmark** (iteration 1): 100% with skill vs. 91% without (+9pp) across 8 evals. Largest gains on euclidean rhythm parameters, scale degree edge cases, and custom sample config.

---

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
    ├── README.md               # File index + benchmark summary
    ├── evals/
    │   └── evals.json          # Evaluation prompts and assertions
    ├── trigger-evals.json      # Trigger detection test cases
    ├── iteration-*/            # Benchmark results per iteration
    │   ├── benchmark.md        # Pass rate summary
    │   ├── benchmark.json      # Full machine-readable results
    │   └── eval-*/             # Per-eval run outputs + grading
    └── run_loop.log            # Description optimiser session log
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

### Install all skills

```bash
npx skills add eXodes/skills-workspace
```

### Install a specific skill

```bash
npx skills add eXodes/skills-workspace -s pdf-viewer
```

| Skill                | Install                                                      |
| -------------------- | ------------------------------------------------------------ |
| **engineering**      | `npx skills add eXodes/skills-workspace -s engineering`      |
| **pdf-viewer**       | `npx skills add eXodes/skills-workspace -s pdf-viewer`       |
| **refactoring-guru** | `npx skills add eXodes/skills-workspace -s refactoring-guru` |
| **refactoring-ui**   | `npx skills add eXodes/skills-workspace -s refactoring-ui`   |
| **strudel**          | `npx skills add eXodes/skills-workspace -s strudel`          |

### List available skills

```bash
npx skills add eXodes/skills-workspace -l
```

### Manual installation

```bash
# From source
cp -r <skill-name> ~/.agents/skills/

# From packaged archive
unzip <skill-name>-workspace/<skill-name>.skill -d ~/.agents/skills/<skill-name>/
```
