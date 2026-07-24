# SCVHS Terminology Glossary

> Canonical definitions for all terms used in the SCVHS methodology.  
> When a term is used in a spec, Decision Log, sprint design, or content, its meaning is governed by this document.

---

## Agent Failure Modes

A pre-researched list of the specific mistakes that AI code generation tools typically make when constructing an artifact for a given technology area. Provided by the content developer in Mode 1 and Mode 2 sprint designs. Tells the learner what to look for before they read the AI output.

Removed in Mode 3 — the learner is expected to derive their own validation criteria from the spec.

Examples for HTML: multiple h1 elements, missing lang attribute, div soup (generic divs used instead of semantic elements), non-descriptive link text.
Examples for CSS: !important to resolve specificity conflicts, magic numbers instead of a spacing scale, px instead of rem for font sizes.

---

## Acceptance Criteria

The section of a Spec file that defines pass/fail tests for the artifact. Each criterion must be:
- Binary (pass or fail — no partial credit in the criterion itself)
- Testable with a specific tool or method
- Derived from the spec constraints, not from general best practice

The Acceptance Criteria IS the VALIDATE checklist. A learner works through it construct by construct.

---

## Comprehension Primitive

A short, hand-written minimal example of the core construct type used in a sprint, produced by the learner BEFORE giving the spec to an AI tool in Modes 2 and 3.

Purpose: establishes reading literacy — the minimum mental model needed to evaluate the AI's version, not just recognize it as plausible.

Properties:
- One minimal construct, not the full artifact
- Written in a scratch file or inline in the spec, committed alongside the spec
- Takes 10-20 minutes
- Does not need to be production-grade, but its structural pattern should be right since it also
  serves as a 1-2 shot example for the AI tool
- Kept, not discarded, part of the deliverable set

Theoretical basis: the generation effect (Slamecka & Graf, 1978), schema theory (Rumelhart, 1980), productive failure (Kapur, 2016).

---

## Construct

The unit of review in the VALIDATE and HARDEN phases. One logical unit of the technology in use for this sprint:

| Technology | What counts as one construct |
|---|---|
| HTML | One landmark section, one semantic element, one form |
| CSS | One rule set, one selector group |
| Tailwind | One component's full class set |
| JavaScript | One function, one event handler, one class |
| TypeScript | One interface, one type, one generic function |
| React | One component, one hook |
| Java | One class, one method, one annotation group |
| Spring Boot | One controller class, one endpoint method, one service method |
| Kafka | One producer config, one consumer listener |
| Docker | One Dockerfile, one service in a compose file |
| LangChain | One chain, one prompt template, one tool definition |
| RAG Pipeline | One retriever config, one generation config |
| CI/CD | One pipeline stage |

"Block" is not used in SCVHS because it is ambiguous across technologies (a div block in HTML, a code block in programming). Always use "construct."

---

## Decision Log

A construct-by-construct record of the VALIDATE and HARDEN phases, produced in real time as the learner reads the AI output. Committed to the repository alongside the artifact.

Each entry covers one construct and records:
1. What the construct does (plain English)
2. Whether it matches the spec (Yes / Partial / No)
3. The defect (if Partial or No) — specific, with spec reference
4. How the defect was caught (tool used, method used)
5. The fix applied (exact change made)

The Decision Log is not:
- A code comment
- A test file
- A code review document
- An after-the-fact summary

It is the evidence of comprehension and ownership.

---

## HARDEN (Phase 4)

The fourth SCVHS phase. Every defect flagged in the Decision Log during VALIDATE is fixed in the code. The fix is recorded in the same Decision Log entry as the defect. Hardening also addresses edge cases, security, accessibility, and robustness where specified.

Harden ≠ "fix obvious bugs." Harden = address everything the spec requires, including scenarios that require deliberate testing (empty states, network failures, accessibility at different zoom levels, security inputs).

---

## Hand-First + Validate AI (Mode 1)

The first SCVHS mode. The learner constructs the full artifact by hand. The AI tool then constructs a parallel version from the same spec. The learner validates the AI version, records findings in the Decision Log, and discards the AI version. The learner's hand-built version ships.

The AI version is the foil — it exists to show what AI gets wrong for this technology, building the learner's anticipatory validation skills.

When to apply: first encounter with a fundamental concept where the mental model must be built by writing.

---

## Hybrid / Generate-then-Explain (Mode 2)

The second SCVHS mode. The AI tool constructs the artifact from the learner's spec. The learner reads the AI output construct by construct, writes a Decision Log entry for EVERY construct (passing and failing), and fixes all defects. The corrected AI output ships.

Distinguishing feature from Mode 3: the content developer provides an Agent Failure Modes list. The learner knows in advance what to look for. The Decision Log requires an explanation of every construct, not just defective ones.

The explain-every-construct requirement is the comprehension mechanism. Even a passing construct requires an entry explaining what it does. This cannot be skipped.

When to apply: the full artifact is too complex to hand-code in the available time, but the learner must comprehend every line.

---

## SCVHS

Acronym: **S**pecify, **C**onstruct, **V**alidate, **H**arden, **S**hip.

Pronounced: "sciv-us."

A five-phase, mode-adaptive engineering methodology for AI-native software development education and production software delivery. Developed by NIIT Limited, 2026.

The invariant across all modes: the engineer specifies before anything is built, can explain every construct before it ships, and has a documented record of every validation and hardening decision.

---

## SCVHS Mode

The parameter that determines who performs the Construct phase and what scaffolding is provided in the Validate phase for a given sprint. Declared in the header of every Spec file.

Three modes exist:
- Mode 1: Hand-First + Validate AI
- Mode 2: Hybrid / Generate-then-Explain
- Mode 3: Full SCVHS

Mode is a per-sprint decision, not a per-learner label. A learner may be in Mode 3 for one technology and Mode 1 for another in the same course.

---

## Scaffolding Fade

The SCVHS model for progressively withdrawing support structures as learner mastery grows. Derived from Vygotsky's Zone of Proximal Development and Wood, Bruner & Ross's scaffolding theory.

In SCVHS, scaffolding fades across three dimensions as mode advances from 1 to 3:
1. Construction support: from full hand-construction (Mode 1) to AI-construction with validation (Modes 2–3).
2. Validation support: from instructor-provided Agent Failure Modes list (Modes 1–2) to independently derived criteria (Mode 3).
3. Decision Log depth: from explain-every-construct (Mode 2) to validate-and-flag-defects (Mode 3).

The invariant across all scaffolding levels: cognitive engagement (specification, evaluation, ownership) stays constant.

---

## SHIP (Phase 5)

The fifth SCVHS phase. The corrected artifact and the completed Decision Log are committed to the repository together, with a meaningful commit message.

The commit is not just a file upload. It is the evidence that the engineer:
1. Built or directed the construction of the artifact.
2. Validated it against a spec.
3. Hardened it against every defect found.
4. Can produce a Decision Log that shows all three.

In CI/CD contexts, the pipeline must pass before the commit is merged. The pipeline is not a substitute for the Decision Log — it tests behavior; the Decision Log records human evaluation.

---

## Ship-Backward Design

A curriculum design methodology derived from SCVHS principles. Sprint design begins with the Ship artifact — what the learner will commit, deploy, and demonstrate — and works backward through Validate, Construct, and Specify to define what the learner must know and do.

Ship-Backward Design prevents scope creep and topic-first curriculum design. If a concept is not required to spec, construct, or validate the Ship artifact, it is not taught in this sprint.

The sequence for sprint design:
1. Define the Ship artifact first.
2. Define the VALIDATE checklist (Acceptance Criteria).
3. Define the CONSTRUCT mode and who builds.
4. Define the SPECIFY requirements (what the spec must contain).
5. Define the KNOW requirements — only what is needed to spec and validate the artifact.

---

## SPECIFY (Phase 1)

The first SCVHS phase. The engineer writes a complete, testable specification of the artifact before any construction begins. The spec is both the instruction to the AI tool and the VALIDATE checklist.

A SPECIFY output (a Spec file) must be:
- Precise enough to direct an AI tool to construct the artifact with no additional instruction.
- Structured with an Acceptance Criteria section containing only binary pass/fail checks.
- Written before any code is written.

---

## Full SCVHS (Mode 3)

The third SCVHS mode. The AI tool constructs the artifact from the learner's spec. The learner validates construct by construct but only writes full Decision Log entries for defective constructs (passing constructs get a pass recorded, not a full explanation). No Agent Failure Modes list is provided — the learner derives their own validation criteria from the spec.

This is the production engineering mode. It is the way a proficient engineer using AI tools works in industry.

Distinguishing feature from Mode 2: the removal of the Agent Failure Modes list is the key scaffold removal. The learner must know what to look for without being told.

When to apply: the learner has sufficient mental model from previous sprints to direct AI with precision and independently catch defects without a pre-supplied checklist.

---

## VALIDATE (Phase 3)

The third SCVHS phase. The engineer reads the constructed artifact against the spec, construct by construct. Every construct gets an entry in the Decision Log (Mode 2) or a pass/fail record (Mode 3, with full entries for defects only).

Validation is active, not passive. It uses tools: W3C Validator, TypeScript compiler, browser DevTools, Postman, docker build, pytest, etc. "It looks right" is not a validation method.

"I cannot explain what this construct does" is itself a defect, recorded in the Decision Log as a comprehension defect. It must be resolved before HARDEN begins.

---

## Worked Example

A completed sprint example showing all five SCVHS phases for one technology, including a sample Decision Log entry with a specific defect, how it was caught, and the fix applied.

Worked Examples are found in [scvhs-examples/](../scvhs-examples/). They are not templates — they are reference artifacts showing the standard of specificity expected in a SCVHS sprint.
