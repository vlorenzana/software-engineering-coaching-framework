# Engineer Development Record

> **PROPOSAL** — This template is proposed for adoption. It is a longitudinal development record complementing `templates/engineer-coaching-assessment.md`, which covers per-sprint activity-level assessments. This record spans multiple cycles and coaches.

**This artifact has three companion files:**
- `templates/engineer-development-record.md` — this blank template
- `examples/example-engineer-development-record.md` — completed example (Valeria Montes, including a coach change in July)
- `templates/organizational-competency-view.csv` — aggregated organizational view across engineers

**One format across all coaches.** The record belongs to the engineer and the organization, not to the coach assigned at any given time. Any coach can pick it up without losing context; data is comparable across teams.

---

## Competency scale (common across all coaches)

Every rating requires at least one entry in Section 5 (Impact Evidence). A level may not be advanced without observable evidence.

| Level | Label | Description |
|---|---|---|
| 1 | Apprentice | Needs guidance to complete the work. |
| 2 | Autonomous | Delivers independently within known scope. |
| 3 | Team reference | Elevates others and resolves ambiguity. |
| 4 | Multi-team reference | Defines standards with organizational impact. |

**Mapping to SECAV-O competency-growth scale** (`coaching-governance/docs/competency-growth-scale.md`):

| This record (4-level) | SECAV-O coaching-cycle scale (6-level) |
|---|---|
| 1 — Apprentice | 1 Observed / 2 Assisted |
| 2 — Autonomous | 3 Performs with Review / 4 Independent |
| 3 — Team reference | 5 Can Review Others |
| 4 — Multi-team reference | 6 Can Coach Others |

Use the 6-level SECAV-O scale within individual sprint records (`templates/engineer-coaching-assessment.md`). Use the 4-level scale here for cycle-level summary and organizational comparisons.

**Competency dimensions evaluated:**

| Dimension | SECAV-O competency types that contribute |
|---|---|
| Technical excellence | `secav:DesignCompetency`, `secav:TestingCompetency`, `secav:SecurityCompetency` |
| Delivery and execution | `secav:PlanningCompetency`, `secav:DesignCompetency` |
| Quality and operations | `secav:ReviewCompetency`, `secav:TestingCompetency`, `secav:SecurityCompetency` |
| Collaboration | `secav:ReviewCompetency` (reviewer role) |
| Communication | (organizational; not modeled in SECAV-O core) |
| Leadership and impact | (organizational; not modeled in SECAV-O core) |

---

## Governance rules

- Use the same scale and the same fields across the entire organization.
- Every rating and every advance must cite at least one `secav:Evidence` entry (Section 5). No evidence — no record.
- The coach completes the session log (Section 4) within 24 hours of each session.
- Every coach change requires a completed handoff summary in Section 7 and a 30-minute transition session with the engineer present.
- Evaluation cycle: semi-annual. Objectives reviewed: monthly.
- The engineer may read and comment on their own record. The record is shared with the engineer's manager and with HR/Talent. Sensitive personal notes remain in the coach's private log and are not part of this document.
- Section 8 organizational indicators are updated at the end of each cycle to feed the organizational view.

---

## 1. General data

| Field | Value |
|---|---|
| Record ID | |
| Name | |
| Role and level | |
| Team / area | |
| Manager | |
| Start date | |
| Current coach | |
| Start date with current coach | |
| Current cycle | |
| Career track (IC / management) | |

---

## 2. Competencies by cycle

Each row is one competency dimension. Record the level at the start and end of the cycle, the target agreed at cycle planning, and at least one `secav:Evidence` reference.

| Competency dimension | Previous level (1–4) | Current level (1–4) | Cycle goal | Supporting evidence |
|---|---|---|---|---|
| Technical excellence | | | | |
| Delivery and execution | | | | |
| Quality and operations | | | | |
| Collaboration | | | | |
| Communication | | | | |
| Leadership and impact | | | | |

---

## 3. Development plan

Objectives must be specific and measurable. Each objective links to at least one competency dimension and has a defined success metric.

| ID | Objective | Competency dimension | Success metric | Deadline | Status | Progress |
|---|---|---|---|---|---|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |

Status values: `planned` / `in-progress` / `completed` / `deferred` / `cancelled`

---

## 4. Session log

The coach completes this table within 24 hours of each session. The log is part of the auditable coaching record.

| Date | Coach | Topics discussed | Agreements | Next steps and date |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

---

## 5. Impact evidence

Each row is one `secav:Evidence` entry. The Type column should match one of: work product, review finding, defect record, measurement, test result, or observation.

| Date | Type | What occurred | Observable impact | Link / source |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

*Type values map to `secav:Evidence` subclasses: `secav:WorkProductEvidence`, `secav:ReviewFinding`, `secav:DefectRecord`, `secav:Measurement`, `secav:TestResult`.*

---

## 6. 360 feedback

Feedback from peers, leaders, and internal clients. This section informs competency assessment but does not replace observable engineering evidence.

| Date | Source (peer / leader / internal client) | Strengths | Areas for improvement |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

---

## 7. Coach history and handoffs

Every coach transition requires a completed handoff summary before the transition session.

| Coach | From | Until | Reason for change | Handoff summary |
|---|---|---|---|---|
| | | | | |
| | | | | |

---

## 8. Organizational indicators

Updated at the end of each cycle. These indicators feed team- and organization-level views. They must not be used for individual ranking or punitive decisions.

| Indicator | Cycle start value | Cycle end value | Trend | Notes |
|---|---|---|---|---|
| Competency level — technical excellence | | | | |
| Competency level — quality and operations | | | | |
| Competency level — delivery and execution | | | | |
| Development plan objectives completed (%) | | | | |
| Coaching actions with supporting evidence (%) | | | | |
| Late-phase defects (from `templates/defect-log.csv`) | | | | |
| Review participation (from `templates/metrics-register.csv`) | | | | |
| Coaching objectives aligned to institutional objectives (Y/N) | | | | |

*See `coaching-governance/docs/metrics-model.md` for metric definitions and interpretation guidance.*