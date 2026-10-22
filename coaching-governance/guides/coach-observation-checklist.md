# Coach Observation Checklist by Engineering Activity

## Purpose

This checklist allows the coach to record, during any observation session, the positive behaviors and alert signals the team exhibits in each engineering activity. Each row is an observable: something the coach can see, hear, or read directly — not an inference.

**Column convention:**
- ✓ Positive behavior — record as `secav:Evidence` for competency assessment
- ⚠ Alert signal — consider `secav:CoachingIntervention`

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
| 1.7 | ✓ | The coach issues a sign-off confirming the requirements review was conducted acceptably before authorizing implementation | `secav:CoachReviewSignOff` · `secav:hasSignOff` |
| 1.8 | ✓ | Review participants flag "vague", "ambiguous", "unclear", or "incomplete" defects using explicit labels — not generic comments | `secav:VagueRequirement` / `secav:AmbiguousRequirement` / `secav:UnclearRequirement` / `secav:IncompleteRequirement` |
| 1.9 | ⚠ | A user story enters the sprint without defined acceptance criteria | `secav:HappyPathOnlyReview` (risk) |
| 1.10 | ⚠ | The team starts coding with ambiguous requirements without requesting clarification | `secav:AmbiguousRequirement` unresolved; `secav:MissingReviewContext` |
| 1.11 | ⚠ | Acceptance criteria are written after implementation (post-hoc) | absence of `secav:AcceptanceCriteriaDefinition` as a preventive activity |
| 1.12 | ⚠ | No traceability exists between acceptance criteria and automated test cases | `secav:QualityCriterion` without `secav:AutomationGate` |
| 1.13 | ⚠ | Implementation begins on requirements that have not been subject to any peer review, walkthrough, or inspection | `secav:MissingRequirementsReview` — highest-risk antipattern in the lifecycle |
| 1.14 | ⚠ | The requirements review was conducted but the coach did not issue a sign-off — findings cannot be used as planning evidence | absence of `secav:CoachReviewSignOff` on `secav:RequirementsReview` |

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
| 5.19 | ✓ | The coach issues a process sign-off confirming the review was conducted acceptably (roles followed, findings documented) | `secav:CoachReviewSignOff` · `secav:hasSignOff` |
| 5.20 | ✓ | When the team agrees on a fix direction during the session, a proposed solution is recorded alongside the finding | `secav:proposedSolution` (optional) |
| 5.21 | ⚠ | The session ends without any written findings — only verbal comments | absence of `secav:producesReviewFinding` |
| 5.22 | ⚠ | The coach does not issue a sign-off — the review findings cannot be used as valid competency evidence | absence of `secav:CoachReviewSignOff` |

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
| 6.14 | ✓ | The coach issues a formal process sign-off confirming the inspection was conducted acceptably | `secav:CoachReviewSignOff` · `secav:hasSignOff` |
| 6.15 | ⚠ | The inspection closes without written findings or the sign-off is not issued — the session findings are not valid as competency evidence | absence of `secav:producesReviewFinding` or `secav:CoachReviewSignOff` |

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
| 7.18 | ✓ | The coach issues a process sign-off confirming the unit test design review was conducted acceptably (roles followed, findings documented, review not rubber-stamped) | `secav:CoachReviewSignOff` · `secav:hasSignOff` |
| 7.19 | ✓ | When the review identifies a test design problem and the team agrees on a fix approach, the proposed solution is recorded alongside the finding | `secav:proposedSolution` (optional) |
| 7.20 | ⚠ | The unit test design review session ends without any written findings — verbal comments only | absence of `secav:producesReviewFinding` |
| 7.21 | ⚠ | The coach does not issue a sign-off on the unit test design review — findings cannot be used as valid competency evidence | absence of `secav:CoachReviewSignOff` |

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

✓ signals are recorded as `secav:WorkProductEvidence` or `secav:ReviewFinding` and feed the `secav:CompetencyAssessment` of the cycle.

⚠ signals that appear more than once in a sprint should escalate to `secav:CoachingIntervention`. If they appear across multiple team members, document a `secavo:ImprovementAction` in the retrospective.

For Group 9, systemic ⚠ signals (present in more than half the team across two consecutive assessments) should lead to an intervention from the responsible `secav:ChangeAgent` — not only the technical coach.

---

## Group 12 — Code Walkthroughs (`secav:CodeWalkthrough`)

> **Source:** Guide to Good and Bad Practices — Software Review Walkthroughs  
> **When to observe:** Before, during, and at the close of each scheduled walkthrough session.  
> **Primary SECAV-O term:** `secav:CodeWalkthrough` (subclass of `secav:ReviewActivity`)

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
| 12.23 | The coach issues a process sign-off confirming the walkthrough was conducted acceptably (scope respected, roles present, findings documented) | ✓ | `secav:CoachReviewSignOff` · `secav:hasSignOff` |
| 12.24 | The walkthrough closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or `secav:CoachReviewSignOff` |

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
| 13.31 | The coach issues a process sign-off confirming the design review was conducted acceptably (roles present, feedback evidence-based, findings documented) | ✓ | `secav:CoachReviewSignOff` · `secav:hasSignOff` |
| 13.32 | The design review closes without written findings or the coach sign-off is not issued | ⚠ | absence of `secav:producesReviewFinding` or `secav:CoachReviewSignOff` |

### Escalation notes — Group 13

- ⚠ signals 13.05, 13.06, or 13.07 must be resolved **before** starting the session; the coach may request rescheduling if preparation is insufficient.
- Recurring ⚠ signal 13.13 or 13.24 in the same reviewer should lead to an individual `secav:CoachingIntervention` to reinforce the "observation + impact" method.
- ⚠ signal 13.18 is equivalent to a session with no traceable value; the coach should request that agreements are documented within 24 h or the review is considered not performed.
- ⚠ signals 13.25–13.28 are role-specific antipatterns: the coach documents them as `secav:AlertBehaviorObservation` linked to the relevant role and person, and designs an individual intervention if they repeat in two or more sessions.
- ⚠ signal 13.29 indicates governance debt: record a `secavo:ImprovementAction` to reinforce the closure and decision archiving process.

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