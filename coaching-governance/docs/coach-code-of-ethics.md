# SECAV-O Code of Ethics for Coaches

## Purpose

SECAV-O coaching is intended to develop engineering capability through evidence, feedback, reflection, and improvement. The coach holds a position of influence and must use that influence responsibly.

## Ethical principles

### 1. Respect and professional dignity
Treat engineers with respect. Coaching must support learning and professional growth and must not use humiliation, intimidation, ridicule, or coercion.

### 2. Evidence before judgment
Distinguish observable evidence from interpretation. Competency assessments and coaching recommendations should be traceable to documented activities, artifacts, acceptance criteria, measurements, and review findings.

### 3. Confidentiality and appropriate use of information
Protect confidential engineering, organizational, personal, and assessment information. Share coaching evidence only with authorized parties and for legitimate purposes.

### 4. Fairness and consistency
Apply defined criteria consistently. Avoid favoritism and discrimination. Account for context, task complexity, role expectations, and evidence quality before drawing conclusions.

### 5. Avoid harmful metric incentives
Do not treat a single metric as a complete representation of engineer quality. Avoid incentives that encourage gaming, concealment of defects, superficial testing, excessive review findings, or other behavior that undermines engineering quality.

### 6. Human accountability in AI-assisted work
AI assistance does not transfer professional accountability away from the engineer or reviewer. Coaches should reinforce appropriate human validation, critical thinking, and independent engineering judgment.

### 7. Competence and scope
Coach within areas of demonstrated competence. Seek appropriate expertise when a matter falls outside the coach's technical, organizational, legal, security, or professional scope.

### 8. Conflicts of interest
Disclose actual or potential conflicts of interest that could affect coaching, assessment, or recommendations. Where necessary, recuse or seek independent review.

### 9. Developmental purpose
Use coaching evidence primarily to support development, learning, quality improvement, and professional growth. If evidence may also be used for formal personnel decisions, that use should be transparent and governed by organizational policy.

### 10. Transparency
Engineers should understand the objectives, metrics, evidence sources, acceptance criteria, assessment approach, and intended use of coaching information.

### 11. Corrective action and appeal
Where practical, engineers should have an opportunity to provide context, correct factual inaccuracies, and discuss assessment results before conclusions become final.

### 12. Continuous improvement of coaching
Coaches should review their own interventions, seek feedback, learn from retrospectives, and adjust methods when evidence shows that an intervention is ineffective or creates unintended consequences.

### 13. Action and results orientation
Coaching is not purely reflective. Each session is designed to conclude with a concrete action plan containing specific, measurable objectives and defined deadlines. Reflection without commitment to action is incomplete; the coach is responsible for ensuring that insight translates into traceable next steps.

### 14. Self-belief and potential
Coaching operates under the firm premise that the engineer possesses the internal resources necessary — or the capacity to develop them — to overcome their obstacles and achieve success. The coach's role is to surface and strengthen that latent capability, not to supply answers or create dependency.

### 15. Absence of judgment and empathy
The coach maintains a neutral, actively listening posture. Coaching sessions take place in an environment of strict confidentiality, where engineers can speak openly without fear of evaluation, exposure, or retaliation. The coach suspends personal judgment, acknowledges the engineer's experience, and responds with empathy — attending to both what is said and what is left unsaid.

### 16. Witness obligation for review sessions
The coach has an obligation to be present — as a silent, non-intervening observer — during peer review, walkthrough, and inspection sessions in order to issue the process sign-off (`secav:CoachReviewSignOff`) that certifies the session was conducted acceptably.

**When the coach cannot attend:**

1. **Notify in advance.** The coach must inform the team before the session, not retroactively.
2. **No retroactive sign-off.** The coach must never issue a sign-off for a session they did not observe. Signing off on an unwitnessed session falsifies the process record and violates this code.
3. **Designate a trained observer.** The coach may designate a qualified team member (e.g., a Technical Lead or Quality Assistant trained by the coach) as an interim observer. The observer documents the session outcome and reports to the coach immediately after.
4. **Findings remain provisional.** Findings from an unwitnessed session are provisional and cannot be used as formal competency evidence until the coach reviews the observer's report and decides whether to endorse the session — documenting the reason for remote endorsement.
5. **Reschedule when necessary.** If no qualified observer is available and the session concerns a critical artifact, the coach must request rescheduling rather than allow the session to proceed without any qualified witness.

Repeated failure to attend review sessions without a valid reason is an ethical concern that should be self-disclosed and addressed through coaching practice improvement (see Principle 12).

### 17. Work plan gate for requirements review
The coach has an active obligation — not merely a recommendation — to confirm that at least one `secav:RequirementsReview` session (peer review, walkthrough, or formal inspection of requirements artifacts) is included in the sprint or feature work plan **before authorizing implementation to begin**. This obligation exists because vague, ambiguous, unclear, and incomplete requirements are invisible to automated tools and carry the highest downstream correction cost in the lifecycle.

**Obligations:**

1. **Sprint planning gate.** During sprint planning (or equivalent planning ceremony), the coach must verify that the work plan contains a scheduled RequirementsReview for every feature or story entering implementation in that sprint. If none is present, the coach must either request its inclusion or document a written exception with justification.
2. **No silent approval.** Approving a sprint plan or signing a kick-off document implicitly authorizes the work plan it describes. A plan without RequirementsReview that the coach signs without noting the omission is a tacit endorsement of the `secav:MissingRequirementsReview` antipattern.
3. **Exception justification.** If a RequirementsReview is genuinely not feasible (e.g., requirements are inherited from a prior sprint and already reviewed), the coach must document the reason explicitly. Silence does not constitute an exception.
4. **Planning endorsement vs. session sign-off.** The planning-gate endorsement confirms the session is planned — it is distinct from the post-session `secav:CoachReviewSignOff` (Principle 16), which certifies the session was conducted acceptably.

Repeated failure to enforce the requirements review planning gate — allowing implementation to begin on unreviewed requirements — is a professional ethics concern that should be self-disclosed and addressed through coaching practice improvement (see Principle 12).

### 18. Observer obligation for all lifecycle phases

The coach has an obligation — not only a recommendation — to be present as a **silent, non-intervening observer** during any scheduled lifecycle phase activity: planning, requirements, high-level design, design, test design, implementation, test execution, walkthrough execution, formal inspection, and release. Presence is the only basis on which the coach can issue observations, sign-offs, and competency evidence for that activity.

**Scope.** This principle generalizes Principle 16 (witness obligation for review sessions) to all lifecycle phases, not only review activities. The quality gate principle is the same: the coach cannot certify what they did not witness.

**What "observer" means.** The coach does not direct, interrupt, or evaluate engineers in real time during the session. They take notes, record observations (`secav:CoachObservation`), and defer feedback to the coaching session that follows. The observer role is silent — attending does not mean intervening.

**Obligations:**

1. **Attend whenever possible.** The ideal is that the coach is present at every scheduled lifecycle phase activity. Repeated absence is a practice quality concern, not a scheduling inconvenience.
2. **Document every absence.** When the coach cannot attend, they must record a `secav:CoachAbsenceRecord` for that activity before the session, not retroactively. The record must state the reason and the consequence.
3. **No implicit approval from absence.** The coach's absence from any activity — review or otherwise — does not constitute approval, sign-off, or certification of what occurred. Absence produces a gap in the observation record, not a neutral endorsement.
4. **For review activities: no sign-off without presence.** Absence from a review activity (peer review, walkthrough, inspection, results review) means no `secav:CoachReviewSignOff` can be issued for that session (see Principle 16 for the full protocol when a designated observer is needed).
5. **For non-review activities: no observation record.** Absence from a non-review activity (planning, design, implementation, test execution) means no `secav:CoachObservation` can be recorded for that session. Competency evidence from that session is unavailable until a follow-up observation opportunity arises.
6. **Designate a trained observer when absent.** When a session concerns a critical artifact or a high-risk phase and the coach cannot attend, they must designate a trained team member to observe and report. The designation and the observer's report must be documented. For review activities, the Principle 16 protocol applies.

Repeated undocumented absences across lifecycle phases signal a systemic coaching availability problem that should be raised with the organizational sponsor of the coaching engagement.

### 19. Prohibition on dismissal recommendations

The coach's role is to develop engineering capability — not to exercise authority over personnel decisions. The coach must never recommend, suggest, or imply that a team member should be dismissed, terminated, or removed from the team.

**Scope.** This prohibition applies in all forms of communication: formal reports, informal conversations, verbal briefings, written assessments, meeting minutes, and any other channel through which the coach interacts with management.

**Obligations:**

1. **No dismissal recommendations — explicit or implicit.** The coach must not recommend that a team member be dismissed or removed, directly or indirectly. Framing findings in ways that predictably lead to a dismissal conclusion — without stating it — is also a violation of this principle. Evidence must be presented neutrally so that the authority draws their own conclusions.
2. **Findings only, not verdicts.** When reporting to management, the coach reports observable findings: behaviors observed, competency evidence collected, coaching interventions applied, and measurable outcomes. The coach does not render personnel verdicts, performance indictments, or suitability conclusions.
3. **Decision authority rests exclusively with management.** The responsibility for personnel decisions — including whether to retain, reassign, or remove a team member from the project or organization — rests exclusively with the manager, director, or whoever holds that organizational authority. The coach has no role in that decision, even when asked to provide an opinion.
4. **Declining an inappropriate request.** If a manager or director asks the coach to recommend dismissal or to frame a report so as to justify dismissal, the coach must decline and document the request. The coach may consult the Coach Committee (if one exists) or escalate through the formal dissent protocol.
5. **Engineer dignity under negative findings.** Even when findings are significantly negative, they must be reported with professional dignity, with acknowledgment of the engineer's capacity to improve (see Principle 14), and within the confidentiality constraints of Principle 3. Negative coaching findings are developmental input, not grounds for organizational action — that determination belongs to management alone.

This principle does not prevent the coach from reporting accurately or completely. Accurate, complete, evidence-based reporting is required by Principle 2. What is prohibited is the coach crossing the role boundary from observer and developer into personnel decision-maker.

## Ethical escalation

A coach should document and escalate situations involving material conflicts of interest, misuse of confidential evidence, pressure to manipulate metrics, discriminatory treatment, unsafe engineering direction, or requests that contradict professional or organizational obligations.
