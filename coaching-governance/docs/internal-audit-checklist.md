# SECAV-O Internal Audit Checklist

## Purpose

This checklist is designed for use by an internal audit function auditing the SECAV-O software engineering coaching process. Each section corresponds to a defined subprocess of the framework. The auditor requests the listed evidence and marks each criterion as Compliant, Partially Compliant, Non-Compliant, or Not Applicable.

---

## How to use this checklist

1. Confirm the audit scope: which team(s), which cycle(s), which coach(es).
2. Request all listed evidence items before the audit session.
3. Mark each criterion during review of evidence and interviews.
4. Document findings in the Observation column.
5. Aggregate findings by area and escalate material gaps to the Lead Coach or sponsoring governance body.

---

## 1. Team Inception and Launch

**Reference:** `coaching-governance/docs/team-coaching-lifecycle.md` §1, `coaching-governance/docs/coaching-cycle.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 1.1 | Coach participated in or was briefed before the team launch event | Launch or planning meeting record, coach preparation notes | | |
| 1.2 | Institutional and project objectives were communicated to the coach before coaching began | Annual coaching plan, project brief, alignment record | | |
| 1.3 | Quality, review, inspection, and unit-test expectations were established at launch | Team launch coaching plan (`templates/team-launch-coaching-plan.md`) | | |
| 1.4 | AI-assistance and human-validation expectations were communicated to the team at launch | Launch plan, member preparation checklist | | |
| 1.5 | Known project risks were reviewed before coaching objectives were set | Risk register in annual coaching plan | | |

---

## 2. Member Preparation and Onboarding

**Reference:** `coaching-governance/docs/team-coaching-lifecycle.md` §2 and §5, `templates/member-preparation-checklist.md`, `templates/new-member-onboarding.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 2.1 | A preparation activity was conducted for each team member before or during launch | Completed member preparation checklists | | |
| 2.2 | Preparation covered project objectives, risks, quality practices, review expectations, and AI-use rules | Member preparation checklist, onboarding records | | |
| 2.3 | New members joining an active team received a structured onboarding | New-member onboarding records (`templates/new-member-onboarding.md`) | | |
| 2.4 | Each new member received a baseline independent of other members' baselines | Engineer development record, baseline section | | |
| 2.5 | The coaching plan was updated after each new-member onboarding | Updated coaching sprint plan or annual plan | | |

---

## 3. Initial Growth Baseline

**Reference:** `coaching-governance/docs/team-coaching-lifecycle.md` §3, `coaching-governance/docs/coaching-cycle.md`, `templates/engineer-development-record.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 3.1 | A baseline was established for each coached engineer | Engineer development record, baseline section | | |
| 3.2 | The baseline records competency levels for relevant engineering activities using the defined six-level scale | Engineer development record, competency assessment | | |
| 3.3 | The baseline is supported by observable evidence (review records, inspection findings, test results, defect data) | Referenced evidence artifacts, review/inspection records | | |
| 3.4 | The baseline is not used as an isolated performance ranking | Documentation confirms developmental purpose | | |
| 3.5 | The baseline feeds the Annual Coaching Plan and sprint objectives | Traceability from baseline to coaching objectives visible in the plan | | |

---

## 4. Annual Coaching Plan

**Reference:** `templates/annual-coaching-plan.md`, `coaching-governance/docs/institutional-alignment.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 4.1 | An annual coaching plan exists for each coached engineer | Completed annual coaching plan per engineer | | |
| 4.2 | The plan identifies institutional or team objectives that coaching supports | Alignment section of annual coaching plan | | |
| 4.3 | Coaching objectives are developmental, not delivery targets | Objective statements in the plan | | |
| 4.4 | Metrics and evidence sources are defined in the plan | Metrics section of annual coaching plan | | |
| 4.5 | Engineering activities and artifacts to be observed are identified | Observation scope in the plan | | |
| 4.6 | A risk register is included in the plan | Risk section of annual coaching plan | | |
| 4.7 | The plan was reviewed and acknowledged by the coach and, where applicable, the engineer | Acknowledgement or sign-off record | | |

---

## 5. Coaching Sprint Planning

**Reference:** `templates/coaching-sprint-plan.md`, `coaching-governance/docs/coaching-cycle.md` §2

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 5.1 | A sprint plan exists for each coaching sprint | Completed sprint plans per sprint per engineer | | |
| 5.2 | The sprint plan references the annual plan and previous sprint results | Sprint plan, prior sprint retrospective | | |
| 5.3 | Sprint objectives are bounded and linked to specific competencies | Sprint objectives section | | |
| 5.4 | Acceptance criteria and evidence requirements are defined per sprint objective | Sprint plan, acceptance criteria section | | |
| 5.5 | Metrics to be collected during the sprint are specified | Sprint metrics section | | |
| 5.6 | AI-assistance and human-validation requirements are addressed in the sprint scope | Sprint plan, activity list | | |

---

## 6. Evidence Collection and Coaching Interventions

**Reference:** `coaching-governance/docs/coaching-cycle.md` §3–4, `coaching-governance/docs/metrics-model.md`, `templates/engineer-development-record.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 6.1 | Engineering activities and work products were observed during the sprint | Observation notes, review/inspection records | | |
| 6.2 | Defect data was collected and recorded with required dimensions (category, phase injected, phase detected) | Defect log or defect records | | |
| 6.3 | Review and inspection findings were recorded | Peer review records, inspection records | | |
| 6.4 | Unit-test evidence was collected where applicable | Test results, unit-test design review records | | |
| 6.5 | AI-assisted activities were identified and human-validation evidence was recorded | Sprint evidence, validation records | | |
| 6.6 | Coaching interventions were linked to observed gaps or recurring findings | Coaching intervention records in engineer development record | | |
| 6.7 | Coaching observations are distinguished from personal judgments (evidence-before-judgment principle) | Coach notes, assessment records | | |

---

## 7. Sprint Retrospective and Replanning

**Reference:** `templates/sprint-retrospective.md`, `coaching-governance/docs/coaching-cycle.md` §5–6

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 7.1 | A retrospective was conducted at the end of each sprint | Completed sprint retrospective records | | |
| 7.2 | Results were compared against the baseline and sprint objectives | Retrospective, metrics section | | |
| 7.3 | Competency trend was assessed and recorded | Competency trend in engineer development record | | |
| 7.4 | Risks were reviewed in the retrospective | Risk review section of retrospective | | |
| 7.5 | Replanning produced updated objectives, metrics, or interventions for the next sprint | Sprint plan for next sprint, or updates to annual plan | | |
| 7.6 | What worked and what did not were documented | Retrospective lessons section | | |

---

## 8. Risk Management

**Reference:** `coaching-governance/guides/risk-management.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 8.1 | A risk register is maintained in the annual coaching plan | Risk register in annual coaching plan | | |
| 8.2 | Each risk records description, category, probability, impact, owner, and status | Risk register entries | | |
| 8.3 | Preventive and corrective actions are defined for each risk | Risk register, action fields | | |
| 8.4 | Risks are reviewed in every sprint retrospective | Retrospective records, risk review section | | |
| 8.5 | New risks discovered during execution were added to the register | Risk register revision history or dated entries | | |
| 8.6 | Materialized risks have documented corrective actions and updated status | Risk register, closed or materialized entries | | |

---

## 9. Coach Committee Governance (multi-coach organizations)

**Reference:** `coaching-governance/docs/coach-committee.md`, `templates/coach-committee-charter.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 9.1 | A Coach Committee exists and has a documented charter | Coach committee charter | | |
| 9.2 | A Lead Coach is designated with a documented rationale and term | Charter, designation record | | |
| 9.3 | The committee meets at the prescribed cadence (annual planning, each sprint cycle, semi-annual standards review, annual ethics review) | Committee meeting records | | |
| 9.4 | An organizational coaching plan exists that aggregates individual team plans | Organizational coaching plan | | |
| 9.5 | Coach assignments are documented with conflict-of-interest review | Assignment matrix in charter or organizational plan | | |
| 9.6 | Escalations and dissent cases were handled and documented | Escalation records, dissent forms (`templates/quality-planning-dissent-and-escalation.md`) | | |
| 9.7 | The organizational competency view was produced at the end of each cycle | Organizational competency view output | | |

---

## 10. Ethics and Confidentiality

**Reference:** `coaching-governance/docs/coach-code-of-ethics.md`, `templates/coach-ethics-acknowledgement.md`

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 10.1 | Each active coach has signed the ethics acknowledgement for the current cycle | Signed ethics acknowledgement forms | | |
| 10.2 | Coaching evidence is not shared with unauthorized parties | Evidence access controls, distribution records | | |
| 10.3 | Coaches operate within their declared area of competence | Coach profile, assignment records | | |
| 10.4 | Conflicts of interest were disclosed and managed | Disclosure records or committee records | | |
| 10.5 | Metric incentives were reviewed for harmful effects (no single metric used as a standalone proxy) | Metrics section of plans, retrospective records | | |
| 10.6 | Engineers were informed of the objectives, evidence sources, and intended use of coaching information | Member preparation records, onboarding records | | |
| 10.7 | Engineers had an opportunity to provide context or correct factual inaccuracies before assessments became final | Coaching session records, engineer development record | | |
| 10.8 | Ethical escalations were documented and handled | Escalation records, Lead Coach records | | |

---

## 11. Traceability

**Reference:** `coaching-governance/docs/institutional-alignment.md`, `coaching-governance/docs/team-coaching-lifecycle.md` §6

| # | Criterion | Evidence to request | Result | Observation |
|---|---|---|---|---|
| 11.1 | The traceability chain from institutional objective to coaching objective is documented | Annual coaching plan, alignment section | | |
| 11.2 | Coaching objectives trace to specific competencies | Annual plan, sprint plan, engineer development record | | |
| 11.3 | Competencies trace to engineering activities and observable evidence | Engineer development record, sprint plans | | |
| 11.4 | Evidence traces to metrics and retrospective conclusions | Retrospective, metrics comparison | | |
| 11.5 | Competency assessments trace to documented evidence, not to unsupported opinion | Competency assessment fields in engineer development record | | |

---

## Audit summary

| Area | Total criteria | Compliant | Partially compliant | Non-compliant | N/A |
|---|---:|---:|---:|---:|---:|
| 1. Team inception and launch | 5 | | | | |
| 2. Member preparation and onboarding | 5 | | | | |
| 3. Initial growth baseline | 5 | | | | |
| 4. Annual coaching plan | 7 | | | | |
| 5. Sprint planning | 6 | | | | |
| 6. Evidence and interventions | 7 | | | | |
| 7. Retrospective and replanning | 6 | | | | |
| 8. Risk management | 6 | | | | |
| 9. Coach committee governance | 7 | | | | |
| 10. Ethics and confidentiality | 8 | | | | |
| 11. Traceability | 5 | | | | |
| **Total** | **67** | | | | |

---

## Auditor notes

**Audit scope:**

**Audit period:**

**Teams / coaches covered:**

**Auditor:**

**Date:**

**Material findings:**

**Recommendations:**