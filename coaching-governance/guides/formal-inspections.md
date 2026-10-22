# Formal Inspections of Critical Modules

## Purpose

Not all system artifacts deserve the same level of scrutiny. Formal inspections are a structured review activity, more rigorous than an ordinary code review, applied selectively to modules that concentrate the greatest impact risk.

It is recommended that the system architect identify critical modules at the start of the project, and that formal inspections backed by the Technical Lead and management be planned for those modules, with the coach present as an observer.

---

## 1. The architect's role: identifying critical modules

The architect is who best understands the distribution of technical risk in the system. Their responsibility in this process is to identify, before development begins, which modules concentrate the greatest potential impact.

A **critical module** is one whose failure, defect, or degradation generates disproportionate consequences for the system or the business. Identification does not require unanimity — it requires documented technical judgment.

### 1.1 Criticality criteria

The architect may apply one or more of the following criteria to designate a module as critical:

| Criterion | Description |
|---|---|
| **Failure impact** | A defect in this module causes cascading failures, data loss, or service unavailability |
| **Breadth of use** | The module is invoked by many other components; a defect propagates widely |
| **Structural complexity** | High cyclomatic complexity, multiple execution paths, edge cases difficult to cover with automated tests |
| **Security or privacy** | Handles authentication, authorization, encryption, personal data, or sensitive information |
| **Data integrity** | Responsible for transactions, cross-system consistency, or referential integrity |
| **Novelty or uncertainty** | Technology new to the team, unproven design pattern in context, or ambiguous requirement |

The list of critical modules must be documented and shared with the Technical Lead, the coach, and management at the start of the project.

---

## 2. The formal inspection

A formal inspection is a structured review in which a group of participants with defined roles examines an artifact (`secav:SourceCodeArtifact` or other `secav:Artifact`) against explicit quality criteria (`secav:QualityCriterion`, `secav:AcceptanceCriterion`), with the goal of identifying defects before they advance to the next phase of development.

The difference from an ordinary code review is the degree of structure: defined roles, mandatory individual preparation, moderated meeting, and formal recording of findings (`secav:ReviewRecord`).

### 2.1 Process phases

| Phase | Responsible | Description |
|---|---|---|
| **1. Planning** | Coach + Technical Lead | Select the module to inspect, define participants, distribute the material in advance (at least 24–48 hours before the meeting). |
| **2. Individual preparation** | All participants | Each inspector reviews the artifact independently and notes observations, questions, and potential defects before the meeting. Individual preparation is mandatory — it cannot be substituted by reading during the meeting. |
| **3. Inspection meeting** | Designated moderator | Structured review of the artifact. The author listens and answers questions; they do not defend. The recorder documents findings (`secav:ReviewFinding`). The coach attends as a silent observer: takes notes, does not intervene verbally. |
| **4. Rework** | Author + Technical Lead | The author corrects identified defects. The Technical Lead may provide guidance when the correction requires design decisions. |
| **5. Follow-up** | Coach | The coach verifies that critical findings were corrected before the module advances. Corrections are recorded in the `secav:ReviewRecord`. |

---

## 3. Roles and responsibilities

| Role | Function in the inspection |
|---|---|
| **Architect** | Defines which modules are critical and why. May participate as an inspector in modules within their domain. |
| **Designated moderator** | Leads the meeting, maintains focus on the artifact and time per point. Is a team inspector designated for this role — not the coach. |
| **Module author** | Briefly presents the artifact. Listens and answers questions without defending design decisions during the meeting. |
| **Inspectors** | Engineers from the team or external parties with domain competence. They reviewed the material individually and bring documented observations. |
| **Recorder** | Documents findings (`secav:ReviewFinding`) during the meeting. May be one of the inspectors. |
| **Technical Lead** | Resolves technical ambiguities during the meeting and supports the author in the rework phase. Ensures the inspection has the necessary time and participants. |
| **Coach** | Attends as a silent observer. Does not participate or moderate. Takes observation notes used after the meeting for group or individual feedback. |
| **Management** | Authorizes the inspection time. Acknowledges findings as quality evidence — does not use them as an instrument for punitively evaluating the author's performance. |

---

## 4. Coach's role

The coach attends all inspection meetings — with the moderator, with the inspectors, with the author — as a silent observer. They do not participate verbally in any of them. They take notes and give feedback afterward.

- **Before the meeting:** verify that individual preparation was performed. If any participant did not prepare the material, coordinate with the Technical Lead to reschedule.
- **During the meeting:** observe and take notes. Does not intervene, moderate, or comment on findings. Records: who participates, how comments are framed (product vs. person), points of tension, agreements and disagreements.
- **After the meeting:** gives feedback — group if the pattern affects the entire team, individual if specific to a participant. Uses documented `secav:ReviewFinding` as evidence for `secav:CompetencyAssessment`.
- **Rework follow-up:** verifies that critical findings were corrected before the module advances. This verification can be done without a meeting — by reviewing the updated `secav:ReviewRecord`.
- **If the inspection reveals a systemic pattern** (the same type of defect appears in multiple modules): document a `secav:CoachingIntervention` or `secavo:ImprovementAction` directed at the team, not the individual author.

---

## 5. Management and Technical Lead support

Formal inspections are only effective when they have explicit backing from management and the Technical Lead:

**Management:**
- Include inspections in the project plan as quality activities with assigned time.
- Do not treat inspection findings as indicators of negative performance for the author — defects found before production are successes of the process, not failures of the individual.
- If management omits planned inspections without technical justification, the coach may document a `secavo:QualityPlanningConcern`.

**Technical Lead:**
- Participate in at least the planning phase and the meeting for the highest-risk modules.
- Ensure the team has capacity for individual preparation — preparation does not happen inside the meeting.
- Guide rework when findings involve broader design decisions.

---

## 6. Inspection outputs

| Output | Description | SECAV-O |
|---|---|---|
| Inspection record | Artifact, participants, findings, severity, correction status | `secav:ReviewRecord` |
| Documented findings | List of defects classified by type and severity | `secav:ReviewFinding` |
| Coach observation notes | Coach's observations during the meeting, basis for feedback | `secav:WorkProductEvidence` |
| Subsequent feedback | Group or individual, according to observed pattern | `secav:CoachingRecommendation` |
| Competency evidence | Findings used to inform competency assessment for author and inspectors | `secav:ReviewFinding` → `secav:CompetencyAssessment` |
| Coaching intervention | If there is a systemic pattern in findings | `secav:CoachingIntervention`, `secavo:ImprovementAction` |
| Quality concern | If the inspection was omitted or reduced without justification | `secavo:QualityPlanningConcern` |

---

## 7. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| Critical module under inspection | `secav:SourceCodeArtifact` (or `secav:Artifact`) |
| Inspection as activity | `secav:CodeReview` (formal code inspection); `secav:DesignReview` (design inspection) |
| Quality criteria evaluated | `secav:QualityCriterion`, `secav:AcceptanceCriterion` |
| Inspection record | `secav:ReviewRecord` (subclass of `secav:Artifact` and `secav:Evidence`) |
| Documented findings | `secav:ReviewFinding` (subclass of `secav:Evidence`) |
| Additional evidence produced | `secav:WorkProductEvidence` |
| Derived competency assessment | `secav:CompetencyAssessment` |
| Intervention for systemic pattern | `secav:CoachingIntervention`, `secavo:ImprovementAction` |
| Recommendation to the team | `secav:CoachingRecommendation` |
| Concern if inspection was omitted | `secavo:QualityPlanningConcern` |
| Risk documented if not performed | `secavo:Risk` |

---

## 8. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/project-kickoff-alignment.md` | Formal inspections must be included as quality activities in project objectives |
| `coaching-governance/docs/project-planning-participation.md` | The coach may raise a `QualityPlanningConcern` if inspections are omitted from the plan |
| `coaching-governance/guides/code-review-best-practices.md` | Basis for ordinary reviews; formal inspections apply a more rigorous standard |
| `coaching-governance/guides/ai-assisted-code-review.md` | Critical modules with AI-generated code require additional formal inspection |
| `templates/quality-planning-dissent-and-escalation.md` | Escalation mechanism if management eliminates planned inspections |
| `templates/engineer-coaching-assessment.md` | Inspection findings feed competency assessment |