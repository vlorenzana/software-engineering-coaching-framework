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

## Important merge note
Version 4 adds team-lifecycle concepts as an extension layer. `TeamCoachingInitiation`, `MemberPreparation`, and `MemberOnboarding` are modeled as specializations of `CoachingIntervention` because each is an intentional coaching action. `MemberBaseline` specializes `Baseline`, which already specializes core `Evidence`. Project objectives remain separate from institutional objectives but can both align to a `CoachingObjective`. Risks reuse the existing `Risk` model rather than introducing a duplicate onboarding-risk concept.

The package currently retains the placeholder namespace `https://example.org/secav-o#` because the canonical namespace of the core ontology was not supplied in this artifact package. Before merging, replace that namespace with the exact namespace used in `ontology/secav-o.ttl` and confirm the exact core class identifiers (`Artifact` vs. `WorkProduct`, `AcceptanceCriterion`, etc.). Do not create duplicate core classes if equivalent terms already exist.

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

## Modeling boundary
This extension does not assert that risk probability, impact, competency levels, or metric thresholds have universal values. Those values are data collected during coaching and should remain context-specific.

## Version 5 — Project planning quality governance alignment

The planning-governance extension is aligned with the existing SECAV-O core rather than introducing a separate quality-management ontology. `ProjectPlanningParticipation` and `Escalation` are specializations of `CoachingIntervention`, because they are actions performed by the coach to influence engineering conditions and improvement. `QualityPlanningConcern`, `FormalDissent`, and `GovernanceDecision` are modeled as `Evidence`, because they preserve observable, auditable records of decisions, risks, rationale and outcomes. `QualityActivityRequirement` links directly to `EngineeringActivity`, allowing reviews, peer reviews, inspections, unit-test activities and other quality practices to remain part of the same engineering activity model already used by SECAV-O.

The resulting governance path is:

`ProjectPlanningParticipation -> PlanningDecision -> EngineeringActivity / QualityActivityRequirement -> QualityPlanningConcern -> Risk -> PreventiveAction -> FormalDissent (if unresolved) -> Escalation -> GovernanceDecision -> SprintRetrospective`

This preserves the core SECAV-O principle that quality and coaching decisions should be traceable through activities, evidence, measurement, risk and improvement actions.
