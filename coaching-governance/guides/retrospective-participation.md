# Coach Participation in the Retrospective

## Purpose

The sprint retrospective (`secavo:SprintRetrospective`) is the space where the team analyzes quality data, reviews risks, and agrees on improvement actions. The coach's role in this space depends on whether the team has a retrospective facilitator — such as a Scrum Master or an equivalent role.

---

## 1. Two participation modes

### 1.1 Without an external facilitator: the coach facilitates the retrospective

When the team does not have a Scrum Master or other role to facilitate the retrospective, the coach may facilitate the session. In this mode:

- They lead the agenda, distribute participation, and manage time.
- They ensure that defect and quality data (`secavo:DefectObservation`, `secavo:Metric`) are presented and analyzed — not just listed.
- They guide the team to derive decisions (`secavo:ImprovementAction`) from the data, not from opinions.
- They record the session's outcome in the retrospective template (`templates/sprint-retrospective.md`) as `secavo:SprintRetrospective`.

Even when facilitating, the coach takes observation notes about the team's process: who participates, how data is debated, what agreements are reached. These notes feed subsequent feedback.

### 1.2 With an external facilitator: the coach is an observer

When the team has a Scrum Master or other retrospective facilitator, the coach attends as a silent observer — consistent with their role in peer reviews (`coaching-governance/guides/peer-review-sessions.md`) and formal inspections (`coaching-governance/guides/formal-inspections.md`).

In this mode:

- They do not facilitate, do not direct the agenda, do not intervene verbally during the session.
- They take notes on the process and content.
- They observe specifically that defect and quality data are analyzed and that the team makes concrete decisions based on them.
- They give feedback after the session.

> The reason for this restriction is the same as in peer reviews: if the coach intervenes, the facilitator loses authority and the team stops directing itself.

---

## 2. What the coach observes (in both modes)

Regardless of the mode, the coach pays attention to:

### 2.1 Quality and defect data analysis

The coach verifies that the retrospective includes:

- **Sprint defect metric review:** volume, escape rate, phase distribution (`secavo:DefectObservation`, `secavo:phaseInjected`, `secavo:phaseDetected`).
- **Review finding analysis:** results from peer reviews and formal inspections of the sprint (`secav:ReviewFinding`).
- **Risk register review:** status of active risks and closure of mitigated ones (`secavo:Risk`).
- **Follow-up on previous sprint actions:** were the agreed `secavo:ImprovementAction` items completed?

**Alert signal:** if the retrospective focuses exclusively on process and team dynamics but omits quality data, the coach records it as an observation and addresses it in subsequent feedback.

### 2.2 Data-driven decision-making

The coach observes that the team does not limit itself to listing problems, but:

- Identifies root causes of recurring defects or findings.
- Agrees on concrete `secavo:ImprovementAction` items with an owner and deadline.
- Prioritizes actions by impact, not by perceived urgency.
- Formally records decisions in the `secavo:SprintRetrospective`.

---

## 3. Feedback after the retrospective

As with peer reviews and inspections, the coach gives feedback outside the session. The form depends on the pattern and the recipient:

### 3.1 Feedback to the team (group)

When the observed pattern affects the team as a whole — for example, the retrospective did not analyze quality data, or decisions made did not derive from evidence — the coach raises it as a topic in the next collective session or at the start of the next sprint.

### 3.2 Individual feedback

When the observation is specific to a participant — the Team Leader who directed the agenda without leaving space for quality data, or a member who systematically blocked decisions — the coach addresses it in an individual session, in private.

### 3.3 Feedback to the organization

If the pattern observed in successive retrospectives indicates an organizational problem — for example, management does not act on agreed `secavo:ImprovementAction` items, or there is pressure not to record defects — the coach documents the observation and escalates it following the formal mechanism (`templates/quality-planning-dissent-and-escalation.md`), or brings it to the Coaches Committee when applicable (`coaching-governance/docs/coach-committee.md`).

---

## 4. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| Retrospective as artifact | `secavo:SprintRetrospective` |
| Defect data analyzed | `secavo:DefectObservation`, `secavo:phaseInjected`, `secavo:phaseDetected` |
| Review findings discussed | `secav:ReviewFinding` |
| Sprint metrics reviewed | `secavo:Metric` |
| Risks reviewed | `secavo:Risk` |
| Agreed improvement decisions | `secavo:ImprovementAction` |
| Coach observation notes | `secav:WorkProductEvidence` |
| Subsequent feedback to team or individual | `secav:CoachingRecommendation` |
| Intervention if there is a systemic pattern | `secav:CoachingIntervention` |
| Escalation to organization | `secavo:QualityPlanningConcern` documented in `secavo:SprintRetrospective` |

---

## 5. Related documents

| Document | Relationship |
|---|---|
| `templates/sprint-retrospective.md` | Template where `secavo:SprintRetrospective` is recorded |
| `coaching-governance/guides/defect-tracking.md` | Defect data that must be reviewed in the retrospective |
| `coaching-governance/guides/peer-review-sessions.md` | Same silent observer protocol with subsequent feedback |
| `coaching-governance/guides/formal-inspections.md` | Inspection findings reviewed in retrospective |
| `coaching-governance/guides/risk-management.md` | Risk review protocol in retrospective |
| `coaching-governance/docs/coaching-cycle.md` | Context of the complete cycle in which the retrospective is embedded |
| `coaching-governance/docs/coach-committee.md` | Escalation of organizational patterns to the Coaches Committee |
| `templates/quality-planning-dissent-and-escalation.md` | Formal escalation mechanism to the organization |