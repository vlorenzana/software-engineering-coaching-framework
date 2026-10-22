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