# Requirements Inspection

## Purpose

Defects introduced in the requirements phase are the most costly to correct: the later they are detected, the more work they invalidate. A formal requirements inspection (`secav:DesignReview` on a `secav:DesignArtifact`) allows detecting ambiguities, vagueness, and inconsistencies before they translate into incorrect code.

The coach attends these inspections as an observer — takes notes and gives feedback after the session, following the same protocol as in formal code inspections (`coaching-governance/guides/formal-inspections.md`) and peer reviews (`coaching-governance/guides/peer-review-sessions.md`).

---

## 1. Why multiple reviewers are needed

Some types of defects in requirements **can only be detected when there is more than one reviewer**. Ambiguity is the clearest case: a requirement is ambiguous when it admits two or more valid interpretations. A single reviewer cannot by themselves generate two distinct interpretations of the same text — they will simply read it one way and not see the problem.

The inspection with multiple reviewers who work independently and then compare their interpretations is the technique that makes these ambiguities visible:

```
Reviewer A reads the requirement → Interpretation A
Reviewer B reads the requirement → Interpretation B
          ↓
  Interpretation A ≠ Interpretation B
          ↓
  The requirement is ambiguous → defect detected
```

This makes individual preparation before the meeting especially critical in requirements inspections: reviewers must note their interpretation of the requirement **before** hearing others'. Once the colleague's interpretation is known, confirmation bias prevents seeing one's own independently.

---

## 2. Types of defects the inspection detects

| Defect type | Description | Requires multiple reviewers to detect? |
|---|---|---|
| **Ambiguity** | The requirement admits two or more valid interpretations | Yes — comparison of independent interpretations |
| **Vagueness** | Imprecise language without operational definition: "fast," "easy to use," "efficient" | Not necessarily, but better detected with multiple perspectives |
| **Incompleteness** | Missing cases, boundary conditions, error scenarios | No — an experienced reviewer can detect it |
| **Inconsistency** | Two requirements that contradict each other | Useful to have reviewers from different areas to see the contradiction between domains |
| **Unverifiability** | The requirement cannot be tested — there is no observable compliance criterion | No — but better detected by those who will write the tests |
| **Infeasibility** | The requirement cannot be implemented as described | Requires a technical reviewer who knows the system's constraints |

---

## 3. Requirements inspection process

The process follows the same five phases as the formal code inspection (`coaching-governance/guides/formal-inspections.md`), with adaptations to the object of review.

| Phase | Responsible | Description |
|---|---|---|
| **1. Planning** | Technical Lead / Architect | Select the requirements to inspect. Prioritize the highest-risk ones: requirements that affect many functionalities, involve integration with external systems, or have frequently generated questions. Distribute material at least 24–48 hours in advance. |
| **2. Individual preparation** | All inspectors | Each inspector reads the requirements independently and records: (a) their interpretation of each requirement, (b) terms they consider vague or undefined, (c) cases or conditions the requirement does not cover. Preparation is mandatory — it is the step that makes detecting ambiguities possible. |
| **3. Inspection meeting** | Designated moderator | Inspectors compare their interpretations point by point. The moderator records each discrepancy as a `secav:ReviewFinding`. The coach attends as a silent observer — does not intervene verbally. |
| **4. Rework** | Requirement author | The author revises and rewrites requirements where defects were found, with support from the Technical Lead or Architect for scope decisions. |
| **5. Follow-up** | Coach | Verifies that requirements marked as defective were corrected before they advance to design or implementation, by reviewing the updated `secav:ReviewRecord`. |

---

## 4. Requirements document glossary

### 4.1 Recommended structure: two levels

A requirements document should include two glossaries:

- **Primary glossary** — at the beginning of the document, before the requirements. Contains terms without which the reader cannot correctly interpret the requirements. If a primary glossary term is ambiguous or interpreted differently by two readers, the requirements that use it inherit that ambiguity.

- **Secondary glossary** — at the end of the document. Contains support terms: acronyms, references to external systems, naming conventions, technical terms that appear occasionally but are not central to understanding the document.

### 4.2 Primary glossary terms are inspectable work products

A primary glossary term is an artifact with the same ambiguity risk as a requirement. As with requirements, **a term is only unambiguous when two or more reviewers interpret it the same way independently**. An author cannot detect the ambiguity of their own definition because they will read it with the interpretation they already have in mind.

Inspectors must verify each primary glossary term in the same way they verify requirements:

| Criterion | Question |
|---|---|
| **Does everyone interpret it the same way?** | Each inspector notes their understanding of the term before the meeting and compares |
| **Is the definition operational?** | Does it allow deciding, without ambiguity, whether something belongs to the concept or not? |
| **Is it consistent with other terms?** | Does it contradict or overlap the meaning of another glossary term? |
| **Does it reflect the business domain?** | Does it coincide with stakeholders' use of the term? |

A primary glossary term with two different interpretations among inspectors is a `secav:ReviewFinding` that must be resolved before requirements using it are approved.

---

## 5. Quality criteria for a requirement

Inspectors evaluate each requirement against these criteria (`secav:QualityCriterion`):

| Criterion | Question it answers |
|---|---|
| **Unambiguous** | Do all readers interpret it the same way? |
| **Verifiable** | Is there an observable criterion that confirms whether it is fulfilled? (`secav:AcceptanceCriterion`) |
| **Complete** | Does it cover normal cases, error cases, and boundary cases? |
| **Consistent** | Does it contradict any other system requirement? |
| **Feasible** | Can it be implemented within known technical and business constraints? |
| **Traceable** | Can it be linked to a business need or project objective? |

---

## 6. Coach's role

The coach attends the inspection meeting as a **silent observer**, consistent with the established protocol for all review meetings:

- Does not participate verbally during the session.
- Takes observation notes on the process: how inspectors compare their interpretations, which requirements generate the most discrepancy, whether findings are recorded correctly.
- Verifies that the `secav:ReviewRecord` is being completed with the necessary data.
- Gives feedback after the session — group, individual, or organizational — following the same criteria as in peer reviews and formal inspections.

### 6.1 What the coach specifically observes

- **Individual preparation:** did the inspectors come with their prior annotations? If not, the moderator should reschedule — the coach records this as an alert signal.
- **Depth of analysis:** are inspectors comparing interpretations or just reading the requirement aloud without contrasting?
- **Finding recording:** are defects being documented with sufficient detail for the author to correct them without a new meeting?
- **Defect pattern:** if the same type of defect (e.g., vagueness) appears in the majority of requirements, it is a process signal — not of an individual author.

### 6.2 Subsequent feedback

| Recipient | When | What |
|---|---|---|
| **Team (group)** | If the pattern affects the collective requirements writing process | Most frequent defect type, process improvement recommendations |
| **Individual (private)** | If the observation is specific to a participant | Insufficient preparation, difficulty articulating interpretations, etc. |
| **Organization** | If requirements exhibit systemic defects reflecting absence of an elicitation process or acceptance criteria | Formal escalation or recommendation to the Coaches Committee |

---

## 7. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| Inspected requirements document | `secav:DesignArtifact` |
| Requirements inspection as activity | `secav:DesignReview` (subclass of `secav:ReviewActivity` and `secav:DesignActivity`) |
| Quality criteria evaluated | `secav:QualityCriterion` |
| Requirement verifiability criterion | `secav:AcceptanceCriterion` |
| Inspection record | `secav:ReviewRecord` |
| Primary glossary term with divergent interpretations | `secav:ReviewFinding` |
| Finding (ambiguity, vagueness, inconsistency in requirement) | `secav:ReviewFinding` |
| Defect recorded when closing | `secav:DefectRecord`; `secavo:DefectObservation` with `secavo:phaseInjected = "requirements"` |
| Detection phase | `secavo:phaseDetected = "requirements review"` |
| Coach observation notes | `secav:WorkProductEvidence` |
| Subsequent coach feedback | `secav:CoachingRecommendation` |
| Competencies developed in inspection | `secav:DesignCompetency`, `secav:ReviewCompetency` |
| Intervention if systemic pattern | `secav:CoachingIntervention`, `secavo:ImprovementAction` |

---

## 8. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/formal-inspections.md` | Base protocol for formal inspections — the same process applied to code |
| `coaching-governance/guides/peer-review-sessions.md` | Same silent observer protocol for the coach |
| `coaching-governance/guides/defect-tracking.md` | Defects found in requirements inspection are recorded with phaseInjected = "requirements" |
| `coaching-governance/docs/project-planning-participation.md` | Requirements inspection must be included in the project plan |
| `coaching-governance/guides/project-kickoff-alignment.md` | Quality objectives may include metrics for defects found in the requirements phase |
| `templates/engineer-coaching-assessment.md` | Participation in requirements inspections is evidence of DesignCompetency |