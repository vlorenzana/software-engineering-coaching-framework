# SECAV-O to CMMI Dev Mapping

## Purpose

This document maps the SECAV-O software engineering coaching framework processes and artifacts to CMMI for Development (CMMI-DEV) practice areas. It is intended for organizations that operate under CMMI-DEV and want to demonstrate how their SECAV-O coaching processes contribute to CMMI compliance, or for auditors conducting CMMI appraisals who need to locate coaching-related evidence.

The mapping references CMMI-DEV v2.0 practice area names.

---

## Coverage overview

| CMMI-DEV Practice Area | Abbr. | SECAV-O coverage |
|---|---|---|
| Organizational Training | OT | Primary — coaching cycle, competency model, baseline, evidence |
| Organizational Process Focus | OPF | Primary — retrospectives, improvements, Coach Committee |
| Organizational Process Definition | OPD | Primary — framework standards, templates, competency scale |
| Measurement and Analysis | MA | Primary — metrics model, sprint metrics, defect data |
| Process Quality Assurance | PQA | Supporting — ethics, evidence criteria, audit checklist |
| Project Monitoring and Control | PMC | Supporting — sprint planning, risk review, retrospective |
| Risk Management | RSKM | Supporting — coaching risk register, sprint risk review |
| Verification | VER | Supporting — code review, peer review, formal inspection |
| Peer Reviews | PR | Primary — peer review guides, inspection guide, review records |

---

## 1. Organizational Training (OT)

OT focuses on developing the skills and knowledge of staff. SECAV-O implements this as a structured, evidence-based engineering coaching cycle.

| CMMI-DEV OT Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **OT 1.1** Establish the strategic training needs of the organization | Institutional alignment model traces coaching objectives to organizational objectives (quality, defect reduction, secure development, etc.) | `coaching-governance/docs/institutional-alignment.md`, Annual coaching plan §Alignment |
| **OT 1.2** Determine which training needs are the organization's responsibility | Coach Committee generates organizational coaching plan; assigns coaches to teams; identifies cross-team competency gaps | `coaching-governance/docs/coach-committee.md`, organizational coaching plan |
| **OT 1.3** Establish an organizational training plan | Annual coaching plan per engineer; organizational coaching plan at committee level | `templates/annual-coaching-plan.md`, coach committee organizational plan |
| **OT 1.4** Provide the necessary training | Coaching sprints, coaching interventions, peer review participation, inspection, unit-test review, project kickoff alignment | `templates/coaching-sprint-plan.md`, `coaching-governance/guides/` |
| **OT 1.5** Establish and maintain records of training | Engineer development record (longitudinal record per engineer per competency, with evidence references) | `templates/engineer-development-record.md` |
| **OT 1.6** Assess the effectiveness of training | Sprint retrospective compares competency results against baseline and sprint objectives; competency trend is recorded longitudinally | `templates/sprint-retrospective.md`, competency trend in development record |

---

## 2. Organizational Process Focus (OPF)

OPF focuses on planning, implementing, and deploying process improvements.

| CMMI-DEV OPF Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **OPF 1.1** Establish and maintain the description of the process needs and objectives of the organization | Institutional alignment model maps organizational engineering objectives to coaching objectives and competencies | `coaching-governance/docs/institutional-alignment.md` |
| **OPF 1.2** Appraise the organization's processes to maintain an understanding of their strengths and weaknesses | Sprint retrospective reviews coaching and engineering process effectiveness; Coach Committee semi-annual standards review | `templates/sprint-retrospective.md`, committee meeting records |
| **OPF 1.3** Identify improvements to the organization's processes | Retrospective §what worked / what did not; replanning produces adjusted interventions; committee standards review updates templates | Retrospective improvement sections, updated templates |
| **OPF 2.1** Establish process action plans | Replanning produces updated sprint plans with specific actions; risk register corrective actions | `templates/coaching-sprint-plan.md`, risk register |
| **OPF 2.2** Implement process action plans | Coaching interventions are executed and recorded in the engineer development record | Engineer development record, intervention records |
| **OPF 2.3** Deploy organizational process assets and incorporate lessons learned | Coach Committee maintains templates and competency scale; disseminates updated standards to all coaches; retrospective lessons propagate to next sprint | Coach committee charter, updated guides and templates |

---

## 3. Organizational Process Definition (OPD)

OPD focuses on establishing and maintaining a usable set of organizational process assets.

| CMMI-DEV OPD Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **OPD 1.1** Establish and maintain the organization's set of standard processes | SECAV-O framework defines the standard coaching process, subprocesses, templates, guides, and acceptance criteria | `coaching-governance/docs/`, `coaching-governance/guides/`, `templates/` |
| **OPD 1.2** Establish and maintain descriptions of life cycle models | Coaching lifecycle (team inception → baseline → annual plan → sprints → retrospective → replanning → new-member onboarding) | `coaching-governance/docs/team-coaching-lifecycle.md`, `coaching-governance/docs/coaching-cycle.md` |
| **OPD 1.3** Establish and maintain the organization's tailoring criteria and guidelines | Incremental adoption guide describes how organizations tailor the framework to their context | `coaching-governance/guides/incremental-adoption.md` |
| **OPD 1.4** Establish and maintain the organization's measurement repository | Metrics model defines dimensions, derived measures, and evidence categories; development records accumulate longitudinal data | `coaching-governance/docs/metrics-model.md`, engineer development records |
| **OPD 1.5** Establish and maintain the organization's process asset library | Framework repository: guides, templates, ontology, glossary, examples | All files under `coaching-governance/`, `templates/`, `examples/` |
| **OPD 1.6** Establish and maintain work environment standards | Design documentation standards, code review best practices, peer review guide, formal inspection guide | `coaching-governance/guides/design-documentation-standards.md`, `coaching-governance/guides/code-review-best-practices.md`, `coaching-governance/guides/formal-inspections.md` |

---

## 4. Measurement and Analysis (MA)

MA focuses on developing and sustaining a measurement capability for management decision support.

| CMMI-DEV MA Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **MA 1.1** Establish measurement objectives | Coaching objectives include specific measurement targets (baseline value, sprint target, evidence source) aligned to institutional objectives | Annual coaching plan, sprint plan metrics sections |
| **MA 1.2** Specify measures | Metrics model defines defect metrics, review metrics, unit-test metrics, and competency-growth metrics with required dimensions | `coaching-governance/docs/metrics-model.md` |
| **MA 1.3** Specify data collection and storage procedures | Sprint plan specifies which activities and artifacts to observe; engineer development record is the longitudinal storage | Sprint plan, engineer development record |
| **MA 1.4** Specify analysis procedures | Metrics model specifies derived measures; retrospective compares actuals against baseline; trend analysis is documented in development record | `coaching-governance/docs/metrics-model.md`, sprint retrospective |
| **MA 2.1** Collect measurement data | Evidence collected during sprint: defect records, review/inspection records, unit-test results, competency observations | Sprint evidence, engineer development record §Evidence |
| **MA 2.2** Analyze measurement data | Sprint retrospective analyzes metrics against baseline targets; interprets trends with context (task complexity, AI assistance, etc.) | Sprint retrospective, metrics comparison section |
| **MA 2.3** Store data and results | Engineer development record maintains longitudinal evidence and competency trend | `templates/engineer-development-record.md` |
| **MA 2.4** Communicate results | Retrospective conclusions are shared with engineer; Coach Committee aggregates organizational view | Retrospective, organizational competency view |

---

## 5. Process Quality Assurance (PQA)

PQA focuses on providing objective insight into the performance of processes and associated work products.

| CMMI-DEV PQA Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **PQA 1.1** Objectively evaluate processes against applicable process descriptions, standards, and procedures | Internal audit checklist (`coaching-governance/docs/internal-audit-checklist.md`) provides objective criteria for evaluating coaching process compliance | Internal audit checklist, audit findings |
| **PQA 1.2** Objectively evaluate work products against applicable process descriptions, standards, and procedures | Evidence in engineer development records must trace to observable artifacts, review records, and acceptance criteria — not to unsupported opinion (evidence-before-judgment principle) | Engineer development record, competency assessment evidence |
| **PQA 2.1** Communicate and ensure resolution of noncompliance issues | Quality-planning dissent and escalation process; Lead Coach escalation chain; Coach Committee extraordinary sessions | `templates/quality-planning-dissent-and-escalation.md`, escalation records |
| **PQA 2.2** Establish and maintain records of quality assurance activities | Audit findings, committee meeting records, ethics acknowledgement records | Audit records, committee records, acknowledgement forms |

---

## 6. Project Monitoring and Control (PMC)

PMC focuses on providing an understanding of project progress. SECAV-O sprint governance maps to PMC at the coaching plan level.

| CMMI-DEV PMC Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **PMC 1.1** Monitor actual values of project planning parameters against the project plan | Sprint retrospective compares actual results against baseline and sprint-plan targets | Sprint retrospective, metrics comparison |
| **PMC 1.2** Monitor commitments against those identified in the project plan | Sprint plan defines coaching commitments; retrospective assesses completion | Sprint plan, retrospective |
| **PMC 1.3** Monitor risks against those identified in the project plan | Risk review section of every sprint retrospective reviews probability, impact, status, and actions | Sprint retrospective §risk review, risk register |
| **PMC 1.4** Monitor the involvement of relevant stakeholders as planned | Coach Committee governance confirms coach assignments and cross-team visibility; Lead Coach manages escalations | Coach committee records, assignment matrix |
| **PMC 1.7** Periodically review the project's progress, performance, and issues | Sprint retrospective is a structured periodic review; annual coaching plan is reviewed at the planning session | Retrospective, annual plan review records |
| **PMC 2.1** Analyze issues and determine corrective actions | Retrospective §what did not work; replanning produces corrective actions; risk corrective actions | Retrospective, updated sprint plans, risk register |
| **PMC 2.2** Take corrective actions on identified issues | Coaching interventions and updated sprint plans implement corrective actions | Coaching intervention records, updated plans |

---

## 7. Risk Management (RSKM)

| CMMI-DEV RSKM Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **RSKM 1.1** Determine risk sources and categories | Risk model defines risk categories: evidence, quality, dependency, confidentiality, metric incentives, AI-validation, ethics | `coaching-governance/guides/risk-management.md` |
| **RSKM 1.2** Define the parameters used to analyze and categorize risks | Probability and impact scales defined (Low/Medium/High); optional numeric mapping | `coaching-governance/guides/risk-management.md` §Suggested scales |
| **RSKM 1.3** Establish and maintain a risk management strategy | Risk register is maintained in the annual coaching plan; reviewed every sprint | Annual coaching plan §risk, `coaching-governance/guides/risk-management.md` |
| **RSKM 2.1** Identify and document risks | Risk register entries with ID, description, category, cause, probability, impact, owner | Annual coaching plan risk register |
| **RSKM 2.2** Evaluate, categorize, and prioritize risks | Probability × impact priority field; retrospective updates assessments | Risk register, sprint retrospective |
| **RSKM 3.1** Develop risk mitigation plans | Preventive and corrective actions defined per risk, with owner and linkage to coaching objectives | Risk register, preventive/corrective action fields |
| **RSKM 3.2** Implement risk mitigation plans | Actions are tracked and reviewed in every retrospective; status updated (open, mitigated, materialized, closed) | Retrospective §risk review, risk status field |

---

## 8. Verification (VER) and Peer Reviews (PR)

SECAV-O provides structured guides for engineering verification activities. These are coaching topics and evidence sources, not only CMMI process support.

| CMMI-DEV Practice | SECAV-O implementation | Artifacts |
|---|---|---|
| **VER 1.1** Select work products to be verified | Sprint plan identifies which work products (code, design, requirements, unit tests) will be reviewed or inspected | Sprint plan §activity scope |
| **VER 2.1** Establish and maintain the environment needed for verification | Review and inspection guides define the environment, roles, entry/exit criteria, and evidence format | `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md` |
| **VER 3.1** Perform peer reviews | Peer review guide provides a structured process; coaching tracks engineer participation and findings | `coaching-governance/guides/peer-review-sessions.md`, review records |
| **PR 1.1** Plan peer reviews | Sprint plan includes peer reviews as coaching evidence activities; kickoff alignment guide establishes review expectations | Sprint plan, `coaching-governance/guides/project-kickoff-alignment.md` |
| **PR 1.2** Conduct peer reviews | Structured peer review process with defined roles, checklists, and finding records | `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/code-review-best-practices.md` |
| **PR 1.3** Analyze data from peer reviews | Review findings feed defect metrics, competency assessment, and retrospective analysis | Review records, sprint retrospective, `coaching-governance/docs/metrics-model.md` §2 |

---

## Evidence cross-reference: CMMI appraisal artifact locator

| CMMI Practice Area | Primary SECAV-O artifact(s) |
|---|---|
| OT | `templates/annual-coaching-plan.md`, `templates/engineer-development-record.md`, `templates/sprint-retrospective.md` |
| OPF | `templates/sprint-retrospective.md`, coach committee meeting records, updated templates and guides |
| OPD | `coaching-governance/docs/`, `coaching-governance/guides/`, `templates/`, `coaching-governance/glossary/glossary.md` |
| MA | `coaching-governance/docs/metrics-model.md`, sprint plan metrics, `templates/engineer-development-record.md` |
| PQA | `coaching-governance/docs/internal-audit-checklist.md`, audit records, `templates/coach-ethics-acknowledgement.md` |
| PMC | `templates/coaching-sprint-plan.md`, `templates/sprint-retrospective.md`, risk register |
| RSKM | Annual coaching plan §risk register, `coaching-governance/guides/risk-management.md`, retrospective §risk review |
| VER / PR | `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md`, review records |

---

## Notes for appraisers

1. **Evidence is longitudinal.** SECAV-O evidence accumulates across sprints in the engineer development record. Single-sprint snapshots may not reflect the full pattern; appraisers should request records across at least two sprint cycles.

2. **Metrics require context.** The metrics model explicitly prohibits using a single metric as a standalone judgment. Appraisers should expect to see metrics paired with interpretation notes (context, task complexity, AI assistance).

3. **Coaching vs. performance management.** SECAV-O explicitly distinguishes coaching from formal personnel evaluation. If an organization uses coaching records in personnel decisions, that use should be disclosed and governed separately (Code of Ethics §9).

4. **Tailoring is expected.** The incremental adoption guide allows organizations to start with a subset of practices. Absence of a practice may reflect planned tailoring rather than non-compliance. Auditors should confirm the tailoring rationale is documented.