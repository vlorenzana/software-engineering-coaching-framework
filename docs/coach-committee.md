# Coach Committee

## Purpose

When an organization has more than one coach, a **Coach Committee** provides the governance structure for coordinating coaching practices, generating organization-wide coaching plans, and ensuring consistent application of the framework across teams.

The committee is not a hierarchy that replaces individual coach autonomy in their assigned teams. It is a coordination and standards body, operating similarly to a cross-functional team: it has a designated lead, defined members, shared responsibilities, and a regular cadence.

---

## 1. When a committee is formed

A Coach Committee is appropriate when:

- the organization has **two or more active coaches**;
- multiple teams are being coached under the same framework; or
- organizational coaching plans need to be compared, aggregated, or coordinated across teams.

A single coach operating alone does not form a committee. When a second coach joins, the committee is established.

---

## 2. Committee composition

| Role | Description |
|---|---|
| **Lead Coach** (`secavo:LeadCoach` — *proposed, see §7*) | Designated coordinator of the committee. Responsible for organizational coaching plan governance, escalation handling, and external communication with management or HR. |
| **Committee Member** (`secav:Coach`) | Any active coach assigned to at least one engineering team. Each member retains full autonomy within their assigned teams. |

Minimum size: 2 coaches (1 Lead + 1 Member).
There is no prescribed maximum, but the committee should remain small enough to make decisions efficiently.

---

## 3. Lead Coach designation

The Lead Coach may be designated by one of two mechanisms. The adopting organization chooses which applies:

### 3.1 Designation by senior management or direction

The organization's management or HR/Talent leadership designates the Lead Coach based on seniority, domain expertise, or organizational fit. The designation should be documented with a rationale and a term duration.

### 3.2 Election by coach consensus

The coaches elect the Lead Coach among themselves by consensus or majority vote. The election process, term, and any tie-breaking rules are agreed by the committee at formation and recorded in the committee charter (`templates/coach-committee-charter.md`).

In both mechanisms:
- The Lead Coach serves for a defined term (recommended: aligned to the annual coaching plan cycle).
- The Lead Coach may be re-designated or re-elected at the end of the term.
- A Lead Coach who is no longer active or available is replaced using the same mechanism.

---

## 4. Committee responsibilities

### 4.1 Organizational coaching plan

The committee generates and maintains an **organizational coaching plan** that aggregates and coordinates the individual team coaching plans. This includes:

- organization-wide coaching objectives aligned to institutional objectives (`secavo:alignsWithInstitutionalObjective`);
- cross-team competency baseline summary;
- organization-wide risk register (`secavo:hasRisk`) covering risks that affect multiple teams;
- coach assignment matrix (which coach covers which team and members);
- shared calendar of coaching cycles and retrospectives.

### 4.2 Standards and practice oversight

The committee is responsible for:

- maintaining the competency scale and ensuring all coaches apply it consistently (`secav:CompetencyAssessment`);
- reviewing and updating coaching templates and evidence standards;
- approving changes to the framework's local configuration (adapted acceptance criteria, added competency types, etc.);
- monitoring that the Code of Ethics (`docs/coach-code-of-ethics.md`) is observed across all coaches.

### 4.3 Coach assignment

The committee assigns coaches to teams and individual engineers. Assignment decisions consider:

- coach capacity;
- domain relevance (a coach with testing expertise assigned to teams with testing gaps);
- conflict-of-interest avoidance (a coach should not evaluate a close direct report or personal relationship);
- continuity (coach changes require a handoff summary, as defined in `templates/engineer-development-record.md` §7).

### 4.4 Escalation and dissent

The Lead Coach is the first point of escalation when:

- a coach-engineer disagreement cannot be resolved at team level;
- a quality-planning dissent (`templates/quality-planning-dissent-and-escalation.md`) requires committee endorsement before reaching management;
- an ethics concern involving a coach is raised.

The Lead Coach may escalate further to management or HR following the chain defined by the adopting organization.

### 4.5 Organizational view

The committee aggregates the organizational indicator data from individual engineer development records (`templates/engineer-development-record.md`, Section 8) into the organizational competency view (`templates/organizational-competency-view.csv`) to produce an organization-level coaching health view at the end of each cycle, including:

- average competency level per dimension across all engineers;
- coaching objective completion rate;
- promotion and retention risk flags;
- cross-team defect and review participation trends.

---

## 5. Committee governance cadence

| Event | Frequency | Purpose |
|---|---|---|
| Committee planning session | Annual (aligned to plan cycle) | Set org-wide coaching plan, objectives, and risk register |
| Committee review | Each sprint cycle | Review org-wide risks, compare team retrospective outputs, adjust assignments |
| Standards review | Semi-annual | Review competency scale, templates, evidence criteria |
| Ethics review | Annual | Confirm all coaches have acknowledged the Code of Ethics |
| Extraordinary session | As needed | Escalations, coach changes, governance disputes |

---

## 6. Coach Committee vs. individual coach authority

The committee coordinates; it does not override. Each coach retains autonomy over their coaching decisions within their assigned teams, following the framework and the Code of Ethics. The committee may set standards, but it cannot direct a coach to issue a specific competency assessment or coaching recommendation.

This boundary is consistent with the principle in `docs/coach-code-of-ethics.md` that coaching evidence must be distinguished from organizational pressure and that engineer dignity and professional autonomy must be preserved.

---

## 7. SECAV-O ontology

The Coach Committee concept requires the following additions to the governance extension ontology (`ontology/secav-o-coaching-governance-extension.ttl`). These are **proposed** and have not yet been added to the TTL.

### Proposed new classes

| Class | Description |
|---|---|
| `secavo:CoachCommittee` | The coordinating body of coaches in a multi-coach organization |
| `secavo:LeadCoach` | Subclass of `secav:Coach`; the designated committee coordinator |

### Proposed new object properties

| Property | Domain → Range | Description |
|---|---|---|
| `secavo:hasLeadCoach` | `secavo:CoachCommittee` → `secavo:LeadCoach` | Links the committee to its designated lead |
| `secavo:hasCommitteeMember` | `secavo:CoachCommittee` → `secav:Coach` | Links the committee to each member coach |
| `secavo:assignsCoachToTeam` | `secavo:CoachCommittee` → `secav:Coach` | Records which coach is assigned to which team context. *Note: the range captures the Coach individual; the team context is captured through the assignment matrix in the charter. A richer model would introduce a dedicated assignment class.* |
| `secavo:generatesOrganizationalPlan` | `secavo:CoachCommittee` → `secavo:AnnualCoachingPlan` | Links the committee to the organization-level plan it produces |

### Existing terms reused

| Term | Reuse in committee context |
|---|---|
| `secav:Coach` | Base class for all committee members |
| `secavo:AnnualCoachingPlan` | The organizational plan produced by the committee |
| `secavo:hasRisk` | Links the organizational plan to cross-team risks |
| `secavo:alignsWithInstitutionalObjective` | Org-wide coaching objectives aligned to institutional goals |
| `secav:CompetencyAssessment` | Committee oversees cross-team consistency |
| `secavo:SprintRetrospective` | Committee reviews outputs from all team retrospectives |

> **Author note:** The proposed classes and properties above should be added to `ontology/secav-o-coaching-governance-extension.ttl` and validated with SHACL constraints once the namespace-merge decision is resolved.