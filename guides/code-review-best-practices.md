# Code Review Best Practices

## Purpose

This document provides evidence-based best practices for code review within the SECAV-O coaching framework. Code review maps to `secav:CodeReview` (a subclass of both `secav:ReviewActivity` and `secav:CodingActivity`) and produces `secav:ReviewFinding` evidence recorded in a `secav:ReviewRecord`. Both inform `secav:CompetencyAssessment` and may trigger `secav:CoachingIntervention`.

These practices apply to the reviewer, the author, and the coach observing both roles.

---

## 1. Scope and size

Small, focused reviews produce better outcomes than large ones.

- Target **200–400 lines of code per review session**. Defect-detection ability drops significantly beyond 400 lines.
- Keep **inspection rate under 500 lines per hour**; above this threshold defect density falls sharply.
- Limit **review sessions to 60 minutes**. Concentration degrades after sustained effort regardless of code quality.
- A review should represent one self-contained change — one part of a feature, not an entire feature.
- When a change is unavoidably large, seek reviewer agreement in advance and expect a longer cycle.

**Why this matters for coaching:** Session length and LOC volume are observable inputs to a `secav:ReviewActivity`. Patterns of oversized reviews or rushed inspection rates are coaching signals, not isolated incidents.

---

## 2. Preparing a change for review (author responsibilities)

The author shares responsibility for review quality.

- **Write a clear description.** Explain *what* changed and *why*, not just *how*.
- **Keep changes logically coherent.** Unrelated changes should be separate reviews.
- **Separate refactoring from functional changes.** Mixing them makes review harder and obscures intent.
- **Include tests in the same review.** Tests committed separately from the code they cover are a review gap.
- **Annotate before submitting.** Self-annotation helps reviewers navigate the intent and often surfaces defects before review begins.
- **New APIs require usage examples** in the same review to prevent unused or undocumented API check-ins.

---

## 3. What reviewers should examine

Review every human-written line. Skim, and defects escape into later phases.

### 3.1 Design
- Does the overall change make architectural sense?
- Does the change belong in this codebase, or should it be a library or shared component?
- Is the timing right for this addition?

### 3.2 Functionality
- Does the change accomplish what the author intended?
- Are edge cases, race conditions, and concurrent-access scenarios considered?
- For UI changes, request a demonstration or screenshot before approving.

### 3.3 Complexity
- Are individual lines, functions, and classes appropriately simple?
- Flag over-engineering: code that is more generic or abstract than the current problem requires.
- Solve present problems; do not design for speculative future requirements.
- Functions with more than three arguments may indicate excessive complexity.

### 3.4 Tests
- Will the tests actually fail when the code breaks?
- Are edge cases covered?
- Do assertions make sense and avoid false positives?
- Treat test code with the same quality standard as production code.
- Review the tests first — they describe the intended behavior and help reviewers understand the change.

### 3.5 Naming
- Names should fully communicate purpose without excessive length.
- Ambiguous names are a defect category, not a style preference.

### 3.6 Comments
- Comments should explain *why* code exists, not *what* it does.
- Check for outdated TODOs or comments that contradict the new change.
- If comments are needed to explain what the code does, the code may need to be clearer.

### 3.7 Style and consistency
- Apply the team's agreed style guide. Style-guide violations are not optional.
- Prefix non-mandatory polish suggestions with `Nit:` so the author can distinguish blocking from advisory feedback.
- Do not block a review over personal preference when the style guide does not address the point.
- Separate style-only changes from functional changes in separate reviews.

### 3.8 Security
- Are there injection, authentication, authorization, or data-exposure risks?
- Is PII or EUII handled correctly, especially in logging?
- Escalate specialized security concerns to a qualified reviewer rather than guessing.

### 3.9 Documentation
- If the change affects build, test, or release processes, update the corresponding documentation.
- Delete or deprecate documentation for removed functionality.

---

## 4. How to give feedback

Effective feedback is specific, grounded in evidence, and separates the code from the person.

- **Explain the why.** State the reason a change is needed, ideally with an example or a reference.
- **Ask questions rather than making demands** when you are uncertain or the issue is subtle.
- **Use "we" or "this line"** rather than "you" to depersonalize comments.
- **Distinguish blocking from advisory.** Prefix advisory suggestions with `Nit:`.
- **Acknowledge good work.** Recognizing quality is part of coaching and builds trust.
- Avoid long comment threads on the same point. If discussion stalls, move to a short conversation and document the outcome in the review record.

---

## 5. Approving a review

The approval standard is: *does this change definitely improve the overall code health of the system, even if it is not perfect?*

- Do not require perfection as a condition for approval. Forward progress matters.
- Do not approve changes that worsen overall code health, except in declared emergencies with documented rationale.
- If multiple approaches are equally valid, defer to the author's preference.
- Style and design decisions rest on engineering principles. Where the style guide does not govern, personal preference is not sufficient grounds to block.

---

## 6. Handling disagreement

- Seek consensus using documented guidelines first.
- If discussion stalls, escalate to a short in-person or synchronous conversation; document the outcome in the review record.
- Further escalation goes to the team lead or manager.
- Never leave a review stalled indefinitely. Stalled reviews are a process failure, not a normal state.

---

## 7. Checklists

Teams tend to repeat the same defect categories. A review checklist targeting team-specific recurring defects is more effective than a generic one. Maintain a checklist derived from the team's `secav:ReviewFinding` history.

Suggested minimum checklist items:

- [ ] Description explains what and why
- [ ] Tests included and cover edge cases
- [ ] No new security risks introduced
- [ ] No PII or sensitive data in logs
- [ ] Naming is clear and unambiguous
- [ ] No dead code or outdated comments introduced
- [ ] Documentation updated where relevant
- [ ] Style guide followed

---

## 8. Code review as coaching evidence

Within SECAV-O, `secav:ReviewFinding` instances are subclasses of `secav:Evidence` and link to `secav:Competency` via `secav:providesEvidenceOf`. The coach should:

- Track recurring `secav:ReviewFinding` categories per engineer as coaching signals pointing to a `secav:ReviewCompetency` gap.
- Track reviewer quality: does the reviewer produce `secav:ReviewFinding` evidence of substance, or only style-level findings?
- Avoid using review metrics (defect counts, approval rates) in isolation as performance measures. High defect counts found in review may reflect effective review, not weak engineering.
- Never use review participation metrics as instruments for performance ranking or punitive decisions.
- Document `secav:ReviewCompetency` growth using the longitudinal scale in `docs/competency-growth-scale.md`.

See `docs/metrics-model.md` §2 for the full set of review and inspection metrics.

---

## 9. AI-assisted code and review

When the artifact under review was produced or modified with AI assistance, additional considerations apply. See `guides/ai-assisted-code-review.md` for the full guidance, including layered pipeline design, risk-based triage, false-positive management, data privacy, and metrics.

Key ontology points:

- The `secav:CodeImplementation` activity that produced the artifact is linked to `secav:assistedByAI` (an ObjectProperty from `secav:EngineeringActivity` to `secav:AISystem`). Note in the `secav:ReviewRecord` that the artifact was produced by an AI-assisted activity, so the evidence chain remains traceable.
- A `secav:CodeReview` of AI-assisted code also qualifies as a `secav:HumanValidationActivity` (both are subclasses of `secav:ReviewActivity`); use `secav:requiresHumanValidation` to link the original AI-assisted activity to this validation step.
- Apply the same review standards as for human-written code. AI assistance is not a substitute for human review.

---

## Sources

- Google LLC. *Google Engineering Practices Documentation — Code Review*. [https://google.github.io/eng-practices/review/](https://google.github.io/eng-practices/review/)
- Microsoft. *Code with Engineering Playbook — Code Reviews: Reviewer Guidance*. [https://microsoft.github.io/code-with-engineering-playbook/code-reviews/process-guidance/reviewer-guidance/](https://microsoft.github.io/code-with-engineering-playbook/code-reviews/process-guidance/reviewer-guidance/)
- SmartBear Software. *Best Practices for Peer Code Review*. Based on Cisco Systems study data. [https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/)