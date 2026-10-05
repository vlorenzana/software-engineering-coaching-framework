# SECAV-O Coaching Lifecycle, Planning, Risk, Alignment and Ethics Artifacts

This package extends the SECAV-O coaching operating model with six connected governance dimensions:

1. team coaching from team inception / planning / launch, including member preparation and onboarding;
2. annual coaching planning executed through Coaching Sprints;
3. risk management with preventive and corrective actions;
4. explicit alignment between coaching objectives and institutional objectives; and
5. a Code of Ethics for coaches; and
6. formal coach participation in project planning, quality advocacy, documented dissent and proportional escalation when material quality activities are omitted or weakened.

## Core cycle

Institutional / Project Objectives -> Project Planning & Quality Governance -> Team Inception & Launch -> Member Preparation -> Initial Baselines -> Annual Coaching Plan -> Risk Plan -> Coaching Sprint -> Evidence & Metrics -> Coaching Intervention -> Sprint Retrospective -> Risk Review -> Replanning -> Competency Trend -> New-Member Onboarding -> Institutional Alignment Review

## Included artifacts

### Operating model
- `coaching-governance/docs/project-planning-participation.md` — coach participation in project planning, quality-gate advocacy, formal dissent and escalation.
- `coaching-governance/docs/team-coaching-lifecycle.md` — coaching from team inception/launch through member preparation, baseline establishment and ongoing onboarding.
- `coaching-governance/docs/coaching-cycle.md` — annual planning, sprint execution, retrospectives and replanning.
- `coaching-governance/guides/retrospective-participation.md` — coach role in sprint retrospectives: facilitates when no Scrum Master is present; acts as silent observer when one is. In both modes, verifies that defect and quality data is analyzed and that concrete improvement actions are agreed. Post-session feedback: group, individual, or organizational escalation as needed.
- `coaching-governance/guides/defect-tracking.md` — coach closes bug tickets in the tracking system (Jira etc.) to collect consistent defect metrics (`secavo:DefectObservation`, `secavo:phaseInjected`, `secavo:phaseDetected`). When the coach is overloaded, a team member can be designated as Quality Assistant after training and under monitored supervision; the assistant role is also a coaching and competency development opportunity.
- `coaching-governance/guides/risk-management.md` — coaching risk-management model.
- `coaching-governance/guides/incremental-adoption.md` — strategic guide for incremental framework adoption using the Fail Fast philosophy: PoC, end-to-end tracer, short feedback loops, Go/Pivot/Stop decision criteria, and phased expansion from PoC to organization-wide adoption.
- `coaching-governance/docs/institutional-alignment.md` — method for connecting individual coaching objectives to institutional objectives.
- `coaching-governance/docs/coach-code-of-ethics.md` — SECAV-O Code of Ethics for coaches.
- `coaching-governance/docs/coach-committee.md` — governance model for multi-coach organizations: Coach Committee structure, Lead Coach designation (by management or coach consensus), committee responsibilities, assignment matrix, escalation, and proposed ontology extension.
- `coaching-governance/docs/metrics-model.md` — defects, reviews, inspections, unit tests and competency-growth metrics.
- `coaching-governance/docs/competency-growth-scale.md` — longitudinal competency maturity scale.
- `coaching-governance/guides/peer-review-sessions.md` — coach observation protocol during peer reviews: coach attends as silent note-taker only (no verbal participation), product-focused review culture, silent observation when team loses focus, and pending-point procedure for unresolved disagreements (mark pending → continue → escalate to Project Leader after the session).
- `coaching-governance/guides/formal-inspections.md` — structured formal inspections of critical system modules: architect identifies critical modules by risk criteria, coach moderates the inspection process (planning → individual preparation → inspection meeting → rework → follow-up), Technical Lead and management provide support. Outputs map to `secav:ReviewRecord`, `secav:ReviewFinding`, and `secav:CompetencyAssessment`.
- `coaching-governance/guides/project-kickoff-alignment.md` — pre-project alignment meeting between the Technical Lead, Coach, and senior management: establishing few but measurable project success objectives (at least one quality/defect metric required), team objectives (may be more aggressive), individual objectives, and the coach's role in preventing goal dilution.
- `coaching-governance/guides/coach-team-behaviors.md` — team leader behaviors the coach observes: facilitation vs. protagonist role, consensus-based decision-making, building plans the team genuinely believes in, participatory risk management, capability-based work assignment, and respectful team culture. Includes a per-sprint observation checklist and SECAV-O mapping from observed behaviors to coaching interventions.
- `coaching-governance/guides/code-review-best-practices.md` — evidence-based best practices for code review, covering reviewer and author responsibilities, feedback culture, AI-assisted code, and integration with coaching evidence.
- `coaching-governance/guides/ai-assisted-code-review.md` — guidance for reviewing AI-assisted code and using AI tools in the review pipeline, including risk triage, false-positive management, data privacy, and SECAV-O integration.

### Templates
- `templates/project-planning-quality-gate-review.md` — planning-time review of required quality activities and evidence.
- `templates/quality-planning-dissent-and-escalation.md` — formal quality concern, dissent, management response and escalation record.
- `templates/team-launch-coaching-plan.md` — launch/planning artifact for team objectives, project context, risks, member preparation and initial coaching baselines.
- `templates/member-preparation-checklist.md` — readiness checklist before team launch.
- `templates/new-member-onboarding.md` — structured onboarding for members joining after launch, including project context, objectives, risks and growth baseline.
- `templates/annual-coaching-plan.md` — annual plan with institutional alignment and annual risk plan.
- `templates/coaching-sprint-plan.md` — sprint planning/replanning, including sprint risk review.
- `templates/sprint-retrospective.md` — retrospective with objective, metric and risk follow-up.
- `templates/risk-register.csv` — risk register including probability, impact, preventive and corrective actions.
- `templates/institutional-alignment-matrix.csv` — mapping between institutional and coaching objectives.
- `templates/coach-ethics-acknowledgement.md` — acknowledgement of coaching ethics obligations.
- `templates/coach-committee-charter.md` — charter template for the Coach Committee: members, Lead Coach designation, decision rules, assignment matrix, conflict-of-interest declarations, and ethics acknowledgement tracking.
- `templates/engineer-coaching-assessment.md` — coaching assessment/evidence template.
- `templates/engineer-development-record.md` — **(proposal)** longitudinal engineer development record spanning multiple cycles and coaches, with competency tracking, session log, 360 feedback, coach handoffs, and organizational indicators.
- `templates/organizational-competency-view.csv` — **(proposal)** aggregated organizational view: one row per engineer per cycle, enabling team-level competency averages, objective progress, and promotion/retention risk flags.
- `examples/example-engineer-development-record.md` — **(proposal)** fully completed example of the engineer development record (fictional engineer Valeria Montes, including a coach change in July).
- `templates/metrics-register.csv` — metric collection register.
- `templates/defect-log.csv` — defect phase-injected / phase-detected log.
- `templates/competency-trend.csv` — competency progression tracker.
- `templates/coaching-backlog.csv` — coaching improvement-action tracker.

### Machine-readable artifacts
- `schemas/project-planning-governance.schema.json` — machine-readable project-planning quality-governance record.
- `examples/example-quality-planning-escalation.yaml` — worked dissent/escalation example.
- `schemas/team-coaching-lifecycle.schema.json` — JSON Schema for team launch/preparation/onboarding records.
- `examples/example-team-launch-and-onboarding.yaml` — worked lifecycle example.
- `ontology/secav-o-coaching-governance-extension.ttl` — OWL-aligned extension for planning, risks, alignment, ethics, metrics and retrospectives.
- `ontology/alignment-matrix.csv` — explicit mapping between extension terms and SECAV-O core concepts.
- `validation/secav-o-coaching-governance.shacl.ttl` — SHACL constraints for annual plans, objectives, risks, retrospectives and ethics acknowledgements.
- `schemas/coaching-sprint.schema.json` — JSON Schema for coaching sprint records with alignment and risk fields.
- `examples/example-coaching-sprint.yaml` — worked example.

## Governance principles

- Coaching objectives should be traceable to an institutional, team, quality, engineering, security, workforce, or learning objective where appropriate.
- Risk management is part of the annual plan and is reviewed during every sprint retrospective.
- Each risk records probability, impact, preventive actions, corrective/contingency actions, owner, status and review history.
- Coaching metrics are evidence for improvement, not instruments for punishment or isolated performance ranking.
- Coaches must protect confidentiality, avoid conflicts of interest, distinguish evidence from opinion, and preserve engineer dignity and professional autonomy.

## Claim boundary

These artifacts define an operating and governance model. They do not claim that the metrics are validated predictors of engineer performance, that any numeric target is universally appropriate, or that SECAV-O has been independently validated, standardized, or adopted by third parties.


## Ontology alignment note

Version 5 explicitly aligns coaching governance with the SECAV-O core pattern: Engineering Activity -> Artifact -> Competency -> Acceptance Criteria -> Evidence/Measurement -> Coaching Intervention. Baselines, observations and competency trends are modeled as Evidence; ImprovementAction is modeled as a CoachingIntervention specialization; CoachingObjectives target Competencies; CoachingSprints observe EngineeringActivities and collect Artifact/Evidence/Metric information.

The namespace in this standalone package is still `https://example.org/secav-o#`. Replace it with the canonical namespace from the core `ontology/secav-o.ttl` before merge, and reuse the exact core class identifiers rather than duplicating equivalent terms.


## Planning participation and quality advocacy

Version 5 adds a formal governance role for the coach in project planning. The recommended model gives the coach an explicit voice in planning and, when granted by the adopting organization, a vote on decisions that materially affect quality, competency development and human validation. The coach can raise a documented quality-planning concern when reviews, peer reviews, inspections, unit-test activities or other material quality controls are omitted or weakened. If the residual risk remains material, the coach can record formal dissent and escalate through the defined management chain. SECAV-O does not create legal or managerial authority by itself and does not assume a universal veto right; actual decision rights are defined by each adopting organization.
