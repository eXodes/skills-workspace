# Engineering Skill — Iteration 1 Benchmark

## Summary

| Metric                | With Skill | Without Skill | Delta        |
| --------------------- | ---------- | ------------- | ------------ |
| **Pass Rate**         | 94.4%      | 61.1%         | **+33.3 pp** |
| **Assertions Passed** | 17/18      | 11/18         | **+6**       |

## Per-Eval Breakdown

### Eval 1: Standup Routing

| Metric         | With Skill                                                  | Without Skill         | Delta  |
| -------------- | ----------------------------------------------------------- | --------------------- | ------ |
| Pass Rate      | 100% (3/3)                                                  | 67% (2/3)             | +33 pp |
| Key Difference | Explicitly loads `standup.md`                               | No reference citation |
| Quality        | Both produce good standups; skill adds routing transparency |

**Analysis:** Non-discriminating. Baseline can write good standups without reference guidance. Skill's value is primarily meta-level (showing which reference was used).

---

### Eval 2: PR Code Review Routing

| Metric         | With Skill                                                               | Without Skill                            | Delta  |
| -------------- | ------------------------------------------------------------------------ | ---------------------------------------- | ------ |
| Pass Rate      | 100% (4/4)                                                               | 50% (2/4)                                | +50 pp |
| Key Difference | Loads `code-review.md`; provides final verdict (Approve/Request Changes) | No verdict; offers to review actual diff |
| Critical Gap   | —                                                                        | Baseline omits structured review outcome |

**Analysis:** Moderate discriminator. Skill ensures structured verdict + reference loading. Baseline misses the "decision" piece.

---

### Eval 3: Deploy Checklist Routing

| Metric         | With Skill                                                                                                  | Without Skill                                                                                | Delta      |
| -------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ---------- |
| Pass Rate      | 100% (4/4)                                                                                                  | 25% (1/4)                                                                                    | **+75 pp** |
| Key Difference | Loads `deploy-checklist.md`; pre-committed rollback thresholds; service-specific checks (discovery, limits) | Generic checklist; reactive triggers; no service discovery                                   |
| Critical Gap   | —                                                                                                           | Baseline lacks "pre-committed thresholds" concept (decide before deploy, not under pressure) |

**Analysis:** Strong discriminator. Skill brings specialized guidance (microservice-specific, pre-committed thresholds) that baseline lacks entirely.

---

### Eval 4: Implicit Tech Debt Routing

| Metric         | With Skill                                                                                                                                   | Without Skill                                                           | Delta      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | ---------- |
| Pass Rate      | 100% (4/4)                                                                                                                                   | 25% (1/4)                                                               | **+75 pp** |
| Key Difference | Routes implicitly to `tech-debt.md`; applies quantitative scoring formula `(Impact + Risk) × (6 − Effort)` with thresholds (≥30, 15–29, <15) | General cost/benefit framing with no formula or scoring method          |
| Critical Gap   | —                                                                                                                                            | Baseline can't quantify refactor priority without the scoring framework |

**Analysis:** Strong discriminator. Skill's quantitative framework is the differentiator — enables decision-making beyond "assess pain."

---

### Eval 5: Incident Response Routing

| Metric         | With Skill                                                                                                                                                            | Without Skill                                                                                                     | Delta       |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ----------- |
| Pass Rate      | 100% (4/4)                                                                                                                                                            | 0% (0/4)                                                                                                          | **+100 pp** |
| Key Difference | Loads `incident-response.md`; covers Triage → Communicate → Mitigate → Postmortem phases; includes role assignment, communication template, 5 Whys, blameless framing | Covers immediate actions but omits: role assignment, communication template, 5 Whys, explicit blameless principle |
| Critical Gap   | —                                                                                                                                                                     | Baseline is operationally incomplete — missing structured incident management                                     |

**Analysis:** Strongest differentiator. Skill brings structured, blameless incident response that baseline cannot replicate without the reference.

---

### Eval 6: Out-of-Scope Routing (Negative Test)

| Metric         | With Skill                                                                      | Without Skill                                                        | Delta |
| -------------- | ------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ----- |
| Pass Rate      | 67% (2/3)                                                                       | 67% (2/3)                                                            | 0 pp  |
| Key Difference | Recognizes out-of-scope; loads no reference; but provides **no Python content** | No scope awareness; delivers concrete Python comparisons + resources |
| Critical Gap   | Skill correctly refuses to route but then abandons user with no helpful content |

**Analysis:** Both fail equally, but for opposite reasons. Skill's failure is a **skill authoring issue**: should acknowledge scope miss but still provide general knowledge (as baseline does).

---

## Recommendations for Iteration 2

### Critical

- **Fix Eval 6 behavior**: When routing fails (query is out-of-scope), provide fallback general knowledge rather than returning only a meta-explanation. Load no engineering reference, but still help.

### Medium Priority

- **Eval 1 assertions**: "Adds specificity" and "structures" are weak discriminators (both configs pass). Consider dropping or reframing to test only the explicit reference-loading value.
- **Consider reference content audit**: Eval 3's "pre-committed thresholds" concept and Eval 5's 5-Whys postmortem structure are where the skill shines. Ensure these are prominent in the reference files.

### Lower Priority

- Evals 2-5 show strong skill value (50–100% delta). Skill is working as intended for these cases.
