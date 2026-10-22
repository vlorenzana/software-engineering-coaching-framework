# Coach Observation Checklist by Engineering Activity

## Purpose

This checklist allows the coach to record, during any observation session, the positive behaviors and alert signals the team exhibits in each engineering activity. Each row is an observable: something the coach can see, hear, or read directly — not an inference.

**Column convention:**
- ✓ Positive behavior — record as `secav:Evidence` for competency assessment
- ⚠ Alert signal — consider `secav:CoachingIntervention`

---

## Cross-cutting rule — Coach presence in all lifecycle phases

> **Code of Ethics, Principle 18.** The coach has an obligation to observe lifecycle phase activities according to a risk-based coverage plan. Presence is required for high-risk sessions; risk-based sampling is permitted for routine sessions with experienced team members (see obligation 1). Presence is the basis for observations, certifications (direct sign-off or remote endorsement), and competency evidence.

| Rule | When | SECAV-O Term |
|------|------|--------------|
| **Prioritize presence at high-risk sessions.** The coach should attend all sessions involving critical artifacts, new or low-competency team members, high-complexity phases, or phases with a history of defect injection. For routine sessions with experienced team members, **risk-based sampling** (a documented subset per sprint) is permitted — provided criteria, coverage targets, and rationale are in the coaching plan. | All phases | `secav:CoachObservation` · `secav:observedDuring` |
| **Planned non-attendance (within approved sample):** the session falls outside the coaching plan's coverage for this sprint. No absence record required — mark it as non-observed in the coverage table. This is an expected sampling outcome, not a gap. | Sampling plan sessions | coaching plan coverage table |
| **Unplanned absence (session was within intended coverage):** the coach must record a `secav:CoachAbsenceRecord` before the session, not retroactively. The record must state the reason and the consequence. Undocumented absence is the worst case — there is no evidence of what occurred. | Unplanned missed session | `secav:CoachAbsenceRecord` · `secav:absenceReason` · `secav:absenceConsequence` |
| **Absence ≠ approval.** The coach not attending a session does not constitute endorsement, sign-off, or certification of what occurred in that session. | All phases | absence of `secav:CoachObservation` is a gap, not a neutral record |
| **For review activities (peer review, walkthrough, inspection, results review):** the session must be certified via either (a) a direct `secav:CoachReviewSignOff` when the coach was present, or (b) a `secav:CoachRemoteEndorsement` when absent — issued only after the coach reviews the designated observer's `secav:ObserverReport`. Both mechanisms are mutually exclusive. Findings remain provisional until one is issued. | Review phases | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` + `secav:ObserverReport` |
| **For non-review activities (planning, design, implementation, test execution): no observation record.** If absent (unplanned), the coach records a `secav:CoachAbsenceRecord` and there is no `secav:CoachObservation` for that session. | Production phases | `secav:CoachAbsenceRecord` |
| **Designate a trained observer for critical sessions.** When unplanned absence is unavoidable for a high-risk phase, the coach must name a `secav:designatedObserver` before the session begins, not after. The observer files a `secav:ObserverReport` immediately after the session. | Critical sessions | `secav:designatedObserver` on `secav:CoachAbsenceRecord` · `secav:ObserverReport` |

> **How to apply this rule per checklist group:** before completing any group's observation signals for a session, confirm coach presence and coverage status. If the coach was not present: (a) do not record ✓ or ⚠ signals for that session; (b) if the session was within the intended coverage (unplanned absence), record a `secav:CoachAbsenceRecord`; if it was outside the approved sample, mark it in the coaching plan as non-observed — no absence record required; (c) if the session was a review activity and no direct sign-off applies, determine whether a `secav:CoachRemoteEndorsement` via a designated observer's `secav:ObserverReport` is appropriate (Principle 16).

---

## Cross-cutting rule — Coach review authority and finding type

> **Code of Ethics, Principle 22.** The coach may review any design artifact for compliance with formally adopted processes. The coach's authority extends to deviations from documented requirements — not to personal preferences. Every finding must be classified as either a **process compliance finding** (`secav:ProcessComplianceFinding`) or a **coaching recommendation** (`secav:CoachingRecommendation`).

| Rule | When | SECAV-O Term |
|------|------|--------------|
| **Process compliance finding = deviation from a documented obligation.** When the artifact deviates from an adopted process, standard, checklist section, or acceptance criterion, record a `secav:ProcessComplianceFinding` and cite the specific requirement. The process — not the coach personally — requires the correction; the coach documents and reports the deviation, and enforcement flows through the team's process governance (Principle 22, consistent with Principle 20). | Any artifact review | `secav:ProcessComplianceFinding` · `secav:referencedProcessRequirement` |
| **Coaching recommendation = improvement not yet in the process.** When the coach sees an improvement opportunity not covered by any adopted process requirement, record a `secav:CoachingRecommendation`. The engineer may accept or decline it (Principle 20). | Any artifact review | `secav:CoachingRecommendation` |
| **Always cite the requirement.** A `secav:ProcessComplianceFinding` without a `secav:referencedProcessRequirement` value is invalid — it cannot distinguish from a personal preference and cannot be used to compel a change. | All compliance findings | `secav:referencedProcessRequirement` required |
| **Framework recommendations become binding only when adopted into the process.** SECAV-O guidance acquires the force of a process requirement only when the team formally adopts it. Until then, framework-based observations are `secav:CoachingRecommendation`. | All sessions | classification gate before recording finding type |
| **Contribute to process evolution.** Repeated `secav:CoachingRecommendation` instances on the same topic are signal for process improvement — propose adoption through the appropriate channel. | Retrospectives / reports | `secavo:QualityPlanningConcern` in management report |

> **How to apply this rule:** before recording any finding during an artifact review, ask: "Is this deviation from a documented, adopted requirement — or is it my professional judgment that the artifact could be better?" The answer determines the finding type. Misclassifying a personal preference as a compliance finding violates Principle 22 and Principle 1.

---

## Cross-cutting rule — Design consultation at the engineer's request

> **Code of Ethics, Principle 23.** When a team member has design questions, the coach may respond — but only within their declared consulting scope. The coach's primary obligation is to know and honestly declare where their technical consulting capacity ends. Consultation is always engineer-initiated.

| Rule | When | SECAV-O Term |
|------|------|--------------|
| **Consultation is engineer-initiated.** The coach does not volunteer unsolicited design opinions during sessions. If an engineer asks, the coach may respond — subject to the rules below. | Any session | `secav:DesignConsultation` created on engineer request only |
| **Self-assess before responding.** Before answering a design question, the coach must verify whether the domain falls within their declared `CoachConsultingScope`. General engineering experience is not a qualification for every domain. | Every consultation | `secav:coachQualified` on `secav:DesignConsultation` |
| **Respond only within declared scope.** If the question falls within the coach's declared consulting scope, the coach may provide design recommendations. The recommendation is advisory — the engineer decides. | In-scope questions | `secav:coachQualified = true` · `secav:consultationDomain` matches declared scope |
| **Declare limits immediately.** If the question falls outside the coach's competence, the coach says so immediately, without offering a guess or partial guidance framed as authoritative. The gap is recorded. | Out-of-scope questions | `secav:coachQualified = false` · knowledge gap in coaching log and management report |
| **Document every consultation.** Whether in-scope or out-of-scope, every design consultation is logged: domain, date, engineer who asked, and whether the coach was qualified to respond. | All consultations | `secav:DesignConsultation` with `secav:consultationDomain` and `secav:coachQualified` |
| **Maintain a current consulting scope declaration.** The coach must keep a `secav:CoachConsultingScope` document listing their qualified domains, reviewed at least every six months. | Ongoing | `secav:CoachConsultingScope` · `secav:scopeDeclarationDate` |
| **No transferred accountability.** The engineer retains full professional accountability for any design decision, even one made by adopting the coach's recommendation directly. | All consultations | `secav:CoachingRecommendation` is advisory; design decision accountability stays with engineer |

---

## 1. Requirements Definition and Acceptance Criteria

> SECAV-O activity: `secav:RequirementsActivity`, `secav:AcceptanceCriteriaDefinition`, `secav:RequirementsReview`
>
> **Key principle:** Defect types "vague", "ambiguous", "unclear", and "incomplete" in requirements are **invisible to automated tools** — they can only be detected through peer review, walkthrough, or formal inspection (preferred). These defects carry the highest downstream cost in the lifecycle: injected at the earliest phase, detected late. The work plan **must** include at least one `secav:RequirementsReview` session for each sprint or feature set before implementation begins, endorsed by a coach sign-off.

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 1.1 | ✓ | The team defines acceptance criteria before starting coding (Given/When/Then format or another explicit format) | `secav:AcceptanceCriteriaDefinition` |
| 1.2 | ✓ | Acceptance criteria produce a documented artifact (BDD scenario, test specification, ticket with complete AC) | `secav:AcceptanceCriteriaDefinition` → `secav:produces` → `secav:Artifact` |
| 1.3 | ✓ | Edge cases and error paths are explicitly stated in the criteria — not only the happy path | `secav:AcceptanceCriterion` |
| 1.4 | ✓ | The engineer can verbally explain the requirement before coding | `secav:WorkProductEvidence` |
| 1.5 | ✓ | The sprint or feature work plan explicitly includes a peer review, walkthrough, or formal inspection of requirements before implementation starts | `secav:RequirementsReview` in work plan |
| 1.6 | ✓ | The requirements review session produces at least one documented finding — including explicit "no defects found" — before coding begins | `secav:producesReviewFinding` · `secav:RequirementsDefect` |
| 1.7 | ✓ | The coach certifies the requirements review via direct sign-off (when present) or remote endorsement via a designated observer's `secav:ObserverReport` (when absent — Principle 16), confirming the session was conducted acceptably before implementation begins | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 1.8 | ✓ | Review participants flag "vague", "ambiguous", "unclear", or "incomplete" defects using explicit labels — not generic comments | `secav:VagueRequirement` / `secav:AmbiguousRequirement` / `secav:UnclearRequirement` / `secav:IncompleteRequirement` |
| 1.9 | ⚠ | A user story enters the sprint without defined acceptance criteria | `secav:HappyPathOnlyReview` (risk) |
| 1.10 | ⚠ | The team starts coding with ambiguous requirements without requesting clarification | `secav:AmbiguousRequirement` unresolved; `secav:MissingReviewContext` |
| 1.11 | ⚠ | Acceptance criteria are written after implementation (post-hoc) | absence of `secav:AcceptanceCriteriaDefinition` as a preventive activity |
| 1.12 | ⚠ | No traceability exists between acceptance criteria and automated test cases | `secav:QualityCriterion` without `secav:AutomationGate` |
| 1.13 | ⚠ | Implementation begins on requirements that have not been subject to any peer review, walkthrough, or inspection | `secav:MissingRequirementsReview` — highest-risk antipattern in the lifecycle |
| 1.14 | ⚠ | The requirements review was conducted but the coach issued neither a direct sign-off nor a remote endorsement — findings cannot be used as planning evidence | absence of `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` on `secav:RequirementsReview` |

---

## 2. Design and API Contracts

> SECAV-O activity: `secav:DesignActivity`, `secav:APIContractDefinition`

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 2.1 | ✓ | The team defines the API contract (schema, endpoints, error responses) before implementing the client or server | `secav:APIContractDefinition` |
| 2.2 | ✓ | A versioned contract artifact exists (OpenAPI, AsyncAPI, Protobuf, or equivalent) | `secav:APIContractArtifact` → `secav:DesignArtifact` |
| 2.3 | ✓ | API contract changes trigger a design review before being merged | `secav:DesignReview` |
| 2.4 | ✓ | The architect has identified and documented critical modules before development starts | `secav:SourceCodeArtifact` with documented criticality |
| 2.5 | ⚠ | Design decisions are made during code review (too late) | `secav:LateArchitecturalDiscussion` |
| 2.6 | ⚠ | The API contract is undocumented — the client infers behavior from the server code | absence of `secav:APIContractArtifact` |
| 2.7 | ⚠ | Interface changes are introduced in the PR without prior notification to consumers | `secav:MissingReviewContext` |
| 2.8 | ⚠ | The critical module list was not communicated to the coach or Technical Lead at project start | absence of risk identification in `secav:DesignActivity` |

---

## 3. Implementation and Developer Cognitive State

> SECAV-O activity: `secav:CodeImplementation`, `secav:DeveloperCognitiveState`

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 3.1 | ✓ | The engineer performs a self-review of the complete diff before opening the PR | `secav:SelfReview` |
| 3.2 | ✓ | The engineer protects deep-work blocks (no interruptions while implementing complex logic) | `secav:DeepWorkCondition` |
| 3.3 | ✓ | The engineer respects cognitive load limits — does not mix multiple unrelated changes in a single PR | `secav:FatigueManagementCondition` |
| 3.4 | ✓ | The PR is a manageable size (most changes fit in a 60-min review session) | `secav:SelfReviewCondition` |
| 3.5 | ⚠ | The engineer shows visible signs of fatigue when reviewing or coding (repeated basic errors, slow responses) | `secav:FatigueManagementCondition` (absent) |
| 3.6 | ⚠ | The engineer merges code without having performed a self-review — confirmed when asked | absence of `secav:SelfReview` |
| 3.7 | ⚠ | PRs consistently arrive with more than 500 lines of effective change | `secav:OversizedPullRequest` |
| 3.8 | ⚠ | The engineer works on multiple features in parallel within the same sprint with no prioritization signals | `secav:DeepWorkCondition` (compromised) |

---

## 4. Automation Gates (Pre-commit, Typing, Coverage)

> SECAV-O activity: `secav:AutomationGate`, `secav:PreCommitHook`, `secav:StrictTypingPolicy`, `secav:CodeCoverageGate`

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 4.1 | ✓ | The repository has active pre-commit hooks that block code with style errors or exposed secrets | `secav:PreCommitHook` |
| 4.2 | ✓ | Strict typing is enabled (TypeScript strict, mypy, etc.) and the team respects it without suppressing errors | `secav:StrictTypingPolicy` |
| 4.3 | ✓ | Test coverage has a defined threshold and the pipeline rejects PRs that reduce it | `secav:CodeCoverageGate` with `secav:coverageThreshold` |
| 4.4 | ✓ | Team members can explain what each gate checks and why it exists | `secav:criterionStatement` present and communicated |
| 4.5 | ⚠ | The team disables or suppresses gates to unblock a deploy ("we'll fix it later") | effective absence of `secav:AutomationGate` |
| 4.6 | ⚠ | Typing errors are suppressed with `// @ts-ignore` comments or equivalents without justification | `secav:StrictTypingPolicy` (compromised) |
| 4.7 | ⚠ | Test coverage drops sprint over sprint without the team mentioning it or taking it as an action | `secav:CodeCoverageGate` without follow-up |
| 4.8 | ⚠ | The team does not know what the CI pipeline checks — they only know "if it passes, fine" | `secav:DeterministicAnalysisActivity` without team ownership |
| 4.9 | ✓ | The complete CI pipeline (build, test, static analysis) runs on every PR and its result is visible to the whole team | `secav:ContinuousIntegrationActivity` |
| 4.10 | ⚠ | The CI pipeline fails intermittently and the team normalizes it — failures are treated as "noise" rather than a signal | `secav:ContinuousIntegrationActivity` compromised |

---

## 5. Peer Code Review

> SECAV-O activity: `secav:CodeReview`, `secav:ReviewAntipattern` and subclasses

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 5.1 | ✓ | The reviewer validates the intent of the change before reading the diff (ticket, spec, or PR description) | `secav:FormalReviewRequest` with `secav:requestDescription` |
| 5.2 | ✓ | Review comments are directed at the code, not the person ("this block could..." vs. "your code is...") | `secav:ReviewerAssertiveClosureCondition` |
| 5.3 | ✓ | The reviewer distinguishes between blocking observations and optional suggestions | `secav:ReviewFinding` with documented severity |
| 5.4 | ✓ | The reviewer arrives rested and having read the material when the session was scheduled in advance | `secav:ReviewerEnergyCondition`, `secav:ReviewerFocusCondition` |
| 5.5 | ✓ | The team closes comment threads explicitly — does not leave conversations open indefinitely | absence of `secav:InfiniteCommentLoop` |
| 5.6 | ✓ | PRs include a clear description of what changed, why, and how to test it | `secav:requestDescription` |
| 5.7 | ⚠ | The reviewer approves the PR without comments in under 2 minutes (rubber-stamp review) | `secav:RubberStampApproval` |
| 5.8 | ⚠ | The review lasts more than 90 minutes without breaks — the reviewer visibly loses concentration | `secav:OversizedReviewSession` |
| 5.9 | ⚠ | The PR arrives without a description or with a generic one ("fixes bug") | `secav:MissingReviewContext` |
| 5.10 | ⚠ | The code arrives in draft state (WIP) marked as ready for review | `secav:PrematureReviewRequest` |
| 5.11 | ⚠ | Reviewers flag style violations that should be caught by the linter | `secav:ManualStyleReview` |
| 5.12 | ⚠ | A single reviewer consistently approves all team PRs | `secav:SingleApproverBottleneck` |
| 5.13 | ⚠ | There are review threads that have been unresolved for more than 3 sprints | `secav:InfiniteCommentLoop` |
| 5.14 | ⚠ | Comments are punitive or dismissive — "this is a mess", "how did you think of this?" | `secav:PunitiveReviewApproach` |
| 5.15 | ⚠ | A reviewer dictates the solution instead of pointing out the problem and leaving the decision to the author | `secav:ReviewerDictatorship` |
| 5.16 | ⚠ | The review only validates the happy path — no edge case or error case was questioned | `secav:HappyPathOnlyReview` |
| 5.17 | ⚠ | Comments are ironic, sarcastic, or condescending — the tone is not deliberately punitive but damages psychological safety | `secav:NonEmpathicReviewFeedback` |
| 5.18 | ✓ | All findings (defects, observations, or explicit "no defects found") are recorded in the tracking tool before closing the session | `secav:producesReviewFinding` |
| 5.19 | ✓ | The coach issues a process sign-off confirming the review was conducted acceptably (roles followed, findings documented) | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 5.20 | ✓ | When the team agrees on a fix direction during the session, a proposed solution is recorded alongside the finding | `secav:proposedSolution` (optional) |
| 5.21 | ⚠ | The session ends without any written findings — only verbal comments | absence of `secav:producesReviewFinding` |
| 5.22 | ⚠ | The coach issues neither a direct sign-off nor a remote endorsement — the review findings cannot be used as valid competency evidence | absence of `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

---

## 6. Formal Inspections of Critical Modules

> SECAV-O activity: `secav:CodeReview` (inspection), `secav:HumanValidationActivity`

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 6.1 | ✓ | Inspection material was distributed at least 24–48 h before the meeting | `secav:ReviewerReadiness` |
| 6.2 | ✓ | All participants arrived at the meeting with documented observations (individual preparation completed) | `secav:ReviewerCriticalAnalysisCondition` |
| 6.3 | ✓ | The moderator keeps focus on the artifact — not on the author or solutions | `secav:ReviewFinding` produced without personalization |
| 6.4 | ✓ | The author listens and responds without defending — does not debate during the meeting | `secav:WorkProductEvidence` (observable attitude) |
| 6.5 | ✓ | The recorder documents findings with type and severity during the meeting | `secav:ReviewFinding` with formal record |
| 6.6 | ✓ | The coach verifies rework of critical findings before the module advances | `secav:ReviewRecord` updated |
| 6.7 | ⚠ | A participant did not prepare the material — the inspection becomes live reading | absence of `secav:ReviewerReadiness` |
| 6.8 | ⚠ | The inspection meeting was cancelled or shortened without technical justification | `secavo:QualityPlanningConcern` |
| 6.9 | ⚠ | The author defends or argues decisions during the meeting instead of listening | `secav:PunitiveReviewApproach` (inverse dynamic) |
| 6.10 | ⚠ | The inspection did not produce a documented `secav:ReviewRecord` | absence of `secav:ReviewRecord` |
| 6.11 | ⚠ | The same defect type appears in multiple inspected modules (systemic pattern) | `secav:CoachingIntervention` → `secavo:ImprovementAction` |
| 6.12 | ⚠ | Management uses inspection findings to evaluate the author's performance punitively | `secavo:QualityPlanningConcern` |
| 6.13 | ✓ | All findings (defects, observations, or explicit "no defects found") are recorded before closing the inspection — including type, severity, and proposed solution when available | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 6.14 | ✓ | The coach issues a formal process sign-off confirming the inspection was conducted acceptably | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 6.15 | ⚠ | The inspection closes without written findings or the sign-off is not issued — the session findings are not valid as competency evidence | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

---

## 7. Unit Testing and Unit Test Design

> SECAV-O activity: `secav:TestingActivity`, `secav:UnitTestDesignReview`, `secav:TestSelectionForReview`
>
> **Key principle:** Unit test code is a work product. It requires individual peer review — preferably a formal inspection for tests covering critical system paths — independently of CI automation results.

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 7.1 | ✓ | Tests have names that describe behavior, not implementation ("should return 404 when user not found") | `secav:WorkProductEvidence` |
| 7.2 | ✓ | Each test has a single identifiable failure point (FIRST principle: Independent) | `secav:QualityCriterion` |
| 7.3 | ✓ | Tests cover error paths and boundary values, not only the success flow | `secav:HappyPathOnlyReview` absent |
| 7.4 | ✓ | Tests run in milliseconds — no network or filesystem dependencies in unit tests | `secav:QualityCriterion` (FIRST: Fast) |
| 7.5 | ✓ | The team knows the project's coverage threshold and can justify it | `secav:CodeCoverageGate` with known `secav:coverageThreshold` |
| 7.6 | ✓ | Test code for critical modules is individually reviewed as a work product before merging — peer review, walkthrough, or inspection | `secav:UnitTestDesignReview` |
| 7.7 | ✓ | The team identifies and schedules critical tests (payment, security, concurrency, data integrity paths) for formal review at sprint start | `secav:TestSelectionForReview` · `secav:CriticalUnitTest` |
| 7.8 | ✓ | When critical tests are selected for review, a formal inspection is the preferred method over a walkthrough or simple peer review | `secav:CriticalUnitTest` → `secav:UnitTestDesignReview` (inspection intensity) |
| 7.9 | ⚠ | Tests only validate the happy path — no tests for null, empty, or out-of-range values | `secav:HappyPathOnlyReview` |
| 7.10 | ⚠ | Unit tests have external dependencies (database, API, system clock without injection) | `secav:QualityCriterion` (FIRST: Fast violated) |
| 7.11 | ⚠ | Multiple tests fail when a single condition fails — high coupling between tests | `secav:QualityCriterion` (FIRST: Independent violated) |
| 7.12 | ⚠ | The team increases coverage with trivial tests to pass the gate, without evaluating real cases | `secav:CodeCoverageGate` compromised in quality |
| 7.13 | ⚠ | PRs do not include tests for new logic (only production code) | absence of associated `secav:TestingActivity` |
| 7.14 | ⚠ | Test code on critical modules is merged without any individual peer review — CI passing is treated as sufficient validation | `secav:UnreviewedTestCode` |
| 7.15 | ⚠ | Assertions in tests always pass regardless of the behavior under test (e.g., asserting a mock value instead of the actual unit result) | `secav:TautologicalAssertion` |
| 7.16 | ⚠ | Tests fail intermittently for reasons unrelated to the behavior they verify (time-dependent, environment-dependent, order-dependent) | `secav:BrittleTest` |
| 7.17 | ✓ | All findings from the unit test design review (defects, observations, or explicit "no defects found") are recorded in the tracking tool before closing the session | `secav:producesReviewFinding` |
| 7.18 | ✓ | The coach issues a process sign-off confirming the unit test design review was conducted acceptably (roles followed, findings documented, review not rubber-stamped) | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 7.19 | ✓ | When the review identifies a test design problem and the team agrees on a fix approach, the proposed solution is recorded alongside the finding | `secav:proposedSolution` (optional) |
| 7.20 | ⚠ | The unit test design review session ends without any written findings — verbal comments only | absence of `secav:producesReviewFinding` |
| 7.21 | ⚠ | The coach issues neither a direct sign-off nor a remote endorsement on the unit test design review — findings cannot be used as valid competency evidence | absence of `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

---

## 8. AI-Assisted Code Review

> SECAV-O activity: `secav:AIAssistedActivity`, `secav:HumanValidationActivity`, `secav:AIReviewPromptConfiguration`, `secav:ReviewDimension`

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 8.1 | ✓ | The review pipeline applies deterministic tools (linter, static scanner) before human review | `secav:DeterministicAnalysisActivity` → `secav:precedes` → human review |
| 8.2 | ✓ | The team configures the AI tool with project context (framework, version, security conventions) | `secav:AIReviewPromptConfiguration` with `secav:hasContextDefinition` |
| 8.3 | ✓ | The configuration includes impact analysis, security evaluation, and test case generation | `secav:hasImpactAnalysisInstruction`, `secav:hasSecurityEvaluationInstruction`, `secav:hasTestGenerationInstruction` |
| 8.4 | ✓ | Reviewers audit AI suggestions before applying them — verifying that methods exist in the version in use | `secav:HumanValidationActivity` active |
| 8.5 | ✓ | AI-generated code PRs are classified by risk before routing (routine / attention / critical) | `secav:ReviewRiskLevel` |
| 8.6 | ✓ | The team monitors false negatives — high-risk PRs that passed as routine | `secav:ReviewObservation` |
| 8.7 | ⚠ | The team accepts AI suggestions without critical review — does not verify that proposed methods exist | `secav:InsufficientAICodeScrutiny` |
| 8.8 | ⚠ | AI is used to approve or block changes autonomously, without human review | violation of `secav:requiresHumanValidation` |
| 8.9 | ⚠ | AI tool false positives are high and the team ignores them instead of adjusting the configuration | `secav:ReviewObservation` (alert fatigue) |
| 8.10 | ⚠ | AI-generated code arrives without the decision history that explains the design | `secav:MissingReviewContext` |
| 8.11 | ⚠ | Critical modules with AI-generated code do not receive additional formal inspection | absence of `secav:HumanValidationActivity` for `secav:AIAssistedActivity` in critical module |
| 8.12 | ⚠ | The team does not question AI code because "it compiles and the tests pass" | `secav:RubberStampApproval` applied to AI code |
| 8.13 | ✓ | Each review dimension (impact, security, tests, context) is explicitly configured in the AI tool prompt | `secav:ReviewDimension` |
| 8.14 | ⚠ | PRs classified as routine reach production with significant defects — the risk classification model has false negatives | `secav:ReviewEscapeObservation` |

---

## 9. Organizational Adoption of the New Working Model

> SECAV-O activity: `secav:AdoptionBehavior` and its seven subclasses, grouped by `secav:AdoptionPillar`
>
> **Context:** This group observes whether leaders, teams, and individuals have internalized the new working model in their daily behaviors. It is not individual supervision — it is a collective signal of cultural adoption. The change agent (`secav:ChangeAgent`) activates interventions when systemic alert signals appear.
>
> **Recommended frequency:** biweekly or monthly. Use direct observation in rituals + eNPS pulse (`secav:PulseSurveyMeasurement`, `secav:DirectRitualObservation`).

### Pillar 1 — Leadership and Modeling (Leaders / PMs)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 9.1 | ✓ | Leaders and PMs use new digital tools as the primary communication channel — not traditional email | `secav:LeaderDigitalToolAdoption` |
| 9.2 | ✓ | Leaders publicly acknowledge (in meetings or institutional channels) collaborators who apply the new behaviors and methodologies | `secav:PublicRecognitionOfNewBehaviors` |
| 9.3 | ⚠ | Leaders continue using email as the primary channel, maintaining dual-process ambiguity | absence of `secav:LeaderDigitalToolAdoption` |
| 9.4 | ⚠ | Public acknowledgements flag errors or non-compliance — new behaviors are never celebrated | absence of `secav:PublicRecognitionOfNewBehaviors` |

### Pillar 2 — Efficient Collaboration (Teams)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 9.5 | ✓ | The team keeps project documentation centralized and up to date in shared platforms (single repository per project) | `secav:CentralizedDocumentationPractice` |
| 9.6 | ✓ | The team replaces long status meetings with short synchronizations focused on blockers | `secav:FocusedSynchronizationPractice` |
| 9.7 | ⚠ | Documentation exists in silos — local files, email threads, private chats — with no centralized access | absence of `secav:CentralizedDocumentationPractice` |
| 9.8 | ⚠ | Weekly status meetings continue in the same long format with no transition toward short blocker-focused syncs | absence of `secav:FocusedSynchronizationPractice` |

### Pillar 3 — Open Communication (Teams)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 9.9 | ✓ | Team members express doubts, errors, and blockers early and transparently — risk and impediment registers are updated promptly | `secav:EarlyTransparentCommunication` |
| 9.10 | ⚠ | Members hold back doubts or errors until they escalate — problems surface late, in production or at the retrospective | absence of `secav:EarlyTransparentCommunication` |

### Pillar 4 — Continuous Adaptability (Everyone)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 9.11 | ✓ | Members apply guides and training materials autonomously before escalating basic questions | `secav:AutonomousGuideApplication` |
| 9.12 | ⚠ | Members escalate basic questions without first consulting available guides or materials, generating support overload | absence of `secav:AutonomousGuideApplication` |

### Pillar 5 — Feedback and Innovation (Everyone)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 9.13 | ✓ | Members contribute constructive proposals about the new model in retrospective sessions — proposals are implemented | `secav:ConstructiveRetrospectiveFeedback` |
| 9.14 | ⚠ | Retrospectives produce no team-adjustment proposals — the format is declarative or complaint-based with no action | absence of `secav:ConstructiveRetrospectiveFeedback` |

---

## 10. Technical Leadership Behaviors (Engineering Managers and Tech Leads)

> SECAV-O activity: `secav:LeaderBehavior` and subclasses, grouped by `secav:TechnicalLeadershipDimension`
>
> **Context:** This group observes the behaviors of the technical leader (Engineering Manager or Tech Lead) across their three strategic dimensions: people, architecture, and strategy. It does not evaluate individual technical skill, but the capacity to multiply collective talent and align solutions with business objectives.
>
> **Recommended frequency:** monthly or per sprint, with quarterly review of the four evaluation indicators (10.12–10.15).

### Dimension 1 — People and Mentorship (35% of leadership weight)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 10.1 | ✓ | The leader holds 1-on-1 sessions on a regular cadence focused on professional growth — not only sprint status | `secav:ActiveMentorship` |
| 10.2 | ✓ | Production post-mortems end with process or tooling actions — never pointing at individuals | `secav:PsychologicalSafetyPromotion` |
| 10.3 | ✓ | The leader defines the "what" and "why" of change, but grants the team autonomy to decide the "how" | `secav:EffectiveDelegation` |
| 10.4 | ✓ | The leader delivers real-time constructive feedback and publicly acknowledges work done well | `secav:ContinuousFeedbackBehavior` |
| 10.5 | ⚠ | The leader reviews and approves every minor technical decision — engineers wait for instructions instead of taking initiative | absence of `secav:EffectiveDelegation` (micromanagement) |
| 10.6 | ⚠ | Post-mortems end in individual blame or silence — no improvement actions are produced | absence of `secav:PsychologicalSafetyPromotion` |
| 10.7 | ⚠ | No 1-on-1 cadence exists — the leader's interaction with engineers occurs only in group meetings or when there are problems | absence of `secav:ActiveMentorship` |

### Dimension 2 — Architecture and Code (30% of leadership weight)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 10.8 | ✓ | Significant architecture decisions are documented in ADRs accessible to the entire team | `secav:ArchitectureDecisionDocumentation` |
| 10.9 | ✓ | The team allocates 15–20% of sprint effort to code health (technical debt, refactoring, maintenance) — negotiated with Product | `secav:TechnicalDebtNegotiation` |
| 10.10 | ⚠ | Architecture decisions are made informally or in ephemeral conversations — not recorded or reviewable | absence of `secav:ArchitectureDecisionDocumentation` |
| 10.11 | ⚠ | Technical debt is never presented to Product as priority work — it accumulates sprint after sprint without negotiation | absence of `secav:TechnicalDebtNegotiation` |

### Dimension 3 — Strategy and Impact (35% of leadership weight)

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 10.12 | ✓ | The leader acts as a filter against external interruptions — engineers have protected deep-work blocks | `secav:TeamShielding` |
| 10.13 | ✓ | Deployments follow a sustainable rhythm — no last-minute rush that compromises technical stability | `secav:DeliveryConsistencyBehavior` |
| 10.14 | ✓ | The leader understands the business metrics the team impacts with their code | `secav:HolisticProductVisionBehavior` |
| 10.15 | ✓ | The leader integrates diverse technical perspectives in decisions — junior and senior engineers contribute on equal terms | `secav:TechnicalDiversityBehavior` |
| 10.16 | ⚠ | Engineers receive direct interruptions from stakeholders and constantly context-switch — the leader does not act as a filter | absence of `secav:TeamShielding` |
| 10.17 | ⚠ | The leader systematically favors one technical perspective without opening space for other team voices | absence of `secav:TechnicalDiversityBehavior` |

---

## 11. Project Risk Management

> SECAV-O activity: `secav:ProjectRisk` and subclasses (`TechnicalRisk`, `ManagementRisk`, `OrganizationalRisk`, `ExternalRisk`); `secav:RiskRegister`, `secav:RiskResponsePlan`
>
> **Context:** The risk register is a living artifact that must be reviewed weekly or at the start of each sprint. The coach observes whether the team actively manages risks, not just whether they list them. A risk with P×I ≥ 12 without an active prevention plan is a systemic alert signal.
>
> **Recommended frequency:** review at the start of each sprint and at each weekly status meeting.

| # | Type | Observable behavior | SECAV-O Term |
|---|------|---------------------|--------------|
| 11.1 | ✓ | The team maintains an active risk register and reviews it at the start of each sprint | `secav:RiskRegister` active |
| 11.2 | ✓ | Each risk is worded with the standard syntax: Cause → Risk event → Impact on the project | `secav:riskRootCause`, `secav:riskEvent`, `secav:riskImpactDescription` |
| 11.3 | ✓ | Each risk has probability (P) and impact (I) documented on a 1–5 scale with P×I calculated | `secav:riskProbability`, `secav:riskImpact`, `secav:riskScore` |
| 11.4 | ✓ | Risks with P×I ≥ 12 have an active prevention plan and an identified owner | `secav:RiskResponsePlan` with `secav:preventionAction` and `secav:riskOwner` |
| 11.5 | ✓ | Each response plan includes a prevention action AND a contingency action | `secav:preventionAction` + `secav:contingencyAction` in `secav:RiskResponsePlan` |
| 11.6 | ✓ | The team proactively identifies new risks before they materialize | `secav:MitigateStrategy` or `secav:AvoidStrategy` applied in advance |
| 11.7 | ✓ | The response strategy (Mitigate / Avoid / Transfer / Accept) is explicit for each risk | `secav:hasResponseStrategy` documented |
| 11.8 | ⚠ | The risk register exists but has not been reviewed or updated in the last sprint | `secav:RiskRegister` out of date |
| 11.9 | ⚠ | Risks are listed without P×I scores or an identified owner | absence of `secav:riskScore` and `secav:riskOwner` |
| 11.10 | ⚠ | Risks with P×I ≥ 12 exist without any active prevention plan | absence of `secav:RiskResponsePlan` for high-priority risk |
| 11.11 | ⚠ | The team only records risks after they have already materialized — reactive mode | absence of preventive strategy (`secav:MitigateStrategy` or `secav:AvoidStrategy`) |
| 11.12 | ⚠ | Risks have a prevention action but no contingency action — no Plan B | absence of `secav:contingencyAction` in `secav:RiskResponsePlan` |
| 11.13 | ⚠ | Risk review is systematically omitted in the retrospective or sprint planning | `secav:RiskRegister` without integration into the sprint cycle |
| 11.14 | ✓ | Transferred risks (insurance, contractual clause, outsourcing) have the transfer mechanism explicitly documented | `secav:TransferStrategy` |
| 11.15 | ✓ | Consciously accepted risks include the decision justification and an activation threshold for reassessment | `secav:AcceptStrategy` |
| 11.16 | ⚠ | The team marks risks as "accepted" by omission — without a response plan or documented rationale (implicit acceptance) | `secav:AcceptStrategy` applied without conscious decision |

---

## Checklist usage summary

| When to use each group | Activity / Sprint |
|---|---|
| Groups 1–2 | Sprint start, refinement, design sessions |
| Group 3 | Any working session — in-context observation |
| Group 4 | CI/CD pipeline review; new member onboarding |
| Groups 5–6 | During or immediately after review / inspection sessions |
| Group 7 | PR review with test changes; sprint coverage review |
| Group 8 | PRs with AI-assisted code; team AI tool configuration |
| Group 9 | Biweekly or monthly — cultural adoption assessment of the new working model |
| Group 10 | Monthly or per sprint — technical leader observation; quarterly review of indicators 10.12–10.15 |
| Group 11 | At the start of each sprint and at each weekly status meeting — risk register review |
| Group 12 | Before, during, and after each scheduled code walkthrough session |
| Group 13 | Before, during, and at the close of each design review (prototype, wireframe, or specification) |
| Group 14 | Before, during, and after each integration test design review session |
| Group 15 | Before, during, and after each system test design review session |
| Group 16 | Before, during, and after each acceptance test design review session |
| Group 17 | After each test execution phase (unit, integration, system, acceptance) — results review |
| Group 18 | Before and during high-level design sessions; at the architecture review session |
| Group 19 | Any time a review method is being selected or a formal inspection is planned or executed |
| Group 20 | Before and during release preparation; at the release review gate |
| Group 21 | At sprint planning — before the plan is endorsed; at planning review session |
| Group 22 | Before, during, and after any design walkthrough or code walkthrough session (full lifecycle: preparation → execution → follow-up review) |

✓ signals are recorded as `secav:WorkProductEvidence` or `secav:ReviewFinding` and feed the `secav:CompetencyAssessment` of the cycle.

⚠ signals that appear more than once in a sprint should escalate to `secav:CoachingIntervention`. If they appear across multiple team members, document a `secavo:ImprovementAction` in the retrospective.

For Group 9, systemic ⚠ signals (present in more than half the team across two consecutive assessments) should lead to an intervention from the responsible `secav:ChangeAgent` — not only the technical coach.

---

## Group 12 — Code Walkthroughs (`secav:CodeWalkthrough`)

> **Source:** Guide to Good and Bad Practices — Software Review Walkthroughs  
> **When to observe:** Before, during, and at the close of each scheduled walkthrough session.  
> **Primary SECAV-O term:** `secav:CodeWalkthrough` (subclass of `secav:Walkthrough` and `secav:CodingActivity`)
>
> **Lifecycle:** `CodeWalkthrough` follows the three-phase walkthrough lifecycle defined in Group 22: **preparation** (this sub-section) → **`secav:WalkthroughExecution`** (live session, §12.2) → **`secav:WalkthroughReview`** (finding verification and coach sign-off, §12.3). `DesignWalkthrough` (Group 22.1) follows the same lifecycle applied to design artifacts.

### 12.1 Preparation

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 12.01 | The author limits scope to 200–400 lines of code before calling the session | ✓ | `secav:CodeWalkthrough` · `secav:walkthroughLineCount` |
| 12.02 | Materials (code, context, objective) are distributed at least 24 h in advance | ✓ | `secav:CodeWalkthrough` · `secav:WorkProductEvidence` |
| 12.03 | The three roles are explicitly assigned: Author/Presenter, Moderator, Recorder | ✓ | `secav:WalkthroughRole` |
| 12.04 | The review focus is declared (architecture, logic, security, concurrency, knowledge transfer) | ✓ | `secav:walkthroughFocus` |
| 12.05 | The session is called without prior materials or defined roles (improvised) | ⚠ | `secav:ImprovisedWalkthrough` |
| 12.06 | Scope exceeds 1,000 lines or the session is scheduled for more than 2 hours | ⚠ | `secav:OversizedWalkthrough` |
| 12.07 | No moderator is designated for the session | ⚠ | `secav:UnmoderatedWalkthrough` |

### 12.2 Execution

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 12.08 | The author spends the first 5–10 min explaining the business context of the code | ✓ | `secav:CodeWalkthrough` |
| 12.09 | Observations are directed at the code, not the person ("this method…" not "you did…") | ✓ | `secav:PositiveBehaviorObservation` |
| 12.10 | The moderator uses a "Parking Lot" to set aside topics outside the declared focus | ✓ | `secav:WalkthroughRole` |
| 12.11 | Findings are classified in real time: Blocking / Improvement / Clarification | ✓ | `secav:ReviewFinding` · `secav:walkthroughSeverity` |
| 12.12 | The debate drifts into style/format that could be resolved with a linter | ⚠ | `secav:StyleDebateDuringWalkthrough` |
| 12.13 | The author responds defensively to observations or interprets questions as attacks | ⚠ | `secav:DefensiveAuthorAttitude` |
| 12.14 | A reviewer monopolizes the session with personal preferences, blocking progress | ⚠ | `secav:WalkthroughMonopolization` |
| 12.15 | Complex code is refactored live during the session | ⚠ | `secav:LiveRefactoringDuringWalkthrough` |

### 12.3 Closure and Follow-up

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 12.16 | All action items are recorded in the tracking tool (Jira / GitHub Issues) with an assigned owner | ✓ | `secav:ReviewFinding` · `secav:MeetingAgreement` |
| 12.17 | Each finding is classified by severity (Blocking / Improvement / Clarification) before closing the session | ✓ | `secav:walkthroughSeverity` |
| 12.18 | The team verifies that changes arising from the walkthrough were applied before the merge | ✓ | `secav:WorkProductEvidence` |
| 12.19 | The session closes without any written record — only verbal agreements | ⚠ | `secav:WalkthroughWithoutRecord` |
| 12.20 | Code is merged without having addressed the recorded observations | ⚠ | `secav:IgnoredWalkthroughFeedback` |
| 12.21 | A full new walkthrough is called to verify minor corrections that could be reviewed asynchronously | ⚠ | `secav:UnnecessaryRewalkthrough` |
| 12.22 | All findings (defects, observations, or explicit "no defects found") are recorded with severity classification before closing the session — proposed solution included when the team agrees on a direction | ✓ | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 12.23 | The coach issues a process sign-off confirming the walkthrough was conducted acceptably (scope respected, roles present, findings documented) | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 12.24 | The walkthrough closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 12

- ⚠ signals 12.05, 12.06, or 12.07 present in the invitation must be resolved **before** starting the session; the coach may request cancellation or rescheduling if they are not addressed.
- Persistent ⚠ signals 12.13 or 12.14 across multiple sessions should lead to an individual `secav:CoachingIntervention` with the involved author or reviewer.
- ⚠ signal 12.20 is blocking: the coach must escalate to a `secav:CoachingIntervention` and document the finding in `templates/rca-defect-analysis.md` if the code has already reached production.

---

## Group 13 — Design Reviews (`secav:DesignReview`)

> **Source:** Guide to Best Practices for Design Review  
> **When to observe:** Before, during, and at the close of each prototype, wireframe, or design specification review.  
> **Primary SECAV-O term:** `secav:DesignReview` (subclass of `secav:ReviewActivity`)

### 13.1 Preparation

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 13.01 | The organizer explicitly declares the review objective (usability, architecture, flow, technical feasibility) | ✓ | `secav:DesignReview` |
| 13.02 | The user profile (personas), the problem to solve, and known constraints are shared before the session | ✓ | `secav:DesignReview` · `secav:WorkProductEvidence` |
| 13.03 | The prototype or documentation is distributed at least 24 h in advance | ✓ | `secav:DesignReview` |
| 13.04 | The design maturity level is declared (exploratory / conceptual / final) to frame the expected type of feedback | ✓ | `secav:designMaturityLevel` |
| 13.05 | The session is called without a concrete objective — discussion drifts to irrelevant details | ⚠ | `secav:UndefinedObjectiveReview` |
| 13.06 | Personas, problem context, and constraints are not shared — participants evaluate visuals instead of solutions | ⚠ | `secav:MissingUserContextReview` |
| 13.07 | Materials are sent during the session or less than 2 h before — comments are reactive and impulsive | ⚠ | `secav:ImpulsiveReactionFeedback` |

### 13.2 Facilitation and Dynamics

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 13.08 | The four key roles are present: Designer, Product Manager, Engineer/Dev, and Stakeholder | ✓ | `secav:DesignReviewRole` |
| 13.09 | Reviewers identify experience failures or inconsistencies with the business, rather than proposing direct solutions | ✓ | `secav:ReviewFinding` |
| 13.10 | Feedback is expressed using the "observation + impact" method (which element and what consequence it has) | ✓ | `secav:observationImpactStatement` |
| 13.11 | Comments are grounded in usability heuristics, user research, or key metrics | ✓ | `secav:ReviewFinding` |
| 13.12 | Reviewers propose specific solutions instead of identifying the experience problem | ⚠ | `secav:SolutionCentricFeedback` |
| 13.13 | Comments are subjective and unsupported ("I don't like this color", "I'd do it differently") | ⚠ | `secav:SubjectiveFeedback` |

### 13.3 Follow-up and Closure

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 13.14 | At closure a prioritized action list is compiled with assigned owners | ✓ | `secav:MeetingAgreement` · `secav:ReviewFinding` |
| 13.15 | Each finding is classified: mandatory change for launch vs. optional improvement for future iterations | ✓ | `secav:mandatoryForLaunch` |
| 13.16 | Decisions made are documented: which alternatives were approved or discarded and why | ✓ | `secav:ReviewFinding` · `secav:WorkProductEvidence` |
| 13.17 | Visual annotation tools are agreed upon for subsequent asynchronous follow-up | ✓ | `secav:MeetingAgreement` |
| 13.18 | The session closes without recording agreements or owners — only verbal comments | ⚠ | `secav:UndocumentedDesignDecision` |
| 13.19 | No documentation of why alternatives were discarded — the same discussions repeat in the next iteration | ⚠ | `secav:UndocumentedDesignDecision` |

### 13.4 Additional antipatterns and role-specific alert signals

> **Complementary source:** Guide to Bad Practices for Design Review

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 13.20 | The presenter shows complex proposals for the first time in the meeting without a pre-read sent in advance | ⚠ | `secav:DesignAmbush` |
| 13.21 | The session has more than 8 participants without defined roles — endless debates and analysis paralysis result | ⚠ | `secav:OvercrowdedDesignReview` |
| 13.22 | The designer moves pixels or changes styles live in response to each audience request | ⚠ | `secav:LiveDesignRedesign` |
| 13.23 | The session spends more than 15 min debating a cosmetic detail (color, shadow) when the main flow has not yet been validated | ⚠ | `secav:PrematureDetailFocus` |
| 13.24 | A reviewer makes vague, unactionable comments ("make it more modern", "more impactful") without identifying the problem or its impact | ⚠ | `secav:VagueFeedback` |
| 13.25 | The designer spends most of the time justifying decisions instead of listening — blocking iteration | ⚠ | `secav:DefensiveDesignerAttitude` |
| 13.26 | The Product Manager introduces requirement or scope changes during the session, invalidating prior work | ⚠ | `secav:LastMinuteRequirementChange` |
| 13.27 | The engineer rejects the proposal immediately without exploring alternative implementations | ⚠ | `secav:ImmediateTechnicalRejection` |
| 13.28 | A stakeholder imposes a design decision by hierarchy without data or user-testing backing | ⚠ | `secav:HierarchyBasedDecision` |
| 13.29 | A debate resolved in previous sessions is reopened without contributing new information | ⚠ | `secav:ReopeningClosedDebates` |
| 13.30 | All findings (defects, experience failures, or explicit "no findings") are recorded before closing the review — with mandatory-for-launch classification and proposed solution when the team agrees | ✓ | `secav:producesReviewFinding` · `secav:mandatoryForLaunch` · `secav:proposedSolution` (optional) |
| 13.31 | The coach issues a process sign-off confirming the design review was conducted acceptably (roles present, feedback evidence-based, findings documented) | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 13.32 | The design review closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 13

- ⚠ signals 13.05, 13.06, or 13.07 must be resolved **before** starting the session; the coach may request rescheduling if preparation is insufficient.
- Recurring ⚠ signal 13.13 or 13.24 in the same reviewer should lead to an individual `secav:CoachingIntervention` to reinforce the "observation + impact" method.
- ⚠ signal 13.18 is equivalent to a session with no traceable value; the coach should request that agreements are documented within 24 h or the review is considered not performed.
- ⚠ signals 13.25–13.28 are role-specific antipatterns: the coach documents them as `secav:AlertBehaviorObservation` linked to the relevant role and person, and designs an individual intervention if they repeat in two or more sessions.
- ⚠ signal 13.29 indicates governance debt: record a `secavo:ImprovementAction` to reinforce the closure and decision archiving process.

---

## Group 14 — Integration Test Design & Review (Phases 7–8)

> **Key principle:** Integration test design artifacts are work products. Like unit test code, they must be individually reviewed before execution. Integration tests detect inter-module defects that unit tests cannot see — a poorly designed integration test suite creates a false sense of quality at the interface level.

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 14.01 | Integration test design includes scenarios covering all documented module interfaces and contracts | ✓ | `secav:IntegrationTestDesign` |
| 14.02 | Integration test cases explicitly reference the requirements or design decisions they verify | ✓ | `secav:IntegrationTestDesignArtifact` |
| 14.03 | Test data and environment assumptions are documented — not left implicit or dependent on local setup | ✓ | `secav:IntegrationTestDesignArtifact` |
| 14.04 | The team can describe which module interaction failures the integration tests would and would not detect | ✓ | `secav:IntegrationTestDesign` |
| 14.05 | Integration tests are written before — or in parallel with — implementation, not as an afterthought post-merge | ✓ | `secav:IntegrationTestDesign` |
| 14.06 | Integration test design artifacts are submitted as a formal review request with change description and acceptance criteria before the review session | ✓ | `secav:FormalReviewRequest` |
| 14.07 | The integration test design review covers interaction correctness, data boundary handling, and environment dependencies — not just syntax | ✓ | `secav:IntegrationTestDesignReview` |
| 14.08 | Integration tests exercise failure paths (timeouts, partial responses, unavailable dependencies) not only happy paths | ✓ | `secav:IntegrationTestDesign` |
| 14.09 | Integration tests are executed only against the reviewed and approved design — not against ad-hoc, unreviewed test code | ✓ | `secav:IntegrationTestDesignReview` |
| 14.10 | Tests are merged or integrated without a prior design review — execution results are not trustworthy without review | ⚠ | `secav:UnreviewedTestCode` |
| 14.11 | Integration test coverage is declared solely by count of test cases — not by interface coverage or scenario coverage | ⚠ | `secav:ReviewAntipattern` |
| 14.12 | All findings from the integration test design review (defects, gaps, explicit "no defects found") are recorded before closing the session | ✓ | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 14.13 | The coach issues a process sign-off confirming the integration test design review was conducted acceptably | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 14.14 | The integration test design review closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 14

- ⚠ signal 14.10 in the same engineer in two or more sprints justifies an individual `secav:CoachingIntervention` on test discipline.
- ⚠ signal 14.11 indicates a measurement gap; record a `secavo:ImprovementAction` to introduce interface coverage criteria.
- ⚠ signal 14.14: pending sign-off must be tracked as an open `secav:MeetingAgreement` in the next meeting.

---

## Group 15 — System Test Design & Review (Phases 9–10)

> **Key principle:** System tests validate the system against end-to-end requirements including non-functional requirements (performance, security, reliability). Defects that escape system test design review are the most expensive to correct — they surface only under real load or after deployment.

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 15.01 | System test cases are traceable to documented functional and non-functional requirements | ✓ | `secav:SystemTestDesign` |
| 15.02 | Non-functional test scenarios (performance baselines, security checks, reliability targets) are designed explicitly — not left to informal observation | ✓ | `secav:SystemTestDesignArtifact` |
| 15.03 | The team can describe which requirement gaps or edge cases the system tests are designed to expose | ✓ | `secav:SystemTestDesign` |
| 15.04 | Test environment specifications (infrastructure, data sets, configuration) are documented and reviewed alongside the test cases | ✓ | `secav:SystemTestDesignArtifact` |
| 15.05 | System test artifacts are submitted as a formal review request before the system test design review session | ✓ | `secav:FormalReviewRequest` |
| 15.06 | The system test design review verifies traceability to requirements, environment feasibility, and coverage of non-functional scenarios | ✓ | `secav:SystemTestDesignReview` |
| 15.07 | Performance and reliability scenarios include defined pass/fail thresholds — not vague "must be fast" criteria | ✓ | `secav:SystemTestDesign` |
| 15.08 | System test execution proceeds without a completed design review — failures are harder to diagnose with unreviewed test code | ⚠ | `secav:UnreviewedTestCode` |
| 15.09 | Non-functional requirements are not covered by any system test scenario — systemic coverage gap | ⚠ | `secav:ReviewAntipattern` |
| 15.10 | All findings from the system test design review are recorded before closing the session | ✓ | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 15.11 | The coach issues a process sign-off confirming the system test design review was conducted acceptably | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 15.12 | The system test design review closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 15

- ⚠ signal 15.08: system test execution without a reviewed design should be flagged as a `secavo:QualityPlanningConcern` and raised in the next retrospective.
- ⚠ signal 15.09: if non-functional requirements exist but no test covers them, record a `secavo:ImprovementAction` to close the coverage gap before release.
- ⚠ signal 15.12: pending sign-off must be tracked as an open `secav:MeetingAgreement`.

---

## Group 16 — Acceptance Test Design & Review (Phases 11–12)

> **Key principle:** Acceptance test design is the translation of business requirements into verifiable scenarios co-created with stakeholders. A flaw in acceptance test design means the team ships something that passes all technical tests but fails business expectations — the most visible type of failure.

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 16.01 | Acceptance test scenarios are written with stakeholder participation or explicit stakeholder review — not by the development team alone | ✓ | `secav:AcceptanceTestDesign` |
| 16.02 | Each acceptance test case references a specific user story, business rule, or acceptance criterion documented in the requirements | ✓ | `secav:AcceptanceTestDesignArtifact` |
| 16.03 | Acceptance criteria are expressed in observable, verifiable terms — "the system displays X within 2 seconds" not "the system is fast" | ✓ | `secav:AcceptanceTestDesign` |
| 16.04 | The acceptance test design includes both successful flows and explicitly designed rejection scenarios (what the system must NOT do or accept) | ✓ | `secav:AcceptanceTestDesignArtifact` |
| 16.05 | Acceptance test artifacts are submitted as a formal review request before the acceptance test design review session | ✓ | `secav:FormalReviewRequest` |
| 16.06 | The acceptance test design review verifies stakeholder traceability, observability of criteria, and coverage of business edge cases | ✓ | `secav:AcceptanceTestDesignReview` |
| 16.07 | Stakeholder representatives can confirm that the acceptance test scenarios match their expectations after the review | ✓ | `secav:AcceptanceTestDesignReview` |
| 16.08 | Acceptance tests are designed by the development team without stakeholder input or review — business alignment risk | ⚠ | `secav:ReviewAntipattern` |
| 16.09 | Acceptance criteria contain vague or unmeasurable language that was not corrected during requirements review | ⚠ | `secav:VagueRequirement` |
| 16.10 | Acceptance tests are executed before the design has been formally reviewed and the stakeholders have confirmed alignment | ⚠ | `secav:UnreviewedTestCode` |
| 16.11 | All findings from the acceptance test design review are recorded before closing the session | ✓ | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 16.12 | The coach issues a process sign-off confirming the acceptance test design review was conducted acceptably | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 16.13 | The acceptance test design review closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 16

- ⚠ signal 16.08: escalate as a `secavo:QualityPlanningConcern`; acceptance tests without stakeholder input cannot serve as release quality gates.
- ⚠ signal 16.09: this is a requirements defect that propagated forward — record as a late-detected `secav:VagueRequirement` finding and trace back to the requirements review phase.
- ⚠ signal 16.13: pending sign-off must be tracked as an open `secav:MeetingAgreement`.

---

## Group 17 — Test Execution & Results Review (Phases 15–22)

> **Key principle:** Test execution produces a `secav:TestExecutionResultArtifact` — a report that is itself a work product requiring review. A test run without a structured results review is a missed quality gate. Results reviews are not just "did it pass?" — they examine defect density, coverage gaps, and the team's readiness decision.

### 17.1 — Unit Test Execution & Results Review (Phases 15–16)

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 17.01 | Unit test execution results are recorded in a structured report (pass/fail counts, coverage, failing test names) — not communicated verbally | ✓ | `secav:TestExecutionResultArtifact` · `secav:UnitTestExecution` |
| 17.02 | The unit test results review assesses defect density against defined thresholds before integration begins | ✓ | `secav:UnitTestResultsReview` |
| 17.03 | Coverage data is reviewed for gaps (untested paths) not just total coverage percentage | ✓ | `secav:UnitTestResultsReview` |
| 17.04 | Flaky or intermittently failing tests are flagged as findings — not dismissed or re-run without investigation | ✓ | `secav:ReviewFinding` |
| 17.05 | The team proceeds to integration testing based on CI pass status alone, without a reviewed results report | ⚠ | absence of `secav:UnitTestResultsReview` |
| 17.06 | The unit test results review records at least one finding (including explicit "no defects, coverage adequate, ready to integrate") | ✓ | `secav:producesReviewFinding` |
| 17.07 | Coach sign-off is issued after confirming the results review was conducted with a coverage and defect density assessment | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |

### 17.2 — Integration Test Execution & Results Review (Phases 17–18)

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 17.08 | Integration test execution results are recorded per interface or module-pair — not only as aggregate pass/fail | ✓ | `secav:TestExecutionResultArtifact` · `secav:IntegrationTestExecution` |
| 17.09 | The integration test results review identifies which module interfaces had failures and whether they are blocking or non-blocking | ✓ | `secav:IntegrationTestResultsReview` |
| 17.10 | Defects found in integration testing are traced back to the phase where the defect was injected (requirements, design, or implementation) | ✓ | `secavo:phaseInjected` · `secav:ReviewFinding` |
| 17.11 | The team advances to system testing before all blocking integration defects are resolved or documented with an explicit exception | ⚠ | `secav:ReviewAntipattern` |
| 17.12 | The integration test results review records at least one finding and is signed off by the coach | ✓ | `secav:producesReviewFinding` · `secav:CoachReviewSignOff` |

### 17.3 — System Test Execution & Results Review (Phases 19–20)

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 17.13 | System test execution results include both functional and non-functional test outcomes (performance, security, reliability) | ✓ | `secav:TestExecutionResultArtifact` · `secav:SystemTestExecution` |
| 17.14 | The system test results review produces an explicit quality assessment with a recommendation for or against advancing to acceptance testing | ✓ | `secav:SystemTestResultsReview` |
| 17.15 | Non-functional test failures (performance regression, security vulnerability) are classified as blocking by default unless the team documents an explicit exception | ✓ | `secav:ReviewFinding` |
| 17.16 | The team advances to acceptance testing before the system test results review is complete — last integration-side quality gate is skipped | ⚠ | absence of `secav:SystemTestResultsReview` |
| 17.17 | The system test results review records at least one finding and is signed off by the coach | ✓ | `secav:producesReviewFinding` · `secav:CoachReviewSignOff` |

### 17.4 — Acceptance Test Execution & Results Review (Phases 21–22)

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 17.18 | Acceptance test execution is conducted with stakeholder participation or explicit stakeholder observation — not by the development team alone | ✓ | `secav:AcceptanceTestExecution` |
| 17.19 | The acceptance test results review includes a formal go/no-go decision with documented justification — not an implicit approval by silence | ✓ | `secav:AcceptanceTestResultsReview` |
| 17.20 | Defects found during acceptance testing are classified by severity and business impact before the release decision is made | ✓ | `secav:ReviewFinding` |
| 17.21 | The acceptance test results review produces a documented go/no-go finding with stakeholder participation — verbal acknowledgment without a written record is not a valid release decision | ✓ | `secav:AcceptanceTestResultsReview` · `secav:ReviewFinding` |
| 17.22 | The team proceeds to production deployment before the acceptance test results review is completed or without stakeholder sign-off | ⚠ | absence of `secav:AcceptanceTestResultsReview` |
| 17.23 | The acceptance test results review records at least one finding and is signed off by the coach before the release decision is finalized | ✓ | `secav:producesReviewFinding` · `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 17

- ⚠ signals 17.05, 17.11, 17.16, or 17.22 represent quality gate bypasses — each must trigger a `secavo:QualityPlanningConcern` and be raised in the next retrospective.
- Defects traced via `secavo:phaseInjected` back to requirements or design (signal 17.10) indicate that the earlier review phases (groups 1–2 or 13) were insufficient. Record as escape observations.
- ⚠ signal 17.22 is the highest-severity bypass: production deployment without acceptance results review. Escalate immediately.

---

## Group 18 — High Level Design & Review

> **Key principle:** High-level design (architecture) defects are the most expensive defects in the lifecycle. A flawed architectural decision propagates into every downstream phase. Every system must have a reviewable high-level design artifact before detailed design begins — and that artifact must go through at least a peer review, with formal inspection recommended for critical systems.

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 18.01 | A high-level design artifact exists before detailed design work begins — architecture decisions are not made implicitly during implementation | ✓ | `secav:HighLevelDesignArtifact` |
| 18.02 | The artifact covers major components, their responsibilities, inter-component interfaces, data flows, and key technology decisions | ✓ | `secav:HighLevelDesign` |
| 18.03 | Architectural decisions are captured as Architecture Decision Records (ADRs) or equivalent — decision, rationale, alternatives considered, and consequences | ✓ | `secav:HighLevelDesignArtifact` |
| 18.04 | Non-functional requirements (scalability, security, reliability, performance) are addressed explicitly in the architecture — not deferred | ✓ | `secav:HighLevelDesign` |
| 18.05 | The high-level design is traceable to specific requirements — each architectural choice can be connected to a requirement that motivates it | ✓ | `secav:HighLevelDesign` |
| 18.06 | The team can explain how the architecture handles the main failure modes of the system | ✓ | `secav:HighLevelDesign` |
| 18.07 | The high-level design artifact is submitted as a formal review request with change description and acceptance criteria before the review session | ✓ | `secav:FormalReviewRequest` |
| 18.08 | The high-level design review covers architectural soundness, requirement traceability, scalability risk, security boundaries, and deployment feasibility | ✓ | `secav:HighLevelDesignReview` |
| 18.09 | For critical systems, the high-level design review uses formal inspection (with assigned roles: Moderator, Reader, Inspectors, Scribe) rather than informal peer review | ✓ | `secav:FormalInspection` |
| 18.10 | Detailed design or implementation begins before the high-level design review is complete — architectural defects will propagate | ⚠ | `secav:ReviewAntipattern` |
| 18.11 | Architecture decisions are made verbally or in Slack without being captured in a reviewable artifact — decisions are irretrievable when challenged | ⚠ | `secav:ReviewAntipattern` |
| 18.12 | Non-functional requirements are absent from the architecture — the system will fail under production load or security audit | ⚠ | `secav:ReviewAntipattern` |
| 18.13 | All findings from the high-level design review (defects, risks, ADR gaps, explicit "no defects found") are recorded before closing the session | ✓ | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 18.14 | The coach issues a process sign-off confirming the high-level design review was conducted acceptably | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 18.15 | The high-level design review closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 18

- ⚠ signal 18.10: implementation proceeding without high-level design review is a `secavo:QualityPlanningConcern` — escalate immediately.
- ⚠ signal 18.11: verbal-only decisions indicate an architecture governance gap; record a `secavo:ImprovementAction` to introduce ADR practice.
- ⚠ signal 18.12: treat as a risk (`secav:ProjectRisk`) requiring a mitigation plan and response before system test.

---

## Group 19 — Review Method Selection: Peer Review vs. Walkthrough vs. Formal Inspection

> **Key principle:** Not all artifacts carry the same risk. The review method must match the criticality of the artifact. Requirements, high-level architecture, and critical test designs warrant formal inspection. Less critical artifacts can be reviewed by peer review or walkthrough. Choosing an insufficient method for a high-risk artifact is an antipattern.

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 19.01 | The team can articulate why they chose a given review method (peer review, walkthrough, or formal inspection) for the artifact — not just because it is habit | ✓ | `secav:PeerReview` · `secav:Walkthrough` · `secav:FormalInspection` |
| 19.02 | Critical artifacts (requirements, high-level architecture, critical unit tests) are reviewed by formal inspection or walkthrough — not by informal async peer review alone | ✓ | `secav:FormalInspection` |
| 19.03 | Formal inspections have a designated Moderator who enforces entry criteria, controls the session, and manages follow-up verification | ✓ | `secav:FormalInspection` |
| 19.04 | Formal inspections include a Reader role who presents the artifact, allowing inspectors to focus on detecting defects rather than navigating the document | ✓ | `secav:FormalInspection` |
| 19.05 | A Scribe captures every defect finding during the inspection meeting — findings are not reconstructed from memory after the session | ✓ | `secav:FormalInspection` · `secav:producesReviewFinding` |
| 19.06 | Peer reviews specify a focus area (logic, security, interface, performance) rather than reviewing everything at once with no declared goal | ✓ | `secav:PeerReview` |
| 19.07 | The inspection follow-up phase verifies that all recorded defects have been corrected — verification is not skipped because "the fix was obvious" | ✓ | `secav:FormalInspection` |
| 19.08 | Formal inspection causal analysis data (defect type, phase injected) is recorded and used in retrospectives for process improvement | ✓ | `secav:FormalInspection` · `secavo:phaseInjected` |
| 19.09 | A peer review is used for a critical requirements or architecture artifact — the method is insufficient for the artifact's defect impact | ⚠ | `secav:ReviewAntipattern` |
| 19.10 | Formal inspection roles are assigned but participants do not prepare before the session — entry criteria failure, the inspection should not proceed | ⚠ | `secav:ReviewAntipattern` |
| 19.11 | Inspection findings are lost because no Scribe was designated or the record was not preserved after the session | ⚠ | `secav:WalkthroughWithoutRecord` |
| 19.12 | All findings from any review session (peer review, walkthrough, or formal inspection) are recorded with severity and proposed resolution before the session closes | ✓ | `secav:producesReviewFinding` · `secav:walkthroughSeverity` · `secav:proposedSolution` (optional) |
| 19.13 | The coach certifies the session via direct sign-off (when present) or remote endorsement via a designated observer's `secav:ObserverReport` (when absent — Principle 16), confirming the session was conducted acceptably under the declared review method | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 19.14 | A review session (peer review, walkthrough, or formal inspection) closes without the coach issuing a direct sign-off or a remote endorsement — findings cannot be used as formal competency evidence | ⚠ | absence of `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 19

- ⚠ signal 19.09: the coach must document a `secavo:QualityPlanningConcern` if a critical artifact was reviewed only by informal peer review. The review may need to be repeated with a stronger method.
- ⚠ signal 19.10: the inspection must not proceed without preparation. Escalate as a rescheduling request.
- ⚠ signal 19.11: session is invalid without a findings record; the coach cannot issue sign-off and must document accordingly.

---

## Group 20 — Release & Release Review

> **Key principle:** Release is not the end of quality governance — it is the point where all prior quality gates either prove their value or reveal their gaps. A release review is a mandatory quality checkpoint that confirms all gates were completed, known risks are documented, and a rollback path exists. No release should proceed without a documented release readiness record.

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 20.01 | A release artifact package exists before the release: release notes, deployment plan, environment configuration, versioned build, and rollback procedure | ✓ | `secav:ReleaseArtifact` · `secav:Release` |
| 20.02 | Release notes document all changes in this release and link to the requirements or user stories that motivated them | ✓ | `secav:ReleaseArtifact` |
| 20.03 | A rollback procedure exists and has been tested or validated — not a theoretical plan that has never been exercised | ✓ | `secav:ReleaseArtifact` |
| 20.04 | The deployment plan identifies environment-specific risks and has been reviewed by someone with production environment knowledge | ✓ | `secav:ReleaseArtifact` |
| 20.05 | The release review verifies that all mandatory quality gates were completed: RequirementsReview, HighLevelDesignReview, DesignReview, code review, and all test phase reviews | ✓ | `secav:ReleaseReview` |
| 20.06 | Open defects are classified by severity with an explicit accept/defer/resolve decision for each before the release proceeds | ✓ | `secav:ReleaseReview` |
| 20.07 | The AcceptanceTestResultsReview has been completed and stakeholder go/no-go is documented before the release review | ✓ | `secav:AcceptanceTestResultsReview` · `secav:ReleaseReview` |
| 20.08 | A release proceeds to production without a completed release review — all prior quality gates are undermined by the last-mile bypass | ⚠ | absence of `secav:ReleaseReview` |
| 20.09 | The rollback procedure has never been tested — the release assumes success and has no recovery path | ⚠ | `secav:ProjectRisk` |
| 20.10 | Open defects are accepted for production without a written rationale and business owner sign-off | ⚠ | `secav:ReviewAntipattern` |
| 20.11 | Release notes are incomplete or absent — users and operators cannot determine what changed or what risks exist | ⚠ | `secav:ReviewAntipattern` |
| 20.12 | One or more mandatory quality gates (requirements review, design review, test design review, results review) were skipped and this was not documented as an explicit exception | ⚠ | `secav:MissingRequirementsReview` · `secav:ReviewAntipattern` |
| 20.13 | All findings from the release review (quality gate gaps, open defects, risks, or explicit "all gates confirmed, release approved") are recorded before the release proceeds | ✓ | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 20.14 | The coach issues a process sign-off confirming the release review was conducted acceptably and all quality gates were verified | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 20.15 | The release review closes without written findings or coach sign-off — the release readiness cannot be traced | ⚠ | absence of `secav:producesReviewFinding` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 20

- ⚠ signal 20.08: production deployment without a release review is the highest-severity bypass in the lifecycle. Escalate immediately and document as a `secavo:QualityPlanningConcern`.
- ⚠ signal 20.09: an untested rollback plan is a `secav:ProjectRisk` — require a rollback rehearsal before the next production release.
- ⚠ signal 20.12: document each skipped quality gate as a gap finding in the release review record. If the pattern repeats, escalate via the formal dissent and escalation protocol.

---

## Group 21 — Planning & Planning Review

> **Key principle:** The plan is a work product. A sprint or iteration plan that omits mandatory review activities (RequirementsReview, DesignReview, test design reviews) creates invisible quality debt from day one. The Planning Review is the coach's quality gate on the plan itself — not on the work described in it. Endorsing a plan without a RequirementsReview is an ethical obligation violation (Code of Ethics, Principle 17).

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 21.01 | A written plan artifact exists before the sprint or iteration begins — tasks, owners, and deadlines are documented, not only communicated verbally | ✓ | `secav:PlanningArtifact` · `secav:PlanningActivity` |
| 21.02 | The plan schedules at least one `secav:RequirementsReview` for every feature entering implementation in this sprint — the planning gate is satisfied | ✓ | `secav:RequirementsReview` · `secav:PlanningArtifact` |
| 21.03 | Review activities in the plan identify a facilitator, scheduled date, and participant list — not just a placeholder task | ✓ | `secav:PlanningArtifact` |
| 21.04 | The plan includes time estimates for review activities — reviews are not squeezed out when implementation tasks run over | ✓ | `secav:PlanningActivity` |
| 21.05 | The plan distinguishes between production activities (design, implementation, test design) and review activities — each is a separately scheduled task | ✓ | `secav:PlanningArtifact` |
| 21.06 | The coach reviews the plan before endorsing the sprint — not during the sprint when review activities can no longer be scheduled | ✓ | `secav:PlanningReview` |
| 21.07 | The planning review confirms that mandatory quality gates are present: RequirementsReview, HighLevelDesignReview (if architecture changed), test design reviews | ✓ | `secav:PlanningReview` |
| 21.08 | The planning review finds no RequirementsReview in the plan — the coach withholds endorsement and documents a QualityPlanningConcern | ✓ | `secavo:QualityPlanningConcern` · `secav:MissingRequirementsReview` |
| 21.09 | The sprint plan contains only implementation tasks — no review, testing, or quality gate activities appear | ⚠ | `secav:MissingRequirementsReview` · `secav:ReviewAntipattern` |
| 21.10 | Review activities in the plan have no identified owner or date — they are planning placeholders with no commitment | ⚠ | `secav:ReviewAntipattern` |
| 21.11 | The coach endorses the plan without checking for a RequirementsReview — planning gate violation (Code of Ethics, Principle 17) | ⚠ | `secav:MissingRequirementsReview` |
| 21.12 | Review activities added to the plan after implementation already started — retroactive scheduling does not satisfy the planning gate | ⚠ | `secav:MissingRequirementsReview` |
| 21.13 | All findings from the planning review (missing gates, incomplete review scheduling, or explicit "plan approved, all gates present") are recorded | ✓ | `secav:producesReviewFinding` · `secav:proposedSolution` (optional) |
| 21.14 | The coach issues a process sign-off confirming the planning review was conducted and the plan meets quality gate requirements | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 21.15 | The sprint begins without a completed planning review or coach sign-off on the plan | ⚠ | absence of `secav:PlanningReview` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 21

- ⚠ signal 21.09: a plan with no review activities is a `secavo:QualityPlanningConcern` — the coach must withhold endorsement and request plan corrections.
- ⚠ signal 21.11: this is a Code of Ethics Principle 17 violation — self-disclose and address through coaching practice improvement.
- ⚠ signal 21.12: retroactive scheduling is not a planning gate fix; record as a `secav:MissingRequirementsReview` observation even if the review subsequently occurs.

---

## Group 22 — Design Walkthrough, Walkthrough Execution & Walkthrough Review

> **Key principle:** A walkthrough has three distinct lifecycle phases — preparation, execution, and follow-up review. Running only the session (execution) without structured preparation or finding verification produces a discussion meeting, not a quality review. Design walkthroughs are the application of this method to design artifacts; they have different focus areas from code walkthroughs but the same three-phase lifecycle and the same requirement for recorded findings and coach sign-off.

### 22.1 — Design Walkthrough (applying walkthrough method to design artifacts)

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 22.01 | A design walkthrough is declared with a specific focus area before the session (e.g., usability, data model, interaction flow, architecture) | ✓ | `secav:DesignWalkthrough` · `secav:walkthroughFocus` |
| 22.02 | The design artifact is distributed to all participants before the session — no one sees it for the first time in the meeting | ✓ | `secav:DesignWalkthrough` |
| 22.03 | The design author presents the artifact and answers questions — reviewers focus on identifying issues, not on debating solutions in the session | ✓ | `secav:DesignWalkthrough` · `secav:WalkthroughRole` |
| 22.04 | A Moderator controls session scope, preventing discussion from drifting into implementation details or adjacent design decisions | ✓ | `secav:DesignWalkthrough` · `secav:WalkthroughRole` |
| 22.05 | A Scribe captures all findings in real time — no reconstruction of findings from memory after the session | ✓ | `secav:DesignWalkthrough` · `secav:WalkthroughRole` |
| 22.06 | Design walkthrough feedback distinguishes between design flaws (must be corrected) and preferences (can be deferred or declined) | ✓ | `secav:ReviewFinding` · `secav:walkthroughSeverity` |
| 22.07 | Design walkthroughs stay within scope — reviewers do not introduce requirement changes or cross-artifact disputes during the session | ✓ | `secav:DesignWalkthrough` |
| 22.08 | The design walkthrough is held as an unstructured discussion without a declared focus or pre-distributed material | ⚠ | `secav:ImprovisedWalkthrough` |
| 22.09 | Reviewers critique design aesthetics (colors, typography) instead of usability flows or structural correctness | ⚠ | `secav:PrematureDetailFocus` · `secav:WalkthroughAntipattern` |
| 22.10 | The session ends without a written list of findings and action items | ⚠ | `secav:WalkthroughWithoutRecord` |

### 22.2 — Walkthrough Execution (the live session)

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 22.11 | Walkthrough entry criteria are confirmed before starting: artifact distributed, all roles assigned, participants prepared | ✓ | `secav:WalkthroughExecution` |
| 22.12 | The session follows the planned walkthrough focus — the moderator redirects off-topic discussion back to the declared scope | ✓ | `secav:WalkthroughExecution` · `secav:walkthroughFocus` |
| 22.13 | Each finding recorded during the session has: a description, severity (Blocking / Improvement / Clarification), and location in the artifact | ✓ | `secav:WalkthroughExecution` · `secav:walkthroughSeverity` |
| 22.14 | The session ends with a closing status: accepted (no blocking findings), conditional (blocking findings to be verified), or rejected (major rework needed) | ✓ | `secav:WalkthroughExecution` |
| 22.15 | The walkthrough session runs without a Scribe — findings are not captured in real time | ⚠ | `secav:WalkthroughWithoutRecord` |
| 22.16 | Participants debate and attempt to solve blocking findings during the session rather than registering them and moving on | ⚠ | `secav:LiveRefactoringDuringWalkthrough` |
| 22.17 | All findings from the walkthrough execution are recorded before the session closes — including an explicit "no defects found" if the artifact is clean | ✓ | `secav:producesReviewFinding` · `secav:WalkthroughExecution` |

### 22.3 — Walkthrough Review (post-session finding verification)

| # | Observable signal | Type | SECAV-O Term |
|---|------------------|------|--------------|
| 22.18 | The author addresses all Blocking findings from the walkthrough execution before the artifact is merged or advanced to the next phase | ✓ | `secav:WalkthroughReview` |
| 22.19 | The Moderator (or delegate) verifies that corrections are adequate for each Blocking finding — corrections are not assumed correct without review | ✓ | `secav:WalkthroughReview` |
| 22.20 | Improvement and Clarification findings are explicitly accepted, deferred with justification, or converted to open action items — not silently ignored | ✓ | `secav:WalkthroughReview` · `secav:MeetingAgreement` |
| 22.21 | The walkthrough review produces a closing record: final state of each finding (resolved / deferred / declined) with rationale | ✓ | `secav:WalkthroughReview` · `secav:producesReviewFinding` |
| 22.22 | The artifact is merged or advanced before Blocking findings from the walkthrough execution are addressed — IgnoredWalkthroughFeedback | ⚠ | `secav:IgnoredWalkthroughFeedback` |
| 22.23 | No walkthrough review takes place — the walkthrough lifecycle closes with execution only and finding follow-up is never verified | ⚠ | absence of `secav:WalkthroughReview` |
| 22.24 | The coach issues a process sign-off confirming the full walkthrough lifecycle was completed: preparation, execution, and finding verification | ✓ | `secav:CoachReviewSignOff` **or** `secav:CoachRemoteEndorsement` |
| 22.25 | The walkthrough lifecycle closes without coach sign-off or without a written closing record | ⚠ | absence of `secav:WalkthroughReview` or both `secav:CoachReviewSignOff` and `secav:CoachRemoteEndorsement` |

### Escalation notes — Group 22

- ⚠ signal 22.08 or 22.10: the walkthrough did not meet minimum standards — findings cannot be considered valid. The coach must withhold sign-off and document the gap.
- ⚠ signal 22.22: each instance must be documented as `secav:IgnoredWalkthroughFeedback`; two instances in the same engineer in the same sprint justify an individual coaching intervention.
- ⚠ signal 22.23: the walkthrough lifecycle is incomplete; the coach sign-off cannot be issued until the WalkthroughReview is performed.
- ⚠ signal 22.25: pending sign-off must appear as an open `secav:MeetingAgreement` in the next meeting.

---

## Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/coach-attitudes.md` | Coach attitudes during observation |
| `coaching-governance/guides/peer-review-antipatterns.md` | Detail of review antipatterns (groups 5 and 8) |
| `coaching-governance/guides/shift-left-prevention.md` | Context for groups 1–4 (shift-left prevention) |
| `coaching-governance/guides/formal-inspections.md` | Complete protocol for group 6 |
| `coaching-governance/guides/ai-assisted-code-review.md` | Complete context for group 8 |
| `templates/rca-defect-analysis.md` | When a ⚠ signal leads to a P1/P2 defect |
| `templates/engineer-coaching-assessment.md` | ✓ evidence feeds the competency assessment |
| `coaching-governance/guides/software-walkthroughs.md` | Complete protocol for group 12 (code walkthroughs) |
| `coaching-governance/guides/design-review.md` | Complete protocol for group 13 (design reviews) |
| `ontology/secav-o.ttl` | Full lifecycle model including High Level Design, review methods (PeerReview, FormalInspection), and Release phases |