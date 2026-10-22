# Robust Process Criteria

> **Status:** criteria CR-1 to CR-5 defined — additional criteria pending incorporation (see summary table).

## Principle

A development process can meet the minimum reasonable quality criterion (`coaching-governance/guides/minimum-quality-criteria.md`) and still show signs of fragility: reviews that find nothing, implicit behavioral design that is undocumented, defects that are not recorded. The **robust process** is the next level: one in which quality practices produce consistent, verifiable, and self-explanatory evidence that they are working.

The fundamental distinction between minimum quality and robust process is that the robust process generates its own evidence of effectiveness. It is not enough to perform the practices; the practices must produce observable findings that confirm they were executed with rigor.

---

## Criteria

### CR-1 — Inspections are performed on critical products

The highest-risk artifacts of each productive phase are formally inspected by more than one reviewer before the phase concludes, following the selection criteria defined in `coaching-governance/guides/minimum-quality-criteria.md` §1.

In a robust process this is not optional or dependent on time pressure: if a critical artifact was not inspected, the coach documents a `secavo:QualityPlanningConcern` and escalates if the pattern repeats.

**Evidence the coach observes:**

- A `secav:ReviewRecord` exists for each critical artifact identified in the sprint.
- At least two reviewers participated in each inspection.
- Absence of inspection on a critical artifact → documented `secavo:QualityPlanningConcern`.

**SECAV-O:** `secav:DesignReview`, `secav:CodeReview`, `secav:UnitTestDesignReview`, `secav:ReviewRecord`, `secavo:QualityPlanningConcern`.

---

### CR-2 — Dynamic behavior is designed with UML activity or sequence diagrams

Any logic whose behavior varies according to control flow, actor interaction, or the order of messages between components must be explicitly modeled using at least one of the following UML diagrams:

- **Activity / flow diagram:** for process logic, workflows, algorithms with branches and loops.
- **Sequence diagram:** for interactions between components, services, actors, or layers in a defined temporal order.

The absence of these diagrams when behavior is dynamic amounts to implicit design: engineers must infer behavior from code, which increases the risk of integration defects, divergent interpretations, and review difficulty.

This criterion complements the state diagram standard in `coaching-governance/guides/design-documentation-standards.md`, which already establishes the requirement for state diagrams for entities with state-dependent behavior.

**When each diagram applies:**

| Situation | Required diagram |
|---|---|
| Process logic with branches (if/else, loops, guard conditions) | Activity / flow |
| Interaction between two or more components, services, or actors with message ordering | Sequence |
| Entity whose behavior depends on its internal state | State (`design-documentation-standards.md`) |
| Combinations of the above | One or more of the above, as applicable |

**Diagram quality criteria:**

An activity or sequence diagram is valid as an inspectable design artifact if it meets:

1. It is consistent with the code or specification it models — it is not decorative or out of date.
2. It covers the main flows and the most relevant alternative or error flows.
3. In activity diagrams: decision points have explicit guard conditions on all branches.
4. In sequence diagrams: each message includes the operation or event name; relevant return values are represented.
5. It is readable without needing to consult the code to interpret the flow.

The absence of a required diagram is a blocking finding in the design artifact review (`secav:ReviewFinding` of type `missingRequiredDiagram`). Systematic omission across multiple sprints triggers a `secavo:QualityPlanningConcern`.

**Evidence the coach observes:**

- `secav:DesignArtifact` includes an activity or sequence diagram when behavior is dynamic.
- The diagram is inspected as part of the `secav:ReviewRecord` of the design artifact.
- Review findings referencing inconsistencies or absences in the diagrams.

**SECAV-O:** `secav:DesignArtifact`, `secav:DesignReview`, `secav:ReviewFinding`, `secav:DesignActivity`, `secav:DesignCompetency`, `secavo:QualityPlanningConcern`.

---

### CR-3 — Defects resulting from inspections and reviews are documented

Every finding generated in an inspection or review is recorded in the tracking system with the minimum fields required by the metrics model:

- defect category;
- severity;
- phase where it was injected (`phaseInjected`);
- phase where it was detected (`phaseDetected`);
- affected artifact;
- associated engineering activity;
- correction action assigned with owner.

Defect documentation is not administrative paperwork: it is the data source that enables identifying injection patterns, evaluating review effectiveness, and calibrating coaching objectives. A process that conducts reviews but does not document findings cannot demonstrate that the reviews work.

**SECAV-O:** `secavo:DefectObservation` with `secavo:phaseInjected` and `secavo:phaseDetected`, `secav:ReviewFinding`, `secav:ReviewRecord`, `coaching-governance/guides/defect-tracking.md`.

---

### CR-4 and CR-5 — Individual reviews generate findings; where they do not, the coach issues a justified waiver

#### CR-4 — Reviews produce findings

An individual review that produces no findings is, in most cases, a signal of superficial review or insufficient preparation — not of a perfect artifact. The systematic absence of findings in individual reviews is the clearest indicator that the practice is being executed as a formality rather than as a quality activity.

In a robust process, reviews are expected to produce findings. The expected quantity depends on artifact complexity, reviewer experience, and process maturity, but **zero findings repeated across successive reviews without justification** is a pattern the coach must intervene in.

The coach observes the `secav:ReviewRecord` of each individual reviewer and evaluates whether the number and type of findings are consistent with the complexity of the reviewed artifact.

#### CR-5 — Coach waiver when the review produces no findings

When an individual review legitimately produces no findings — because the artifact was exhaustively corrected before review, because the reviewer has objective evidence that the artifact meets all acceptance criteria, or because the artifact is low-complexity with bounded scope — the coach issues a **waiver** that justifies the absence of findings.

The waiver documents:

1. **Identity of the artifact and reviewer.**
2. **Objective justification:** why the absence of findings is considered legitimate in this case (not an opinion; evidence must be referenced: prior correction history, reduced complexity, bounded scope, etc.).
3. **Validity criterion:** which acceptance criteria were verified and how.
4. **Coach signature** and date.

The waiver does not exempt the reviewer from the required preparation; it confirms that the coach verified that the absence of findings has an objective explanation. A waiver without objective justification is invalid.

**When NOT to issue a waiver:**

- The reviewer did not individually prepare the artifact before the session.
- The artifact is highly complex and there is no evidence of exhaustive preparation.
- The pattern of zero findings repeats in the same reviewer across multiple sprints without a changing justification.

In those cases, the coach records a `secav:CoachingIntervention` targeting the development of the engineer's review competency.

**SECAV-O (CR-4):** `secav:ReviewRecord`, `secav:ReviewFinding`, `secav:CompetencyAssessment`, `secav:ReviewCompetency`, `secav:CoachingIntervention`.

**SECAV-O (CR-5):** `secavo:CoachWaiver` *(proposed term — see §SECAV-O)*, `secav:ReviewRecord`.

---

## SECAV-O — proposed term

Criterion CR-5 introduces a new concept that requires representation in the ontology:

| Proposed term | Class / Property | Description |
|---|---|---|
| `secavo:CoachWaiver` | Class | Document issued by the coach that objectively justifies the absence of findings in an individual review. |
| `secavo:waiverJustification` | Data property (`xsd:string`) | Text of the objective waiver justification. |
| `secavo:waiverIssuedBy` | Object property → `secav:Coach` | Coach who issues the waiver. |
| `secavo:waiverForReviewRecord` | Object property → `secav:ReviewRecord` | The review record to which the waiver applies. |
| `secavo:waiverDate` | Data property (`xsd:date`) | Date of issuance. |

> These terms are proposed and must be added to `ontology/secav-o-coaching-governance-extension.ttl` when the criterion is incorporated into the framework baseline.

---

## Criteria summary (current status)

| ID | Criterion | Status |
|---|---|---|
| CR-1 | Inspections over critical products | Defined |
| CR-2 | Dynamic behavior designed with UML activity or sequence diagrams | Defined |
| CR-3 | Defects resulting from reviews documented | Defined |
| CR-4 | Individual reviews generate findings | Defined |
| CR-5 | Justified coach waiver when the review produces no findings | Defined |
| CR-6… | *(pending incorporation)* | Pending |

---

## Relationship to the framework quality scale

| Level | Description |
|---|---|
| **Below minimum** | Critical artifacts are not inspected. Defects accumulate between phases. |
| **Minimum reasonable quality** (`minimum-quality-criteria.md`) | Critical artifacts of each phase are inspected by more than one reviewer. |
| **Robust process** *(this document)* | Quality practices produce verifiable evidence of their effectiveness: documented findings, explicit behavioral design, justified waivers when reviews produce no findings. |
| **Aspirational quality** | Defined in `coaching-governance/guides/minimum-quality-criteria.md` — most or all artifacts of each phase are inspected; organizations mature toward this level incrementally. |

---

## Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/minimum-quality-criteria.md` | Previous quality level — framework floor |
| `coaching-governance/guides/design-documentation-standards.md` | State diagram standard — CR-2 complements it with activity and sequence diagrams |
| `coaching-governance/guides/formal-inspections.md` | Formal inspection protocol — basis for CR-1 |
| `coaching-governance/guides/peer-review-sessions.md` | Peer review protocol — basis for CR-4 and CR-5 |
| `coaching-governance/guides/requirements-inspection.md` | Requirements inspection — instance of CR-1 |
| `coaching-governance/guides/defect-tracking.md` | Defect recording — basis for CR-3 |
| `coaching-governance/docs/metrics-model.md` | Metrics model — interpretation of findings and trends |