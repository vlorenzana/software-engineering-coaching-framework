# Antipatterns in Peer Reviews: Coach Observation Guide

## Purpose

This guide catalogs the most frequent operational and cultural errors in peer reviews — each with its observable impact and mitigation strategy. The coach uses these antipatterns as signals for `secav:CoachingIntervention`: if a pattern appears recurrently in observed sessions, it is a candidate for an individual or group conversation.

This guide is the counterpart to `coaching-governance/guides/code-review-best-practices.md`, which describes what to do. This guide describes what to avoid.

---

## 1. Reviewing style manually

**Impact:** The team spends analytical energy on trivial debates — indentation, braces, spaces — diverting attention from design and logic.

**Observable signal for the coach:**
- Review comments concentrate on formatting instead of architecture, security, or business logic.
- Engineers debate style conventions during the session instead of delegating it to tools.
- The CI/CD pipeline has no linters or formatters configured, or engineers ignore them.

**Mitigation strategy:**
Delegate formatting 100% to linters and automatic formatters in CI/CD. Human energy in a review is a scarce resource: it must be invested in what automation cannot detect.

**Reference:** `coaching-governance/guides/code-review-best-practices.md` §3.7 — Style and consistency.

---

## 2. Overly long sessions

**Impact:** Visual acuity drops dramatically after 60 continuous minutes. Complex errors go unnoticed when the reviewer is already in analytical fatigue.

**Observable signal for the coach:**
- Review sessions exceed 60 continuous minutes or 400 lines of code (LOC) per block.
- Findings documented in the second half of the session are superficial or low-impact compared to those from the first.
- Engineers report exhaustion or loss of concentration after long reviews.

**Mitigation strategy:**
Limit each review block to a maximum of 60 minutes or 400 LOC. If the change is larger, split it into blocks with a break between them or into separate sessions.

**Reference:** `coaching-governance/guides/code-review-best-practices.md` §1 — Scope and size.

---

## 3. Missing initial context

**Impact:** The reviewer spends time trying to guess the purpose of the changes, slowing the cycle and increasing the risk of approving code without understanding its intent.

**Observable signal for the coach:**
- Pull Requests (PRs) do not include a description of the *why*, *how*, and acceptance criteria.
- Reviewers ask the author about the purpose of the change during the session — a signal that context was not available beforehand.
- Reviewers report having needed to review tickets or external documents to understand the change.

**Mitigation strategy:**
Require each PR to include a structured description with at least: purpose of the change, implementation approach, and acceptance criteria. This is the author's responsibility, not the reviewer's.

**Reference:** `coaching-governance/guides/code-review-best-practices.md` §2 — Preparing a change for review.

---

## 4. Unfinished or WIP code

**Impact:** Premature reviews invalidate prior effort when code changes mid-session. They generate rework and erode reviewers' trust in the process.

**Observable signal for the coach:**
- Reviewers receive PRs that still have unresolved TODOs, failing tests, or changes marked as drafts.
- The author modifies code while the review is in progress, invalidating comments already written.
- Reviewers express frustration because their comments become obsolete between one review iteration and the next.

**Mitigation strategy:**
Use *Draft PR* status for work in progress. Formal review is only requested when automated tests pass completely and the author considers the code ready.

---

## 5. Lack of empathy in feedback

**Impact:** Comments perceived as personal attacks destroy team trust and generate defensiveness, reducing the quality of technical dialogue in future reviews.

**Observable signal for the coach:**
- Comments are directed at the author: *"you did X wrong,"* *"you never handle this case."*
- The author adopts a defensive posture — justifies decisions instead of exploring them.
- Engineers avoid submitting their code for review or delay requesting review.
- Comments do not include severity prefixes: no distinction between suggestions and blockers.

**Mitigation strategy:**
Always comment on the code, never on the person. Use phrasings like *"module X could..."* instead of *"you did X wrong."* Label comments with explicit prefixes: `[Suggestion]`, `[Blocker]`, `Nit:`.

**Reference:** `coaching-governance/guides/code-review-best-practices.md` §4 — How to give feedback.

---

## 6. Lack of rigor with AI-assisted code

**Impact:** Code generated or modified by automated assistants may contain logical hallucinations, subtle duplication, or vulnerabilities that are not detectable by superficial inspection. Automatic approval of AI code introduces unaudited technical debt and security risks.

**Observable signal for the coach:**
- Reviewers approve AI code without evidence that they explicitly reviewed the business logic.
- The `secav:ReviewRecord` does not indicate that the artifact was produced with AI assistance (`secav:assistedByAI`).
- Engineers assume that AI-generated code is correct if the tests pass.

**Mitigation strategy:**
The human reviewer must exhaustively validate the business logic of all AI-assisted code — especially boundary conditions and data flows. AI does not replace human review; human review of AI code is mandatory, not optional.

**Reference:** `coaching-governance/guides/code-review-best-practices.md` §9 — AI-assisted code and review; `coaching-governance/guides/ai-assisted-code-review.md`.

---

## 7. Mental verification checklist for the efficient reviewer

Before starting a review session, the engineer checks their bio-cognitive state. The coach observes whether the team applies these conditions systematically or omits them under pressure.

| Phase | Required check | Alert signal for the coach |
|---|---|---|
| **Biological energy** | Perform complex reviews during windows of greatest mental clarity (preferably in the morning); never under extreme fatigue at the end of the day. | Reviews systematically scheduled at end-of-day or outside normal hours. |
| **Isolation** | Block 30–60 minutes on the calendar; silence Slack, Teams, and email notifications to avoid focus loss from context switching. | Engineers review code between meetings or with active notifications. |
| **Critical analysis** | Ignore aesthetic details already covered by automated tools; focus mental energy on architecture, input security, and business logic. | Review findings are mostly stylistic rather than design- or security-related. |
| **Assertive closure** | Qualify contributions explicitly: if the code fulfills its purpose with minor details, approve the change and leave suggestions as optional improvements. | Reviews end without a clear decision — no approval or defined list of blockers. |

---

## 8. SECAV-O Integration

| Antipattern | SECAV-O term |
|---|---|
| Manual style review (without automation) | `secav:ReviewActivity` with low-impact findings; coaching signal on tool usage |
| Overly long session | Degraded `secav:ReviewActivity` precondition; observable as precondition of `secav:HumanValidationActivity` |
| Missing context in PR | `secav:Artifact` without adequate description; change traceability is incomplete |
| WIP code in formal review | Premature `secav:ReviewActivity`; invalidates potential `secav:ReviewFinding` |
| Non-empathic feedback | `secav:ReviewFinding` directed at the person, not the artifact; signal for `secav:CoachingIntervention` |
| AI code without scrutiny | Incomplete `secav:HumanValidationActivity`; `secav:assistedByAI` without recorded validation |

---

## 9. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/code-review-best-practices.md` | Positive practices that are the counterpart of each antipattern in this guide |
| `coaching-governance/guides/peer-review-sessions.md` | Protocol for the coach as silent observer during the review session |
| `coaching-governance/guides/ai-assisted-code-review.md` | Complete guide for AI-assisted code review |
| `coaching-governance/guides/formal-inspections.md` | Formal inspection process for critical modules — more rigorous than peer review |
| `templates/engineer-coaching-assessment.md` | Template where competency observations derived from reviews are recorded |
| `templates/defect-log.csv` | Defect log that allows identifying recurring patterns by type and author |