# Peer Reviews: Coach Observation Protocol

## Purpose

This guide describes the coach's presence protocol during peer reviews (`secav:CodeReview`, `secav:DesignReview`). The coach attends but is not an active participant — their role is to observe, take notes, and collect evidence. The review is conducted by the engineers.

---

## 1. Coach's role: silent observer

**The coach is present but does not participate.**

This means:

- They do not offer their technical opinion during the session.
- They do not approve or reject findings.
- They do not actively mediate disagreements.
- They do not correct engineers aloud during the meeting.

The coach takes notes. Their observations become `secav:ReviewFinding` and `secav:WorkProductEvidence` that inform the subsequent `secav:CompetencyAssessment`, and may derive into a `secav:CoachingIntervention` in the individual session, not in the review itself.

> The reason for this restriction is structural: if the coach intervenes, engineers stop resolving and wait for their judgment. The review ceases to be a peer review.

---

## 2. Core principle: review the product, not the person

From the start of the session, engineers must focus the review on the artifact — the code, the design, the document — not on the author.

Indicators that the focus is on the product:

- Comments are directed at the artifact: *"This block does not handle the null case,"* not *"you never handle null cases."*
- Questions are directed at the code: *"What happens here if the value is negative?"*
- The author listens without becoming defensive, because the object of evaluation is the artifact.
- Technical disagreement is treated as an open question about the product, not as a judgment about the author's competence.

The coach notes when comments drift toward judgments about the person. That observation feeds a subsequent conversation with whoever is appropriate — outside the session.

---

## 3. Focus discipline: coach observation when the team drifts

If the coach notices that engineers are losing focus — debating topics unrelated to the artifact, drifting toward designing new features, discussing unrelated processes, or prolonging a point without moving forward — the coach records it as an observation.

**The coach does not intervene verbally.** They may use a signal previously agreed with the team (for example, a visible card, an established gesture) to indicate that time on the point is being consumed, if the team requested this at the start. Beyond that, they do not interrupt.

The pattern of systematic drifts is a coaching signal: it may indicate that the review criteria are not clear, that the session is poorly scoped, or that the team needs practice in review discipline. The coach brings this to the next individual session or retrospective.

---

## 4. Unresolved disagreements: pending point and escalation to the Project Lead

When engineers cannot reach agreement on a review point and consider it sufficiently debated, the procedure is:

1. **Mark the point as pending** — do not continue debating. The point is recorded in the `secav:ReviewRecord` as an unresolved finding.
2. **Continue with the rest of the review** — do not block the entire session over a single disputed point.
3. **At the end of the session,** the team notifies the **Project Lead** about the pending points so they can resolve or escalate them as appropriate.

The coach notes pending points during the session. They do not decide or cast a tie-breaking vote — that is the Project Lead's responsibility.

### Criterion for declaring a point "sufficiently debated"

A point is sufficiently debated when:
- Both positions have been expressed with their technical arguments.
- No new evidence or argument has emerged in the last rounds of exchange.
- The debate has exceeded a time proportional to the importance of the point (guideline: more than 5–10 minutes on a point without progress is a signal for escalation).

---

## 5. Coach notes: what to record

During the session the coach records:

| What to observe | Why it matters |
|---|---|
| Who participates and who does not | Participation distribution — signal of mastery or inhibition |
| How comments are framed (product vs. person) | Indicator of review culture |
| Points where debate extends without resolution | Candidates for escalation; possible ambiguity of criteria |
| Focus drifts | Signal that review criteria are not sufficiently clear |
| Agreed technical decisions | Evidence of collective reasoning |
| Points marked as pending | To be transferred to the Project Lead |
| Significant technical findings | `secav:ReviewFinding` informing `secav:CompetencyAssessment` |

The coach's notes are internal to the coaching process. They are not shared with management as individual performance evaluations.

---

## 6. After the session: feedback and use of observations

Immediately after the session or at an agreed nearby moment, the coach gives feedback based on their notes. The form depends on the observed pattern:

- **Group feedback** — when the pattern affects the entire team (for example, the review systematically drifted toward judgments about the person, or focus drifts were recurrent). Given in a collective team space.
- **Individual feedback** — when the observation is specific to a participant (for example, an engineer who had not prepared the material, or whose tone was consistently dismissive). Given in private.

In both cases the observations belong to the coach — not to the author, inspectors, or management. They derive from observed facts, not from judgments about the person.

The coach's observations are also used in:

1. **Sprint retrospective** — if the pattern of drifts or disagreements is systematic, the coach introduces it as an improvement topic (`secavo:ImprovementAction`).
2. **Competency assessment** — technical and process findings inform each engineer's `secav:CompetencyAssessment` in `secav:ReviewCompetency`.

---

## 7. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| Peer review as activity | `secav:CodeReview` or `secav:DesignReview` (subclasses of `secav:ReviewActivity`) |
| Session record | `secav:ReviewRecord` (subclass of `secav:Artifact` and `secav:Evidence`) |
| Documented findings | `secav:ReviewFinding` (subclass of `secav:Evidence`) |
| Unresolved point recorded | `secav:ReviewFinding` with "pending" status |
| Coach observation notes | `secav:WorkProductEvidence` |
| Subsequent competency assessment | `secav:CompetencyAssessment` on `secav:ReviewCompetency` |
| Subsequent feedback to the engineer | `secav:CoachingRecommendation` |
| Intervention if there is a systemic pattern | `secav:CoachingIntervention`, `secavo:ImprovementAction` |

---

## 8. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/code-review-best-practices.md` | Review practices for author and reviewer; complements this protocol |
| `coaching-governance/guides/peer-review-antipatterns.md` | Frequent operational and cultural antipatterns — coaching signals derived from reviews |
| `coaching-governance/guides/formal-inspections.md` | More rigorous process for critical modules; the coach has a moderator role (not silent observer) |
| `coaching-governance/guides/coach-team-behaviors.md` | Team leader behaviors the coach observes, including in review sessions |
| `templates/sprint-retrospective.md` | Space to introduce review patterns as an improvement topic |
| `templates/engineer-coaching-assessment.md` | Template where derived competency observations are recorded |
| `templates/engineer-development-record.md` | Longitudinal record accumulating review evidence by cycle |