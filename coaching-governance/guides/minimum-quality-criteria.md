# Minimum Quality Criterion per Phase

## Principle

Every productive phase of software development generates artifacts that condition the quality of all subsequent phases. A defect introduced in requirements that is not detected until system testing can invalidate weeks of work. A defective unit test design can go unnoticed indefinitely if no one inspects it.

**The minimum reasonable quality criterion is: the critical artifacts of each phase must be inspected before that phase concludes.**

---

## Definition: minimum reasonable quality

> **Scope note:** "Minimum reasonable quality" is a criterion proposed by this framework, not a universally recognized certification standard. The goal is to provide a concrete operational reference point — not to automatically declare bad practice for every organization that operates differently.

**Minimum reasonable quality** is, according to the SECAV-O proposal, the threshold below which the risk of defect accumulation between phases is unacceptable — regardless of time or budget constraints invoked to justify it. It is not the quality standard to aspire to, but the floor below which this framework considers inspection coverage insufficient.

The reason for establishing a *minimum* rather than an *optimum* is that most organizations do not have the capacity to inspect every software artifact generated during development: requirements, architecture design, detailed design, code, unit test design, system test design, acceptance test design, test execution results, and other derivatives. Inspecting everything is an ideal to approximate progressively; assuming every organization can achieve it from the outset is unrealistic.

What is achievable in most projects — and what this framework establishes as the reasonable minimum — is **identifying the highest-risk artifacts in each phase and ensuring that at least those are formally reviewed by more than one reviewer before advancing to the next phase**.

| Level | Description |
|---|---|
| **Below minimum** | Bad practice: no critical artifact in any phase is formally inspected. Defects accumulate between phases and are detected late, when their correction cost is highest. |
| **Minimum reasonable quality** | The highest-risk artifacts of each phase are inspected by more than one reviewer before advancing. This is the framework's floor. |
| **Robust process** | Quality practices produce verifiable evidence of their effectiveness: inspections over critical products, dynamic behavior design with UML diagrams, findings documented in individual reviews, and justified waivers when none exist. Defined in `coaching-governance/guides/robust-process-criteria.md`. |
| **Aspirational quality** | Most or all artifacts of each phase are inspected. Organizations mature toward this level incrementally (`coaching-governance/guides/incremental-adoption.md`). |

A second criterion that reinforces this minimum: if time pressure systematically leads to omitting inspections in any phase — any phase — that is a signal that the project plan underestimates quality effort, not that inspection is dispensable. The coach documents these omissions as `secavo:QualityPlanningConcern`.

---

## Phase and inspection model

The following table maps the productive phases of software development, the artifacts they produce, the SECAV-O review type, and the framework guide that establishes the protocol.

| Phase | Inspected artifact | SECAV-O activity | Review type | Framework guide |
|---|---|---|---|---|
| **Requirements** | Requirements document, user stories, use cases | `secav:RequirementsActivity` | `secav:DesignReview` on `secav:DesignArtifact` | `coaching-governance/guides/requirements-inspection.md` |
| **Architecture design** | Architectural decisions, component diagrams, ADRs | `secav:ApplicationDesign` | `secav:DesignReview` on `secav:DesignArtifact` | `coaching-governance/guides/formal-inspections.md` |
| **Detailed design** | Class diagrams, API contracts, module specifications | `secav:DesignActivity` | `secav:DesignReview` on `secav:DesignArtifact` | `coaching-governance/guides/formal-inspections.md` |
| **Code implementation** | Source code of critical modules | `secav:CodingActivity` | `secav:CodeReview` on `secav:SourceCodeArtifact` | `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/peer-review-sessions.md` |
| **Unit test design** | Unit test code and test cases | `secav:UnitTestDesign` | `secav:UnitTestDesignReview` on `secav:UnitTestDesignArtifact` | `coaching-governance/guides/unit-test-review.md` |
| **System test design** | System test plan, integration test cases | `secav:TestingActivity` | `secav:DesignReview` on `secav:DesignArtifact` | *(pending — see §3)* |
| **Acceptance test design** | Acceptance criteria, UAT scripts | `secav:TestingActivity` | `secav:DesignReview` on `secav:DesignArtifact` | *(pending — see §3)* |

---

## 1. Criteria for selecting what to inspect

Not every artifact in each phase warrants formal inspection. The selection criterion is the same across all phases: risk. An artifact is a candidate for formal inspection if it meets at least one of these criteria:

| Criterion | Examples |
|---|---|
| **Impact scope** | The artifact affects many features or many other artifacts that depend on it |
| **Breadth of use** | Many engineers or modules consult it as a reference |
| **Structural complexity** | High cyclomatic complexity, nested conditional logic, multiple edge cases |
| **Security or privacy risk** | Handles authentication, authorization, personal data, cryptography |
| **Data integrity** | Affects persistence, transactional consistency, or referential integrity |
| **Technology novelty** | Uses a technology, pattern, or dependency the team has little experience with |

The architect identifies critical artifacts for each phase at sprint start or project start. The list must be visible and agreed upon with the Technical Lead.

---

## 2. The coach in the phase model

The coach's role is consistent across all phases: **silent observer** during the inspection session, with post-session feedback to the team, individual, or organization.

What varies by phase:

- **Requirements:** the coach pays special attention to whether reviewers compare independent interpretations, since ambiguity is only visible when two reviewers arrive at different interpretations.
- **Design and architecture:** the coach observes whether reviewers validate the design against the acceptance criteria of the originating requirement.
- **Code:** the coach observes whether the review covers both functional correctness and non-functional quality criteria (security, performance, maintainability).
- **Unit test design:** the coach observes whether reviewers evaluate the *test cases* (what is tested) in addition to the *test implementation* (how it is tested).
- **System and acceptance test design:** the coach observes whether test cases cover the acceptance criteria of the original requirement and the relevant edge cases.

In all cases, the coach records their observations as `secav:WorkProductEvidence` and uses them to feed the `secav:CompetencyAssessment` of participants after the session.

---

## 3. Phases without a dedicated guide yet

The framework currently has no dedicated guides for:

- **System test design** — test plans covering module integration, external interfaces, and non-functional requirements.
- **Acceptance test design** — executable acceptance criteria, UAT scripts, customer-verifiable definition of Done.

In the absence of a specific guide, these phases follow the general formal inspection protocol (`coaching-governance/guides/formal-inspections.md`), adapting the inspected object from a code artifact to a test design artifact.

---

## 4. Phase-advance criterion

An artifact should not advance to the next phase without passing its minimum quality inspection. This does not require all findings to be corrected before advancing — it does require:

1. Findings are documented in the `secav:ReviewRecord`.
2. Critical or blocking findings are assigned with an owner and deadline.
3. The coach verifies in follow-up (Phase 5 of the inspection) that blocking findings were resolved.

Time pressure that leads to omitting inspections is the most frequent cause of technical debt accumulation and late-phase defects. The coach documents omissions as `secavo:QualityPlanningConcern` and escalates if the pattern is recurring.

---

## 5. Integration with SECAV-O

| Concept | SECAV-O term |
|---|---|
| Requirements phase | `secav:RequirementsActivity` |
| Design phase (architecture, detail, testing) | `secav:DesignActivity`, `secav:ApplicationDesign`, `secav:UnitTestDesign` |
| Code implementation phase | `secav:CodingActivity`, `secav:CodeImplementation` |
| Testing phase (system, acceptance) | `secav:TestingActivity` |
| Design or requirements artifact | `secav:DesignArtifact` |
| Code artifact | `secav:SourceCodeArtifact` |
| Unit test artifact | `secav:UnitTestDesignArtifact` |
| Design review (requirements, architecture, system/acceptance tests) | `secav:DesignReview` |
| Code review | `secav:CodeReview` |
| Unit test review | `secav:UnitTestDesignReview` |
| Critical artifact selection criteria | `secav:QualityCriterion` |
| Phase-advance criterion | `secav:AcceptanceCriterion` |
| Inspection finding | `secav:ReviewFinding` |
| Inspection record | `secav:ReviewRecord` |
| Coach observation notes | `secav:WorkProductEvidence` |
| Documented inspection omission | `secavo:QualityPlanningConcern` |
| Derived competency assessment | `secav:CompetencyAssessment` |

---

## 6. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/requirements-inspection.md` | Inspection protocol for the requirements phase |
| `coaching-governance/guides/formal-inspections.md` | Base formal inspection protocol — applicable to design, architecture, and code |
| `coaching-governance/guides/peer-review-sessions.md` | Peer reviews — complement to formal inspections in the code phase |
| `coaching-governance/guides/unit-test-review.md` | Review protocol for the unit test design phase |
| `coaching-governance/guides/defect-tracking.md` | Defects found in each phase are recorded with the corresponding `phaseInjected` |
| `coaching-governance/guides/project-kickoff-alignment.md` | Inspection coverage by phase must be included in project quality objectives |
| `coaching-governance/docs/metrics-model.md` | Defect metrics by phase — `phaseInjected` distribution as an indicator of inspection coverage |