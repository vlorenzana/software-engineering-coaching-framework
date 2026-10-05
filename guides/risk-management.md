# SECAV-O Coaching Risk Management

## Purpose

Risk management is part of the coaching plan rather than an administrative add-on. Each `secavo:AnnualCoachingPlan` maintains a risk register linked via `secavo:hasRisk`, and every `secavo:CoachingSprint` retrospective (`secavo:SprintRetrospective`) reviews whether risks changed, materialized, were mitigated, or require new actions via `secavo:reviewedInRetrospective`.

---

## Risk model

Each `secavo:Risk` should record:

| Field | Ontology term | Notes |
|---|---|---|
| Risk ID | — | Local identifier |
| Description | — | Plain-language statement of the risk |
| Category | — | e.g. evidence, quality, dependency, confidentiality |
| Cause / trigger | — | Condition that would cause the risk to materialize |
| Probability of occurrence | `secavo:riskProbability` | Qualitative or decimal value |
| Impact if it occurs | `secavo:riskImpact` | Qualitative or decimal value |
| Overall priority / exposure | — | Derived from probability × impact |
| Preventive action(s) | `secavo:hasPreventiveAction` → `secavo:PreventiveAction` | Actions to reduce probability |
| Corrective / contingency action(s) | `secavo:hasCorrectiveAction` → `secavo:CorrectiveAction` | Actions if risk materializes |
| Risk owner | `secavo:riskOwner` | Person responsible for monitoring and actions |
| Related coaching or institutional objective | `secavo:riskRelatedToObjective` → `secavo:CoachingObjective` | Traceability to the objective at risk |
| Status | `secavo:riskStatus` | e.g. open, mitigated, closed, materialized |
| Last review date | — | Date of most recent retrospective review |
| Evidence / notes | `secav:Evidence` | Supporting observation or measurement |

---

## Suggested qualitative scales

### Probability

| Level | Description |
|---|---|
| Low | Unlikely under current conditions. |
| Medium | Plausible and should be monitored. |
| High | Likely or already showing indicators. |

### Impact

| Level | Description |
|---|---|
| Low | Limited effect on a sprint objective or local activity. |
| Medium | Material effect on coaching progress, quality, evidence collection, or team objectives. |
| High | Could invalidate a key objective, create significant quality/security exposure, or materially impair the coaching plan. |

The framework may optionally use numeric scoring, but it does not prescribe a universal formula. Numeric values map to `secavo:riskProbability` and `secavo:riskImpact` as `xsd:decimal`.

---

## Preventive and corrective actions

**Preventive actions** (`secavo:PreventiveAction`) reduce the probability that a risk occurs. They are linked to the risk via `secavo:hasPreventiveAction`. Examples: clarifying `secav:AcceptanceCriterion`, scheduling peer reviews, providing training before a new activity, increasing `secav:ReviewActivity` frequency, or obtaining needed access early.

**Corrective / contingency actions** (`secavo:CorrectiveAction`) define what to do if the risk materializes. Linked via `secavo:hasCorrectiveAction`. Examples: changing the sprint objective, adding an independent reviewer (`secav:HumanValidationActivity`), introducing an additional `secav:TestingActivity`, escalating a dependency, or revising the baseline.

Both action types are specializations of `secav:CoachingIntervention` in the governance extension and may produce `secav:Evidence` that feeds the next `secav:CompetencyAssessment`.

---

## Retrospective integration

Every `secavo:SprintRetrospective` should answer:

1. Which `secavo:Risk` instances were reviewed? (via `secavo:reviewedInRetrospective`)
2. Did `secavo:riskProbability` or `secavo:riskImpact` change?
3. Which `secavo:PreventiveAction` instances were completed?
4. Did any risk materialize? Update `secavo:riskStatus`.
5. Were `secavo:CorrectiveAction` instances activated?
6. Were new risks discovered? Add them via `secavo:hasRisk` or `secavo:sprintHasRisk`.
7. Which risks carry forward to the next sprint?

---

## Coaching-specific risk examples

| Example risk | Relevant SECAV-O concept |
|---|---|
| Insufficient evidence to assess a competency | `secav:Evidence` / `secav:CompetencyAssessment` |
| Metrics that create misleading incentives | `secav:Measurement` |
| Late-phase defect recurrence | `secav:DefectRecord` |
| Lack of peer-review participation | `secav:ReviewActivity` / `secav:ReviewFinding` |
| Insufficient unit-test evidence | `secav:TestResult` / `secav:TestingActivity` |
| Over-reliance on AI-generated outputs without adequate human validation | `secav:HumanValidationActivity` / `secav:assistedByAI` |
| Lack of time or access to relevant engineering artifacts | `secav:Artifact` |
| Conflict between coaching objectives and institutional priorities | `secavo:riskRelatedToObjective` |
| Confidentiality or privacy constraints affecting evidence collection | `secav:Evidence` / ethics obligations |

---

## SECAV-O integration table

| Concept | Term | Namespace |
|---|---|---|
| Risk | `secavo:Risk` | governance extension |
| Annual plan holds risks | `secavo:hasRisk` (AnnualCoachingPlan → Risk) | governance extension |
| Sprint holds risks | `secavo:sprintHasRisk` (CoachingSprint → Risk) | governance extension |
| Preventive action | `secavo:PreventiveAction` | governance extension |
| Corrective action | `secavo:CorrectiveAction` | governance extension |
| Link risk → preventive action | `secavo:hasPreventiveAction` | governance extension |
| Link risk → corrective action | `secavo:hasCorrectiveAction` | governance extension |
| Link risk → retrospective | `secavo:reviewedInRetrospective` | governance extension |
| Link risk → coaching objective | `secavo:riskRelatedToObjective` | governance extension |
| Risk probability | `secavo:riskProbability` (xsd:decimal) | governance extension |
| Risk impact | `secavo:riskImpact` (xsd:decimal) | governance extension |
| Risk status | `secavo:riskStatus` (xsd:string) | governance extension |
| Risk owner | `secavo:riskOwner` (xsd:string) | governance extension |
| Supporting evidence / notes | `secav:Evidence` | core |
| Sprint retrospective | `secavo:SprintRetrospective` | governance extension |
| Coaching intervention (parent of actions) | `secav:CoachingIntervention` | core |

> **Namespace note:** `secavo:` refers to the governance extension (`ontology/secav-o-coaching-governance-extension.ttl`). `secav:` refers to the SECAV-O core ontology (`ontology/secav-o.ttl`). Both namespaces are currently set to `https://example.org/secav-o#`; they will be separated when the extension is merged into the canonical namespace.