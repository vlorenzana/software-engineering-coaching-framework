# Defect Tracking and Quality Assistant Role

## Purpose

When the team has a ticket tracking system — such as Jira, Azure DevOps, Linear, or an equivalent — closing tickets related to defects (bugs) is the coach's responsibility. This practice allows defect metrics to be collected consistently and traceably, feeding the `secavo:DefectObservation` and the `templates/defect-log.csv`.

If the coach is overloaded, they may delegate this activity to a previously trained team member under supervision, formally designating them as a **Quality Assistant**.

---

## 1. Why the coach closes defect tickets

The coach closes defect tickets — not the author who corrected them nor the reporter who opened them. The reason is twofold:

**Classification consistency.** Each defect must be recorded with the phase in which it was injected (`secavo:phaseInjected`) and the phase in which it was detected (`secavo:phaseDetected`). Without a single classification criterion, these phases are recorded inconsistently and the resulting metrics are not comparable across sprints or teams.

**Metric integrity.** If the person closing the ticket is also the one who corrected it, there is an implicit incentive to classify it favorably. The coach is a neutral observer who applies the agreed definition of each phase.

The coach does not need to technically reproduce or verify the correction — their role when closing the ticket is to record the defect classification: type, severity, injection phase, detection phase, and detection method (`secavo:detectionMethod`).

---

## 2. Data to record when closing a defect ticket

| Field | Description | SECAV-O |
|---|---|---|
| Injection phase | In which development phase the defect was introduced (requirements, design, coding, testing) | `secavo:phaseInjected` |
| Detection phase | In which phase it was found (code review, unit testing, integration, production) | `secavo:phaseDetected` |
| Detection method | How it was found (formal inspection, peer review, automated test, user report) | `secavo:detectionMethod` |
| Severity | Functional impact of the defect (critical, major, minor, cosmetic) | `secavo:DefectObservation` |
| Module or component | For defect density analysis by module | `secav:SourceCodeArtifact` |

These data are transferred to `templates/defect-log.csv` at the end of each sprint as part of metric collection (`secavo:collectsMetric`).

---

## 3. Metrics obtained from ticket closure

Systematic defect recording allows calculating:

| Metric | Description |
|---|---|
| **Defects per sprint** | Total volume of defects detected in the cycle |
| **Escape rate** | Percentage of defects found in production vs. in prior phases |
| **Density by module** | Defects per module — identifies higher-risk components |
| **Review effectiveness** | Percentage of defects detected in code review or formal inspection |
| **Distribution by injection phase** | Indicates whether defects originate primarily in design, coding, or requirements |

These metrics are reviewed in each `secavo:SprintRetrospective` and feed the `templates/metrics-register.csv` and the quality objectives agreed upon at the pre-start meeting (`coaching-governance/guides/project-kickoff-alignment.md`).

---

## 4. Quality Assistant: delegation when the coach is overloaded

When the coach cannot sustain ticket closure on an ongoing basis — for example, if they manage multiple teams simultaneously — they may delegate this activity to a team member designated as a **Quality Assistant**.

This delegation is not automatic. It requires:

1. **Prior training** — the coach trains the assistant in defect classification: phase definitions, severity criteria, detection method, and use of the ticketing system.
2. **Initial supervision** — for at least two sprints, the coach reviews and validates the closures made by the assistant before considering them final.
3. **Formal designation** — the coach documents the Quality Assistant's designation in the cycle coaching plan (`templates/annual-coaching-plan.md`), including the scope of the delegation and the supervision period.

### 4.1 Quality Assistant responsibilities

| Responsibility | Description |
|---|---|
| Closing defect tickets | Applies the agreed classification criteria; does not close if they have doubts about the phase or cause |
| Recording in the defect log | Transfers data to `templates/defect-log.csv` at the end of each sprint |
| Consulting the coach | Escalates to the coach any defect that does not clearly fit the established criteria |
| Reporting anomalies | Informs the coach when they detect unusual patterns in defect volume or type |

### 4.2 What the Quality Assistant does NOT do

- Does not define or modify classification criteria — that is the coach's responsibility.
- Does not close tickets that are not defects (tasks, improvements, change requests).
- Does not make decisions about the severity of critical defects without consulting the coach.
- Does not report metrics directly to management — the coach consolidates and communicates.

### 4.3 The assistant as a development opportunity

The designation as Quality Assistant is also a coaching intervention. The engineer who assumes this role develops competencies in:

- Understanding the defect lifecycle and its impact on product quality.
- Analyzing defect patterns — a signal of `secav:ReviewCompetency` and `secav:DesignCompetency`.
- Discipline in recording and classifying evidence (`secav:DefectRecord`).

The coach may use the assistant's experience as evidence for the cycle's `secav:CompetencyAssessment`.

---

## 5. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| Defect recorded when closing the ticket | `secav:DefectRecord` (subclass of `secav:Evidence`) |
| Defect observation with phase and method | `secavo:DefectObservation` (subclass of `secavo:MeasurementObservation`) |
| Defect injection phase | `secavo:phaseInjected` |
| Defect detection phase | `secavo:phaseDetected` |
| Detection method | `secavo:detectionMethod` |
| Sprint defect metric | `secavo:Metric`; collected in `secavo:CoachingSprint` |
| Metric collection | `secavo:collectsMetric` (domain: `secavo:CoachingSprint`) |
| Module where defect originated | `secav:SourceCodeArtifact` |
| Quality assistant training | `secav:CoachingIntervention` |
| Competencies developed by the assistant | `secav:CompetencyAssessment` on `secav:ReviewCompetency`, `secav:DesignCompetency` |

---

## 6. Related documents

| Document | Relationship |
|---|---|
| `templates/defect-log.csv` | Log where data from each closed ticket is consolidated |
| `templates/rca-defect-analysis.md` | Root Cause Analysis (RCA) template for P1/P2 defects — complements each log row with the 5-Whys chain and corrective/preventive action plan |
| `templates/metrics-register.csv` | Defect metrics by sprint |
| `templates/annual-coaching-plan.md` | Where the Quality Assistant designation is documented |
| `coaching-governance/guides/project-kickoff-alignment.md` | Agreed quality objectives define the defect metric thresholds |
| `coaching-governance/guides/formal-inspections.md` | Formal inspections are a defect detection method before production |
| `coaching-governance/docs/metrics-model.md` | Complete model of defect, review, and inspection metrics |