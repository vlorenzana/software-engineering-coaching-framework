# Pessimistic Defect Prevention Techniques

## Purpose

This guide covers five engineering techniques that treat failure as a certainty to be analyzed before it occurs, rather than a probability to be managed reactively. Unlike traditional risk analysis — which evaluates probabilities from a neutral or optimistic perspective — these techniques force the assumption that the worst scenario has already happened. By simulating collapse before the construction phase, teams overcome confirmation bias and surface architectural vulnerabilities, erroneous assumptions, and single points of failure before they are built in.

The coach uses this guide to verify that the team applies at least one pessimistic technique before committing to an architecture, and to identify coaching interventions when no structured defect prevention practice exists.

Source: original document "Prevención de Defectos Basada en Escenarios Pesimistas — Ingeniería de Software y Arquitectura Resiliente."

---

## Psychological foundation

Research in cognitive psychology demonstrates that imagining a future negative event has already occurred increases by 30% the brain's ability to correctly identify the causal reasons for failure before executing a project. This is called **prospective hindsight** (pre-mortem effect): when the failure is treated as historical fact rather than a hypothetical, participants contribute more freely and with greater specificity — social pressure to express critical doubts is removed.

---

## 1. Pre-Mortem Analysis

**Premise:** "The system launched and was a complete collapse."

The team convenes before starting the project and assumes the disaster as established historical fact. Each member independently documents all hypothetical causes that led to the failure. Independence is essential: the exercise must prevent social dynamics from suppressing critical observations.

**When to apply:** Design or project start phase, before architecture decisions are committed.

**Output:** A `secav:PreMortemReport` — a documented list of hypothetical failure causes, grouped and prioritized. The report feeds directly into the risk register.

**Coach signal:** A project that begins implementation without a Pre-Mortem or equivalent structured failure-assumption exercise has not surfaced its assumption blind spots. The coach raises this as a gap in the coaching plan review.

---

## 2. FMEA / AMFE (Failure Mode and Effects Analysis)

**Premise:** Systematically evaluate how each individual component can fail.

FMEA quantifies three factors for each failure mode:
- **Severity (S):** The impact on the system or user if the failure occurs (scale 1–10).
- **Occurrence (O):** The probability that the failure will occur (scale 1–10).
- **Detectability (D):** The difficulty of detecting the failure before it reaches the end user (scale 1–10; 10 = undetectable).

**Risk Priority Number (RPN):** `RPN = S × O × D`. High-RPN failure modes are prioritized for resilience patterns: circuit breakers, fallbacks, retry mechanisms, and redundancy.

**When to apply:** Detailed design or architecture definition, when specific components and their interactions are known.

**Output:** A `secav:FMEARegister` — a structured table with failure modes, effects, causes, and RPN scores.

**Coach signal:** A critical component (payment gateway, authentication, data integrity boundary) that has no documented FMEA analysis is a coaching signal on design-phase defect prevention.

---

## 3. Fault Tree Analysis (FTA)

**Premise:** Top-down deductive analysis from the main catastrophic scenario.

Starting from a declared top-level failure event (e.g., "complete service outage"), FTA decomposes the combination of software, hardware, and human errors required for that event to occur. The decomposition uses Boolean logic: AND gates (all sub-events must occur simultaneously) and OR gates (any sub-event alone is sufficient). The result is a visual tree that reveals critical paths and single points of failure.

**When to apply:** Security analysis or systems safety analysis, when the architecture of a critical module is defined.

**Output:** A fault tree diagram (documented in the design artifact). The primary result is **elimination of single points of failure** — nodes that appear in multiple paths to the top event.

**Coach signal:** A critical module whose failure would be catastrophic (payment, authentication, regulatory compliance) lacks a documented fault tree — the coach records this as a design review gap.

---

## 4. Threat Modeling (STRIDE)

**Premise:** "The attacker has full access or malicious intent."

Threat modeling simulates the adversary's perspective on the architecture. STRIDE is the standard classification for threat categories:

| STRIDE Category | Threat |
|---|---|
| **S**poofing | Impersonation of a legitimate user or system component |
| **T**ampering | Unauthorized modification of data in transit or at rest |
| **R**epudiation | A party denying they performed an action, with no audit trail |
| **I**nformation Disclosure | Unauthorized access to sensitive data (data leaks, log exposure) |
| **D**enial of Service | Making a service unavailable to legitimate users |
| **E**levation of Privilege | Gaining permissions beyond what was granted |

**When to apply:** Architecture definition phase, before committing security boundaries and trust zones.

**Output:** A `secav:ThreatModel` — a documented analysis of the attack surface, identified threats by STRIDE category, and the controls planned for each.

**Coach signal:** An architecture that exposes user data, handles authentication, or interfaces with external systems, without a documented threat model, represents an unmitigated security risk. The coach escalates this to the Technical Lead as a `secav:ProcessComplianceFinding` if threat modeling is an adopted process requirement.

---

## 5. Chaos Engineering

**Premise:** "Active fault injection to verify actual resilience."

Chaos Engineering deliberately injects failures into a system (in a staging or controlled production environment) to verify that resilience patterns perform as designed under real conditions. It differs from the other four techniques in that it is empirical and applied — not analytical. It validates the resilience decisions made during FMEA and FTA.

**When to apply:** Testing or pre-production phase, after resilience patterns have been implemented.

**Output:** Resilience verification evidence documenting which failure modes were tested, what the actual system behavior was, and whether the response met the expected graceful degradation or recovery targets.

**Coach signal:** A system that implements circuit breakers or bulkheads without ever having tested them under actual fault conditions provides false confidence. The coach records this as a gap in the test coverage plan.

---

## Technique comparison

| Technique | When to apply | Primary focus | Key output |
|---|---|---|---|
| Pre-Mortem | Design / project start | Project risk and assumption biases | Assumption and requirement adjustment |
| FMEA / AMFE | Detailed design / architecture | Individual component failure modes | Redundancy and retry mechanism prioritization |
| FTA | Security / systems analysis | Critical total-failure paths | Elimination of single points of failure |
| STRIDE / Threat Modeling | Architecture definition | Attack surface and security boundaries | Access controls and encryption requirements |
| Chaos Engineering | Testing / pre-production | Active fault injection | Live resilience verification |

---

## Impact on software quality

Applying these techniques shifts quality from a reactive detection activity (QA at testing) to a design-phase filter:

- **Reduces correction costs.** Identifying a design failure through a Pre-Mortem costs a fraction of correcting a defect in production. Early detection is the highest-ROI quality investment.
- **Promotes defensive architecture.** Structured failure analysis creates explicit demand for patterns such as Rate Limiting, Bulkheads, Graceful Degradation, and compensating transactions — patterns that would not be prioritized without a quantified failure mode.
- **Builds a culture of resilience.** Teams that conduct Pre-Mortems and FMEA sessions normalize technical transparency. Engineers lose the fear of flagging weak points in architectural proposals — a psychological safety condition the coach reinforces.

---

## 6. SECAV-O integration

| Concept | SECAV-O term | Notes |
|---|---|---|
| Pessimistic defect prevention session | `secav:DefectPreventionActivity` | Parent class for all five techniques |
| Pre-Mortem Analysis | `secav:PreMortemAnalysis` | Subclass of `secav:DefectPreventionActivity`; output: `secav:PreMortemReport` |
| FMEA / AMFE | `secav:FMEAAnalysis` | Subclass of `secav:DefectPreventionActivity`; output: `secav:FMEARegister` |
| Fault Tree Analysis | `secav:FaultTreeAnalysis` | Subclass of `secav:DefectPreventionActivity` |
| Threat Modeling (STRIDE) | `secav:ThreatModelingActivity` | Subclass of `secav:DefectPreventionActivity`; output: `secav:ThreatModel` |
| Chaos Engineering | `secav:ChaosEngineeringActivity` | Subclass of `secav:DefectPreventionActivity` and `secav:TestingActivity` |
| Pre-Mortem output | `secav:PreMortemReport` | Subclass of `secav:Artifact`; feeds `secav:RiskRegister` |
| FMEA table | `secav:FMEARegister` | Subclass of `secav:Artifact`; contains RPN scores |
| Threat model document | `secav:ThreatModel` | Subclass of `secav:Artifact` |
| RPN score (S × O × D) | `secav:rpnScore` | DatatypeProperty `xsd:integer` on FMEA entries |
| FMEA severity component | `secav:fmeaSeverity` | DatatypeProperty `xsd:integer` (1–10) |
| FMEA occurrence component | `secav:fmeaOccurrence` | DatatypeProperty `xsd:integer` (1–10) |
| FMEA detectability component | `secav:fmeaDetectability` | DatatypeProperty `xsd:integer` (1–10; 10 = undetectable) |
| Failure mode description | `secav:failureMode` | DatatypeProperty `xsd:string` |
| Failure effect on system | `secav:failureEffect` | DatatypeProperty `xsd:string` |
| Resilience pattern demand | `secav:MitigateStrategy` via `secav:RiskResponsePlan` | FMEA high-RPN items map to response plans with explicit resilience patterns |
| Project risk surfaced by Pre-Mortem | `secav:ProjectRisk` via `secav:RiskRegister` | Pre-Mortem report feeds the risk register |

---

## 7. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/risk-management.md` | Risk register and response planning — pessimistic techniques feed the register |
| `coaching-governance/guides/formal-inspections.md` | Formal inspection of critical modules — FMEA identifies which modules warrant inspection |
| `coaching-governance/guides/coach-observation-checklist.md` | Group 23 — coach observation signals for pessimistic defect prevention activities |
| `coaching-governance/docs/coach-code-of-ethics.md` | Principle 18 (risk-based coverage plan) — pessimistic techniques inform the risk classification |