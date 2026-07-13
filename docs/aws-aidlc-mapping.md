# SCVHS and AWS AI-DLC: Complementary Framework Mapping

> This document maps SCVHS phases and concepts to the AWS AI-Driven Life Cycle (AI-DLC) framework.  
> Purpose: establish that SCVHS and AWS AI-DLC address the same problem space from complementary angles,  
> and that engineers trained through SCVHS are effective participants in AI-DLC delivery workflows.

**AWS AI-DLC reference:** https://github.com/awslabs/aidlc-workflows

---

## 1. Framework Summary

### AWS AI-DLC

AWS AI-DLC (AI-Driven Life Cycle) is a production delivery framework that provides adaptive workflow steering rules for AI agents in software engineering teams. It defines three phases:

1. **Inception** — Requirements analysis, user story creation, risk assessment, design review
2. **Construction** — Component design, code generation, quality validation, security checks
3. **Operations** — Deployment automation, production readiness, monitoring

AI-DLC is platform-agnostic: it works with Amazon Q, Cursor, Cline, Claude Code, GitHub Copilot, and other AI coding environments. It emphasizes human-in-the-loop oversight, reproducibility, and audit trails at the team level.

### SCVHS

SCVHS is a mastery methodology for individual engineers operating in AI-native environments. It defines a five-phase pipeline (Specify, Construct, Validate, Harden, Ship) and three operating modes that adapt to the learner's current mastery level. SCVHS focuses on the individual: their comprehension, their ownership, and their ability to direct AI with precision and validate the output with expertise.

---

## 2. The Complementarity Principle

AI-DLC and SCVHS are not competing frameworks. They operate at different levels:

| Dimension | AWS AI-DLC | SCVHS |
|---|---|---|
| **Level** | Team delivery pipeline | Individual mastery and sprint practice |
| **Primary user** | Engineering team, delivery lead | Individual learner, content developer |
| **AI role** | Governed workflow participant (rules-based) | Construction agent directed by learner spec |
| **Specification** | User stories, design docs (team artifacts) | Spec file written by the individual learner |
| **Validation** | Automated quality gates, pipeline checks | Human construct-by-construct reading |
| **Artifact of record** | Verified, auditable deliverable | Decision Log + corrected artifact |
| **Primary concern** | Delivery efficiency, auditability | Comprehension, ownership, mastery |
| **Scope** | Production software delivery | Learning and professional development |

**The key relationship:** An engineer who has trained through SCVHS brings individual competencies that make them a high-quality participant in an AI-DLC delivery workflow.

---

## 3. Phase-Level Mapping

### 3.1 AI-DLC Inception ↔ SCVHS SPECIFY

| AI-DLC Inception | SCVHS SPECIFY |
|---|---|
| Requirements analysis at team level | Specification authored by the individual engineer |
| User story creation (team input) | Spec written by the learner alone |
| Risk assessment | Constraints section of the spec |
| Design review | Acceptance Criteria section |

**What a SCVHS-trained engineer brings to AI-DLC Inception:**
- Disciplined specification habits: they write constraints and acceptance criteria before construction, not after.
- Technology-stack-specific precision: they name constructs, not just features ("a `<section>` element" not "a section").
- Specification-as-contract orientation: they treat the spec as binding, not aspirational.

### 3.2 AI-DLC Construction ↔ SCVHS CONSTRUCT + VALIDATE

| AI-DLC Construction | SCVHS |
|---|---|
| Component design | SPECIFY phase + Comprehension Primitive |
| Code generation (AI agent) | CONSTRUCT phase |
| Quality validation (automated gates) | VALIDATE phase (human, construct by construct) |

**Critical distinction:** AI-DLC's quality validation is primarily automated (linters, tests, security scans). SCVHS's VALIDATE is human, construct-by-construct, against a human-authored spec. These are not the same activity — they complement each other. Automated tests verify behavior; SCVHS VALIDATE verifies comprehension and spec adherence.

**What a SCVHS-trained engineer brings to AI-DLC Construction:**
- The ability to write a precise spec that the AI agent can execute correctly.
- The ability to read AI-generated code construct by construct, not just run it and see if tests pass.
- A trained eye for AI failure patterns (agent failure modes built up across sprints).

### 3.3 AI-DLC Operations ↔ SCVHS HARDEN + SHIP

| AI-DLC Operations | SCVHS |
|---|---|
| Production readiness checks | HARDEN phase (edge cases, security, accessibility, robustness) |
| Deployment automation | SHIP phase (commit with Decision Log, pipeline must pass) |
| Monitoring and observability | Post-SHIP (not in SCVHS scope — operational concern) |

**What a SCVHS-trained engineer brings to AI-DLC Operations:**
- Systematic hardening discipline: they address edge cases and robustness requirements before considering a feature ready to ship.
- A Decision Log that provides the audit trail AI-DLC requires: what was changed, why, what defects were caught and fixed.
- A commit discipline: the Decision Log is committed alongside the artifact, providing traceability from code to design decision.

---

## 4. Artifact Mapping

| SCVHS Artifact | AI-DLC Analog | Notes |
|---|---|---|
| Spec file (`Spec_S0N_*.md`) | User story + design doc | SCVHS spec is more technically precise than a user story; closer to an API contract or design doc |
| Decision Log (`AI_Decision_Log_*.md`) | Code review record + quality gate log | Decision Log is human-authored; AI-DLC quality gates are automated. Both contribute to auditability. |
| Comprehension Primitive (scratch file) | No direct analog | SCVHS-specific learning mechanism; not a production artifact |
| Corrected artifact (committed) | Verified deliverable | Both represent code that has passed review; SCVHS's review is human-authored |
| Commit message convention | Deployment record | SCVHS commits are designed to be meaningful; AI-DLC tracks deployment events |

---

## 5. The Training-to-Production Pipeline

A complete view of how SCVHS and AI-DLC connect in an organization that uses both:

```
[SCVHS Training]                    [AI-DLC Production]
     │                                      │
     ├── Learns to write precise specs ─────┤── Writes user stories and design docs
     ├── Learns to direct AI tools ──────────┤── Participates in AI-DLC Construction
     ├── Learns to validate AI output ───────┤── Performs code review and quality checks
     ├── Learns to harden systematically ────┤── Addresses production readiness checks
     └── Learns to commit with evidence ─────┴── Provides audit trail for AI-DLC
```

Engineers who have trained through SCVHS:
1. Write better specifications (AI-DLC Inception quality improves).
2. Produce better AI-directed construction (Construction phase requires fewer iteration cycles).
3. Catch more defects before they reach automated gates (Construction quality validation is more thorough).
4. Harden more systematically (Operations readiness is better prepared).
5. Provide better audit trails (Decision Log maps to AI-DLC's auditability requirements).

---

## 6. Positioning Statement for Trademark and Registration

SCVHS does not compete with AWS AI-DLC. It fills the gap that AI-DLC leaves open: how individual engineers develop the competency to participate effectively in AI-DLC workflows.

AWS AI-DLC answers: how should a team govern its AI-assisted delivery pipeline?
SCVHS answers: how should an individual engineer build mastery to be a high-quality participant in that pipeline?

The two frameworks are designed for the same engineering world. They are built to coexist and reinforce each other. An organization that adopts AI-DLC for its delivery pipelines and SCVHS for its engineering education program has a coherent, end-to-end approach to AI-native software development.
