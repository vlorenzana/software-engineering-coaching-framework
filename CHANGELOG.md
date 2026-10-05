# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added

- `docs/code-review-best-practices.md` — evidence-based best practices for code review (reviewer and author responsibilities, size limits, feedback culture, AI-assisted code, coaching integration). Sources: Google Engineering Practices, Microsoft Code with Engineering Playbook, SmartBear/Cisco peer review research.
- `docs/ai-assisted-code-review.md` — dedicated guidance for AI-assisted code review: context data, layered pipeline, risk triage, false-positive management, data privacy, SECAV-O integration. 13 sources including Google AutoCommenter study and Faros AI data.

### Added — Coaching Governance Extension (v5)

**Operating model documents**
- `docs/project-planning-participation.md` — coach participation in project planning, quality-gate advocacy, formal dissent and escalation.
- `docs/team-coaching-lifecycle.md` — coaching from team inception/launch through member preparation, baseline establishment and ongoing onboarding.
- `docs/coaching-cycle.md` — annual planning, sprint execution, retrospectives and replanning.
- `docs/risk-management.md` — coaching risk-management model.
- `docs/institutional-alignment.md` — method for connecting individual coaching objectives to institutional objectives.
- `docs/coach-code-of-ethics.md` — SECAV-O Code of Ethics for coaches.
- `docs/metrics-model.md` — defects, reviews, inspections, unit tests and competency-growth metrics.
- `docs/competency-growth-scale.md` — longitudinal competency maturity scale.
- `docs/ontology-alignment.md` — explicit alignment between extension terms and SECAV-O core concepts.

**Templates**
- `templates/project-planning-quality-gate-review.md` — planning-time review of required quality activities and evidence.
- `templates/quality-planning-dissent-and-escalation.md` — formal quality concern, dissent, management response and escalation record.
- `templates/team-launch-coaching-plan.md` — launch/planning artifact for team objectives, project context, risks, member preparation and initial coaching baselines.
- `templates/member-preparation-checklist.md` — readiness checklist before team launch.
- `templates/new-member-onboarding.md` — structured onboarding for members joining after launch.
- `templates/annual-coaching-plan.md` — annual plan with institutional alignment and annual risk plan.
- `templates/coaching-sprint-plan.md` — sprint planning/replanning, including sprint risk review.
- `templates/sprint-retrospective.md` — retrospective with objective, metric and risk follow-up.
- `templates/coach-ethics-acknowledgement.md` — acknowledgement of coaching ethics obligations.
- `templates/engineer-coaching-assessment.md` — coaching assessment/evidence template.
- `templates/risk-register.csv` — risk register including probability, impact, preventive and corrective actions.
- `templates/institutional-alignment-matrix.csv` — mapping between institutional and coaching objectives.
- `templates/metrics-register.csv` — metric collection register.
- `templates/defect-log.csv` — defect phase-injected / phase-detected log.
- `templates/competency-trend.csv` — competency progression tracker.
- `templates/coaching-backlog.csv` — coaching improvement-action tracker.

**Machine-readable artifacts**
- `schemas/project-planning-governance.schema.json` — JSON Schema for project-planning quality-governance records.
- `schemas/team-coaching-lifecycle.schema.json` — JSON Schema for team launch/preparation/onboarding records.
- `schemas/coaching-sprint.schema.json` — JSON Schema for coaching sprint records with alignment and risk fields.
- `examples/example-quality-planning-escalation.yaml` — worked dissent/escalation example.
- `examples/example-team-launch-and-onboarding.yaml` — worked lifecycle example.
- `examples/example-coaching-sprint.yaml` — worked coaching sprint example.
- `ontology/secav-o-coaching-governance-extension.ttl` — OWL-aligned extension for planning, risks, alignment, ethics, metrics and retrospectives.
- `ontology/alignment-matrix.csv` — mapping between extension terms and SECAV-O core concepts.
- `validation/secav-o-coaching-governance.shacl.ttl` — SHACL constraints for annual plans, objectives, risks, retrospectives and ethics acknowledgements.

### Fixed

- `ontology/alignment-matrix.csv`: seven rows added in v5 (planning governance) were missing the `alignment_type` column; split and populated from corresponding TTL declarations.
- `ontology/alignment-matrix.csv` line 12: `AcceptanceCriteria` corrected to `AcceptanceCriterion` to match the class identifier declared in `secav-o.ttl`.
- `docs/ontology-alignment.md`: two occurrences of `AcceptanceCriteria` corrected to `AcceptanceCriterion`.

### Known issues (pending author decision)

- `ontology/secav-o-coaching-governance-extension.ttl` line 60: `rdfs:range secavo:AcceptanceCriteria` references an undeclared class. Correct reference is `secav:AcceptanceCriterion`; resolution requires namespace-merge decision noted in README.
- `validation/secav-o-coaching-governance.shacl.ttl`: `CoachingObjectiveShape` enforces `sh:minCount 1` on `alignsWithInstitutionalObjective`, making institutional alignment mandatory, while `docs/institutional-alignment.md` treats it as a recommendation. Alignment between constraint and documentation is pending author decision.
- `README.md`: core artifacts (`ontology/secav-o.ttl`, `validation/secav-o.shacl.ttl`, `examples/design-review.ttl`) are not listed; pending decision on whether to add a "Core artifacts" section.

## [0.1.0] - 2026-09-30

### Added

- Initial public repository structure.
- SECAV-O ontology prototype.
- Initial engineering activity, artifact, competency, evidence, measurement, AI-assistance, human-validation, assessment, and coaching concepts.
- Initial object and data properties.
- SHACL prototype constraints.
- Worked AI-assisted Design Review example.
- Conceptual architecture documentation.
- Initial competency questions.
- Draft pilot protocol.
- Citation metadata.
- MIT License.

### Status

This is an experimental prototype. It is not represented as complete, standardized, independently validated, or adopted by third parties.
