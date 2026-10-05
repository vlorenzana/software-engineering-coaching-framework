# Engineer Development Record — Example (Fictional)

> This is a fictional example for illustrative purposes. The engineer, coach names, and all data are invented. Use this as a reference when filling out `templates/engineer-development-record.md`.

---

## Competency scale reference

| Level | Label |
|---|---|
| 1 | Apprentice |
| 2 | Autonomous |
| 3 | Team reference |
| 4 | Multi-team reference |

---

## 1. General data

| Field | Value |
|---|---|
| Record ID | EXP-2026-047 |
| Name | Valeria Montes |
| Role and level | Software Engineer II |
| Team / area | Platform Engineering |
| Manager | Andrés Ruiz |
| Start date | 2024-03-10 |
| Current coach | Laura Ibáñez |
| Start date with current coach | 2026-07-15 |
| Current cycle | 2026-H2 (July–December 2026) |
| Career track | IC (Individual Contributor) |

---

## 2. Competencies by cycle

### Cycle 2026-H1 (January–June 2026)

| Competency dimension | Previous level (1–4) | Current level (1–4) | Cycle goal | Supporting evidence |
|---|---|---|---|---|
| Technical excellence | 2 | 2 | Reach 3 | EV-031: design review of auth module accepted with no major findings |
| Delivery and execution | 2 | 3 | Reach 3 | EV-033: delivered migration feature 2 weeks ahead of deadline |
| Quality and operations | 1 | 2 | Reach 2 | EV-029: first independent code inspection completed |
| Collaboration | 2 | 2 | Maintain | EV-034: positive 360 from two peers (Section 6) |
| Communication | 2 | 2 | Maintain | Session log 2026-05-12 |
| Leadership and impact | 1 | 1 | Maintain | No evidence of multi-person impact yet |

### Cycle 2026-H2 (July–December 2026) — in progress

| Competency dimension | Previous level (1–4) | Current level (1–4) | Cycle goal | Supporting evidence |
|---|---|---|---|---|
| Technical excellence | 2 | — | Reach 3 | In progress — see objective OBJ-03 |
| Delivery and execution | 3 | — | Maintain 3 | |
| Quality and operations | 2 | — | Reach 3 | In progress — see objective OBJ-04 |
| Collaboration | 2 | — | Reach 3 | |
| Communication | 2 | — | Maintain | |
| Leadership and impact | 1 | — | Reach 2 | |

---

## 3. Development plan

### Active objectives — cycle 2026-H2

| ID | Objective | Competency dimension | Success metric | Deadline | Status | Progress |
|---|---|---|---|---|---|---|
| OBJ-03 | Lead the design review of the payments service refactor without coach present | Technical excellence | Zero reopened major findings after review | 2026-10-31 | in-progress | 60% — first review session completed |
| OBJ-04 | Complete formal inspection of two peer pull requests per month using team checklist | Quality and operations | 6 formal inspections recorded with findings in defect log | 2026-12-15 | in-progress | 2/6 completed |
| OBJ-05 | Present architecture decision for caching layer to Platform team | Communication | Recorded presentation; at least one decision adopted by team | 2026-11-30 | planned | — |
| OBJ-06 | Onboard one new team member through their first sprint | Leadership and impact | New member reaches Autonomous on delivery within 4 weeks | 2026-12-01 | planned | — |

### Completed objectives — cycle 2026-H1

| ID | Objective | Competency dimension | Success metric | Deadline | Status | Progress |
|---|---|---|---|---|---|---|
| OBJ-01 | Independently complete design and implementation of auth module | Technical excellence | Design review accepted with ≤ 2 major findings | 2026-06-01 | completed | Accepted with 1 major finding (EV-031) |
| OBJ-02 | Lead database migration feature end to end | Delivery and execution | Feature delivered within sprint; no production escapes | 2026-05-15 | completed | Delivered; 0 production escapes (EV-033) |

---

## 4. Session log

| Date | Coach | Topics discussed | Agreements | Next steps and date |
|---|---|---|---|---|
| 2026-01-08 | Marco Solis | Cycle H1 planning; objectives OBJ-01 and OBJ-02; baseline review | Agreed on 4-week check-ins; Valeria to submit design draft by Jan 22 | Design draft review: 2026-01-22 |
| 2026-02-05 | Marco Solis | Auth module design progress; first inspection attempt | Coaching on inspection techniques; practice with two low-risk PRs | Follow-up inspection: 2026-02-19 |
| 2026-03-12 | Marco Solis | Mid-cycle check; migration feature scope confirmed | Risk flagged: tight deadline on OBJ-02; add buffer review step | Risk review: 2026-03-26 |
| 2026-05-12 | Marco Solis | OBJ-01 and OBJ-02 completed ahead of schedule; H1 retrospective | Document evidence; plan H2 objectives for next cycle | H2 planning: 2026-07-10 |
| 2026-07-10 | Marco Solis | Coach handoff session (Marco departing team); introduced Laura Ibáñez | Transition completed; H2 plan reviewed together | First session with Laura: 2026-07-17 |
| 2026-07-17 | Laura Ibáñez | Onboarding to record; confirmed H2 objectives; reviewed open risks | Laura familiar with context; adjusted OBJ-05 deadline to Nov 30 | Check-in: 2026-08-07 |
| 2026-08-07 | Laura Ibáñez | Payments design review preparation (OBJ-03); inspection log review | Valeria to run first payments design review session independently | Payments review: 2026-09-04 |
| 2026-09-04 | Laura Ibáñez | Payments review debrief; 1 major finding reopened, resolved same session | Strong evidence for quality growth; document as EV-041 | OBJ-03 check: 2026-10-03 |

---

## 5. Impact evidence

| Date | Type | What occurred | Observable impact | Link / source |
|---|---|---|---|---|
| 2026-02-19 | Review finding (`secav:ReviewFinding`) | Identified missing null-check in peer's auth service PR; defect corrected before merge | Defect removed pre-production; first independent review finding recorded | PR #284 — defect-log entry DEF-018 |
| 2026-04-28 | Work product (`secav:WorkProductEvidence`) | Auth module design accepted in formal review with 1 major finding | Design competency advancing; first major design accepted independently | Design review record DR-2026-09 |
| 2026-05-09 | Measurement (`secav:Measurement`) | Migration feature delivered 2 weeks early; 0 production escapes across 3-week observation period | Delivery and execution at level 3 confirmed | Sprint report S26-H1-09; defect-log zero escapes |
| 2026-06-10 | Review finding (`secav:ReviewFinding`) | Completed formal inspection of 3 PRs in H1; 2 medium findings accepted by authors | Quality participation evidence; enables coaching on inspection depth | Inspection records INS-2026-04, INS-2026-05, INS-2026-06 |
| 2026-09-04 | Work product (`secav:WorkProductEvidence`) | Led payments design review; 1 reopened major finding resolved within session | Independent review leadership; no coach facilitation needed | Review record DR-2026-17 (EV-041) |

---

## 6. 360 feedback

| Date | Source | Strengths | Areas for improvement |
|---|---|---|---|
| 2026-03-20 | Peer — Carlos Vega | Clear written communication; identifies blockers early; follows up on agreements | Could push back sooner when scope expands |
| 2026-03-21 | Peer — Diana Salas | Reliable delivery; asks good clarifying questions in reviews | Design explanations sometimes assume too much prior context |
| 2026-06-05 | Leader — Andrés Ruiz | Grew significantly in H1; now a dependable contributor; proactive about quality | Needs to grow into more visible team impact; leadership dimension still at 1 |

---

## 7. Coach history and handoffs

| Coach | From | Until | Reason for change | Handoff summary |
|---|---|---|---|---|
| Marco Solis | 2024-03-10 | 2026-07-10 | Marco moved to a different team | H1 cycle completed successfully; OBJ-01 and OBJ-02 closed. Key risk: leadership dimension at level 1 — needs deliberate objectives in H2. Valeria is a strong candidate for promotion to Engineer III if quality and leadership dimensions reach level 3 by end of H2. Transition session held 2026-07-10 with Valeria present. |
| Laura Ibáñez | 2026-07-15 | — | Current | — |

---

## 8. Organizational indicators — cycle 2026-H1 (closed)

| Indicator | Cycle start value | Cycle end value | Trend | Notes |
|---|---|---|---|---|
| Competency level — technical excellence | 2 | 2 | → stable | OBJ-03 in H2 targets level 3 |
| Competency level — quality and operations | 1 | 2 | ↑ improved | First formal inspections completed |
| Competency level — delivery and execution | 2 | 3 | ↑ improved | Level 3 confirmed by two independent observations |
| Development plan objectives completed (%) | — | 100% (2/2) | ↑ | Both OBJ-01 and OBJ-02 closed |
| Coaching actions with supporting evidence (%) | — | 100% | ↑ | All 5 evidence entries link to objectives |
| Late-phase defects (from defect log) | 3 | 0 | ↑ improved | 0 production escapes in H1 |
| Review participation | 0 inspections | 3 inspections | ↑ | Baseline established |
| Coaching objectives aligned to institutional objectives | No | Yes | ↑ | OBJ-02 linked to platform reliability goal |

> **Promotion / retention flags (for organizational view):**
> - Promotion candidate for Engineer III: **Yes** — delivery at level 3, quality improving, two completed objectives
> - Retention risk: **Low** — engaged; clear growth plan in H2; new coach onboarded smoothly