# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added

- `coaching-governance/docs/internal-audit-checklist.md` — structured checklist for internal audit functions auditing SECAV-O coaching processes. 67 criteria organized into 11 areas: team inception and launch, member preparation and onboarding, initial growth baseline, annual coaching plan, sprint planning, evidence collection and coaching interventions, retrospective and replanning, risk management, Coach Committee governance, ethics and confidentiality, and traceability. Each criterion specifies the evidence to request and provides a pass/fail result field and observation column. Includes a summary table aggregating compliance results by area.
- `coaching-governance/docs/cmmi-mapping.md` — mapping of SECAV-O processes and artifacts to CMMI for Development (CMMI-DEV) v2.0 practice areas. Covers OT, OPF, OPD, MA, PQA, PMC, RSKM, VER, and PR. For each practice area, lists the specific CMMI practice, the SECAV-O implementation, and the primary artifacts that provide appraisal evidence. Includes a cross-reference artifact locator table and notes for appraisers on longitudinal evidence, metric interpretation, the distinction between coaching and performance management, and tailoring expectations.

## [0.2.0] - 2026-10-07

### Changed

- `coaching-governance/guides/code-review-best-practices.md` (moved from `coaching-governance/docs/`) — code review guides relocated to `coaching-governance/guides/` to separate reference guides from operating-model documents.
- `coaching-governance/guides/ai-assisted-code-review.md` (moved from `coaching-governance/docs/`) — same relocation. All internal cross-references updated.
- `coaching-governance/guides/risk-management.md` (moved from `coaching-governance/docs/`) — relocated to `coaching-governance/guides/` for consistency; SECAV-O ontology references added inline and in integration table at end of document.

### Added

- `coaching-governance/glossary/glossary.md` — authoritative glossary of all framework-specific terms: 30 entries across 8 thematic sections (quality criteria, roles, review and inspection activities, unit testing, coaching cycle, defect metrics and traceability, incremental adoption, risk management). Each entry includes definition, source guide, and SECAV-O term mapping.
- `coaching-governance/guides/design-documentation-standards.md` — mandatory design artifacts guide. First standard: state diagrams are required for any entity whose behavior varies by state; must include explicit initial state, all reachable states, explicit final states, labeled transitions (event/condition/guard), and transition actions. Six quality criteria verified during `secav:DesignReview`: complete, explicit initial state, explicit final states, labeled transitions, no implicit transitions, consistent with code. Absence of a required diagram is a blocking `secav:ReviewFinding`. Systemic absence of diagrams across reviews triggers `secavo:QualityPlanningConcern`. SECAV-O: `secav:DesignArtifact`, `secav:DesignReview`, `secav:QualityCriterion`, `secav:ReviewFinding`, `secav:DesignCompetency`, `secav:CompetencyAssessment`.
- `coaching-governance/guides/minimum-quality-criteria.md` — defines "calidad mínima razonable" (minimum reasonable quality) as a formal framework term: the threshold below which an organization is in bad engineering practice, regardless of time or budget constraints invoked to justify it. Inspecting the critical artifacts of each productive phase is that threshold. Maps seven development phases (requirements, architecture design, detailed design, code, unit test design, system test design, acceptance test design) to SECAV-O activity classes, artifact types, review types, and existing framework guides. Defines the six risk-based criteria for selecting which artifacts warrant formal inspection. Establishes the phase-advance rule: critical findings must be documented in a `secav:ReviewRecord` and resolved before the artifact advances; coach documents omissions as `secavo:QualityPlanningConcern`. Identifies system test design and acceptance test design as phases without dedicated guides yet. SECAV-O: `secav:RequirementsActivity`, `secav:DesignActivity`, `secav:ApplicationDesign`, `secav:CodingActivity`, `secav:TestingActivity`, `secav:UnitTestDesign`, `secav:DesignReview`, `secav:CodeReview`, `secav:UnitTestDesignReview`, `secav:DesignArtifact`, `secav:SourceCodeArtifact`, `secav:UnitTestDesignArtifact`, `secav:QualityCriterion`, `secav:AcceptanceCriterion`, `secav:ReviewFinding`, `secav:ReviewRecord`, `secavo:QualityPlanningConcern`.
- `coaching-governance/guides/unit-test-review.md` — checklist and guide for unit test design review (`secav:UnitTestDesignReview`): FIRST principles mapped to `secav:QualityCriterion`, boundary value analysis (numeric limits, empty/single-element collections, string edge cases), null/undefined state, time and date abstraction via injectable Clock, exception and error message validation, AAA/GWT structure, mock discipline, and descriptive naming conventions. Coach attends as silent observer; post-session feedback is group (systemic omission patterns), individual in private (recurring design issues), or organizational (when unit test review is omitted under schedule pressure). SECAV-O: `secav:UnitTestDesignReview`, `secav:UnitTestDesignArtifact`, `secav:TestingCompetency`, `secav:TestResult`, `secav:ReviewRecord`, `secav:ReviewFinding`, `secav:WorkProductEvidence`, `secav:CoachingRecommendation`, `secav:CoachingIntervention`, `secavo:ImprovementAction`, `secavo:DefectObservation` with `phaseInjected = "unit-test-design"`.
- `coaching-governance/guides/requirements-inspection.md` — formal inspection of requirements documents: central insight that ambiguous requirements can only be detected by comparing independent interpretations from multiple reviewers (a single reviewer cannot self-generate two conflicting readings); six defect types (ambiguity, vagueness, incompleteness, inconsistency, unverifiability, infeasibility); five-phase process with mandatory individual preparation; coach is silent observer with post-session feedback (group, individual, or organizational). SECAV-O: DesignReview, DesignArtifact, ReviewRecord, ReviewFinding, QualityCriterion, AcceptanceCriterion, DefectObservation with phaseInjected/phaseDetected, DesignCompetency, ReviewCompetency.
- `coaching-governance/guides/retrospective-participation.md` — coach role in sprint retrospectives: two modes — (1) facilitator when no Scrum Master or equivalent is present; (2) silent observer when a facilitator exists, consistent with peer-review and inspection protocols. In both modes, coach verifies that defect metrics (DefectObservation, phaseInjected, phaseDetected), review findings, and risks are analyzed and that ImprovementActions are agreed based on data. Post-session feedback: group when pattern affects whole team, individual in private for specific participants, organizational escalation (QualityPlanningConcern or Coach Committee) for systemic patterns across sprints.
- `coaching-governance/guides/defect-tracking.md` — defect tracking via ticket closure and Quality Assistant role: coach closes bug tickets in the tracking system to collect consistent `secavo:DefectObservation` data (phaseInjected, phaseDetected, detectionMethod, severity, module); metrics feed defect-log.csv and sprint metrics review. When coach is overloaded, a team member is designated Quality Assistant after explicit training and at least two sprints of supervised validation; the role also develops ReviewCompetency and DesignCompetency.
- `coaching-governance/guides/peer-review-sessions.md` — coach observation protocol during peer review sessions: coach is a silent observer (no verbal participation, notes only); focus-on-product principle from the start; coach notes silently when team drifts off-topic (no verbal intervention); when engineers cannot reach agreement after sufficient debate, they mark the point pending, continue the session, and escalate to the Project Leader afterwards. Coach observations feed `secav:ReviewFinding`, `secav:CompetencyAssessment`, and `secavo:ImprovementAction` outside the session — never during it.
- `coaching-governance/guides/formal-inspections.md` — guide for formal inspections of critical system modules: architect identifies critical modules using six risk criteria (failure impact, breadth of use, structural complexity, security/privacy, data integrity, novelty); coach moderates a five-phase process (planning → individual preparation → inspection meeting → rework → follow-up); inspectors must prepare individually before the meeting; coach uses `secav:ReviewFinding` as evidence for `secav:CompetencyAssessment`; systemic patterns trigger `secav:CoachingIntervention`; omitted inspections trigger `secavo:QualityPlanningConcern`. Management must authorize time and must not use inspection findings as individual performance instruments.
- `coaching-governance/guides/project-kickoff-alignment.md` — pre-project alignment meeting guide: Technical Lead + Coach + senior management establish measurable project success objectives (at least one quality/defect metric required), team objectives (equal or more aggressive than org commitments), and individual objectives. Coach role: verify measurability, propose quality objective if absent, prevent goal dilution via `secavo:QualityPlanningConcern` if needed. Full SECAV-O mapping: `secavo:ProjectObjective`, `secavo:alignsWithProjectObjective`, `secavo:DefectObservation`, `secavo:ReviewObservation`, `secavo:Metric`, `secavo:QualityPlanningConcern`.
- `coaching-governance/guides/coach-team-behaviors.md` — team leader behaviors the coach observes and uses as coaching evidence, organized into six areas: (1) facilitation vs. protagonist role; (2) consensus-based decision-making anchored in visible constraints; (3) building plans the team genuinely believes in — active buy-in verification, listening to disagreement, finding alternatives collectively, formal escalation when unresolved; (4) participatory risk management — team-built risk register, collective preventive brainstorming, blame-free corrective action; (5) capability-based work assignment; (6) respectful team culture — correcting in private, praising in public. Each area lists positive indicators (`secav:Evidence`) and red flags that trigger a `secav:CoachingIntervention`. Includes an 11-item per-sprint observation checklist and a SECAV-O integration table.
- `coaching-governance/docs/coach-committee.md` — governance model for multi-coach organizations: Coach Committee (formed when ≥ 2 coaches exist), Lead Coach designation by management or coach consensus, committee responsibilities (org-wide coaching plan, standards oversight, coach assignment, escalation, organizational view), governance cadence, and proposed ontology extension (`secavo:CoachCommittee`, `secavo:LeadCoach`, `secavo:hasLeadCoach`, `secavo:hasCommitteeMember`, `secavo:generatesOrganizationalPlan`).
- `templates/coach-committee-charter.md` — charter template: members, Lead Coach election rules, decision-making rules, assignment matrix, conflict-of-interest declarations, ethics acknowledgement tracking, and amendment history.
- `coaching-governance/guides/incremental-adoption.md` — strategic guide for incremental framework adoption: Fail Fast philosophy, PoC technique, end-to-end tracer, short feedback loops, Go/Pivot/Stop decision table, 5-phase expansion model, SECAV-O integration table. References: The Pragmatic Programmer, The Lean Startup, Agile Manifesto. Philosophy borrowed without prescribing Scrum or SAFe.
- `templates/engineer-development-record.md` — **(proposal)** longitudinal engineer development record: 8-section template (general data, competencies by cycle, development plan, session log, impact evidence typed to `secav:Evidence` subclasses, 360 feedback, coach handoffs, organizational indicators). 4-level competency scale with explicit mapping to SECAV-O 6-level scale. Designed to be coach-independent and comparable across teams.
- `templates/organizational-competency-view.csv` — **(proposal)** aggregated organizational view: one row per engineer per cycle, enabling team-level competency averages, objective progress, and promotion/retention risk flags. Populated with Valeria Montes example row.
- `examples/example-engineer-development-record.md` — **(proposal)** fully completed fictional example (Valeria Montes, Platform Engineering, cycles H1 and H2 2026) showing a coach change in July, 2 completed objectives, 5 evidence entries, 360 feedback, and promotion/retention flags in Section 8.
- `coaching-governance/guides/code-review-best-practices.md` — evidence-based best practices for code review (reviewer and author responsibilities, size limits, feedback culture, AI-assisted code, coaching integration). Sources: Google Engineering Practices, Microsoft Code with Engineering Playbook, SmartBear/Cisco peer review research.
- `coaching-governance/guides/ai-assisted-code-review.md` — dedicated guidance for AI-assisted code review: context data, layered pipeline, risk triage, false-positive management, data privacy, SECAV-O integration. 13 sources including Google AutoCommenter study and Faros AI data.

### Added — Coaching Governance Extension (v5)

**Operating model documents**
- `coaching-governance/docs/project-planning-participation.md` — coach participation in project planning, quality-gate advocacy, formal dissent and escalation.
- `coaching-governance/docs/team-coaching-lifecycle.md` — coaching from team inception/launch through member preparation, baseline establishment and ongoing onboarding.
- `coaching-governance/docs/coaching-cycle.md` — annual planning, sprint execution, retrospectives and replanning.
- `coaching-governance/guides/risk-management.md` — coaching risk-management model.
- `coaching-governance/docs/institutional-alignment.md` — method for connecting individual coaching objectives to institutional objectives.
- `coaching-governance/docs/coach-code-of-ethics.md` — SECAV-O Code of Ethics for coaches.
- `coaching-governance/docs/metrics-model.md` — defects, reviews, inspections, unit tests and competency-growth metrics.
- `coaching-governance/docs/competency-growth-scale.md` — longitudinal competency maturity scale.
- `coaching-governance/docs/ontology-alignment.md` — explicit alignment between extension terms and SECAV-O core concepts.

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

- `coaching-governance/docs/coach-committee.md` Section 2: `secavo:LeadCoach` was presented without a "(proposed)" qualifier — it does not yet exist in the TTL. Added cross-reference to §7.
- `coaching-governance/docs/coach-committee.md` Section 4.5: corrected erroneous description "individual engineer development records (`templates/organizational-competency-view.csv`)" — the CSV is the aggregated organizational view, not individual records. Fixed to clarify that individual data comes from `templates/engineer-development-record.md` §8 and is aggregated into the CSV.
- `coaching-governance/docs/coach-committee.md` Section 7: added design note to `secavo:assignsCoachToTeam` explaining that the current `range secav:Coach` captures the coach individual only; team context is held in the charter assignment matrix and a richer model would need a dedicated assignment class.
- `ontology/alignment-matrix.csv`: seven rows added in v5 (planning governance) were missing the `alignment_type` column; split and populated from corresponding TTL declarations.
- `ontology/alignment-matrix.csv` line 12: `AcceptanceCriteria` corrected to `AcceptanceCriterion` to match the class identifier declared in `secav-o.ttl`.
- `coaching-governance/docs/ontology-alignment.md`: two occurrences of `AcceptanceCriteria` corrected to `AcceptanceCriterion`.
- `coaching-governance/guides/code-review-best-practices.md`: three ontology alignment corrections — (1) `secav:CodeReview` subclass relationship clarified and `secav:ReviewRecord`/`secav:CoachingIntervention` added to Purpose; (2) Section 8 updated to use `secav:providesEvidenceOf` and `secav:ReviewCompetency` explicitly; (3) Section 9 corrected `secav:assistedByAI` usage (ObjectProperty on `EngineeringActivity`, not a flag on the review record) and added `secav:requiresHumanValidation` link.
- `coaching-governance/guides/code-review-best-practices.md` Section 9: reworded "Record this in the `secav:ReviewRecord`" — `secav:assistedByAI` belongs to the `secav:EngineeringActivity`, not to the ReviewRecord. Clarified as "Note in the ReviewRecord that the artifact was produced by an AI-assisted activity."
- `coaching-governance/docs/coaching-cycle.md` SECAV-O chain: corrected two ontologically invalid hops — (1) `Artifact → Competency` has no OWL property; (2) `Observable Evidence → Measurement` is wrong because `secav:Measurement` is a *subclass* of `secav:Evidence`, not a successor. Fixed chain: `Engineering Activity (produces Artifact, assessedAgainst AcceptanceCriterion, requiresCompetency) → Evidence/Measurement → Competency Gap → Coaching Intervention`.
- `coaching-governance/guides/ai-assisted-code-review.md`: removed inline citations [14], [15], [16] whose source URLs were garbled/cut off in the source PDF and could not be verified; statements retained; disclosure note added to Sources section.

### Fixed — 0.2.0 consistency corrections

- `ontology/secav-o-coaching-governance-extension.ttl`: replaced provisional namespace `https://example.org/secav-o#` with stable extension namespace `https://github.com/vlorenzana/software-engineering-coaching-framework/ontology/secav-o-coaching-governance#`; added `secav:` prefix for core ontology and `owl:imports` declaration; corrected all core-class references (`secav:Evidence`, `secav:CoachingIntervention`, `secav:Competency`, `secav:EngineeringActivity`, `secav:Artifact`) to use the `secav:` prefix instead of `secavo:`.
- `ontology/secav-o-coaching-governance-extension.ttl` line 60 (former): corrected `secavo:AcceptanceCriteria` (undeclared class) to `secav:AcceptanceCriterion` (the class declared in `secav-o.ttl`).
- `validation/secav-o-coaching-governance.shacl.ttl`: updated namespace prefix to match stable extension namespace; added `secav:` prefix; corrected `sh:class` references for core classes to use `secav:` prefix; removed `sh:minCount 1` from `alignsWithInstitutionalObjective` in `CoachingObjectiveShape` — the documentation presents institutional alignment as a recommendation, not an obligation for all records; adopting organizations may enforce it in their own SHACL profiles.
- `README.md`: added "Core artifacts" section; updated "Ontology alignment note" to reflect that the extension now uses a stable namespace and explicitly imports the core ontology; replaced internal version label "Version 5" with public version "0.2.0"; added evidence boundary note in "Claim boundary" section.
- `CITATION.cff`: updated `version` to `0.2.0` and `date-released` to `2026-10-07`.
- `coaching-governance/glossary/glossary.md`: updated "Coach" entry to distinguish observer, facilitator, and moderator roles by activity and to clarify that engineers retain technical responsibility; updated "Calidad mínima razonable" to present it as a SECAV-O framework proposal rather than a universally recognized standard.
- `coaching-governance/guides/minimum-quality-criteria.md`: added framing note that the criterion is a SECAV-O proposal.
- `coaching-governance/guides/ai-assisted-code-review.md`: fixed formatting error ("e-" prefix on a list item); rephrased unsupported statistical claims as reported observations pending source verification.

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
