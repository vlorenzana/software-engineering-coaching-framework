# Coach Meeting Minutes

<!-- Complete one instance of this template for every formal meeting facilitated by the coach.
     Distribute the draft to participants within 24 hours after the meeting.
     Each agreement is a secav:MeetingAgreement traceable in subsequent meetings. -->

> **MANDATORY MINIMUM ELEMENTS — the minutes are only valid if they contain all three:**
>
> | # | Element | Section | Without this... |
> |---|----------|---------|-----------------|
> | 1 | **Participants** — name and role of every attendee | § 1 | No traceability of who made the agreements |
> | 2 | **Topics discussed** — at least one topic with its outcome or decision | § 2 | No record of what was discussed |
> | 3 | **Agreements with date** — at least one agreement with owner and explicit deadline | § 3 | No traceable commitment or follow-up possible |
>
> Minutes that omit any of these three elements cannot close the meeting and must be completed before distribution.

---

## Header

- **Minutes code:** MIN-`YYYY`-`XXXX`
- **Date:** DD/MM/YYYY
- **Start / end time:** HH:MM – HH:MM
- **Meeting type:**
  - [ ] Project kick-off
  - [ ] Sprint planning
  - [ ] Retrospective
  - [ ] 1-on-1 session
  - [ ] Technical review / inspection
  - [ ] Follow-up on prior agreements
  - [ ] Ad-hoc / urgent
- **Facilitator (coach):** [Name]
- **Sprint / Cycle:** [Sprint ID or period]

**SECAV-O:** These minutes are an instance of `secav:MeetingMinutes`, produced in a `secav:CoachingMeeting` and linked to the `secav:CoachingIntervention` of the current cycle.

---

## 1. Participants

> **Mandatory.** Record all attendees. A meeting without documented participants has no traceability.

| Name | Role | Attendance |
|------|------|------------|
| [Name] | [Role] | [ ] Present  [ ] Excused absence |
| [Name] | [Role] | [ ] Present  [ ] Excused absence |
| [Name] | [Role] | [ ] Present  [ ] Excused absence |

---

## 2. Context and Purpose

> Why was this meeting held? What situation, observation, or artifact prompted the call?

_

---

## 3. Topics Discussed

> **Mandatory.** Record at least one topic with its outcome or decision. Without this there is no record of what was discussed.

| # | Topic | Decision / Outcome | SECAV-O term |
|---|-------|--------------------|--------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |

> Add or remove rows as needed.
>
> **If a review session (peer review, walkthrough, or inspection) was discussed:** record whether the `secav:CoachReviewSignOff` was issued — Yes / No / Pending — in the Decision / Outcome column. A pending sign-off must appear as an open agreement in § 4.

---

## 4. Agreements and Commitments

> **Mandatory.** Each agreement must have an owner and an explicit deadline. Without a date there is no follow-up possible.
>
> Open agreements are reviewed **always at the start of the next meeting** of this type.

Each row is a `secav:MeetingAgreement` with owner, deadline, and follow-up status.

| ID | Agreement / Commitment | Owner | **Deadline** | Status |
|----|------------------------|-------|--------------|--------|
| ACU-01 | | [Name] | **DD/MM/YYYY** | [ ] Open |
| ACU-02 | | [Name] | **DD/MM/YYYY** | [ ] Open |
| ACU-03 | | [Name] | **DD/MM/YYYY** | [ ] Open |

**Agreement escalation:**
- If an agreement requires individual follow-up → record `secav:CoachingIntervention` in `templates/engineer-coaching-assessment.md`
- If an agreement produces a systemic process improvement → record as `secavo:ImprovementAction` in `templates/sprint-retrospective.md`
- If an agreement leads to a root-cause analysis → initiate `templates/rca-defect-analysis.md`

---

## 5. Review of Agreements from Previous Meetings

| Prior ID | Agreement | Owner | Status at close |
|----------|-----------|-------|-----------------|
| ACU-XX | [description of prior agreement] | [Name] | [ ] Completed  [ ] Pending  [ ] Cancelled |

---

## 5b. Review Session Record *(complete only when meeting type is "Technical review / inspection")*

> If this meeting is a peer review, walkthrough, or formal inspection session, the following fields are mandatory per `secav:CoachReviewSignOff` governance.

| Field | Value |
|-------|-------|
| **Artifact reviewed** | [file / module / requirements section / design artifact] |
| **Review type** | [ ] Peer code review  [ ] Walkthrough  [ ] Formal inspection  [ ] Unit test design review  [ ] Requirements review  [ ] Design review |
| **Findings recorded** | [ ] Yes — count: __  [ ] No defects found (explicit)  [ ] Not recorded (session not valid) |
| **Proposed solutions recorded** | [ ] Yes (for agreed-upon directions)  [ ] N/A |
| **Coach sign-off issued** | [ ] Yes — `secav:CoachReviewSignOff` issued (date: _____)  [ ] No — findings are provisional, not valid as competency evidence |
| **Sign-off statement** | _Brief statement confirming the session was conducted acceptably (or reason for withholding)_ |

> If no sign-off is issued, note the reason here and in the agreements section (§ 4) with a follow-up action.

---

## 5c. Sprint Planning Gate *(complete only when meeting type is "Sprint planning")*

> Verify the following before finalizing the sprint plan (per `secav:RequirementsReview` obligation and Code of Ethics Principle 17).

- [ ] At least one `secav:RequirementsReview` session is included in the sprint work plan for features entering implementation this sprint
- [ ] The RequirementsReview session has an assigned facilitator, scheduled date, and identified participants
- [ ] The coach has endorsed the inclusion of the RequirementsReview in the plan (endorsement counts as the planning-gate sign-off — not as the post-session sign-off)
- [ ] If no RequirementsReview is planned: a written justification is recorded below and the coach has approved the exception

> **Exception justification (if applicable):** _

> Features that begin implementation without a completed RequirementsReview are in `secav:MissingRequirementsReview` antipattern state — the highest-risk antipattern in the development lifecycle.

---

## 6. Open Items

Topics requiring additional information, analysis, or a follow-up session to resolve.

| # | Open item | Next step | Owner |
|---|-----------|-----------|-------|
| 1 | | | [Name] |
| 2 | | | [Name] |

---

## 7. Next Meeting

- **Proposed date:** DD/MM/YYYY
- **Time:** HH:MM
- **Tentative agenda:**
  1. Review of agreements (ACU-01, ACU-02, ...)
  2. [Topic 1]
  3. [Topic 2]

---

## Closure and Distribution

> Before distributing, verify that the minutes meet the three mandatory elements:
> - [ ] § 1 complete — all participants recorded with name and role
> - [ ] § 3 complete — at least one topic with decision or outcome
> - [ ] § 4 complete — at least one agreement with owner and **explicit deadline**
> - [ ] *(Sprint planning only)* At least one `secav:RequirementsReview` is included in the work plan before implementation begins — or a `secavo:QualityPlanningConcern` has been raised (Principle 17)

These minutes were distributed to participants on: DD/MM/YYYY

| Participant | Role | Receipt confirmation |
|-------------|------|---------------------|
| [Name] | [Role] | [ ] Received |
| [Name] | [Role] | [ ] Received |

> The coach archives minutes in the channel or repository agreed with the team. Minutes are not distributed outside the team without participant consent.

---

## Related documents

| Document | Relationship |
|---|---|
| `templates/sprint-retrospective.md` | Agreements that improve the process are recorded as ImprovementActions |
| `templates/engineer-coaching-assessment.md` | Individual coaching interventions derived from this meeting |
| `templates/rca-defect-analysis.md` | If the meeting analysed a P1/P2 defect |
| `templates/annual-coaching-plan.md` | Long-term agreements that affect the cycle coaching plan |
| `coaching-governance/guides/coach-observation-checklist.md` | Coach observations that motivated this meeting |
| `coaching-governance/guides/coach-attitudes.md` | Coach attitudes during facilitation |