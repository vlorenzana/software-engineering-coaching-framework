# Review Scenarios Catalog — SECAV-O Pilots

## Status

Draft v0.1 — proposed scenarios, no pilot results yet.

## Purpose

This catalog records 50 code review proposals classified by interaction type and execution mode. Each scenario is a candidate for implementation as an observable engineering activity within the SECAV-O framework, with evidence collectable through the `ReviewObservation` and `MeasurementObservation` model.

The scenarios serve as input for designing pilots with a control group and an experimental group, enabling comparison of current practices against specific proposals before formally adopting them.

Original source: *50 Code Review Ideas: Human, Human-AI, AI-AI — SECAV-O Framework* (proposals document, 2026).

---

## Experimental design: control group and experimental group

### Principle

The framework does not presuppose that any of the 50 scenarios improves software quality. The purpose of the experimental design is to generate observable evidence for each proposal before formally adopting it in the engineering process.

### Control group

The control group applies the team's current review practices without modification during the observation period. Its results constitute the `Baseline` against which the experimental group's findings are compared.

The control group:
- does not adopt any scenario from the catalog during the active pilot period;
- records the same set of metrics as the experimental group;
- may use the tools and processes it already uses normally.

### Experimental group

The experimental group adopts one or more scenarios selected from the catalog during the observation period. The selection must be justified before the pilot starts, with acceptance criteria and metrics agreed with the coach.

The experimental group:
- incorporates the selected scenario alongside its usual practices, unless the pilot design requires explicit substitution;
- documents any adjustment to the scenario during execution as an observed variant;
- cannot switch scenarios mid-period without documenting the change as an event.

### Assignment criteria

- Assignment to each group must be documented before data collection begins.
- Groups of 2–4 engineers minimum are recommended so that results are comparable.
- The coach documents the assignment criteria and possible selection biases in the pilot record.
- A small team can run the groups sequentially (A/B rollover): control during the first weeks, experimental afterwards, comparing the same engineers before and after.

### Comparison metrics

The metrics defined in `pilot-protocol.md` apply to both groups. Additionally recording the following is recommended:

| Metric | Description |
|---|---|
| Applied scenario | Scenario ID and name |
| Review time per PR / artifact | Minutes from opening to approval |
| Findings by category | Security, logic, style, test coverage |
| Late findings | Found post-merge or in production |
| Reviewer comprehension | Can the reviewer explain the reviewed code? (observable evidence) |
| Passive AI dependency | Proportion of approvals without substantive human verification |

No metric should be interpreted in isolation.

---

## Scenario catalog

Classification: **H** = Pure Human · **HA** = Human-AI · **AA** = AI-AI  
Mode: **Individual** · **Pair** · Formal **Inspection**

---

### Group H — Pure Human (H-01 to H-10)

| ID | Mode | Scenario | Objective |
|---|---|---|---|
| H-01 | Individual | Self-review with OWASP security checklist before commit | Reviewer checks their own diff against the OWASP Top 10 list |
| H-02 | Individual | Desk-check with requirement traceability — no AI | Verifies each line against the corresponding functional requirement |
| H-03 | Pair | 30-min synchronous walkthrough — author explains logic | Pair focused on logic, not style |
| H-04 | Inspection | Formal Fagan inspection: planning, overview, preparation, inspection, rework, follow-up | Formal process with moderator / author / inspector roles |
| H-05 | Pair | Asynchronous peer review with 200–400 LOC per hour limit | Prevents review fatigue; focus on defects |
| H-06 | Individual | Code reading with security questions: where does user data enter? | Mental taint analysis |
| H-07 | Inspection | Inspection with project-specific defect checklist (Known Pitfalls Doc) | Maintain a living document of past team errors |
| H-08 | Pair | Competency review: does this code preserve the junior engineer's skill? | Evaluates whether the junior understands AI-generated code |
| H-09 | Individual | Evidence review: unit tests, logs, screenshots — do not approve without observable evidence | Do not approve without recorded observable evidence |
| H-10 | Inspection | Role-based inspection: security, test, and domain expert review the same PR | Separate roles by competency area |

**Recommended pilot:** H-01 to H-10 are candidates for the experimental group in **Pilot 1** (months 6–12). They require no additional tools and carry the lowest adoption risk.

---

### Group HA — Human-AI (HA-11 to HA-30)

| ID | Mode | Scenario | Objective |
|---|---|---|---|
| HA-11 | Individual | AI pre-review: Copilot / CodeRabbit does first pass, human validates | AI flags style and obvious bugs; human contributes strategic judgment |
| HA-12 | Pair | Human-in-the-loop: AI generates, human spot-checks for logical coherence | Detects legacy API violations |
| HA-13 | Inspection | AI + human checklist: AI generates a PR-adapted checklist, human uses it | Dynamic checklist by PR context |
| HA-14 | Individual | Behavior review, not just syntax: what does the AI code do? | Treat AI output as untrusted by default |
| HA-15 | Pair | Known AI pitfalls review: human reviews list of common LLM errors (API hallucinations) | Detect methods invented by the LLM |
| HA-16 | Inspection | Secure path review: human mandatory for authz, payments, PII, shell exec from LLM output | Critical paths always require manual validation |
| HA-17 | Individual | Prompt-to-code traceability: review the prompt that generated the code + output | Verifies whether the prompt contained security constraints |
| HA-18 | Pair | AI explains, human decides: AI explains PR in natural language, human approves | Reduces superficial LGTM (Gön et al. ICSME 2024: 64.7%) |
| HA-19 | Individual | Feedback loop: human corrects AI suggestion, AI learns | HITL to reduce accumulated false positives |
| HA-20 | Inspection | Two-stage: Stage 1 AI — basic style/security; Stage 2 human — architecture/domain | Splits review by risk level |
| HA-21 | Pair | AI-generated tests review: human reviews whether AI tests cover real edge cases | Generated tests may be weak or tautological |
| HA-22 | Individual | Requirement conformance check: LLM judges conformant but overcorrects — human verifies | Risk of systematic overcorrection (Jin & Chen 2026) |
| HA-23 | Inspection | SHACL/OWL validation: AI validates against SECAV-O ontology, human interprets violations | Automates ontological validation of the framework |
| HA-24 | Pair | Pair programming with Copilot: one drives, one observes, AI suggests | Driver/observer + AI as third participant |
| HA-25 | Individual | AI debt flagging: AI marks technical debt, human prioritizes | Continuous refactor based on AI signals |
| HA-26 | Inspection | Evidence gate: no merge without recorded evidence of human validation against acceptance criteria | SECAV-O acceptance criteria as a mandatory gate |
| HA-27 | Pair | Cross-file review: human asks AI to analyze cross-file impact not shown in the diff | AI-assisted taint analysis beyond the diff |
| HA-28 | Individual | Security review pre-commit: Copilot /security-review on unpushed diff vs CodeQL post-push | Coverage difference between pre- and post-push |
| HA-29 | Pair | Competency check: can the junior explain the AI code? If not, coaching is required | Preserve skill; avoid passive AI dependency |
| HA-30 | Inspection | Review retrospective: measure depth (not just comment count) and late escapes | Falsifiable metrics for review quality |

**Recommended pilot:** HA-11, HA-14, HA-16, HA-18, HA-20 for **Pilot 1** (months 6–12). HA-21 to HA-30 for **Pilot 2** (months 12–24, 12–20 engineers).

---

### Group AA — AI-AI (AA-31 to AA-50)

| ID | Mode | Scenario | Objective |
|---|---|---|---|
| AA-31 | Individual | AI linter + AI security scanner: ESLint AI + Semgrep AI rules | Two AIs with different perspectives on the same code |
| AA-32 | Pair | AI-AI peer: CodeRabbit reviews PR generated by Copilot | Dual LLM as an automated review layer |
| AA-33 | Inspection | CodeQL (deterministic) + Copilot Autofix (LLM) = detection + proposed fix | GitHub Advanced Security integrated |
| AA-34 | Individual | Snyk Code (static) + Snyk DeepCode AI (semantic) cross-check | Security; two complementary engines on the same code |
| AA-35 | Pair | SonarQube AI Quality Gate + Sonar AI vulnerability detection | Quality + security in CI pipeline |
| AA-36 | Inspection | AI chain: AI-1 generates, AI-2 generates tests, AI-3 reviews tests vs requirements | Multi-agent AI pipeline with cross-validation |
| AA-37 | Individual | LLM self-critique: same LLM reviews its own code with a different prompt (self-refine) | Self-review; evaluates LLM autocorrection limits |
| AA-38 | Pair | AI-AI adversarial: attacker AI tries to exploit code, defender AI patches it | Automated red team |
| AA-39 | Inspection | Pixee / Corgea auto-remediation: AI scanner + AI fixer opens draft PR | Auto-fix with mandatory pending human review |
| AA-40 | Individual | Veracode ML-enhanced scanning + LLM explanation | Enterprise scanner with natural-language explanation |
| AA-41 | Pair | Claude Code review loops with cap (avoid >50 rounds) — measure human approvals per PR | Anthropic method; iteration cap to prevent endless loops |
| AA-42 | Inspection | Tool calling: Copilot code review with CodeQL + ESLint integrated (GitHub 2025) | Deterministic + LLM combined in a single tool |
| AA-43 | Individual | AI coverage check: AI verifies that each requirement has a test, another AI verifies test quality | Requirement coverage with dual AI layer |
| AA-44 | Pair | AI format gate: Prettier AI + AI commit message review | Code hygiene and commit message quality |
| AA-45 | Inspection | AI secret scanning: GitHub secret scanning AI + AI false positive filter | Secret detection with AI false positive filter |
| AA-46 | Individual | Performance AI: AI predicts performance regression, another AI suggests optimization | Preventing performance degradation |
| AA-47 | Pair | AI documentation sync: AI detects undocumented code, AI generates doc, AI verifies doc vs code | Continuous documentation synchronization |
| AA-48 | Inspection | Dependency AI: Dependabot AI + Snyk AI evaluate risk of AI-generated dependencies | Supply chain of AI-generated dependencies |
| AA-49 | Individual | AI policy enforcement: OPA policy + LLM explains violation in natural language | Policy as code with engineer-readable explanation |
| AA-50 | Inspection | Full SECAV-O pipeline: OWL validator AI + SHACL AI + Evidence recorder AI + Report AI | Complete automated framework pipeline |

**Recommended pilot:** AA-33, AA-34, AA-42 for **Pilot 2** (months 12–24). AA-50 is the long-term production objective. AA scenarios always require a final HA gate for critical paths (authz, payments, PII); they must not run as the sole review layer.

---

## Pilot map

| Pilot | Indicative period | Team size | Recommended scenarios (experimental) | Control group |
|---|---|---|---|---|
| Pilot 1 | Months 6–12 | 4–6 engineers | H-01 to H-10 + HA-11, HA-14, HA-16, HA-18, HA-20 | Current practices unchanged |
| Pilot 2 | Months 12–24 | 12–20 engineers | HA-21 to HA-30 + AA-33, AA-34, AA-42 | Pilot 1 results as new baseline |
| Production | Month 24+ | Scale | AA-31 to AA-50 with mandatory HA gate | Pilot 2 metrics as reference |

---

## Ontological alignment (SECAV-O)

Each scenario in the catalog is instantiated as a `QualityActivityRequirement` within a `CoachingSprint`. Collected findings are recorded as `ReviewObservation` (subclass of `MeasurementObservation` → `Evidence`).

The control group and experimental group produce distinct `Baseline` instances comparable through `CompetencyTrend`. The difference between the two `Baseline` values is the observable evidence of the scenario's effect.

Scenarios HA-23 and AA-50 directly apply the SECAV-O OWL/SHACL model as an automated verification mechanism, closing the loop between the conceptual framework and the validation tool.

---

## Sources

- NIST SP 800-218 / 218A (SSDF)
- OWASP Code Review Guide / OWASP Top 10 for LLM Apps
- Gön et al., ICSME 2024 — LGTM study (64.7% superficial approval rate)
- Jin & Chen 2026 — systematic overcorrection in LLM-based code review
- GitHub Copilot Code Review docs (2024–2025)
- CodeQL / GitHub Advanced Security docs
- Anthropic Claude Code review method (cap <50 rounds)
- SonarQube AI / Snyk Code / Semgrep / Pixee / Corgea / Veracode