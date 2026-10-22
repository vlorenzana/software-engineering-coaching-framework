# Project Objective Alignment: Pre-Start Meeting

## Purpose

Before starting a project, a meeting is recommended between the **Technical Lead**, the **Coach**, and the **senior management responsible** to establish the measurable objectives that will define the project's success. This meeting sets the reference point against which the team's progress and coaching results will be measured.

Without this explicit alignment, objectives remain implicit or scattered; the team optimizes for what they perceive they will be evaluated on, and the coach has no agreed basis to guide coaching interventions.

---

## 1. Participants

| Role | Function in the meeting |
|---|---|
| **Senior management responsible** | Defines and validates the project's organizational objectives (`secavo:InstitutionalObjective`, `secavo:ProjectObjective`). Authorizes resource and deadline commitments. |
| **Technical Lead** | Translates organizational objectives into achievable technical and operational goals. Identifies technical constraints that affect goal definition. |
| **Coach** | Verifies that objectives are measurable and traceable. Proposes at least one software quality objective if none has been included. Connects project objectives with the cycle coaching plan (`secavo:AnnualCoachingPlan`). |

---

## 2. Criteria for project objectives

### 2.1 Few, but meaningful

Project objectives must be few — sufficient to guide work without dispersing focus. An excessive number of objectives dilutes attention and makes real accountability impossible.

### 2.2 Measurable and verifiable

Each objective must be evaluable with observable data at project close:

- What metric represents it? (`secavo:Metric`)
- What is the success threshold?
- How and when is it measured? (`secavo:MeasurementObservation`)

### 2.3 At least one software quality objective

It is recommended that at least one of the objectives agreed with management be explicitly related to defects or software quality. Measurable examples:

| Quality objective | SECAV-O term |
|---|---|
| Production defect rate below a threshold | `secavo:DefectObservation` + threshold in `secavo:Metric` |
| Percentage of changes covered by code review | `secavo:ReviewObservation` + threshold in `secavo:Metric` |
| Percentage of defects detected in review (vs. in production) | `secavo:DefectObservation` by phase (`templates/defect-log.csv`) |
| Mean resolution time for critical defects | `secavo:Metric` of time; observed in `secavo:MeasurementObservation` |

Including a quality objective ensures that engineering quality has explicit representation in project commitments — not just as technical debt managed after the fact.

---

## 3. Team objectives

Once objectives are established with management, the team may set their own internal objectives. These **can be more aggressive** than management commitments — they are excellence goals, not the floor of the contract.

The coach facilitates this session and verifies that:

- Team objectives are aligned with management commitments and meet or exceed them.
- **The coach does not allow team objectives less demanding than those agreed with management.** If the team proposes weaker goals, the coach identifies the discrepancy and facilitates revision.
- The team understands the difference between the organizational commitment (agreed minimum) and their internal aspiration (excellence goal).

---

## 4. Individual objectives

Analogously, each engineer may establish individual objectives aligned with the team's. These may also be more aggressive — personal development goals connected to the competencies the project will demand.

The coach is responsible for:

- Verifying that individual objectives are connected to the competencies required by the project (`secav:CompetencyAssessment` as baseline).
- **Not allowing individual objectives less demanding than the expected contribution to the team.** If an individual objective is below the minimum expected contribution, the coach identifies this in the individual planning session.
- Documenting individual objectives in the cycle coaching plan (`secavo:AnnualCoachingPlan`, `secavo:CoachingObjective`).

---

## 5. Coach's role in the management meeting

The coach is not a spectator in this meeting. Their specific responsibilities are:

- **Verify that each proposed objective is measurable.** If an objective cannot be answered with observable data, they identify this in the moment — not afterward.
- **Propose or request at least one quality objective.** If none of the proposed objectives includes a defect or software quality dimension, the coach introduces it as a framework requirement.
- **Record the agreed objectives** as `secavo:CoachingObjective` linked to `secavo:ProjectObjective` via `secavo:alignsWithProjectObjective`, and to `secavo:InstitutionalObjective` via `secavo:alignsWithInstitutionalObjective`.
- **Not allow objective dilution.** If during the meeting commitments are weakened without valid technical justification, the coach may document a formal planning concern (`secavo:QualityPlanningConcern`) following the mechanism in `templates/quality-planning-dissent-and-escalation.md`.

---

## 6. Expected outputs of the meeting

| Output | Where it is recorded |
|---|---|
| Organizational project objectives (few, measurable, with at least one quality objective) | `templates/annual-coaching-plan.md` §Institutional alignment |
| Metrics and success thresholds for each objective | `templates/metrics-register.csv` |
| Team objectives (equal to or more aggressive than organizational ones) | `templates/annual-coaching-plan.md` §Team objectives |
| Individual objectives per engineer | `templates/engineer-development-record.md` §Competency plan |
| Record of formal concern if objectives were diluted | `templates/quality-planning-dissent-and-escalation.md` |

---

## 7. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| Organizational project objective | `secavo:ProjectObjective` |
| Institutional objective (organization level) | `secavo:InstitutionalObjective` |
| Coaching objective derived from the project | `secavo:CoachingObjective` |
| Alignment coaching objective ↔ project | `secavo:alignsWithProjectObjective` |
| Alignment coaching objective ↔ institutional | `secavo:alignsWithInstitutionalObjective` |
| Success metric | `secavo:Metric` |
| Defect measurement as quality objective | `secavo:DefectObservation` (subclass of `secavo:MeasurementObservation`) |
| Code review measurement | `secavo:ReviewObservation` (subclass of `secavo:MeasurementObservation`) |
| Individual competency baseline | `secav:CompetencyAssessment` |
| Formal concern if objectives are diluted | `secavo:QualityPlanningConcern` |
| Updated coaching plan | `secavo:AnnualCoachingPlan` |
| Documented planning decision | `secavo:PlanningDecision` |

---

## 8. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/docs/project-planning-participation.md` | Formal coach participation in planning and escalation |
| `coaching-governance/docs/institutional-alignment.md` | Method for connecting coaching objectives with institutional objectives |
| `templates/annual-coaching-plan.md` | Plan where agreed objectives are recorded |
| `templates/quality-planning-dissent-and-escalation.md` | Formal mechanism if objectives are diluted without justification |
| `templates/metrics-register.csv` | Record of agreed metrics and thresholds |
| `templates/defect-log.csv` | Defect log for quality objectives |
| `templates/engineer-development-record.md` | Record of individual objectives per engineer |