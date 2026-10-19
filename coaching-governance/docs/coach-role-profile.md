# SECAV-O Coach Role Profile

## Purpose

This document defines the activity domains, responsibilities, and expected capabilities of a software engineering coach operating within the SECAV-O framework. It provides a reference for coach selection, onboarding, self-assessment, and committee calibration.

This profile describes what the coach does and must be able to do — not how to do it. Operational guidance for each domain is contained in the referenced guides and templates.

---

## Core Activity Domains

### 1. Quality Knowledge and Process Mastery

The coach holds formal knowledge of software production and quality control activities, including personal reviews, peer reviews, formal inspections, unit tests, and system and acceptance testing. This knowledge is not passive: the coach applies it to detect deviations in the actual use of quality and production processes, and intervenes when established practices are not being followed.

**Expected capabilities:**
- Recognize correct and incorrect execution of each quality activity type.
- Distinguish between a review, a peer review, and a formal inspection, and know when each is appropriate.
- Identify when production processes are being bypassed, weakened, or not documented.

**Key artifacts:** `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/unit-test-review.md`, `coaching-governance/guides/minimum-quality-criteria.md`

---

### 2. Instruction, Feedback, and Mentoring

The coach provides specialized instruction on quality issues, quality planning, best practices, programming logic development, algorithms, and mature software development methods. Instruction is adapted to the individual, team, or organizational level.

The coach gives positive, evidence-based feedback — at all three levels — that develops competency and promotes professional growth. Feedback is not limited to correction; it also reinforces observable strengths and attributes achievement explicitly to those responsible.

**Expected capabilities:**
- Deliver feedback that is specific, traceable to observable evidence, and developmentally oriented.
- Provide instruction calibrated to the recipient's current competency level.
- Distinguish between feedback that is appropriate in a group setting and feedback that must remain individual and confidential.

**Key artifacts:** `coaching-governance/docs/competency-growth-scale.md`, `templates/engineer-coaching-assessment.md`, `templates/engineer-development-record.md`, `coaching-governance/docs/coach-code-of-ethics.md`

---

### 3. Design Promotion and Process Improvement

The coach acts as a development consultant, reinforcing and promoting design as one of the highest-leverage mechanisms for reducing software defects. Design review — including state diagrams, architectural decisions, and interface contracts — is positioned as a quality activity comparable in rigor to code review.

The coach also supports improvement of organizational processes, including processes that are by-products of software engineering (documentation, defect tracking, review records). Improvement actions are proposed with evidence and tracked through the coaching cycle.

**Expected capabilities:**
- Explain the empirical relationship between early design investment and downstream defect reduction.
- Identify where missing or incomplete design artifacts increase risk.
- Propose and track organizational process improvements using the coaching improvement-action mechanism.

**Key artifacts:** `coaching-governance/guides/design-documentation-standards.md`, `coaching-governance/guides/code-review-best-practices.md`, `templates/coaching-backlog.csv`

---

### 4. Quality Planning and Risk Management

The coach establishes good practices for quality planning within a project, including the identification of quality risks and the formulation of preventive and corrective actions. This is not limited to advising; the coach participates formally in project planning, raises quality-planning concerns when material activities are omitted, and exercises the documented dissent and escalation protocol when needed.

**Expected capabilities:**
- Define a quality plan that maps engineering phases to required quality activities and artifacts.
- Identify quality risks and propose preventive and corrective actions traceable to specific failure modes.
- Exercise formal dissent and escalate when the residual quality risk is material and unresolved.

**Key artifacts:** `coaching-governance/docs/project-planning-participation.md`, `coaching-governance/guides/risk-management.md`, `templates/project-planning-quality-gate-review.md`, `templates/quality-planning-dissent-and-escalation.md`

---

### 5. Metrics and Project Success Criteria

The coach helps management, teams, and individual members define achievable, measurable, and time-bound quality objectives and success criteria. The coach does not impose metrics; it facilitates the negotiation of metrics that are meaningful, actionable, and resistant to gaming.

The coach collects and maintains quality metrics — defect rates, inspection yields, review coverage, test coverage, competency trends — as evidence to inform continuous improvement, not as instruments for ranking or punishment.

**Expected capabilities:**
- Distinguish a valid metric from a proxy that incentivizes undesirable behavior.
- Facilitate a structured objective-setting conversation at project, team, and individual levels.
- Maintain a metrics register and interpret trends over time.

**Key artifacts:** `coaching-governance/docs/metrics-model.md`, `coaching-governance/guides/project-kickoff-alignment.md`, `templates/metrics-register.csv`, `templates/defect-log.csv`, `templates/competency-trend.csv`

---

### 6. Architecture Quality Support

The coach helps architects understand and implement quality processes in architectural design. This includes integrating quality attributes — performance, resilience, integrity, and security — into the design process through planned quality activities, using techniques analogous to those applied in code implementation (e.g., design review checklists, quality attribute scenarios, architecture inspections).

The coach does not replace the architect's technical judgment; it ensures that the architectural design process includes explicit quality activities and that their outputs are inspected and tracked.

**Expected capabilities:**
- Identify which architectural artifacts require quality activities and at what level of formality.
- Recognize quality attribute scenarios and their relevance to inspection criteria.
- Facilitate architecture inspections using the formal inspection protocol.

**Key artifacts:** `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/design-documentation-standards.md`, `coaching-governance/guides/minimum-quality-criteria.md`

---

### 7. AI Adoption Guidance and Governance

The coach is the primary organizational consultant for the adoption of AI in software production processes. This involves two complementary responsibilities:

**Conceptual clarity:** The coach explains why AI-generated artifacts (code, tests, documentation, designs) do not replace but complement quality processes. The coach answers the "what" and "how" of responsible AI use: what validation is still required, how to review AI-generated output, and how to maintain human accountability.

**Adoption governance:** The coach monitors AI adoption at the individual, team, and organizational level, tracking the metrics associated with productivity, quality control, and planning. The coach identifies where AI adoption increases risk (e.g., reduced scrutiny of generated code, metric inflation) and proposes corrective controls.

**Expected capabilities:**
- Articulate the distinction between AI-assisted production and human-validated quality assurance.
- Define adoption metrics and thresholds appropriate to the team's maturity.
- Facilitate structured discussions about AI adoption decisions without dismissing or uncritically accepting AI tools.

**Key artifacts:** `coaching-governance/guides/ai-assisted-code-review.md`, `coaching-governance/guides/code-review-best-practices.md`, `coaching-governance/docs/coach-code-of-ethics.md` (§ Human accountability in AI-assisted work)

---

### 8. Organizational and Audit Collaboration

The coach actively participates with the organizational quality auditor to identify objectives and failures at any organizational level, and works with senior management toward continuous improvement. This participation is structured: the coach brings coaching evidence (competency assessments, defect records, inspection findings, metric trends) to audit-facing discussions.

**Expected capabilities:**
- Translate coaching observations into organizational-level findings relevant to the auditor's scope.
- Present coaching evidence in terms of measurable process outcomes, not individual assessments.
- Participate in continuous improvement planning at the senior management level when coaching data is relevant.

**Key artifacts:** `coaching-governance/docs/internal-audit-checklist.md`, `coaching-governance/docs/cmmi-mapping.md`, `coaching-governance/docs/institutional-alignment.md`, `templates/institutional-alignment-matrix.csv`

---

### 9. Facilitation and Leadership Support

The coach acts as a facilitator in team discussions, applying good leadership practices, supporting constructive conflict resolution, and contributing to decision-making throughout the development lifecycle. Facilitation is not protagonist-driven: the coach enables the team to reach its own conclusions rather than supplying answers.

This domain includes observing and coaching the team leader's facilitation behaviors, without substituting for the leader or assuming managerial authority.

**Expected capabilities:**
- Facilitate discussions where the coach's own view is not the primary input.
- Identify and address facilitation failures — dominant voices, suppressed dissent, unconsidered alternatives.
- Distinguish a leadership coaching intervention from a managerial directive.

**Key artifacts:** `coaching-governance/guides/coach-team-behaviors.md`, `coaching-governance/guides/retrospective-participation.md`, `coaching-governance/guides/peer-review-sessions.md`

---

## SECAV-O Mapping

| Activity Domain | SECAV-O Term |
|---|---|
| Quality knowledge and deviation detection | `secav:ReviewActivity`; `secav:ReviewFinding`; `secavo:QualityPlanningConcern` |
| Feedback and competency assessment | `secav:CompetencyAssessment`; `secav:CoachingRecommendation`; `secav:Evidence` |
| Specialized instruction | `secav:CoachingIntervention`; `secavo:ImprovementAction` |
| Design promotion | `secav:ReviewActivity` (design); `secav:ReviewFinding`; `secavo:QualityPlanningConcern` |
| Process improvement | `secavo:ImprovementAction`; `secavo:AnnualCoachingPlan`; `secavo:SprintPlan` |
| Quality planning and risk management | `secavo:Risk`; `secavo:PreventiveAction`; `secavo:CorrectiveAction`; `secavo:PlanningDecision` |
| Metrics and success criteria | `secav:Measurement`; `secav:AcceptanceCriterion`; `secavo:CoachingObjective` |
| Architecture quality support | `secav:ReviewActivity` (architectural); `secav:Artifact`; `secav:AcceptanceCriterion` |
| AI adoption governance | `secav:AISystem`; `secav:HumanValidationActivity`; `secavo:QualityPlanningConcern` |
| Audit and organizational collaboration | `secavo:GovernanceDecision`; `secavo:InstitutionalAlignment` |
| Facilitation and leadership support | `secav:CoachingIntervention`; `secav:Evidence`; `secavo:ImprovementAction` |

---

## Role Boundaries

The coach is not:

- **A manager.** The coach does not have authority over hiring, firing, promotion, or project decisions unless explicitly granted by the adopting organization.
- **A technical lead.** The coach does not own technical decisions. When promoting design or quality practices, the coach informs and challenges — it does not override.
- **An auditor.** The coach collaborates with the auditor but operates from a developmental, not compliance-enforcement, stance. The coach's primary obligation is to the engineer's growth.
- **An AI tool evaluator.** The coach's role in AI adoption is governance, adoption tracking, and quality assurance — not tool selection or technical benchmarking.

When a request or situation exceeds these boundaries, the coach escalates or refers to the appropriate authority, consistent with the Code of Ethics.

---

## Related Documents

| Document | Relation |
|---|---|
| `coaching-governance/docs/coach-code-of-ethics.md` | Ethical obligations that govern all coach activity domains |
| `coaching-governance/docs/coaching-cycle.md` | How activity domains are executed across annual planning and sprints |
| `coaching-governance/docs/coach-committee.md` | Multi-coach calibration and assignment against this profile |
| `coaching-governance/docs/competency-growth-scale.md` | Scale used to assess coach-facing competency dimensions |
| `coaching-governance/docs/metrics-model.md` | Metric definitions referenced in the planning and metrics domain |
| `coaching-governance/docs/project-planning-participation.md` | Formal planning participation and escalation protocol |
| `coaching-governance/docs/institutional-alignment.md` | Connecting coaching objectives to organizational objectives |
| `coaching-governance/guides/minimum-quality-criteria.md` | Defines the baseline quality bar the coach enforces across all phases |
| `coaching-governance/guides/incremental-adoption.md` | Adoption strategy when introducing the framework into a new organization |
| `templates/coach-ethics-acknowledgement.md` | Formal acknowledgement of the obligations in this profile |