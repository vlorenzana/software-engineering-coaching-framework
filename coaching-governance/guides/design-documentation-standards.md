# Design Documentation Standards

## Purpose

This guide establishes which design artifacts are mandatory based on system characteristics, and which quality criteria apply to each. The artifacts listed here are verified during formal design inspections (`secav:DesignReview`) as `secav:QualityCriterion` applied to `secav:DesignArtifact`.

The absence of a mandatory artifact — when the system has the characteristics that require it — is a `secav:ReviewFinding` that must be resolved before the design advances to implementation.

---

## 1. State diagrams

### 1.1 When they are mandatory

A state diagram is mandatory for any system entity — class, module, process, external resource, or business flow — that can be in more than one distinguishable state and whose behavior varies depending on which state it is in.

Signals that a state diagram is needed:
- The code contains enumerations or constants representing states: `PENDING`, `ACTIVE`, `SUSPENDED`, `CLOSED`, `PROCESSING`, etc.
- Business logic includes conditions of the type "if the resource is in state X, then..."
- An operation is valid in some states of the object but not in others.
- There is a resource lifecycle with a defined beginning and end.

### 1.2 What it must contain

A complete and useful state diagram for developers includes:

| Element | Description | Signal of omission |
|---|---|---|
| **Initial state** | The state the object is in when created. Visually marked with the standard symbol (filled circle → arrow). | If there is no explicit initial state, developers assume different starting points. |
| **Final states** | States in which the object ceases to exist or can no longer transition. Visually marked (filled circle inside an empty circle). | If there are no final states, it is not clear when the lifecycle concludes. |
| **All possible states** | Every distinguishable state the object can occupy. | Implicit states in code that do not appear in the diagram generate undocumented behaviors. |
| **Transitions** | Directed edges between states, labeled with the event or condition that triggers them. | Transitions without a label are ambiguous: developers do not know what activates them. |
| **Guard conditions** | Additional conditions that must be met for a transition to occur (`[condition]`). | Without guards, developers do not know when a transition is available and when it is not. |
| **Transition actions** | What the system does when executing the transition (`/ action`), when applicable. | Implicit actions in code that do not appear in the diagram create divergence between design and implementation. |

### 1.3 Diagram quality criteria (verified in inspection)

Inspectors verify these criteria (`secav:QualityCriterion`) during the design review:

| Criterion | Question |
|---|---|
| **Complete** | Are all states that appear in the code or business logic present? |
| **Explicit initial state** | Is there exactly one marked initial state? |
| **Explicit final states** | Are all states in which the lifecycle concludes marked? |
| **Labeled transitions** | Do all transitions have an event or condition label? |
| **No implicit transitions** | Can a developer determine, from the diagram alone, which state follows given an event? |
| **Consistent with code** | Does the diagram reflect the system's actual behavior, not the originally desired behavior? |

A state diagram that fails any of these criteria is a `secav:ReviewFinding`. A missing state diagram when the system has states is a blocking `secav:ReviewFinding` for advancing to implementation.

### 1.4 Why it is mandatory, not optional

A state diagram serves developers in ways code cannot replace:

- **Global visibility:** code shows how each transition is implemented individually; the diagram shows all lifecycle transitions simultaneously.
- **Trap state detection:** states from which there is no exit, or from which the only exit leads to unintended final states, are visible in the diagram but invisible in code until they occur.
- **Missing transition detection:** if an event can occur in a state and the diagram has no transition for that (state, event) pair, the behavior is undefined — and that is a design defect.
- **Maintenance reference:** when a developer modifies the system months later, the diagram is the only way to understand the full lifecycle without reading all the code.

---

## 2. Coach's role in design documentation review

The coach attends as a silent observer during design artifact inspections. They specifically observe:

- Whether inspectors verify the presence of mandatory artifacts before reviewing their content.
- Whether inspectors distinguish between "the diagram exists" and "the diagram is correct and complete."
- Whether findings of diagram absence or incompleteness are recorded with sufficient detail for the designer to correct them without a new meeting.

The coach records as `secavo:QualityPlanningConcern` if the systematic lack of state diagrams in reviewed designs indicates the absence of an agreed documentation standard in the team.

---

## 3. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| State diagram as design artifact | `secav:DesignArtifact` |
| Diagram review | `secav:DesignReview` |
| Diagram quality criteria | `secav:QualityCriterion` |
| Missing or incomplete diagram | `secav:ReviewFinding` |
| Review record | `secav:ReviewRecord` |
| Systemic pattern of missing diagrams | `secavo:QualityPlanningConcern` |
| Competency developed by producing complete diagrams | `secav:DesignCompetency` |
| Competency assessment derived from review | `secav:CompetencyAssessment` on `secav:DesignCompetency` |

---

## 4. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/formal-inspections.md` | Inspection protocol that applies to the design artifacts documented here |
| `coaching-governance/guides/minimum-quality-criteria.md` | The architecture and detailed design phase requires inspection of its critical artifacts |
| `coaching-governance/guides/requirements-inspection.md` | The primary glossary of the requirements document must define the domain states before they appear in the design diagram |
| `coaching-governance/glossary/glossary.md` | Definitions of critical module, formal inspection, QualityPlanningConcern |