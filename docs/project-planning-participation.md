# Project Planning Participation, Quality Advocacy, Dissent and Escalation

## Purpose

SECAV-O treats the coach as an active participant in project planning rather than as a downstream observer. The coach should be involved early enough to influence the engineering plan, especially the planning of quality activities that generate review evidence and protect technical outcomes.

The recommended governance model gives the coach a defined voice in planning decisions and, where the organization grants it, a formal vote on decisions that materially affect engineering quality, competency development, verification, validation, and the collection of evidence needed for coaching.

SECAV-O does **not** assume that every organization gives a coach unilateral veto authority. The organization's governance model must define the coach's actual decision rights. At minimum, the coach should have a documented right to raise a quality-planning concern, record formal dissent when a material quality activity is omitted without adequate rationale, and escalate the concern through the project's management chain when necessary.

## Planning participation

The coach should participate in project inception, launch, release planning, milestone planning, sprint/release planning, or an equivalent planning forum whenever decisions affect:

- requirements and requirements review;
- architecture and design review;
- peer review and structured code inspection;
- unit-test design, execution and review;
- integration, system, security and acceptance testing;
- defect prevention, defect detection and escape analysis;
- AI-assisted development controls and accountable human validation;
- technical-debt controls;
- evidence and metrics needed to evaluate engineering and competency growth;
- time and capacity allocated for coaching and quality improvement.

## Quality-planning expectation

A project plan should explicitly identify the quality activities appropriate to its risk profile. SECAV-O does not mandate the same ceremony for every project. It does require that omissions of material quality activities be conscious, risk-informed and documented.

For each applicable quality activity, planning should identify at least:

1. activity and objective;
2. responsible role(s);
3. work product or artifact to be reviewed/tested;
4. entry/exit or acceptance criteria;
5. planned timing and capacity;
6. evidence to be retained;
7. related risks and preventive controls;
8. metrics or observations, when useful.

## Coach concern and formal dissent

The coach may raise a `QualityPlanningConcern` when a planning decision may materially reduce the ability to prevent, detect or learn from defects, or may undermine competency development or accountable human validation.

Examples include:

- no design review for a high-risk component;
- no peer review or inspection for critical code;
- inadequate unit-test planning;
- schedule compression that removes agreed quality gates;
- AI-generated or AI-modified work being accepted without appropriate human validation;
- quality activities being planned but with no accountable owner or usable acceptance criteria.

A concern should state the evidence, the quality activity affected, the risk created, the recommended alternative and the decision owner. If the concern is not resolved and the coach concludes the residual risk is material, the coach may record a `FormalDissent`.

Formal dissent is not a personal objection. It is a traceable professional-quality record based on engineering evidence, risk and the coach's ethical duty to distinguish observation from opinion.

## Escalation path

If a material concern remains unresolved, the coach should follow the organization's defined escalation path. A typical sequence is:

Project / Team Planning Forum -> Project Manager or Engineering Lead -> Quality / Engineering Manager -> Program or Delivery Management -> Director / Executive Sponsor

The actual path is organization-specific. Escalation should be proportional to risk and should not bypass normal governance without reason.

Each escalation record should capture:

- original planning decision;
- quality activity or control at issue;
- evidence and risk assessment;
- probability and impact;
- coach recommendation;
- response received;
- residual risk;
- level escalated to;
- final decision and rationale;
- whether the risk was accepted, mitigated, deferred or rejected;
- follow-up date and outcome.

## Retrospective follow-up

Planning concerns, formal dissents and escalations should be reviewed in relevant retrospectives. The retrospective should ask whether the decision produced the expected outcome, whether defects escaped into later phases, whether quality evidence was sufficient, and whether future planning rules should change.

This connects governance to the SECAV-O improvement loop:

Planning Decision -> Quality Concern -> Risk Assessment -> Preventive Action / Alternative -> Decision -> Evidence -> Retrospective -> Replanning

## Ethical safeguards

The coach should:

- advocate for quality without misrepresenting authority;
- use evidence and risk rather than status or personal preference;
- respect confidentiality and decision ownership;
- document unresolved material concerns honestly;
- avoid retaliation, humiliation or coercion;
- escalate proportionally and through the defined governance path;
- distinguish a professional dissent from a personal disagreement;
- accept a documented management risk decision when it falls within lawful organizational authority, while preserving the technical record.

## Claim boundary

This governance model defines a recommended coaching practice. It does not grant legal or managerial authority by itself, does not establish a universal veto right, and does not require every organization to use the same planning structure. Decision rights and escalation paths must be established by the adopting organization.
