# SCVHS — Specify, Construct, Validate, Harden, Ship

> A specification-driven methodology for AI-native engineering education and production software delivery.

**Developed by:** NIIT Limited — Instructional Design, AI-Native Engineering Program  
**Version:** 1.0  
**Status:** Methodology Specification (Pre-Registration)  
**License:** Proprietary — NIIT Limited. See [LICENSE](LICENSE).

---

## What Is SCVHS?

SCVHS (pronounced "sciv-us") is a five-phase engineering workflow designed for the era of AI-assisted software development. It defines not just what to build, but **who builds it**, **how comprehension is preserved**, and **what constitutes ownership** when an AI tool does the construction.

The five phases:

| Phase | What happens |
|---|---|
| **Specify** | The engineer writes a precise, testable specification before any code is written. The spec is both the instruction to the AI tool and the validation checklist. |
| **Construct** | The artifact is built — by hand, by an AI tool directed by the spec, or by both — depending on the SCVHS Mode in use. |
| **Validate** | The engineer checks the artifact against the spec construct by construct. Every finding is recorded in the Decision Log. |
| **Harden** | Every defect flagged in the Decision Log is fixed. Edge cases, security, accessibility, and robustness are addressed. |
| **Ship** | The corrected artifact and the completed Decision Log are committed together with a meaningful message. |

SCVHS answers a question the industry has not resolved: **how do engineers maintain mastery, comprehension, and ownership when an AI tool generates most of the code?**

---

## Why SCVHS?

Research shows a measurable comprehension gap when engineers delegate construction to AI without a structured re-engagement protocol:

- AI delegation without re-engagement: **< 40% comprehension retention** (Anthropic, 2026)
- Generate-then-comprehend (structured re-reading + explanation): **65%+ comprehension retention** (Anthropic, 2026)
- Minimal guidance without scaffolding produces worse outcomes than guided discovery (Kirschner, Sweller & Clark, 2006)

SCVHS closes this gap through three mechanisms:
1. **Spec-first design** — forces the engineer to think before directing AI
2. **The Comprehension Primitive** — guarantees reading literacy before validation begins
3. **The Decision Log** — creates an externalized record of understanding, construct by construct

See the full evidence base in the [Research Paper](docs/SCVHS_Research_Paper_v1.docx).

---

## Repository Structure

```
scvhs/
├── README.md                          — this file
├── CONTRIBUTING.md                    — how to contribute to this methodology
├── LICENSE                            — proprietary license
│
├── scvhs-core/                        — methodology specification
│   ├── 00-pipeline.md                 — the five phases in full detail
│   ├── 01-modes.md                    — the three SCVHS modes
│   ├── 02-comprehension-primitive.md  — the Comprehension Primitive concept
│   ├── 03-decision-log.md             — the Decision Log artifact
│   └── 04-scaffolding-progression.md — scaffolding fade across sprints
│
├── scvhs-templates/                   — operational artifacts for learners and content developers
│   ├── Spec_Template.md               — generic specification template
│   ├── AI_Decision_Log_Template.md    — generic Decision Log template
│   └── Sprint_Design_Checklist.md     — checklist for content developers
│
├── scvhs-examples/                    — worked examples by course and technology
│   ├── C04-Web-Applications/          — HTML, CSS, Tailwind, JavaScript
│   │   ├── Spec_S01_Portfolio_Structure.md
│   │   ├── Spec_S02_Portfolio_Stylesheet.md
│   │   ├── Spec_S03_Portfolio_Layout.md
│   │   └── AI_Decision_Log_S01_Example.md
│   ├── C06-Spring-Boot/               — Java, Spring Boot REST APIs
│   │   ├── Spec_S02_Task_API.md
│   │   └── AI_Decision_Log_S02_Example.md
│   └── cross-course-examples.md       — examples across courses (aligned to product note v6)
│
└── docs/                              — research and positioning documents
    ├── SCVHS_Research_Paper_v1.docx   — formal research paper (trademark base)
    ├── terminology-glossary.md        — canonical definitions of all SCVHS terms
    └── aws-aidlc-mapping.md           — SCVHS mapped to AWS AI-DLC
```

---

## Quick Start for Content Developers

**Step 1:** Read [01-modes.md](scvhs-core/01-modes.md) — understand which mode applies to each sprint.

**Step 2:** Read [Sprint_Design_Checklist.md](scvhs-templates/Sprint_Design_Checklist.md) — before designing any sprint.

**Step 3:** Use [Spec_Template.md](scvhs-templates/Spec_Template.md) to write the learner-facing spec for each sprint.

**Step 4:** See [C04-Web-Applications/](scvhs-examples/C04-Web-Applications/) for worked examples at all three mode levels.

---

## Quick Start for Learners

**Before Sprint 1:** Read [terminology-glossary.md](docs/terminology-glossary.md).

**Before each sprint:** Read the Spec file your instructor provides. Note the SCVHS Mode declared in the header — it tells you who constructs and what your role in Validate is.

**During Validate:** Fill your [AI_Decision_Log_Template.md](scvhs-templates/AI_Decision_Log_Template.md) construct by construct. Do not wait until you have read the whole file.

**At Ship:** Commit both the corrected artifact and the completed Decision Log together.

---

## Relationship to AWS AI-DLC

SCVHS and AWS AI-DLC address the same problem from complementary angles:

| | AWS AI-DLC | SCVHS |
|---|---|---|
| **Purpose** | Govern AI agents in production software delivery workflows | Build individual mastery for engineers working with AI tools |
| **Unit of application** | Team-level delivery pipeline | Individual sprint-level practice |
| **Primary user** | Engineering team, delivery lead | Individual learner, content developer |
| **Primary output** | Verified, auditable software deliverables | Mastery + owned artifacts + Decision Log |

An engineer who has trained through SCVHS is prepared to operate effectively within an AWS AI-DLC workflow. See [aws-aidlc-mapping.md](docs/aws-aidlc-mapping.md) for the full mapping.

---

## Trademark and Intellectual Property

SCVHS is a proprietary methodology developed by NIIT Limited. The methodology specification, terminology, templates, and examples in this repository are protected intellectual property.

- **Methodology name:** SCVHS (Specify, Construct, Validate, Harden, Ship)
- **Proprietary terms:** Comprehension Primitive, Decision Log (as used in SCVHS), SCVHS Mode, Scaffolding Fade (as used in SCVHS), Ship-Backward Design
- **Registration status:** Pre-registration — see the [Research Paper](docs/SCVHS_Research_Paper_v1.docx) for priority establishment
- https://zenodo.org/records/20748753

Contact: NIIT Limited, Instructional Design — AI-Native Engineering Program
