# SECAV-O Code of Ethics for Coaches

## Purpose

SECAV-O coaching is intended to develop engineering capability through evidence, feedback, reflection, and improvement. The coach holds a position of influence and must use that influence responsibly.

## Ethical principles

> **Structure note.** Principles 1–15 are foundational value statements — each is expressed as a single authoritative paragraph. Principles 16–23 are procedural rules with specific observable obligations; each follows the three-part structure: introductory statement → **Obligations:** → numbered obligation list. Both levels carry equal ethical weight; the procedural elaboration in Principles 16–23 exists because those principles involve judgment calls that benefit from explicit, checkable obligations.

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

### 20. Engineer autonomy and non-coercion

The coach facilitates, observes, and recommends. The coach does not argue, pressure, or compel. Once a finding has been communicated clearly and with evidence, the coach's role in that interaction is complete. The engineer holds the right to accept or decline any coaching recommendation.

**Obligations:**

1. **No debate beyond the finding.** Once a finding has been communicated and acknowledged, the coach must not extend the discussion into argument, repeated insistence, or pressure. Presenting a finding once — clearly, with evidence, and respectfully — fulfills the coach's obligation. The finding is documented regardless of the engineer's response.
2. **No compelled changes.** The coach must not oblige, pressure, or coerce a team member into making changes the engineer does not wish to make. Recommendations are offered; whether to act on them is the engineer's decision.
3. **Record the decline, not the argument.** When a team member declines a coaching recommendation, the coach records the refusal in the coaching log — noting the recommendation made, the engineer's decision to decline, and the date. The record is objective and neutral. No further debate or pressure on that specific recommendation is initiated by the coach.
4. **Escalation through proper channels only.** If the declined recommendation concerns a material quality or process risk, the coach may raise it as a `secavo:QualityPlanningConcern` through the formal escalation protocol — not by reinitiating the discussion with the engineer or applying indirect pressure.
5. **Respect for professional autonomy.** Engineers are professionals who bear responsibility for their own technical decisions. The coach surfaces findings and risk — but does not override the engineer's judgment. Treating an engineer's decision to decline as an obstacle to be overcome rather than a right to be respected violates this principle and Principle 1.

### 21. Technical training — at the engineer's request and within coach competence

The coach may participate in the technical training of a team member, but only when explicitly requested by that member and only within the limits of the coach's demonstrated knowledge. Technical instruction is not imposed — it is offered in response to an explicit request.

**Obligations:**

1. **Training is engineer-initiated.** The coach must not propose, schedule, or initiate technical training sessions without an explicit request from the engineer. Training offered without request risks creating dependency or imposing an agenda, and crosses the boundary between coaching and instruction.
2. **Competence boundary.** The coach may only deliver technical training on topics where they possess the knowledge to do so responsibly — accurately, completely, and without creating misconceptions or harmful gaps. This is a specific application of the scope obligation in Principle 7.
3. **When competence is insufficient.** If an engineer requests technical training on a topic outside the coach's knowledge, the coach must: (a) acknowledge the gap honestly to the engineer without deflection; (b) record the training request and the competency gap in the coaching log; and (c) include it in the management report so that appropriate resources — an internal expert, external training, or documentation — can be identified and provided.
4. **No transferred accountability.** When the coach provides technical training at the engineer's request, the coach acts as a resource — not as the accountable party for the engineer's subsequent technical decisions. The engineer's professional accountability for their own work is not transferred to the coach by the training interaction.
5. **Document every training session.** Technical training sessions provided by the coach must be recorded in the coaching log: topic covered, date, duration, name of the engineer who requested it, and the coach's honest self-assessment of their competence level on the topic.

### 22. Design review authority and process compliance

The coach has the authority to review design artifacts produced during any lifecycle phase and to assess whether they comply with the processes, standards, and criteria that the engineering team has formally adopted. This review authority is grounded in the documented process — not in the coach's personal preferences or general best-practice knowledge alone.

**Obligations:**

1. **Process-grounded review only.** The coach's authority to raise a compliance finding against a design artifact extends only to deviations from processes, standards, and acceptance criteria that are formally documented and adopted by the team. The coach may not impose requirements that are absent from those documents.
2. **Framework recommendations as process input.** The organization's engineering processes may reference, adopt, or incorporate recommendations from this framework (SECAV-O). When they do, those recommendations acquire the force of process requirements, and the coach may raise deviations from them as `secav:ProcessComplianceFinding` — a finding backed by a documented obligation.
3. **Distinguish compliance findings from coaching recommendations.** The coach must clearly mark the difference between: (a) a **process compliance finding** — the design deviates from a documented, adopted process requirement — and (b) a **coaching recommendation** — the design could be improved in ways not yet formalized in the process. Both are legitimate, but they carry different authority and impose different obligations on the team.
4. **No process-less requirements.** The coach may not compel a design change on the basis of personal technical preference, independent best-practice knowledge, or framework guidance that has not been adopted into the team's process. Such observations are recorded as recommendations, not findings, and the engineer's decision to accept or decline them is protected by Principle 20.
5. **Contribute to process evolution.** When repeated coaching observations reveal that the team's processes omit important quality requirements, the coach may formally propose process improvements through the appropriate channel. This is how framework recommendations gain normative force — through adoption into the process — not by being enforced unilaterally as if already required.

### 23. Design consultation — at the engineer's request and within coach qualifications

When a team member has questions or doubts about design decisions, the coach may provide technical recommendations in response — provided the coach's qualifications and knowledge cover that specific design domain. This is distinct from structured training (Principle 21): it is ad-hoc design consultation in response to an explicit technical question. The coach's primary obligation in this context is to know and honestly declare the boundary of their consulting capacity.

**Obligations:**

1. **Consultation is engineer-initiated.** The coach does not volunteer design opinions unsolicited. When the engineer asks a design question, the coach may respond. When no question is asked, the coach observes and, if warranted, raises a `secav:CoachingRecommendation` through the finding record — not through spontaneous design advice during the session.
2. **Qualification self-assessment before responding.** Before answering a design question, the coach must honestly assess whether their knowledge of that specific design domain is sufficient to give responsible guidance. General engineering experience is not a qualification for every domain — the coach must distinguish between areas where they can advise reliably and areas where their knowledge is insufficient or outdated.
3. **Respond only within demonstrated competence.** The coach may offer design recommendations only on topics where they possess the knowledge to do so accurately and without creating misconceptions or harmful design choices. This is a specific application of Principle 7.
4. **Declare limits immediately and transparently.** When an engineer asks a design question that falls outside the coach's competence, the coach must say so immediately and without deflection. Offering a guess, an approximation, or a partial answer framed as authoritative guidance in a domain outside the coach's competence is a violation of this principle. The declaration of a knowledge limit is recorded in the coaching log.
5. **Document the consulting scope.** The coach must maintain and periodically review a declared consulting scope: the design domains, technologies, and architectural areas in which they are qualified to advise. This scope is made available to the team and to management. When a question falls outside that scope, the coach records it as a gap and, where relevant, includes it in the management report so that an appropriate expert can be identified.
6. **No transferred accountability for design decisions.** When the coach provides design consultation, the engineer retains full professional accountability for the design decisions they ultimately make. The coach's input is advisory; the engineer's judgment is final. This applies even when the engineer adopts the coach's recommendation directly.

## Ethical escalation

A coach should document and escalate situations involving material conflicts of interest, misuse of confidential evidence, pressure to manipulate metrics, discriminatory treatment, unsafe engineering direction, or requests that contradict professional or organizational obligations.
