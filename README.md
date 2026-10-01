# Software Engineering Coaching Framework

**Prototype version:** 0.1.0  
**Status:** Initial experimental prototype

This repository contains an open, competency-based and ontology-supported framework intended to assist developer coaching in AI-assisted software engineering.

The framework connects:

**Engineering Activity → Artifact → Competency → Acceptance Criteria → Observable Evidence → Measurement → AI Assistance → Human Validation → Coaching Intervention**

Its purpose is to help coaches, engineering leaders, educators, and software teams make engineering expectations, evidence, review responsibilities, and coaching decisions more explicit and reusable.

## Problem addressed

AI-assisted development can increase the speed and volume of software production, but software teams still require engineering judgment, architecture, testing, security review, maintainability, quality measurement, planning discipline, and continued development of human engineering competencies.

This project does **not** assume that AI-generated code is inherently unsafe, nor that automation can replace accountable engineering judgment. Instead, it models AI assistance and human validation as distinct concepts.

## Design principles

1. **Competency-based:** competencies are connected to observable engineering activities and evidence.
2. **Evidence-oriented:** assessment should rely on work products, review findings, measurements, and repeated observations.
3. **Human-accountable:** AI assistance is represented separately from human validation.
4. **Methodology-agnostic:** the model is not tied to Scrum, TSP/PSP, CMMI, or another single process framework.
5. **Open and reusable:** the project is intended to support independent review, adaptation, teaching, and experimentation.
6. **Ontology-supported:** engineering concepts and relationships are represented explicitly in RDF/OWL-compatible form.
7. **Incremental:** v0.1 covers a deliberately small domain and will be extended through expert review and pilot evidence.

## Repository structure

- `ontology/secav-o.ttl` — initial ontology prototype
- `validation/secav-o.shacl.ttl` — initial SHACL validation shapes
- `examples/design-review.ttl` — worked design-review example
- `docs/architecture.md` — conceptual architecture and scope
- `docs/competency-questions.md` — competency questions guiding the ontology
- `pilot/pilot-protocol.md` — initial protocol for future pilot validation
- `CHANGELOG.md` — version history
- `CITATION.cff` — citation metadata
- `LICENSE` — open-source license

## Initial scope

The first prototype focuses on:

- requirements
- design
- coding
- testing
- implementation vs. review activities
- engineering artifacts
- technical competencies
- observable evidence
- measurements and quality criteria
- AI-assisted work
- human validation
- competency assessment
- coaching interventions

## Example design decomposition

```text
Software Engineering Process
└── Design
    ├── Application Design
    │   ├── Design Implementation
    │   └── Design Review
    └── Unit Test Design
        ├── Unit Test Design Implementation
        └── Unit Test Design Review
```

A Design Implementation activity can produce a Design Artifact. A Design Review evaluates that artifact and produces Review Findings or a Review Record. Both activities may require distinct competencies. If AI assists in creating an artifact, that assistance can be recorded separately from the Human Validation Activity responsible for accepting or rejecting the result.

## Alignment with existing software-engineering ontologies

This project is intended to **reuse or align with existing software-engineering ontology work where technically and legally appropriate**, rather than redefine equivalent concepts unnecessarily.

SEON (Software Engineering Ontology Network) is being evaluated as a reference source for software-process, design, coding, testing, quality, and measurement concepts. Version 0.1 does **not** import SEON modules directly. Alignment will be added only after relevant ontology identifiers, semantics, maintenance status, and reuse/licensing conditions are verified.

Reference:
- https://dev.nemo.inf.ufes.br/seon/SEON.html

## Validation approach

The ontology expresses domain concepts and relationships. SHACL shapes express selected data-quality and governance constraints.

For example, a recorded AI-assisted engineering activity should identify:
- the AI system involved;
- the human-validation activity, where the implementation policy requires it;
- relevant evidence or work products.

SHACL is used for graph validation, not as a claim that the engineering process itself has been empirically validated.

## Prototype boundary

Version 0.1 is an **initial technical prototype**. It is not represented as:
- a completed ontology;
- an industry standard;
- an accredited assessment method;
- a validated predictor of engineer performance;
- an endorsed framework;
- evidence of third-party adoption.

Those claims would require separate evidence.

## Roadmap

### v0.1
- core classes and relationships
- initial design-review example
- competency questions
- basic SHACL constraints
- pilot protocol

### v0.2
- requirements, coding, testing, architecture, and security examples
- competency-level representation
- expanded evidence and measurement model
- candidate alignment mappings to existing ontologies

### v0.3+
- expert review
- pilot feedback
- evidence-driven revisions
- documented interoperability/alignment decisions

## Author

Victor Hugo Lorenzana González, M.Eng. in Software Engineering

## License

MIT License. See [LICENSE](LICENSE).
