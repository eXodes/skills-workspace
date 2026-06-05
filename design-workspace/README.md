# design-workspace

Development artefacts for the `design` skill.

## Benchmark

| Metric                   | Target  |
| ------------------------ | ------- |
| Pass rate with skill     | ≥ 90%   |
| Delta over baseline      | ≥ +20pp |
| Trigger precision/recall | ≥ 95%   |

_Not yet benchmarked — run iteration-1 to establish baseline._

## File Index

| File                 | Purpose                                                           |
| -------------------- | ----------------------------------------------------------------- |
| `design.skill`       | Packaged zip — install via `npx skills add` or manual unzip       |
| `evals/evals.json`   | 4 evals covering critique, UX copy, research synthesis, handoff   |
| `trigger-evals.json` | 20 trigger cases (10 true, 10 false) for description optimization |
| `README.md`          | This file                                                         |

## Skill Coverage

| Reference                 | Eval covered       |
| ------------------------- | ------------------ |
| `design-critique.md`      | eval 1             |
| `ux-copy.md`              | eval 2             |
| `research-synthesis.md`   | eval 3             |
| `design-handoff.md`       | eval 4             |
| `accessibility-review.md` | trigger evals only |
| `design-system.md`        | trigger evals only |
| `user-research.md`        | trigger evals only |

## Install

```bash
# From packaged archive
unzip design-workspace/design.skill -d ~/.agents/skills/design/

# Via npx (once published)
npx skills add eXodes/skills-workspace -s design
```
