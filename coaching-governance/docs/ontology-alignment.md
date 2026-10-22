# SECAV-O Coaching Governance Ontology Alignment

## Purpose
This document explains how the coaching-governance artifacts extend the existing SECAV-O core model rather than creating a parallel ontology.

## Core SECAV-O concepts reused
The extension is designed to reuse these core concepts already present in the framework model:

- `EngineeringActivity`
- `Artifact`
- `Competency`
- `AcceptanceCriterion`
- `Evidence`
- `CoachingIntervention`
- AI-assistance / human-validation concepts remain in the core ontology and can be linked to observed engineering activities and artifacts.

## Alignment rules

| Coaching/governance concept | Core alignment | Rationale |
|---|---|---|
| `Baseline` | subclass of `Evidence` | A baseline is recorded evidence of the initial state. |
| `MeasurementObservation` | subclass of `Evidence` | Measurements are observable evidence. |
| `DefectObservation` | subclass of `MeasurementObservation` | A defect record is a specialized measurement/evidence item. |
| `ReviewObservation` | subclass of `MeasurementObservation` | Review findings are evidence from review activities. |
| `UnitTestObservation` | subclass of `MeasurementObservation` | Unit-test results are engineering evidence. |
| `CompetencyTrend` | subclass of `Evidence` | Longitudinal competency change is derived from repeated observations. |
| `ImprovementAction` | subclass of `CoachingIntervention` | Corrective developmental action is a coaching intervention. |
| `CoachingObjective` | targets `Competency` | Coaching objectives should identify the capability being developed. |
| `CoachingSprint` | observes `EngineeringActivity` | Sprint evidence comes from real engineering work. |
| `CoachingSprint` | uses `Artifact`, `AcceptanceCriterion`, `Evidence`, `Metric` | Keeps coaching connected to the existing SECAV-O activity/artifact/evidence pattern. |

## Governance alignment

Institutional alignment is modeled at the objective level: a `CoachingObjective` `alignsWithInstitutionalObjective` an `InstitutionalObjective`. This prevents the institutional goal from replacing the engineer-level competency objective.

Risk governance is attached to the `AnnualCoachingPlan`, with sprint-level risks optionally linked through `sprintHasRisk`. Each `Risk` can carry probability, impact, status, owner, preventive actions, corrective/contingency actions, and retrospective reviews.

Ethics governance is modeled through a `CoachEthicsCode` and an `EthicsAcknowledgement`. The annual plan can be governed by an ethics code, while individual acknowledgements provide evidence that a coach accepted those obligations.

## Integration note
Version 4 adds team-lifecycle concepts as an extension layer. `TeamCoachingInitiation`, `MemberPreparation`, and `MemberOnboarding` are modeled as specializations of `CoachingIntervention` because each is an intentional coaching action. `MemberBaseline` specializes `Baseline`, which already specializes core `Evidence`. Project objectives remain separate from institutional objectives but can both align to a `CoachingObjective`. Risks reuse the existing `Risk` model rather than introducing a duplicate onboarding-risk concept.

As of v0.2.0, the extension uses the stable namespace `https://github.com/vlorenzana/software-engineering-coaching-framework/ontology/secav-o-coaching-governance#` and explicitly imports the core ontology via `owl:imports`. Core class references use the `secav:` prefix (e.g., `secav:Artifact`, `secav:AcceptanceCriterion`, `secav:CoachingIntervention`). The placeholder namespace `https://example.org/secav-o#` is no longer present in any framework artifact.

## Team lifecycle alignment

| Lifecycle concept | Alignment | Rationale |
|---|---|---|
| `TeamCoachingInitiation` | subclass of `CoachingIntervention` | Coaching begins at team inception/launch as an intentional intervention. |
| `MemberPreparation` | subclass of `CoachingIntervention` | Preparation is a developmental coaching action before normal delivery. |
| `MemberOnboarding` | subclass of `CoachingIntervention` | Onboarding provides context, risk awareness, expectations and an initial coaching baseline. |
| `MemberBaseline` | subclass of `Baseline` -> `Evidence` | The member baseline is initial comparison evidence for longitudinal growth. |
| `CoachingObjective` -> `ProjectObjective` | `alignsWithProjectObjective` | Individual development can be tied to project as well as institutional outcomes. |
| onboarding / launch -> `Risk` | `communicatesRisk` | Reuses the existing risk-governance model rather than duplicating risks. |
| preparation -> `EngineeringActivity` / `Competency` | `preparesMemberForActivity` / `preparesMemberForCompetency` | Keeps preparation connected to the core activity/competency model. |

## Version 6 — Review scenario catalog alignment

The review-scenario catalog (`pilot/review-scenarios-catalog.md`) introduces 50 candidate review scenarios classified as H (human-only), HA (human-AI), and AA (AI-AI). These are aligned with the existing SECAV-O core as follows:

| Catalog concept | Core alignment | Rationale |
|---|---|---|
| `ReviewScenario` | subclass of `QualityActivityRequirement` | A review scenario is a specific form of quality activity requirement scoped to a pilot. |
| `ReviewScenarioExecution` | subclass of `ReviewObservation` → `MeasurementObservation` | Executing a scenario produces review observations that are measurable evidence. |
| `ControlGroupBaseline` | subclass of `Baseline` → `Evidence` | The control group's initial state is a baseline used for comparison. |
| `ExperimentalGroupBaseline` | subclass of `Baseline` → `Evidence` | The experimental group's initial state is a separate baseline for the same comparison. |
| `ScenarioComparisonTrend` | subclass of `CompetencyTrend` → `Evidence` | The difference between control and experimental baselines over time is derived longitudinal evidence. |

The control/experimental group design maps to the existing governance path:

`ProjectPlanningParticipation -> ReviewScenario (QualityActivityRequirement) -> ReviewScenarioExecution (ReviewObservation) -> ControlGroupBaseline / ExperimentalGroupBaseline -> ScenarioComparisonTrend -> CoachingObjective`

This keeps the pilot experimental design fully traceable through the existing SECAV-O evidence and measurement model without introducing a parallel quality-management structure.

## Version 7 — AI-assisted code review guide alignment

The guide `coaching-governance/guides/ai-assisted-code-review.md` introduces operational concepts for AI-assisted review that extend the existing SECAV-O activity/evidence/risk model.

| Guide concept | Core alignment | Rationale |
|---|---|---|
| `ReviewDimension` | DataProperty on `HumanValidationActivity` | A dimension (syntax, optimization, business logic, security) is an attribute of the review activity, not a separate activity. |
| `aiPrimaryForDimension` | ObjectProperty: `AISystem` → `ReviewDimension` | Records which dimensions the AI system was primarily responsible for in a given review pass. |
| `humanPrimaryForDimension` | ObjectProperty: `HumanValidationActivity` → `ReviewDimension` | Records which dimensions required primary human judgment. |
| `AIReviewPromptConfiguration` | subclass of `QualityActivityRequirement` | The 4-step prompt configuration (context → impact → security → tests) is a precondition for a valid AI review pass. |
| `ReviewRiskLevel` | DataProperty on `EngineeringActivity` (values: Routine / Attention / SecurityCritical) | PR risk classification determines the review path and whether `requiresHumanValidation` is mandatory. |
| `ReviewEscapeObservation` | subclass of `DefectObservation` → `MeasurementObservation` → `Evidence` | A high-risk PR incorrectly cleared at a lower tier is a measurable defect in the review process. |
| `DeterministicAnalysisActivity` | subclass of `EngineeringActivity` | Linters, type checkers, secret scanners and static analysis tools execute before the AI review pass. |
| `ContinuousIntegrationActivity` | subclass of `EngineeringActivity` | CI (tests, integration checks) runs after human review; it is the final pipeline stage before merge. |

The review pipeline stages are ordered via `secav:precedes`:

`DeterministicAnalysisActivity → AIAssistedActivity (review pass) → HumanValidationActivity → ContinuousIntegrationActivity`

`AIReviewPromptConfiguration` is attached to the `AIAssistedActivity` that performs the review pass as a `QualityActivityRequirement`, not to the code-generation activity. This preserves the boundary between generation and review in the ontology.

`ReviewRiskLevel = SecurityCritical` is the trigger condition for `requiresHumanValidation`; the other levels do not remove human review but reduce its mandatory scope.

## Version 8 — Reviewer readiness and cognitive preparation alignment

The reviewer readiness section in `coaching-governance/guides/code-review-best-practices.md` (§10) introduces precondition concepts that are observable before a `ReviewActivity` begins. These are modeled as coaching-observable conditions rather than activity properties.

| Guide concept | Core alignment | Rationale |
|---|---|---|
| `ReviewerReadinessCondition` | subclass of `Evidence` | The reviewer's cognitive state at session start is an observable, recordable condition that affects review quality. |
| `CognitiveFatigueObservation` | subclass of `MeasurementObservation` → `Evidence` | Patterns of after-hours reviews, oversized sessions, or session overruns are measurable coaching signals. |
| `ReviewSessionLimit` | DataProperty on `ReviewActivity` (maxLOC: 400, maxMinutes: 60) | The LOC and time limits are constraints on the review activity, consistent with §1 of the guide. |
| `TechnicalExecutionSequence` | subclass of `QualityActivityRequirement` | The 5-step ordered execution sequence (context → AI filter → human security → maintainability → feedback) is a quality precondition for the `HumanValidationActivity`. |

The `TechnicalExecutionSequence` is distinct from `AIReviewPromptConfiguration` (Version 7): the prompt configuration governs how the AI tool is instructed, while the execution sequence governs how the human reviewer proceeds step by step.

`CognitiveFatigueObservation` instances are coaching inputs, not performance measures. They should link to `ImprovementAction` (subclass of `CoachingIntervention`) targeting working-condition changes, not individual competency gaps.

The two new role-matrix dimensions (edge case detection and architecture/design) extend `ReviewDimension` from Version 7 without new classes — they are additional named values of the existing `ReviewDimension` DataProperty.

## Modeling boundary
This extension does not assert that risk probability, impact, competency levels, or metric thresholds have universal values. Those values are data collected during coaching and should remain context-specific.

## Version 5 — Project planning quality governance alignment

The planning-governance extension is aligned with the existing SECAV-O core rather than introducing a separate quality-management ontology. `ProjectPlanningParticipation` and `Escalation` are specializations of `CoachingIntervention`, because they are actions performed by the coach to influence engineering conditions and improvement. `QualityPlanningConcern`, `FormalDissent`, and `GovernanceDecision` are modeled as `Evidence`, because they preserve observable, auditable records of decisions, risks, rationale and outcomes. `QualityActivityRequirement` links directly to `EngineeringActivity`, allowing reviews, peer reviews, inspections, unit-test activities and other quality practices to remain part of the same engineering activity model already used by SECAV-O.

The resulting governance path is:

`ProjectPlanningParticipation -> PlanningDecision -> EngineeringActivity / QualityActivityRequirement -> QualityPlanningConcern -> Risk -> PreventiveAction -> FormalDissent (if unresolved) -> Escalation -> GovernanceDecision -> SprintRetrospective`

This preserves the core SECAV-O principle that quality and coaching decisions should be traceable through activities, evidence, measurement, risk and improvement actions.
