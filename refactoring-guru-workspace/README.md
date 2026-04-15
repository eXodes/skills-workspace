All skill files are in place at ~/.agents/skills/refactoring-guru/:

┌─────────────────────────────────────────┬─────────────────────────────────────────────────────┐
│ File                                    │ Size                                                │
├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
│ SKILL.md                                │ 6,057 chars — workflow, vocabulary, reference index │
├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
│ references/design-patterns.md           │ 426 lines — all 22 GoF patterns                     │
├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
│ references/code-smells.md               │ 343 lines — all smell categories + treatments       │
├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
│ references/refactoring-techniques.md    │ 158 lines — all 6 technique groups                  │
├─────────────────────────────────────────┼─────────────────────────────────────────────────────┤
│ references/pattern-selection-guide.md   │ 173 lines — symptom→pattern decision guide          │
└─────────────────────────────────────────┴─────────────────────────────────────────────────────┘

Packaged skill: ~/.agents/skills/refactoring-guru-workspace/refactoring-guru.skill (22KB zip)

Benchmark: 100% pass rate with skill vs. 61.1% without (+39%) across 3 evals covering code review, pattern selection, and smell+refactoring scenarios.
