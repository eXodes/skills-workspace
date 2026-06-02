All skill files are in place at pdf-viewer/:

┌──────────────────────────────────────┬────────────────────────────────────────────────────────────────────┐
│ File                                 │ Size                                                               │
├──────────────────────────────────────┼────────────────────────────────────────────────────────────────────┤
│ SKILL.md                             │ 3,583 chars / 55 lines — trigger description, reference table,     │
│                                      │ quick decision guide                                               │
├──────────────────────────────────────┼────────────────────────────────────────────────────────────────────┤
│ references/view-pdf.md               │ 6,240 chars / 147 lines — full tool API (display_pdf, interact),   │
│                                      │ annotation types, coordinate system — always-load core reference   │
├──────────────────────────────────────┼────────────────────────────────────────────────────────────────────┤
│ references/open.md                   │ 1,109 chars / 29 lines — opening workflow, supported sources,      │
│                                      │ when NOT to use viewer                                             │
├──────────────────────────────────────┼────────────────────────────────────────────────────────────────────┤
│ references/annotate.md               │ 1,865 chars / 46 lines — collaborative annotation workflow,        │
│                                      │ batch patterns, tips                                               │
├──────────────────────────────────────┼────────────────────────────────────────────────────────────────────┤
│ references/fill-form.md              │ 2,856 chars / 68 lines — form-filling workflows (user-driven vs    │
│                                      │ AI-assisted), unnamed field handling                               │
├──────────────────────────────────────┼────────────────────────────────────────────────────────────────────┤
│ references/sign.md                   │ 1,809 chars / 49 lines — signature/initials placement workflow,    │
│                                      │ coordinate tips                                                    │
└──────────────────────────────────────┴────────────────────────────────────────────────────────────────────┘

Packaged skill: pdf-viewer-workspace/pdf-viewer.skill (8KB zip)

Benchmark: 100% pass rate with skill vs. 11% without (+89%) across 5 evals covering contract annotation, form filling, signing, summarization routing, and arXiv paper annotation.
