# SECAV-O Framework Glossary

This glossary collects terms introduced or redefined by the SECAV-O coaching framework. General-use software engineering terms (retrospective, sprint, requirement, unit test, etc.) are not included unless the framework gives them a specialized meaning.

---

## Thematic index

- [Quality and minimum criteria](#quality-and-minimum-criteria)
- [Documentation and glossaries](#documentation-and-glossaries)
- [Framework roles](#framework-roles)
- [Review and inspection activities](#review-and-inspection-activities)
- [Unit testing](#unit-testing)
- [Coaching cycle](#coaching-cycle)
- [Metrics and defect traceability](#metrics-and-defect-traceability)
- [Incremental adoption](#incremental-adoption)
- [Risk management](#risk-management)

---

## Quality and minimum criteria

### Minimum Reasonable Quality
*Source: `coaching-governance/guides/minimum-quality-criteria.md`*

A criterion proposed by the SECAV-O framework to define the minimum inspection threshold for each development phase. It is not a universally recognized certification standard; it is a framework convention that establishes the floor below which this coaching model considers inspection coverage insufficient.

The proposed operational criterion is: the critical artifacts of each productive phase must be inspected by more than one reviewer before that phase concludes.

An organization that does not apply this criterion may have technical, maturity, or contextual reasons that justify a different approach; the framework invites reflection on accumulated risk rather than automatically declaring bad practice. The coach documents the omission as a `secavo:QualityPlanningConcern` so that the organization can make an informed decision.

Contrasts with [aspirational quality](#aspirational-quality), which is the level organizations mature toward progressively.

**Associated SECAV-O term:** `secav:QualityCriterion`, `secavo:QualityPlanningConcern`

---

### Robust Process
*Source: `coaching-governance/guides/robust-process-criteria.md`*

A SECAV-O framework quality level defined above [minimum reasonable quality](#minimum-reasonable-quality) and below [aspirational quality](#aspirational-quality). A robust process not only performs the required quality practices — it performs them in a way that generates its own verifiable evidence of effectiveness.

A process is considered robust when it meets the criteria defined in `coaching-governance/guides/robust-process-criteria.md`. Currently defined criteria:

| ID | Criterion |
|---|---|
| CR-1 | Inspections are performed on critical products |
| CR-2 | Dynamic behavior is designed with UML activity or sequence diagrams |
| CR-3 | Defects resulting from reviews and inspections are documented with complete fields |
| CR-4 | Individual reviews generate findings |
| CR-5 | When a review generates no findings, the coach issues a justified [coach waiver](#coach-waiver) |

The fundamental distinction from minimum reasonable quality is that the robust process produces evidence that practices work — not just evidence that they were performed.

**Associated SECAV-O term:** Individual criteria reference `secav:ReviewRecord`, `secav:ReviewFinding`, `secav:DesignArtifact`, `secavo:DefectObservation`, `secavo:CoachWaiver` *(proposed)*.

---

### Coach Waiver
*Source: `coaching-governance/guides/robust-process-criteria.md` §CR-5*

A document issued by the coach that objectively justifies the absence of findings in an individual review. Applies when a review legitimately produces no findings — because the artifact was exhaustively corrected before review, because the reviewer has objective evidence that the artifact meets all acceptance criteria, or because the artifact is low-complexity with bounded scope.

The waiver must document: identity of the artifact and reviewer, objective justification referencing evidence, acceptance criteria verified, coach signature and date. A waiver without objective justification is invalid.

Robust process criterion CR-5: if the absence of findings has no documented justification, the coach records a `secav:CoachingIntervention` targeting the development of the engineer's review competency.

**Associated SECAV-O term:** `secavo:CoachWaiver` *(proposed — not yet declared in TTL)*

---

### Aspirational Quality
*Source: `coaching-governance/guides/minimum-quality-criteria.md`*

The quality level at which most or all artifacts produced in each phase are formally inspected. It is the ideal toward which organizations should progress incrementally; assuming every organization can achieve it from the outset is unrealistic.

Organizations mature toward this level using the incremental adoption model (`coaching-governance/guides/incremental-adoption.md`).

---

### Phase-Advance Criterion
*Source: `coaching-governance/guides/minimum-quality-criteria.md`*

The condition an artifact must meet before advancing to the next development phase: (1) inspection findings are documented in the `secav:ReviewRecord`; (2) critical or blocking findings are assigned with an owner and deadline; (3) the coach verifies in follow-up that blocking findings were resolved.

Time pressure that leads to omitting this criterion is recorded as `secavo:QualityPlanningConcern`.

---

### Critical Module
*Source: `coaching-governance/guides/formal-inspections.md`*

A module whose failure, defect, or degradation produces disproportionate consequences for the system or business. The architect identifies critical modules using at least one of these six risk criteria:

| Criterion | Description |
|---|---|
| Failure impact | Its failure affects core functionality or causes irreversible damage |
| Breadth of use | It is used or referenced by many other modules or teams |
| Structural complexity | High cyclomatic complexity, nested conditional logic, many edge cases |
| Security / privacy | Handles authentication, authorization, personal data, or cryptography |
| Data integrity | Affects persistence, transactional consistency, or referential integrity |
| Novelty / uncertainty | Uses a technology or pattern with which the team has little experience |

**Associated SECAV-O term:** `secav:SourceCodeArtifact`, `secav:QualityCriterion`

---

### QualityPlanningConcern
*Source: `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/minimum-quality-criteria.md`*

An escalation artifact generated by the coach when a mandatory quality activity — formal inspection, peer review, unit test review, or another — is omitted or significantly reduced without technical justification.

The coach documents the artifact, communicates it to the Technical Lead and management, and if the pattern is recurring, brings it to the Coach Committee.

**Associated SECAV-O term:** `secavo:QualityPlanningConcern`

---

## Documentation and glossaries

### Primary Glossary
*Source: `coaching-governance/guides/requirements-inspection.md`*

A glossary located at the **beginning** of a requirements document (or any technical document) that contains the terms without which the reader cannot correctly interpret the document. If a primary glossary term is ambiguous, all requirements that use it inherit that ambiguity.

Primary glossary terms are inspectable work products with the same rigor as a requirement: **they must be discussed by two or more reviewers independently** before being accepted. A term that two reviewers interpret differently is a `secav:ReviewFinding` that must be resolved before approving the requirements that use it.

Quality criteria for a primary glossary term: unambiguous interpretation among reviewers, operational definition (allows deciding whether something belongs to the concept or not), consistency with other terms, and correspondence with business domain usage.

Contrasts with [secondary glossary](#secondary-glossary).

**Associated SECAV-O term:** `secav:DesignArtifact` (part of the document), `secav:QualityCriterion`, `secav:ReviewFinding`

---

### State Diagram
*Source: `coaching-governance/guides/design-documentation-standards.md`*

A mandatory design artifact (`secav:DesignArtifact`) for any system entity — class, module, process, resource, or business flow — whose behavior varies according to its current state. Its function is to simultaneously make visible the entire lifecycle of the object: possible states, initial state, final states, transitions, guard conditions, and actions.

A complete state diagram must include: explicit initial state (marked with the standard symbol), all possible states, explicit final states, transitions labeled with the triggering event or condition, guard conditions, and transition actions where applicable.

The absence of a state diagram when the system has states, or an incomplete diagram that omits final states or transitions, is a blocking `secav:ReviewFinding` before advancing to implementation.

**Associated SECAV-O term:** `secav:DesignArtifact`, `secav:DesignReview`, `secav:QualityCriterion`, `secav:ReviewFinding`, `secav:DesignCompetency`

---

### Activity / Flow Diagram
*Source: `coaching-governance/guides/robust-process-criteria.md` §CR-2*

A mandatory design artifact (`secav:DesignArtifact`) for any logic whose behavior varies by control flow: processes with branches (if/else), loops, guard conditions, and algorithms with multiple execution paths.

A valid activity diagram as an inspectable artifact must: be consistent with the code or specification it models, cover the main flows and the most relevant alternative or error flows, and show explicit guard conditions at all decision points.

The absence of this diagram when behavior is dynamic is a `secav:ReviewFinding` of type `missingRequiredDiagram`. It is distinguished from [sequence diagram](#sequence-diagram) in that it models control flow within a process, not messages between components.

**Associated SECAV-O term:** `secav:DesignArtifact`, `secav:DesignReview`, `secav:ReviewFinding`, `secav:DesignCompetency`

---

### Sequence Diagram
*Source: `coaching-governance/guides/robust-process-criteria.md` §CR-2*

A mandatory design artifact (`secav:DesignArtifact`) for any interaction between components, services, actors, or system layers in which the temporal order of messages is relevant.

A valid sequence diagram as an inspectable artifact must: be consistent with the code or specification it models, cover the main flows and include relevant alternative or error flows, and show the operation or event name in each message along with relevant return values.

The absence of this diagram when interactions with a defined temporal order exist is a `secav:ReviewFinding` of type `missingRequiredDiagram`. It is distinguished from [activity diagram](#activity--flow-diagram) in that it models collaboration between participants, not the internal flow of a process.

**Associated SECAV-O term:** `secav:DesignArtifact`, `secav:DesignReview`, `secav:ReviewFinding`, `secav:DesignCompetency`

---

### Secondary Glossary
*Source: `coaching-governance/guides/requirements-inspection.md`*

A glossary located at the **end** of a requirements document that contains supporting terms: acronyms, references to external systems, naming conventions, and technical terms that appear occasionally but are not central to understanding the document.

Unlike the [primary glossary](#primary-glossary), secondary glossary terms carry lower risk of propagating ambiguity and do not require the same level of formal inspection, although they should still be reviewed by at least one reviewer additional to the author.

---

## Framework roles

### Quality Assistant
*Source: `coaching-governance/guides/defect-tracking.md`*

A team member designated to close defect tickets in the tracking system when the coach cannot sustain this activity on an ongoing basis. The designation requires: prior training provided by the coach, at least two sprints of supervised follow-up with explicit validation, and formal documentation of the designation in the coaching plan.

The role has a defined scope: it can only classify and close defects using the agreed criteria; it does not make decisions about quality thresholds or which defects to escalate. The role is also a development opportunity in `secav:ReviewCompetency` and `secav:DesignCompetency`.

**Associated SECAV-O term:** `secav:Engineer`, `secav:CoachingIntervention` (training), `secav:CompetencyAssessment`

---

### Coach
*Source: `ontology/secav-o.ttl`, general framework*

A Stakeholder (`secav:Coach`, subclass of `secav:Stakeholder`) responsible for observing engineering activities, collecting evidence, producing competency assessments, and generating coaching interventions.

The role the coach adopts varies by activity:

| Activity | Coach role |
|---|---|
| Peer reviews and formal inspections | [Silent observer](#silent-observer): takes notes, does not intervene during the session |
| Retrospectives without a Scrum Master or facilitator | Facilitator: leads the session following the defined protocol |
| Retrospectives with an external facilitator | Silent observer |
| Project planning | Participant: quality voice; may record concerns, dissent, and escalate |

**Engineer technical responsibility:** the coach observes and provides feedback but does not design tests, decide which defects to fix, or technically approve the advancement of artifacts. Verifying that the process was followed is not equivalent to replacing technical approval, which belongs to the Technical Lead and responsible engineers.

---

### Coach Committee
*Source: `coaching-governance/docs/coach-committee.md`*

A governance structure formed when an organization has more than one coach. The committee coordinates coaching practices, generates the organizational coaching plan, ensures consistent application of the framework across teams, and manages the escalation of problems that no individual coach can resolve alone.

It is not a hierarchy that replaces the coach's autonomy within their team; it is a coordination and standards body.

**Associated SECAV-O term:** `secavo:CoachCommittee` *(proposed, not yet declared in TTL)*

---

### Lead Coach
*Source: `coaching-governance/docs/coach-committee.md`*

The designated coordinator of the Coach Committee. Responsible for organizational coaching plan governance, cross-team escalation management, and external communication with management or HR. Designation may be made by management or by committee consensus.

**Associated SECAV-O term:** `secavo:LeadCoach` *(proposed, not yet declared in TTL)*

---

### Silent Observer
*Source: `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/retrospective-participation.md`*

The role the coach adopts in all review, inspection, and retrospective meetings (when there is an external facilitator). The coach:
- Does not express a technical opinion during the session.
- Does not approve or reject findings.
- Does not actively mediate disagreements.
- Does not correct engineers aloud.
- Takes observation notes as `secav:WorkProductEvidence`.
- Provides feedback — group, individual, or organizational — after the session.

**Reason:** if the coach intervenes during the session, engineers stop resolving issues independently and wait for the coach's judgment. The review ceases to be a peer review.

---

## Review and inspection activities

### ImprovementAction
*Source: `coaching-governance/guides/retrospective-participation.md`, `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md`*

A concrete improvement action agreed upon in a retrospective, with a defined owner and deadline, derived from observed data (review findings, defect metrics, risks) rather than opinions. It is a specialization of `secav:CoachingIntervention`.

**Associated SECAV-O term:** `secavo:ImprovementAction` (subclass of `secav:CoachingIntervention`)

---

### Formal Inspection
*Source: `coaching-governance/guides/formal-inspections.md`*

A structured review in which a group of participants with defined roles examines an artifact against explicit quality criteria, with the goal of identifying defects before they advance to the next development phase.

It differs from an ordinary code review in its degree of structure: defined roles (designated moderator, recorder, inspectors), mandatory individual preparation before the meeting, a moderated meeting with an agenda, and formal recording of findings in a `secav:ReviewRecord`.

The coach attends as a [silent observer](#silent-observer). The moderator is a designated inspector, not the coach.

**Associated SECAV-O term:** `secav:CodeReview` / `secav:DesignReview` / `secav:UnitTestDesignReview`, `secav:ReviewRecord`, `secav:ReviewFinding`

---

### Pending Point
*Source: `coaching-governance/guides/peer-review-sessions.md`*

An unresolved disagreement in a peer review that has been "sufficiently debated": both positions were expressed with technical arguments, no new evidence emerges, and the debate consumed disproportionate time. It is recorded in the `secav:ReviewRecord` as an unresolved finding and escalated to the Project Leader after the session, not during it.

---

### Peer Review
*Source: `coaching-governance/guides/peer-review-sessions.md`*

A structured review session in which engineers — not the coach — examine a code or design artifact. It differs from a formal inspection in its lower degree of structure: it does not require a mandatory individual preparation protocol or a recorder role. The coach attends as a [silent observer](#silent-observer).

**Associated SECAV-O term:** `secav:CodeReview` / `secav:DesignReview`

---

## Unit testing

### Boundary Value Analysis (BVA)
*Source: `coaching-governance/guides/unit-test-review.md`*

A systematic test-case design technique that identifies values at the extremes of each equivalence partition: numeric limits (minimum, maximum, zero, negative), collection limits (empty, one element, maximum capacity), and string limits (empty, space, one character, very long). Source: Beizer, *Software Testing Techniques* (1990).

---

### AAA / GWT Pattern (Arrange-Act-Assert / Given-When-Then)
*Source: `coaching-governance/guides/unit-test-review.md`*

A three-part structure for unit tests:
- **Arrange / Given:** configuration of input data and mock behavior.
- **Act / When:** execution of the method under test, preferably in a single line.
- **Assert / Then:** explicit verification of the expected result.

A test that has control flow logic (`if`, `for`) in the Act or Assert section has a test case design defect. Source: Meszaros, *xUnit Test Patterns* (2007).

---

### FIRST Principles
*Source: `coaching-governance/guides/unit-test-review.md`*

Five quality criteria (`secav:QualityCriterion`) that every unit test must satisfy:

| Principle | Criterion |
|---|---|
| **Fast** | Executes in milliseconds; no real I/O (databases, network, filesystem) |
| **Isolated** | No test depends on the result of another; no shared mutable global state |
| **Repeatable** | Same result in any environment, date, or time of execution |
| **Self-Validating** | Binary Pass / Fail result; no manual interpretation of logs |
| **Timely** | Written in parallel with or before production code (TDD) |

Source: Martin, *Clean Code* (2008), Chapter 9.

---

## Coaching cycle

### Initial Growth Baseline
*Source: `coaching-governance/docs/coaching-cycle.md`*

An engineer's competency profile established at the start of the coaching cycle or immediately after team launch. Includes: demonstrated competency, autonomy, review and inspection evidence, defect patterns, relevant training history, and contextual constraints. It is not a punitive ranking: it is the comparison point for measuring longitudinal growth.

**Associated SECAV-O term:** `secav:CompetencyAssessment`, `secav:WorkProductEvidence`

---

### Annual Coaching Plan
*Source: `coaching-governance/docs/coaching-cycle.md`*

An artifact that defines competency-development priorities for the year, establishes the initial baseline, sets objectives and expected outcomes, selects metrics and evidence sources, and identifies the activities and artifacts the coach will observe. It is the framework within which coaching sprints are executed.

**Associated SECAV-O term:** `secavo:AnnualCoachingPlan`

---

### Organizational Coaching Plan
*Source: `coaching-governance/docs/coach-committee.md`*

A plan generated by the Coach Committee that aggregates and coordinates the individual plans for each team. Includes organization-wide coaching objectives, cross-team competency baseline, organizational risk register, coach assignment matrix, and a shared calendar of coaching activities.

**Associated SECAV-O term:** `secavo:AnnualCoachingPlan` (organizational scope)

---

### Member Preparation
*Source: `coaching-governance/docs/coaching-cycle.md`*

An activity that occurs before team launch or when a new member joins, in which the engineer receives: project purpose and objectives, delivery model, engineering practices, quality expectations, known risks, key artifacts, review and inspection expectations, testing practices, human validation responsibilities for AI-assisted work, and metrics that will be collected. Its focus is developmental, not eligibility assessment.

---

### Coaching Sprint
*Source: `coaching-governance/docs/coaching-cycle.md`*

A bounded coaching iteration that: reviews the annual plan, selects competency objectives for the sprint, observes engineering activities and collects evidence, applies coaching interventions, and conducts a retrospective. Duration is not prescribed; it must be long enough to produce observable evidence and short enough to allow timely replanning.

**Associated SECAV-O term:** `secavo:CoachingSprint`

---

## Metrics and defect traceability

### detectionMethod
*Source: `coaching-governance/guides/defect-tracking.md`*

A data property of `secavo:DefectObservation` that records how the defect was found: formal inspection, peer review, automated test, manual test, user report, or other. Enables calculating the relative effectiveness of each detection technique.

**Associated SECAV-O term:** `secavo:detectionMethod`

---

### Defect Density per Module
*Source: `coaching-governance/guides/defect-tracking.md`*

A metric that counts the number of defects recorded per module or component in a given period. Identifies the highest-risk components that should be priority candidates for formal inspection.

**Associated SECAV-O term:** `secavo:Metric`, `secavo:DefectObservation`

---

### Review Effectiveness
*Source: `coaching-governance/guides/defect-tracking.md`*

The percentage of defects detected in code review or formal inspection activities relative to the total defects recorded in the period. A low value indicates that reviews are not capturing defects before they escape to later phases.

**Associated SECAV-O term:** `secavo:Metric`, `secavo:ReviewObservation`

---

### phaseDetected
*Source: `coaching-governance/guides/defect-tracking.md`*

A data property of `secavo:DefectObservation` that records in which development phase the defect was found: code review, formal inspection, unit test, integration, system, acceptance, production. Together with `phaseInjected` it enables calculating the relative cost of late detection.

**Associated SECAV-O term:** `secavo:phaseDetected`

---

### phaseInjected
*Source: `coaching-governance/guides/defect-tracking.md`*

A data property of `secavo:DefectObservation` that records in which development phase the defect was introduced: requirements, architecture design, detailed design, coding, unit test design, system test design, acceptance test design. The distribution of `phaseInjected` across sprints indicates which phases generate the most defects and should be prioritized for inspection.

**Associated SECAV-O term:** `secavo:phaseInjected`

---

### Escape Rate
*Source: `coaching-governance/guides/defect-tracking.md`*

The percentage of defects found in production or late phases (integration, system, acceptance) relative to the total defects recorded. A high escape rate indicates that inspections and reviews in early phases are not effective or are not occurring.

**Associated SECAV-O term:** `secavo:Metric`, `secavo:DefectObservation`

---

## Incremental adoption

### Go / Pivot / Stop Decision
*Source: `coaching-governance/guides/incremental-adoption.md`*

Three possible outcomes of evaluating a pilot framework iteration:

| Decision | Condition |
|---|---|
| **Go (Scale)** | Evidence is consistent, the complete chain is documented, no governance blockers |
| **Pivot (Correct)** | Systematic friction detected; a correction is applied and the iteration repeats |
| **Stop** | A foundational assumption is invalid and uncorrectable; findings are documented to avoid a larger investment in something that does not work in this context |

---

### Fail Fast
*Source: `coaching-governance/guides/incremental-adoption.md`*

An incremental adoption philosophy whose goal is to make incorrect assumptions, bottlenecks, and technical or governance constraints visible at the earliest possible stage, when the cost of correction is minimal. A controlled failure with empirical data is a successful learning outcome, not a failure.

---

### Proof of Concept (PoC)
*Source: `coaching-governance/guides/incremental-adoption.md`*

A minimal experiment that answers a single question: Is this feasible in this context? In the framework context: executing one engineering activity with a coach and one engineer before launching a full pilot, to verify that the basic observation and evidence mechanisms work.

---

### End-to-End Tracer
*Source: `coaching-governance/guides/incremental-adoption.md`*

A thin but complete vertical slice of the coaching system: one complete cycle from activity selection through evidence collection, `secav:CompetencyAssessment`, `secav:CoachingIntervention`, and `secavo:SprintRetrospective`, before expanding scope. Verifies that the complete chain works before investing in scaling.

---

## Risk management

### Corrective / Contingency Action
*Source: `coaching-governance/guides/risk-management.md`*

A predefined action executed when a risk materializes. Examples: change the sprint objective, add an independent reviewer, escalate a blocked dependency, review the baseline.

**Associated SECAV-O term:** `secavo:CorrectiveAction`

---

### Preventive Action
*Source: `coaching-governance/guides/risk-management.md`*

A predefined action to reduce the probability that a risk occurs. Examples: clarify acceptance criteria, schedule peer reviews, provide training, increase inspection frequency in high-risk modules.

**Associated SECAV-O term:** `secavo:PreventiveAction`