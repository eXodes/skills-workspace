# Skill Benchmark: strudel

**Model**: claude-sonnet-4.6
**Date**: 2026-04-21T10:41:57Z
**Evals**: 1, 2, 3, 4, 5, 6, 7, 8 (1 run each per configuration)

## Summary

| Metric | With Skill | Without Skill | Delta |
|--------|------------|---------------|-------|
| Pass Rate | 100% ± 0% | 90.6% ± 13.6% | +9.4pp |
| Time | 44.5s ± 12.5s | 18.8s ± 4.0s | +25.7s |

## Per-Eval Results

| Eval | Description | With Skill | Without Skill | Delta |
|------|-------------|-----------|--------------|-------|
| 1 | drum-beat | 4/4 (100%) | 4/4 (100%) | +0pp |
| 2 | euclidean-rhythm | 4/4 (100%) | 3/4 (75%) | **+25pp** |
| 3 | reverb-delay | 4/4 (100%) | 4/4 (100%) | +0pp |
| 4 | scale-notes | 4/4 (100%) | 3/4 (75%) | **+25pp** |
| 5 | multiply-replicate | 4/4 (100%) | 4/4 (100%) | +0pp |
| 6 | synth-bass | 4/4 (100%) | 4/4 (100%) | +0pp |
| 7 | custom-samples | 4/4 (100%) | 3/4 (75%) | **+25pp** |
| 8 | house-pattern | 5/5 (100%) | 5/5 (100%) | +0pp |

**Overall: 33/33 with skill vs 30/33 without skill**

## Analysis

### Where the skill wins

- **Eval 2 — Euclidean rhythm**: Baseline hedges on the optional offset parameter ("there may be additional parameters, check the docs"). The skill confidently names all three `(beats,segments,offset)` parameters with concrete examples like `s("bd(3,8,2)")`.

- **Eval 4 — Scale degrees**: Baseline hedges on large integers ("I'm not fully certain how large numbers behave"). The skill explicitly states any integer works, wrapping through the scale and adjusting octave, with examples for 0, negative, and large values.

- **Eval 7 — Custom samples**: Baseline vaguely mentions "a JSON config file" without naming `strudel.json`. The skill names the file exactly and explains the `_base` key format.

### Where baseline is competitive

Broad assertions like "provides runnable code" and "mentions sawtooth waveforms" are easy for any capable model. Evals 1, 3, 5, 6, and 8 test concepts documented widely enough in TidalCycles/Strudel that general AI holds up.

### Recommendation

Current assertions test the presence of concepts, not precision. To widen the delta:
- Add assertions for specific API names (`.lpenv()`, `.lpq()`, `.bank()`)
- Add assertions that verify mini-notation correctness (`[~ sd]*2` vs `~ sd ~ sd`)
- Add negative assertions that catch common hallucinations (wrong parameter names, fake functions)
