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

### 17. Planning gate obligation for requirements review
Before endorsing a sprint or iteration plan that includes implementation work, the coach must verify that at least one `secav:RequirementsReview` (peer review, walkthrough, or formal inspection of requirements) is explicitly scheduled in the work plan and will complete before implementation begins on those requirements.

This is a distinct duty from the witness obligation (Principle 16). The coach's responsibility here is at planning time — not only at session time.

**Obligations:**

1. **Review the plan, not only the sessions.** The coach must check that the sprint plan includes a `secav:RequirementsReview` activity for any requirements being implemented in that sprint.
2. **Withhold endorsement when the gate is missing.** If the plan proceeds to implementation without a scheduled requirements review, the coach must document a quality planning concern (`secavo:QualityPlanningConcern`) and, if not resolved, invoke the formal dissent and escalation protocol.
3. **No retroactive satisfaction.** A requirements review conducted after implementation has already started does not fulfill the planning gate — it may still produce valuable findings, but the implementation risk materializes from day one of unreviewed requirements.
4. **This is an ethical obligation, not only a process step.** Starting implementation on unreviewed requirements is the highest-risk lifecycle antipattern (`secav:MissingRequirementsReview`). Endorsing a plan that omits this gate makes the coach complicit in accepting that risk without disclosure.

## Ethical escalation

A coach should document and escalate situations involving material conflicts of interest, misuse of confidential evidence, pressure to manipulate metrics, discriminatory treatment, unsafe engineering direction, or requests that contradict professional or organizational obligations.
