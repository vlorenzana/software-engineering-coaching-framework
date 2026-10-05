# SECAV-O Coaching Metrics Model

## Measurement principles

Metrics are coaching evidence, not standalone judgments. They should be interpreted together with activity type, artifact complexity, review context, engineer experience, AI assistance, and baseline conditions.

## 1. Defect metrics

Recommended defect dimensions:

- Defect ID
- Defect category
- Severity
- Phase injected
- Phase detected
- Artifact affected
- Engineering activity
- AI-assisted activity? (yes/no/unknown)
- Human validation performed? (yes/no/partial)
- Root cause / contributing factor
- Competency linked
- Coaching action linked

Useful derived measures:

- defects detected per phase;
- defects escaping the phase where they were introduced;
- late-phase defects;
- production escapes;
- repeated defect categories;
- defect-removal distribution across review, inspection, unit test, integration, system test, and production.

The model should avoid rewarding raw defect counts. A high number of defects found during an inspection may indicate either an effective inspection or a weak work product. Interpretation requires context.

## 2. Review and inspection metrics

Possible measures:

- work products reviewed;
- peer-review participation;
- formal inspection participation;
- review findings by category;
- recurring findings;
- findings resolved before downstream testing;
- escaped defects after review;
- ability to review another engineer's work;
- adherence to defined review acceptance criteria.

## 3. Unit-test metrics

Possible measures:

- unit-test artifacts produced;
- unit-test design reviewed;
- defects detected by unit tests;
- recurring test-failure patterns;
- test completeness against acceptance criteria;
- test coverage where useful;
- quality of assertions and edge-case coverage;
- evidence that AI-generated or AI-modified code was independently validated.

Code coverage is supporting evidence, not a proxy for test quality.

## 4. Competency-growth metrics

Competency growth should be assessed longitudinally using observable evidence from real engineering work. Recommended maturity states:

1. Observed
2. Assisted
3. Performs with Review
4. Independent
5. Can Review Others
6. Can Coach Others

The assessment should record the evidence that supports movement between levels.

## 5. Baseline and comparison

For each sprint objective, record:

- baseline value or state;
- sprint target;
- actual observation;
- trend direction;
- interpretation;
- confidence / evidence quality;
- action for next sprint.

## 6. Example metric set

| Metric | Baseline | Sprint Target | Evidence Source | Interpretation |
|---|---:|---:|---|---|
| Late-phase design defects | 6 / quarter | <= 3 / quarter | defect log | Track reduction in design escapes |
| Design-review recurring findings | 8 | <= 4 | review records | Track recurring design gaps |
| Unit-test defects found pre-integration | 10 | >= 14 | unit-test results | Earlier detection may be positive |
| Code-inspection participation | Assisted | Independent | inspection records | Competency growth |
| Unit-test design competency | Performs with Review | Independent | reviewed test artifacts | Competency growth |
