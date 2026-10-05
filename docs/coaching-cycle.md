# SECAV-O Coaching Planning and Improvement Cycle

## Purpose

The SECAV-O coaching cycle treats coaching as a longitudinal engineering-improvement process rather than a sequence of isolated interventions. Each engineer has an Annual Coaching Plan that is executed through short Coaching Sprints. Each sprint collects evidence from real engineering work, measures outcomes against a baseline, performs a retrospective, and replans the next sprint.


## Team inception, launch and continuous onboarding

Coaching begins with the team, not only with the first individual coaching sprint. The coach should participate from the earliest practical team-formation event—project planning, team inception, kickoff, launch, or an equivalent organizational ceremony. The purpose is to establish shared context before delivery pressure obscures assumptions, risks, roles, quality expectations, and development needs.

Before launch, the framework recommends a **Member Preparation** step. Members receive or review the project purpose, institutional and project objectives, delivery model, engineering practices, quality expectations, known risks, key artifacts, review/inspection expectations, unit-testing practices, AI-assistance and human-validation responsibilities, and the evidence/metrics that may be collected for coaching. Preparation is developmental rather than gatekeeping: gaps identified before launch become inputs to coaching objectives and support plans.

At or immediately after launch, the coach helps establish an **Initial Growth Baseline** for each member where practical. The baseline may include demonstrated competency, autonomy, review/inspection evidence, unit-test evidence, defect patterns, relevant training history, and contextual constraints. The baseline is not a punitive ranking; it is the comparison point for longitudinal growth.

Coaching continues when team composition changes. For each **New-Member Onboarding**, the coach helps the new member understand project context, institutional/project objectives, architecture and delivery expectations, current risks and mitigations, quality practices, review/inspection norms, testing expectations, AI-use and human-validation rules, and current team coaching priorities. A new baseline is then established for that member and incorporated into the annual/sprint coaching plan.

This extends the lifecycle to:

`Team Inception/Launch -> Member Preparation -> Context & Risk Orientation -> Initial Baseline -> Annual Plan -> Coaching Sprints -> Retrospectives/Replanning -> New-Member Onboarding -> Updated Baseline & Plan`

## Operating cycle

1. **Annual Coaching Plan**
   - Define competency-development priorities for the year.
   - Establish the initial baseline.
   - Define objectives and expected outcomes.
   - Select metrics and evidence sources.
   - Identify engineering activities and artifacts to observe.

2. **Coaching Sprint Planning**
   - Review the annual plan and previous sprint results.
   - Select a bounded set of competency objectives.
   - Identify activities, work products, reviews, inspections, and unit-test evidence to observe.
   - Define the metrics to collect during the sprint.
   - Define acceptance criteria and evidence requirements.

3. **Execution and Evidence Collection**
   - Observe engineering activities and resulting work products.
   - Capture review findings, inspection findings, test results, defects, and coaching observations.
   - Record where AI assistance was used and what human-validation activity occurred.

4. **Coaching Intervention**
   - Link observed gaps or recurring findings to targeted coaching actions.
   - Record feedback, practice assignments, review activities, and follow-up evidence.

5. **Sprint Retrospective**
   - Compare results with the baseline and sprint objectives.
   - Review trends in defects, review effectiveness, unit-test evidence, and competency growth.
   - Identify what worked, what did not, and what should change.

6. **Replanning**
   - Adjust objectives, metrics, activities, and coaching interventions for the next sprint.
   - Escalate or retire objectives based on evidence.
   - Update the competency trend.

## Baseline principle

Every measurable coaching objective should begin with a documented baseline where practical. The baseline is the comparison point used to evaluate change over time. It may include:

- defects found by phase;
- late-phase or escaped defects;
- review and inspection findings;
- unit-test evidence;
- competency assessment level;
- level of engineer autonomy;
- recurring quality or review patterns.

A baseline should not be treated as a performance score in isolation. It is contextual evidence used for longitudinal comparison.

## Sprint cadence

The framework does not prescribe one universal sprint duration. A coaching sprint may align with a software-development sprint or use a separate cadence. The chosen cadence should be long enough to produce observable engineering evidence and short enough to support timely replanning.

## SECAV-O linkage

The coaching cycle extends the existing SECAV-O chain:

`Engineering Activity -> Artifact -> Competency -> Acceptance Criteria -> Observable Evidence -> Measurement -> Gap -> Coaching Intervention`

with a longitudinal loop:

`Baseline -> Objective -> Coaching Sprint -> Evidence -> Measurement -> Retrospective -> Replanning -> Competency Trend`


## Institutional alignment and risk governance

The Annual Coaching Plan should explicitly identify the institutional or team objectives that the coaching plan supports. Alignment is traceable from institutional objective to coaching objective, competency, engineering activity, evidence, and metric.

The Annual Coaching Plan also maintains a risk plan. Risks are reviewed in every Sprint Retrospective, including changes in probability and impact, preventive-action status, whether a risk materialized, corrective actions taken, and whether the risk carries forward.

The coach must apply the SECAV-O Code of Ethics throughout planning, evidence collection, assessment, retrospective, and replanning.
