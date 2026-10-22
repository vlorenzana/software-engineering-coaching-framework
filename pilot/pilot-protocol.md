# Pilot Protocol — Draft v0.1

## Status

Initial draft for future validation. No pilot results are claimed by this document.

## Purpose

The pilot is intended to test whether the framework can be applied consistently in a real or educational software-development setting and whether its concepts produce useful, observable evidence for coaching.

The pilot does **not** begin with a predetermined claim that the framework improves software quality by a specific percentage.

## Candidate scope

A pilot may focus on one bounded engineering area, such as:

**Application Design → Design Implementation → Design Review**

or

**Code Implementation → Code Review**

A small scope is preferred for the first pilot.

## Participants

Potential roles:
- 3–8 software engineers or students;
- 1 developer coach/facilitator;
- 1 engineering leader, instructor, or independent observer where available.

Participation, consent, confidentiality, intellectual-property restrictions, and organizational policies must be addressed before collecting data.

## Pilot stages

### 1. Baseline and context

Document:
- development context;
- methodology and tooling;
- participant roles;
- selected engineering activity;
- expected work products;
- relevant quality/acceptance criteria;
- whether AI assistance is permitted or used.

### 2. Competency mapping

For the selected activity:
- identify required competencies;
- distinguish implementation from review competencies;
- define observable evidence;
- define acceptance criteria;
- identify measurements that are useful and feasible.

### 3. Activity execution

Record, where permitted:
- activity performed;
- artifact produced;
- AI assistance used;
- human validation performed;
- review findings;
- measurements;
- coaching observations.

Do not collect confidential source code or personal data unless explicitly authorized.

### 4. Evidence-based coaching

The coach:
- reviews permitted evidence;
- identifies recurring or material gaps;
- avoids drawing broad conclusions from a single observation;
- documents a targeted coaching recommendation;
- identifies the competency targeted by the intervention.

### 5. Follow-up observation

Repeat comparable engineering work when feasible and collect the same classes of evidence.

The purpose is to determine whether the framework supports a consistent coaching process, not to manufacture a predetermined outcome.

## Candidate measurements

Depending on context:
- review findings by category;
- defects found before merge/release;
- rework identified during review;
- acceptance-criterion conformance;
- test adequacy indicators;
- review completion time;
- proportion of AI-assisted changes receiving required human validation;
- repeated evidence of independent performance.

Metrics should not be interpreted in isolation.

## Evidence to retain

Where legally and organizationally permitted:
- anonymized activity records;
- competency mappings;
- acceptance criteria;
- review records;
- measurement definitions;
- coaching recommendations;
- participant/observer feedback;
- revisions made to the framework as a result of pilot findings.

## Pilot outputs

A completed pilot should produce:
1. pilot description;
2. version of the framework used;
3. mapping of activities/competencies/evidence;
4. anonymized findings;
5. limitations;
6. framework revisions;
7. evidence supporting any factual claims made about the pilot.

## Experimental design — control and experimental groups

Pilots that test a specific review scenario from the catalog (`review-scenarios-catalog.md`) must define two groups before data collection begins.

**Control group** — applies current review practices without modification. Produces the `Baseline` against which experimental results are compared.

**Experimental group** — adopts one or more scenarios from the catalog. The selected scenario ID must be recorded in the pilot description before the pilot starts.

Assignment criteria, group size, and potential selection biases must be documented. A team too small for parallel groups may run a sequential A/B design (control period first, then experimental period) using the same engineers, provided the period boundary is documented as a variable.

Both groups collect the same metrics. No metric is interpreted in isolation. See `review-scenarios-catalog.md` for the recommended comparison metrics per scenario type.

## Limitations

A small pilot cannot establish industry-wide effectiveness. Results should be reported as context-specific observations unless replicated evidence supports broader conclusions.
