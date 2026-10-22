# Root Cause Analysis — Defect (RCA)

<!-- Complete one instance of this template for every P1 (Critical) or P2 (Major) defect.
     For minor defects, record directly in defect-log.csv without a full RCA. -->

## Header

- **Incident code:** INC-`YYYY`-`XXXX`
- **Report date:** DD/MM/YYYY
- **Analysis lead:** [Name]
- **Responsible coach:** [Name]
- **Severity:** [ ] P1 — Critical  [ ] P2 — Major
- **Sprint / Cycle:** [Sprint ID]

---

## 1. Development environment metadata

| Field | Value |
|---|---|
| Repository / Microservice | e.g. `github.com/org/payment-gateway` |
| Affected branch | e.g. `main` / `release/v2.4.0` |
| Defective commit (SHA) | e.g. `a1b2c3d4e5f6...` |
| Rollback / fix commit | e.g. `f7e6d5c4b3a2...` |
| Impacted environment | [ ] Production  [ ] Staging  [ ] Beta |
| Associated pull request | PR #`NNN` |

**SECAV-O:** The defective commit is the `secav:SourceCodeArtifact` that originated the `secav:DefectRecord`. The associated PR is the `secav:FormalReviewRequest` that introduced it to the main repository.

---

## 2. Impact summary

- **Failure description:**
  > e.g. The `/v1/charge` endpoint returned 500 errors at scale, blocking payment processing.

- **Downtime:** ___ hours, ___ minutes
- **Affected users / customers:** e.g. 15% of active users on the web platform
- **Injection phase** (`secavo:phaseInjected`): [ ] Requirements  [ ] Design  [ ] Coding  [ ] Testing
- **Detection phase** (`secavo:phaseDetected`): [ ] Code review  [ ] Unit test  [ ] Integration  [ ] Production
- **Detection method** (`secavo:detectionMethod`): [ ] Formal inspection  [ ] Peer review  [ ] Automated test  [ ] Monitoring alert  [ ] User report

---

## 3. Software lifecycle timeline

Record key events from change approval to resolution. Use format `HH:MM (Day N)`.

| Time | Event | Owner |
|---|---|---|
| HH:MM (Day 1) | **PR approval** — PR #NNN approved in peer review without critical observations | Reviewer |
| HH:MM (Day 1) | **CI/CD pipeline** — automated build runs; unit tests pass | CI/CD |
| HH:MM (Day 1) | **Deployment** — defective commit deployed to Production | CI/CD |
| HH:MM (Day 1) | **Detection** — APM metrics (Datadog / New Relic) record anomalous exception spike | Monitor |
| HH:MM (Day 1) | **Temporary mitigation** — team executes rollback to previous stable commit | [Name] |
| HH:MM (Day N) | **Permanent fix** — definitive correction deployed | [Name] |

> Add or remove rows to match the actual incident timeline.

---

## 4. Root cause analysis — 5 Whys (engineering)

Answer each question concretely. If the chain ends before the fifth why, the root cause is identified at that point.

**Why did the system fail in production?**

> Answer: _

**Why did that failure condition occur?**

> Answer: _

**Why did the code not handle that case safely?**

> Answer: _

**Why did the automated tests in CI/CD not detect the vulnerability?**

> Answer: _

**Why was the pull request approved with this logic weakness? ← Root cause**

> Answer: _

**Root cause identified (one-sentence summary):**

> _

**Root cause category:**

| Category | Applies? | Associated SECAV-O antipattern |
|---|---|---|
| Review under cognitive fatigue | [ ] | `secav:OversizedReviewSession`, `secav:ReviewerEnergyCondition` |
| Incomplete tests (happy path only) | [ ] | `secav:HappyPathOnlyReview` |
| PR too large to review properly | [ ] | `secav:OversizedPullRequest` |
| Approval without real reading | [ ] | `secav:RubberStampApproval` |
| Late architectural discussion | [ ] | `secav:LateArchitecturalDiscussion` |
| Missing context in the PR | [ ] | `secav:MissingReviewContext` |
| Static analysis not configured | [ ] | `secav:ManualStyleReview`, missing `secav:AutomationGate` |
| Other cause | [ ] | — |

---

## 5. Corrective action plan (SMART)

Each action must be: Specific, Measurable, Assignable, Realistic, and Time-bound.

| ID | Required technical action | Owner | Deadline | Status |
|---|---|---|---|---|
| SOFT-01 | Implement defensive validation for the affected field/case and push the fix | [Name] | DD/MM/YYYY | [ ] Pending |
| SOFT-02 | Add integration tests that simulate corrupt or empty payloads for the affected case | [Name] | DD/MM/YYYY | [ ] Pending |
| SOFT-03 | Configure a linter / SonarQube / static-analyser rule to enforce verification of the affected data type | [Name] | DD/MM/YYYY | [ ] Pending |

**SECAV-O:** Each row is a `secavo:CorrectiveAction` linked to the `secav:DefectRecord` of this incident. Rows SOFT-02 and SOFT-03 may additionally become `secav:PreventiveAction` entries if adopted as team standards.

---

## 6. Systemic preventive actions

If the root cause reveals a process or culture gap that could recur, record here the actions to prevent it from happening again in other modules or teams.

| ID | Preventive action | Owner | Deadline | Status |
|---|---|---|---|---|
| PREV-01 | | [Name] | DD/MM/YYYY | [ ] Pending |
| PREV-02 | | [Name] | DD/MM/YYYY | [ ] Pending |

**SECAV-O:** Each row is a `secav:PreventiveAction` aimed at eliminating the defect class, not just the instance. Recorded in `secavo:SprintRetrospective` as a `secavo:ImprovementAction`.

---

## 7. Derived coaching intervention

The coach completes this section when closing the RCA. It is not shared with management as an individual performance evaluation.

- **Affected competency** (`secav:Competency`): [ ] ReviewCompetency  [ ] TestingCompetency  [ ] SecurityCompetency  [ ] DesignCompetency
- **Observed pattern:** _
- **Planned intervention** (`secav:CoachingIntervention`): _
- **Individual session scheduled:** DD/MM/YYYY

---

## 8. Closure and verification

- **RCA closure date:** DD/MM/YYYY
- **Fix verified in production:** [ ] Yes  [ ] No  — Date: DD/MM/YYYY
- **Corrective actions completed:** [ ] All  [ ] Partial — pending: ___
- **Preventive actions completed:** [ ] All  [ ] Partial — pending: ___
- **Defect recorded in** `templates/defect-log.csv`: [ ] Yes
- **RCA archived in engineer coaching record** (`templates/engineer-coaching-assessment.md`): [ ] Yes

---

## Related documents

| Document | Relationship |
|---|---|
| `templates/defect-log.csv` | Structured defect record; this RCA complements each P1/P2 severity row |
| `coaching-governance/guides/defect-tracking.md` | Coach protocol for classifying and closing defect tickets |
| `coaching-governance/guides/peer-review-antipatterns.md` | Review antipatterns this RCA may identify as root cause |
| `coaching-governance/guides/shift-left-prevention.md` | Preventive actions that reduce the probability of this defect type |
| `templates/sprint-retrospective.md` | Systemic preventive actions (§6) are added as ImprovementActions in the retrospective |
| `templates/engineer-coaching-assessment.md` | The coaching intervention (§7) is recorded in the engineer assessment |