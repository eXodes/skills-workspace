All skill files are in place at /Users/exodes/Projects/skills-workspace/engineering/:

┌─────────────────────────────────┬─────────────────────────────────────────────────────────┐
│ File                            │ Size                                                    │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ SKILL.md                        │ 3,504 chars — workflow, routing logic, reference index  │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/standup.md           │ 74 lines — daily standup updates from git/PR activity   │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/code-review.md       │ 117 lines — code review criteria (security, perf, style)│
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/architecture.md      │ 84 lines — architecture decision records & design       │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/system-design.md     │ 41 lines — system/API design, data models, boundaries   │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/debug.md             │ 94 lines — structured debugging (reproduce→diagnose)    │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/deploy-checklist.md  │ 77 lines — pre-deploy verification & rollback planning  │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/incident-response.md │ 157 lines — incident triage, comms, blameless PM        │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/tech-debt.md         │ 31 lines — identifying, categorizing, prioritizing      │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/testing-strategy.md  │ 32 lines — test design tradeoffs & coverage             │
├─────────────────────────────────┼─────────────────────────────────────────────────────────┤
│ references/documentation.md     │ 48 lines — API docs, runbooks, READMEs                  │
└─────────────────────────────────┴─────────────────────────────────────────────────────────┘

Packaged skill: /Users/exodes/Projects/skills-workspace/engineering-workspace/engineering.skill (15.2KB zip)

Benchmark (Iteration 1): 94.4% pass rate with skill vs. 61.1% without (+33.3pp) across 6 evals. Strongest on routing to specialized references (deploy, tech debt, incident response); weak discriminator on standup routing and out-of-scope fallback.
