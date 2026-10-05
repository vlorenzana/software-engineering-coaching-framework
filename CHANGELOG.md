# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Fixed

- `ontology/alignment-matrix.csv`: seven rows added in v5 (planning governance) were missing the `alignment_type` column; split and populated from corresponding TTL declarations.
- `ontology/alignment-matrix.csv` line 12: `AcceptanceCriteria` corrected to `AcceptanceCriterion` to match the class identifier declared in `secav-o.ttl`.
- `docs/ontology-alignment.md`: two occurrences of `AcceptanceCriteria` corrected to `AcceptanceCriterion`.

### Known issues (pending author decision)

- `ontology/secav-o-coaching-governance-extension.ttl` line 60: `rdfs:range secavo:AcceptanceCriteria` references an undeclared class. Correct reference is `secav:AcceptanceCriterion`; resolution requires namespace-merge decision noted in README.
- `validation/secav-o-coaching-governance.shacl.ttl`: `CoachingObjectiveShape` enforces `sh:minCount 1` on `alignsWithInstitutionalObjective`, making institutional alignment mandatory, while `docs/institutional-alignment.md` treats it as a recommendation. Alignment between constraint and documentation is pending author decision.
- `README.md`: core artifacts (`ontology/secav-o.ttl`, `validation/secav-o.shacl.ttl`, `examples/design-review.ttl`) are not listed; pending decision on whether to add a "Core artifacts" section.

## [0.1.0] - 2026-09-30

### Added

- Initial public repository structure.
- SECAV-O ontology prototype.
- Initial engineering activity, artifact, competency, evidence, measurement, AI-assistance, human-validation, assessment, and coaching concepts.
- Initial object and data properties.
- SHACL prototype constraints.
- Worked AI-assisted Design Review example.
- Conceptual architecture documentation.
- Initial competency questions.
- Draft pilot protocol.
- Citation metadata.
- MIT License.

### Status

This is an experimental prototype. It is not represented as complete, standardized, independently validated, or adopted by third parties.
