# Incremental Adoption and Fail Fast

## Purpose

This guide describes the strategic approach for adopting the SECAV-O coaching framework incrementally — validating assumptions, detecting problems early, and correcting course before expanding adoption. It draws on the Fail Fast philosophy and techniques from iterative delivery practice.

The operational protocol for running a pilot is in `pilot/pilot-protocol.md`. This guide provides the strategic rationale and decision structure for sequencing that pilot and any subsequent expansion.

---

## 1. Why incremental adoption

Adopting a new coaching framework changes how engineering work is observed, documented, and coached. Attempting organization-wide adoption immediately carries several risks:

- the framework's concepts may not translate directly to the organization's engineering activities;
- coaches may apply terms or scales inconsistently;
- evidence collection may conflict with existing tooling, privacy policy, or organizational norms;
- metrics may be misinterpreted before a shared understanding is established.

Incremental adoption limits the blast radius of these risks. A small, bounded pilot answers the questions that matter most before the cost of correction becomes high.

---

## 2. Fail Fast philosophy

The framework explicitly adopts the Fail Fast principle: the goal of a pilot is not to avoid failure at all costs, but to surface incorrect assumptions, bottlenecks, and technical or governance constraints at the earliest possible stage — when the cost of correction is lowest [3].

```
INITIAL HYPOTHESIS
        |
        v
SHORT EXPERIMENT / CONTROLLED TEST
(PoC, end-to-end tracer, reduced pilot iteration)
        |
        +------------------+------------------+
        |                                     |
        v                                     v
[Failure / Deviation]               [Success / Validation]
        |                                     |
        v                                     v
EARLY DETECTION +                    EXPAND ADOPTION /
LESSONS LEARNED                      SCALE TO NEXT SCOPE
        |
        v
PIVOT OR CORRECTION
```

A controlled failure with empirical data is a successful learning outcome. The cost of declaring a hypothesis invalid in week two is far lower than discovering the same problem after organization-wide rollout.

### Benefits of this philosophy

- **Lower correction cost.** Problems detected in a 2-week iteration cost a fraction of the effort needed to correct the same problems after full deployment.
- **Shared calibration.** Coaches and engineers develop a shared understanding of terms, scales, and evidence types through real work before the framework scales.
- **Evidence-based confidence.** Decisions to expand are grounded in observed data, not assumptions.
- **Psychological safety.** Teams know that declaring a hypothesis invalid is expected and valued, not a failure of the team [3].
- **Reduced governance risk.** Confidentiality, consent, and data-handling constraints are resolved at small scale before they become organization-wide blockers.

---

## 3. Key techniques

### 3.1 Proof of Concept — validate feasibility

A Proof of Concept (PoC) is a minimal experiment that answers one question: *Is this feasible in this context?*

Applied to framework adoption:
- Before applying the full coaching cycle to a team, run a PoC on one engineering activity (e.g., a single `secav:CodeReview` or `secav:DesignReview`) with one coach and one engineer.
- Validate that evidence can be collected, that the competency scale can be applied consistently, and that the `secav:ReviewRecord` and `secav:ReviewFinding` concepts map to the team's actual artifacts.
- A PoC is not a pilot — it does not need to be representative. It needs to answer the feasibility question fast.

### 3.2 End-to-end tracer — validate the full coaching chain

The tracer concept, from Hunt & Thomas [1], involves building a thin but complete vertical slice through the entire system rather than completing horizontal layers one by one.

Applied to framework adoption:
- Run one complete coaching cycle — from `secav:EngineeringActivity` selection through `secav:Evidence` collection, `secav:CompetencyAssessment`, `secav:CoachingIntervention`, and `secavo:SprintRetrospective` — before attempting to cover multiple activities or engineers.
- The tracer confirms that the full ontological chain is operational end-to-end in the organization's context.
- Gaps discovered in the tracer (e.g., missing evidence types, inapplicable acceptance criteria) are corrected before scope expands.

### 3.3 Short feedback loops

Short iterations (one to four weeks) force hypotheses to be validated quickly. If a coaching cadence, evidence format, or competency definition does not work, it is discovered in days, not months.

Applied to framework adoption:
- From Phase 1 (Tracer) onwards, use the `secavo:CoachingSprint` and `secavo:SprintRetrospective` structure. The PoC (Phase 0) is pre-sprint and does not require a full sprint cadence.
- Review the `secavo:Risk` register at every `secavo:SprintRetrospective`.
- Retrospective outputs directly inform whether to persist, pivot, or stop.

---

## 4. Go / Pivot / Stop decision criteria

| Decision | Criterion |
|---|---|
| **Persist / Scale** | Evidence collection is consistent and traceable. Coaches apply the competency scale with agreement. At least one full coaching chain was completed and documented. No open governance blockers. |
| **Pivot** | Systematic friction detected (evidence format mismatch, consent constraints, scale ambiguity). Apply lessons and run a second short iteration with the correction applied. |
| **Stop** | A foundational assumption is invalid and no correction resolves it (e.g., the organization cannot collect observable engineering evidence; the coaching role does not exist). Document findings and report. |

A Stop is a valid and valuable outcome. It produces data that prevents a larger failed investment.

---

## 5. Pilot scope selection

When selecting the initial scope for adoption:

- **Choose 1–3 engineering activities** from the SECAV-O core pattern (e.g., `secav:CodeReview`, `secav:DesignReview`, or `secav:UnitTestDesignImplementation`).
- **Choose a team of representative complexity** — not a team in active crisis, and not a trivial zero-risk project. See `pilot/pilot-protocol.md` §Candidate scope.
- **Avoid starting with the full governance extension.** The core pattern (EngineeringActivity → Artifact → Evidence → CompetencyAssessment → CoachingIntervention) is sufficient for the first iteration. Governance, ethics, and risk management artifacts are added in later cycles.
- **Limit the initial set of competencies** to those directly observable in the selected activities.

---

## 6. Expansion phases

| Phase | Scope | Goal |
|---|---|---|
| 0 — PoC | 1 activity, 1 engineer, 1 coach | Validate feasibility of evidence collection and ontology application |
| 1 — Tracer | 1 complete coaching cycle, 1 team | Validate the full chain end-to-end |
| 2 — Pilot | 1–3 activities, 1 team, full sprint cadence | Validate consistency and sustainability |
| 3 — Controlled expansion | 2–4 teams | Validate coach calibration and cross-team comparability |
| 4 — Broad adoption | Organization or business unit | Scale with established calibration |

Each phase requires a Stop/Pivot/Persist decision before the next phase begins. No phase is skipped.

---

## 7. SECAV-O integration

The following framework concepts are directly relevant to incremental adoption:

| Adoption concept | SECAV-O term |
|---|---|
| Feasibility test (PoC) | `secav:Evidence` — can it be collected? `secav:AcceptanceCriterion` — can it be evaluated? |
| End-to-end tracer | Full chain: `secav:EngineeringActivity` → `secav:Artifact` → `secav:Evidence` → `secav:CompetencyAssessment` → `secav:CoachingIntervention` |
| Short feedback loop | `secavo:CoachingSprint` + `secavo:SprintRetrospective` |
| Risk of adoption failure | `secavo:Risk` + `secavo:PreventiveAction` + `secavo:CorrectiveAction` |
| Evidence of adoption progress | `secav:WorkProductEvidence`, `secav:ReviewFinding`, `secav:Measurement` |
| Coach calibration | `secav:CompetencyAssessment` applied consistently across coaches |
| Pivot decision | `secavo:ImprovementAction` (subclass of `secav:CoachingIntervention`) |
| Stop decision | Documented in `secavo:SprintRetrospective`; feeds risk register update |

---

## 8. Relationship to pilot-protocol.md

| Document | Role |
|---|---|
| `guides/incremental-adoption.md` (this file) | Strategic philosophy, decision structure, and phasing |
| `pilot/pilot-protocol.md` | Operational protocol: participants, stages, measurements, evidence to retain, pilot outputs |

Use this guide to decide *when and how to phase* adoption. Use the pilot protocol to *execute* each phase.

---

## References

[1] Hunt, A., & Thomas, D. (1999). *The Pragmatic Programmer: From Journeyman to Master.* Addison-Wesley Professional. (Source for the Tracer Bullet concept.)

[2] Leffingwell, D. (2017). *SAFe 4.5 Reference Guide: Scaled Agile Framework for Lean Enterprises.* Addison-Wesley Professional. (Source for PI Planning and incremental team synchronization concepts, used here as a philosophical reference only — this framework does not prescribe SAFe or any specific scaled agile methodology.)

[3] Ries, E. (2011). *The Lean Startup: How Today's Entrepreneurs Use Continuous Innovation to Create Radically Successful Businesses.* Crown Business. (Source for the Fail Fast principle and short feedback loops in environments of uncertainty.)

[4] Beck, K., et al. (2001). *Manifesto for Agile Software Development.* https://agilemanifesto.org. (Philosophical basis for iterative delivery and responding to change over following a plan.)