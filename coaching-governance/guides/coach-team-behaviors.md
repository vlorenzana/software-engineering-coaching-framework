# Team Leader Behaviors: Coach Observation Guide

## Purpose

This guide describes concrete, verifiable behaviors that the coach must observe in the **team leader** during their daily work. Each behavior is an observable indicator that the coach can collect as `secav:Evidence` to inform a `secav:CompetencyAssessment` and, when appropriate, plan a `secav:CoachingIntervention`.

Unlike the Code of Ethics (`coaching-governance/docs/coach-code-of-ethics.md`), which establishes the coach's principles, this guide is an observation tool: it tells the coach what positive signals to look for and what alert signals should lead to an intervention.

> The coach does not evaluate the leader as a hierarchical superior — they evaluate behaviors as evidence of facilitation competencies, team leadership, and decision-making.

---

## 1. Facilitation and team ownership

An effective team leader makes the team find the answers, not provide them themselves. The coach observes the balance of participation and the distribution of solution authorship.

**Positive indicators (the coach records them as competency evidence):**

- The leader asks questions instead of giving answers when the team has the capacity to find them. (*"What options do you see for this?"* instead of *"The solution is X."*)
- Speaking time is distributed — no individual systematically dominates the conversation.
- When an idea or solution emerges from the team, the leader explicitly attributes it to whoever proposed it.
- The leader invites quieter members to participate before closing a point.
- In planning or review sessions, the leader opens the space for the team to reach their own conclusions before sharing their own perspective.

**Alert signals (the coach considers an intervention):**

- The leader speaks more than 50% of the time in team meetings.
- Technical or process decisions are only made when the leader is present.
- Team members wait for the leader's approval before acting, even in tasks within their competence.
- Ideas are recurrently attributed to the leader, not to whoever originated them.

---

## 2. Decision-making: consensus and visible constraints

The coach observes whether the leader anchors decisions in the project's real constraints and whether they build agreement before imposing.

**Positive indicators:**

- Before proposing a vote, the leader exhausts the deliberation space to seek a collectively built agreement.
- Project constraints — deadlines, budget, technical requirements, policies — are explicit and visible during the discussion.
- When a decision is made, the leader briefly documents the reasoning and the constraint that justified it.
- The leader differentiates between collective decisions and decisions that are the individual engineer's responsibility within their area of competence.
- When the team reaches a reasonable alternative within the constraints, the leader accepts it even if it is not their preference.

**Alert signals:**

- Project constraints are known to the leader but not communicated to the team.
- Decisions are justified with the leader's authority, not with objective criteria.
- A vote is forced before all members have had the opportunity to express their position.
- The outcome of discussions systematically coincides with the leader's initial position, regardless of the debate.

---

## 3. Building plans the team believes in

The coach observes whether the leader verifies the team's genuine commitment to the plan — not just nominal agreement — and whether they handle disagreements constructively.

**Positive indicators:**

- After building a plan, the leader actively checks whether the team considers it achievable; they do not assume silence is agreement. (*"Do you see any reason why this plan wouldn't work?"*)
- When someone expresses a doubt or disagreement, the leader listens without interrupting and without dismissing it as obstruction.
- If there is a disagreement, the leader turns it into a team conversation — involves others in finding a resolution: *"Does anyone see an alternative that addresses X's concern?"*
- The leader distinguishes between "the team agreed" and "the team resigned" — and acts on the second.
- Disagreements that cannot be resolved internally and affect organizational commitments are formally documented and escalated to management, rather than suppressed (`templates/quality-planning-dissent-and-escalation.md`).

**Alert signals:**

- The plan is presented as closed before the team has had the opportunity to question it.
- Expressed doubts are recorded but change nothing — archived without real response.
- When someone disagrees, the leader resolves it unilaterally.
- Unresolved internal disagreements are not escalated — they are ignored or suppressed.
- The team executes the plan without being able to explain why it was built that way.

---

## 4. Participatory risk management

The coach observes whether the leader guides the team in identifying and mitigating risks or manages them alone.

**Positive indicators:**

- In each retrospective, the leader proposes reviewing the risk register as a structured point, not an occasional one.
- Risk identification sessions open with questions: *"What could prevent us from completing this objective?"*, *"What assumption are we making that might turn out to be incorrect?"*
- The risk register is built with the team; the leader acknowledges the specific contributions of each member.
- When a risk materializes, the leader guides the team to identify a corrective action without assigning blame to individuals.
- Preventive actions are proposed by the team before the leader suggests their own.

**Alert signals:**

- The risk register is developed solely by the leader and presented to the team as information, not as a collective construction.
- Risk sessions are omitted when time is tight.
- When a risk materializes, the discussion focuses on who failed, not on what can be learned.
- Preventive and corrective actions are assigned by the leader without consulting the team's capacity or availability.

---

## 5. Work distribution

The coach observes whether the leader assigns work according to the team's capabilities and whether they avoid concentrating tasks on the same individuals.

**Positive indicators:**

- Most of the sprint's technical work is distributed among engineers; the leader does not concentrate delivery tasks on themselves.
- Assignments consider the current competency level of each engineer and their development objectives.
- Challenging tasks are assigned to engineers whose development objective includes that area — not only to whoever already masters it.
- Critical work is distributed among several members; it is not systematically concentrated on the most senior engineer.
- When the leader takes on an operational task, they do so explicitly and temporarily, with a clear criterion for when they return it to the team.

**Alert signals:**

- The most visible or technically complex tasks systematically fall to the same engineer.
- Assignments ignore agreed development objectives and respond only to urgency.
- No team member can explain why they were assigned their task.

---

## 6. Respect and team culture

The coach observes the leader's tone and patterns of recognition and correction — especially in situations of tension or error.

**Positive indicators:**

- **Correct in private, praise in public.** Behavioral corrections happen in an individual space; achievement recognition is expressed in the collective space.
- The leader maintains the same tone of respect in written communications as in in-person conversations.
- Treats all team members with the same level of consideration, regardless of seniority or personal relationship.
- Acknowledges their own mistakes in front of the team when appropriate — models that making mistakes and correcting them is part of the process.
- Does not interrupt team members while they are explaining their reasoning.
- Distinguishes between feedback on the work and judgments about the person.

**Alert signals:**

- Corrections or criticism are delivered in front of other team members or in group channels.
- Recognition is scarce or generic; achievements are not attributed to specific individuals.
- The written tone is noticeably sharper than the tone in direct conversations.
- Certain members systematically receive more attention or opportunities than others without justification in development objectives.

---

## 7. Per-sprint observation verification checklist

The coach completes this list at the end of each sprint or observation cycle. Items marked "Not observed" or "Alert signal" are candidates for a `secav:CoachingIntervention` in the next individual session with the leader.

| Behavior observed in the leader | Yes | Partial | Alert signal | Not observed |
|---|---|---|---|---|
| The team proposed and built solutions without waiting for the leader's answers | | | | |
| Speaking time was distributed in meetings | | | | |
| Project constraints were visible and used as the basis for decisions | | | | |
| Consensus was sought before voting or deciding unilaterally | | | | |
| The leader verified the team believes in the plan — did not assume silence is agreement | | | | |
| Disagreements with the plan were heard and handled constructively | | | | |
| Unresolved internal disagreements were escalated when appropriate | | | | |
| The risk register was reviewed with the team in the retrospective | | | | |
| The team proposed preventive actions — the leader did not dictate them | | | | |
| Work assignments considered each engineer's development objectives | | | | |
| Corrections to individuals were given in private; achievements were recognized publicly | | | | |

---

## 8. SECAV-O Integration

| Observed behavior | SECAV-O term |
|---|---|
| Observation of leader meetings and activities | `secav:ReviewActivity`; `secav:EngineeringActivity` |
| Evidence of effective facilitation | `secav:WorkProductEvidence`, `secav:ReviewFinding` |
| Leadership competency assessment | `secav:CompetencyAssessment` on `secav:Engineer` (the leader) |
| Intervention when an alert signal is detected | `secav:CoachingIntervention` |
| Specific recommendation to the leader | `secav:CoachingRecommendation` |
| Improvement plan agreed with the leader | `secavo:ImprovementAction` (subclass of `secav:CoachingIntervention`) |
| Plan built with the team | `secavo:AnnualCoachingPlan`, `secavo:SprintPlan` |
| Plan adjustment for disagreement | `secavo:ImprovementAction`, `secavo:PlanningDecision` |
| Formal escalation of disagreement | `secavo:GovernanceDecision`; documented in `secavo:SprintRetrospective` |
| Risks identified with the team | `secavo:Risk` in `secavo:SprintRetrospective` |
| Preventive actions proposed by the team | `secavo:PreventiveAction` |
| Corrective actions when a risk materializes | `secavo:CorrectiveAction` |

---

## 9. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/docs/coach-code-of-ethics.md` | Ethical principles guiding the coach's observation and intervention |
| `coaching-governance/docs/coach-committee.md` | The Committee may review observation patterns across coaches for calibration |
| `coaching-governance/docs/project-planning-participation.md` | Formal coach participation in planning and quality escalation |
| `templates/quality-planning-dissent-and-escalation.md` | Template for documenting and escalating unresolved internal disagreements |
| `coaching-governance/guides/risk-management.md` | Detailed risk management protocol |
| `templates/sprint-retrospective.md` | Space where the coach records leader observations |
| `templates/engineer-coaching-assessment.md` | Competency assessment template for the observed leader |
| `templates/engineer-development-record.md` | Longitudinal record accumulating cycle observations and evidence |