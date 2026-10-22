# Ideal Conditions for Code Review

## Purpose

This guide defines the standards and preconditions that must be met before and during a code review session. The coach uses it to verify compliance and identify coaching interventions when conditions are consistently violated. It is the counterpart to `coaching-governance/guides/peer-review-antipatterns.md`, which describes what to avoid; this guide describes what conditions enable a review to succeed.

Source: original document "Condiciones Ideales para una Revisión de Código — Guía de Buenas Prácticas y Estándares de Ingeniería de Software."

---

## Key metrics

| Metric | Target |
|---|---|
| PR size | < 400 lines of code per review block |
| Session duration | < 60 continuous minutes |
| CI gate | 100% automated tests and linters passing before review begins |
| Response SLA | Maximum 24 business hours per review cycle |

---

## 1. Author preparation

A successful code review begins before the reviewer is assigned. The author is responsible for ensuring the change is clear, focused, and self-documented to minimize the cognitive load imposed on the rest of the team.

### Small, focused pull requests

Limit each PR to a single objective or feature. Keep changes below 400 lines of code. Massive refactors must be submitted separately from business logic changes. Large, unfocused PRs increase the probability of superficial approval and undocumented defects.

**Coach signal:** A PR that mixes refactoring with new features, or that exceeds 400 LOC without a justified exception, is a candidate for `secav:CoachingIntervention` on change decomposition practice.

### Context and description

The PR description must explain the *what* and the *why*, not just the *how*. Required elements:

- Link to the corresponding task (Jira, GitHub Issues, or equivalent).
- Summary of the implementation approach and any relevant decisions.
- Screenshots or GIFs for UI changes.

**Coach signal:** Reviewers asking the author during the session what a change is for is evidence that context was not provided upfront — a `secav:MissingReviewContext` condition.

---

## 2. CI/CD automation gate

The human reviewer's time must focus on design, architecture, and maintainability. Everything that can be validated automatically must be automated before the review begins.

**Golden Rule:** No pull request should be manually reviewed if unit tests or automatic linters are in a failing state.

### Required automated checks

- Format linters (ESLint, Prettier, Black, or equivalent).
- Static security and quality analysis (SonarQube or equivalent).
- Successful execution of the full test suite (unit and integration).

### Benefits of enforcing the gate

- Eliminates code-style debates in review comments.
- Guarantees main branch stability.
- Reduces reviewer fatigue by focusing review effort on logic and design.

**Coach signal:** If a review session begins while the CI pipeline is red, the coach documents this as a `secav:AutomationGate` violation and initiates a conversation about the team's entry criteria for formal review.

---

## 3. Team mindset and culture

Code review is a collaborative, continuous-learning activity — not a control mechanism or a personal judgment instance. The coach observes both reviewer and author behavior to detect cultural antipatterns.

### For the reviewer

- Criticize the code, never the author.
- Ask constructive questions instead of issuing absolute demands.
- Acknowledge and praise elegant or well-structured solutions.
- Distinguish blocking errors from optional suggestions by using explicit prefixes: `[Blocker]`, `[Suggestion]`, `nit:`.

**Coach signal:** Comments directed at the person ("you never handle this case") rather than the artifact are a signal for `secav:NonEmpathicReviewFeedback` and a candidate for `secav:CoachingIntervention`.

### For the author

- View feedback as an improvement opportunity, not a personal attack.
- Respond to all comments or explicitly resolve threads when applying changes.
- Thank reviewers for the time they invested in the session.

**Coach signal:** Authors who adopt a defensive posture — justifying decisions instead of exploring them — or who delay responding beyond the 24-hour SLA indicate a cultural condition that requires coaching attention.

---

## 4. Technical evaluation criteria

During human review, prioritize solution simplicity and soundness over personal coding preferences. The table below defines the evaluation areas the reviewer must cover.

| Evaluation area | Key aspects to inspect |
|---|---|
| Design and architecture | Does the change integrate well with the existing system? Does it follow the project's established patterns? |
| Functionality | Does the code meet the stated requirement? Does it handle edge cases and errors correctly? |
| Maintainability | Is the code easy to read and understand? Are variable and function names clear and intention-revealing? |
| Performance and security | Are there inefficient database queries? Are there security vulnerability risks? |
| Documentation | Were relevant inline comments, API documentation, or README sections updated? |

**Coach signal:** Findings concentrated only in the "Documentation" row and absent from "Design and architecture" or "Performance and security" may indicate a superficial review — a coaching signal on review depth.

---

## 5. Time management and response SLA

A blockage in code review is a blockage in value delivery. Responding to reviews within a maximum of 24 business hours is the recommended standard to avoid context accumulation and integration conflicts.

This SLA applies to both directions: the reviewer's initial response to a PR submission and the author's response to review comments. When either side consistently violates this window, work-in-progress inventory grows and merge conflicts multiply.

**Coach signal:** Systematic response times beyond 24 business hours are observable in the team's PR history. The coach uses this as a coaching conversation trigger on flow management and WIP limits.

---

## 6. SECAV-O integration

| Concept from this guide | SECAV-O term | Notes |
|---|---|---|
| Small, focused PR (< 400 LOC) | `secav:Artifact` size precondition; `secav:ReviewActivity` entry criterion | Violation: `secav:PrematureReviewRequest` or oversized artifact |
| Full PR description (what, why, task link) | `secav:FormalReviewRequest` with `secav:requestDescription` | Missing description: `secav:MissingReviewContext` coaching signal |
| CI/CD golden rule (no review with failing tests) | `secav:AutomationGate`; `secav:ContinuousIntegrationActivity` | Gate violation triggers `secav:CoachingIntervention` |
| Code/not person feedback | Absence of `secav:NonEmpathicReviewFeedback`; `secav:PunitiveReviewApproach`; `secav:ReviewerDictatorship` | Coach observes comment tone during session |
| Blocking vs. optional distinction (`[Blocker]` / `nit:`) | `secav:ReviewFinding` with severity level | Lack of distinction: coaching signal on feedback quality |
| Design and architecture evaluation | `secav:QualityCriterion`; `secav:AcceptanceCriterion` | Absence of findings in this area: coaching signal on review depth |
| Functionality (edge cases, error handling) | `secav:ReviewFinding` | No edge-case findings: signal for `secav:HappyPathOnlyReview` antipattern |
| Performance and security evaluation | `secav:ReviewFinding` with security or performance category | Security findings must be escalated per Principle 17 |
| 24-hour response SLA | `secav:WorkProductEvidence` timeliness; flow metric observable in PR history | Systematic SLA breach: `secav:CoachingIntervention` on WIP management |

---

## 7. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/peer-review-antipatterns.md` | Counterpart guide cataloging what to avoid; maps to the same conditions from the failure perspective |
| `coaching-governance/guides/code-review-best-practices.md` | Broader practices guide covering scope, feedback, and tool usage |
| `coaching-governance/guides/ai-assisted-code-review.md` | Extension for AI-assisted code; automation gate criteria apply equally |
| `coaching-governance/guides/peer-review-sessions.md` | Protocol for the coach as silent observer during the review session |
| `coaching-governance/guides/formal-inspections.md` | Formal inspection process for critical modules — more rigorous than peer review; same entry criteria apply |