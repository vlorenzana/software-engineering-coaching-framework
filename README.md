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
- `docs/project-planning-participation.md` — coach participation in project planning, quality-gate advocacy, formal dissent and escalation.
- `docs/team-coaching-lifecycle.md` — coaching from team inception/launch through member preparation, baseline establishment and ongoing onboarding.
- `docs/coaching-cycle.md` — annual planning, sprint execution, retrospectives and replanning.
- `docs/risk-management.md` — coaching risk-management model.
- `docs/institutional-alignment.md` — method for connecting individual coaching objectives to institutional objectives.
- `docs/coach-code-of-ethics.md` — SECAV-O Code of Ethics for coaches.
- `docs/metrics-model.md` — defects, reviews, inspections, unit tests and competency-growth metrics.
- `docs/competency-growth-scale.md` — longitudinal competency maturity scale.
- `docs/code-review-best-practices.md` — evidence-based best practices for code review, covering reviewer and author responsibilities, feedback culture, AI-assisted code, and integration with coaching evidence.

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
- `templates/engineer-coaching-assessment.md` — coaching assessment/evidence template.
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
