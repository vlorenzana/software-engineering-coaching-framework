# Preventive Actions in Software Development: Shift-Left Guide

## Purpose

This guide describes the technical and bio-cognitive strategies engineers must apply **before** submitting their code for peer review. Its goal is to mitigate defects in the earliest phases of the lifecycle — when the cost of correction is minimal — rather than depending on the review to discover them.

The coach uses these actions as signals for `secav:PreventiveAction`: their presence or absence in the engineer's daily work is observable evidence of technical competence and cognitive self-management.

> Preventive actions do not replace peer review. They reduce noise in the review so the reviewer can focus their energy on what automation cannot detect.

---

## 1. Early prevention matrix (Shift-Left)

Efficient defect mitigation occurs in the initial phases of the lifecycle. Late intervention is costly: a defect found in production costs significantly more than one found in the requirements phase.

| Phase | Preventive action | Technical impact |
|---|---|---|
| **Requirements mapping** | Clear Acceptance Criteria (BDD/TDD) | Eliminates logical ambiguity before writing the first line of code |
| **Architectural design** | API Contract and Interface Definition | Prevents integration errors and decouples the development of independent modules |
| **Active coding** | Automatic static analysis in the IDE | Detects antipatterns, typing problems, and possible memory leaks in real time |

### 1.1 Clear acceptance criteria (BDD/TDD)

**Why it matters for coaching:** If the engineer cannot articulate the acceptance criteria for their task before starting to code, any implementation evidence they produce is of limited value — there is nothing to evaluate it against.

**Observable signal:**
- The engineer formulates acceptance criteria in verifiable language before writing production code.
- Unit tests are written before or alongside the code they test (TDD), not after.
- The acceptance criterion is recorded in the activity's artifact (`secav:AcceptanceCriterion`).

**Alert signal for the coach:**
- The engineer starts implementation without defined acceptance criteria.
- Tests are written only to reach a coverage threshold, not to verify behavior.

### 1.2 API contract and interface definition

**Why it matters for coaching:** Integration is the most frequent source of late defects. A contract defined before implementation is evidence of design competence (`secav:DesignCompetency`).

**Observable signal:**
- Interfaces between modules or services are defined and agreed upon before teams begin implementing them in parallel.
- The contract design appears as a reviewable artifact (`secav:DesignArtifact`) before implementation.

**Alert signal for the coach:**
- Integration between modules is resolved in the review or merge phase — a signal that design was skipped.
- Integration errors are recurrent in the team's code reviews.

### 1.3 Automatic static analysis in the IDE

**Why it matters for coaching:** Real-time static analysis extends the engineer's ability to detect antipatterns, typing errors, and memory leaks before they reach the CI/CD pipeline.

**Observable signal:**
- The engineer's IDE has linters and static analyzers active and configured according to project standards.
- Static analyzer warnings are addressed before committing, not allowed to accumulate.

**Alert signal for the coach:**
- The engineer systematically disables or ignores IDE warnings.
- PRs contain static analysis violations that should have been detected locally.

---

## 2. Automation protocol in the local environment

Automation acts as the first line of defense, blocking mechanical errors before they reach the shared repository. The coach observes whether the team has this infrastructure active and whether engineers respect it.

### 2.1 Git pre-commit hooks

**Recommended configuration:** Block local commits if the code does not pass basic unit tests or contains exposed environment variables.

**Observable signal:**
- The repository has pre-commit hooks configured and active for all team members.
- Engineers do not disable hooks to bypass the control (`--no-verify`).

**Alert signal for the coach:**
- Frequent commits that introduce exposed environment variables or failing tests — a signal that the hook is not active or is systematically bypassed.
- The team perceives hooks as obstacles rather than as a safety net.

### 2.2 Strict typing policies

**Recommended configuration:** Configure the compiler to prohibit implicit types (e.g., `noImplicitAny` in TypeScript), dramatically reducing runtime errors.

**Observable signal:**
- The compiler configuration has strict mode active and the project compiles without typing warnings.
- Engineers resolve typing errors as they appear, not suppressing them with `any` or equivalents.

**Alert signal for the coach:**
- Systematic use of `any`, unjustified casts, or typing warning suppressions — a signal that the policy is not being internalized as a quality practice.

### 2.3 Automated unit tests with coverage threshold

**Recommended configuration:** Define a minimum code coverage threshold (Code Coverage > 80%) enforced locally before allowing a push.

**Observable signal:**
- The local pipeline has coverage verification configured as a push condition.
- Tests are written to verify behavior, not just to numerically reach the threshold.

**Alert signal for the coach:**
- Coverage is high but tests are trivial — they test getters/setters instead of business logic.
- The engineer writes tests at the end of the sprint to meet the metric, not while developing.

---

## 3. Developer's cognitive infrastructure

The engineer's mental state directly influences the density of defects introduced in the code. The coach observes whether the team operates under cognitive conditions that favor quality or whether it systematically works under conditions that degrade it.

### 3.1 Focused work blocks (Deep Work)

**Recommended practice:** Schedule intervals of complex coding of 45 to 60 minutes without external notifications (Slack, Teams, email) to maintain the mental map of the logic.

**Observable signal:**
- Engineers have protected blocks in their calendar for deep technical work.
- The team has explicit agreements on response times in synchronous channels during development blocks.

**Alert signal for the coach:**
- Engineers report they cannot work more than 20 minutes without being interrupted.
- Recurring defects correspond to boundary cases easily detected with sustained concentration — a signal that work is performed in a fragmented manner.

### 3.2 Mental fatigue limits

**Recommended practice:** Establish mandatory breaks after extended development blocks. Accumulated fatigue deteriorates the ability to identify logical edge cases.

**Observable signal:**
- The engineer takes active breaks between intense work blocks instead of chaining them.
- The team does not schedule cognitively demanding tasks at the end of already saturated days.

**Alert signal for the coach:**
- The most frequent defects appear in code written during low-energy hours (late afternoons, last hours of the sprint).
- Engineers report systematic exhaustion or cannot explain decisions made under pressure.

### 3.3 Self-review before commit (Self-Review)

**Recommended practice:** Take a brief 5-minute break before reviewing one's own local changes, allowing detection of obvious errors with a fresh eye before submitting them for peer review.

**Observable signal:**
- The engineer's PRs have a low density of trivial defects (typos, commented-out code, unused imports) — a signal that there was a self-review before submission.
- The engineer can describe what they reviewed in their own code before requesting the formal review.

**Alert signal for the coach:**
- Reviewers report that PRs arrive with errors the author would have detected with a second reading.
- The engineer never pauses between "finishing the code" and "opening the PR."

---

## 4. Per-sprint verification checklist: preventive actions

The coach reviews this list with the team at the start of each sprint or in the retrospective to assess whether the preventive infrastructure is active.

| Preventive action | Active | Partial | Absent |
|---|---|---|---|
| Acceptance criteria defined before coding | | | |
| API contracts and interfaces agreed before parallel implementation | | | |
| Automatic static analysis active in the IDE for all members | | | |
| Pre-commit hooks configured and respected | | | |
| Strict typing policy active with no unjustified suppressions | | | |
| Unit test coverage threshold active in the local pipeline | | | |
| Focused work blocks protected in the team calendar | | | |
| Team agreements on fatigue limits and breaks | | | |
| Self-review before opening PR (individual practice) | | | |

---

## 5. SECAV-O Integration

| Preventive action | SECAV-O term |
|---|---|
| Acceptance criterion defined before coding | `secav:AcceptanceCriterion` associated with `secav:RequirementsActivity` |
| API contract as design artifact | `secav:DesignArtifact` produced in `secav:DesignActivity` |
| Automatic static analysis | `secav:Measurement` associated with `secav:CodeImplementation` |
| Active pre-commit hook | Precondition of `secav:CodeImplementation`; violation is `secav:DefectRecord` |
| Test coverage > 80% | `secav:AcceptanceCriterion` of `secav:TestingActivity` |
| Absence of preventive action as coaching signal | `secav:ReviewFinding` or `secav:WorkProductEvidence` triggering `secav:CoachingIntervention` |
| Preventive action agreed after intervention | `secav:PreventiveAction` in `secavo:SprintRetrospective` |
| Engineer's cognitive state as precondition | Analogous to `secav:ReviewerReadiness` in `secav:CodeImplementation` |

---

## 6. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/peer-review-antipatterns.md` | Review antipatterns that these preventive actions aim to avoid |
| `coaching-governance/guides/code-review-best-practices.md` | Review practices; preventive actions reduce the review burden |
| `coaching-governance/guides/unit-test-review.md` | Unit test design review guide |
| `coaching-governance/guides/defect-tracking.md` | Defect log that allows identifying whether prevention is working |
| `templates/sprint-retrospective.md` | Space where the coach introduces the state of preventive infrastructure as an improvement point |
| `templates/engineer-coaching-assessment.md` | Competency assessment where preventive actions are observable evidence |
| `pilot/pilot-protocol.md` | The pilot can use pre-merge defect density as a metric to evaluate the impact of these actions |