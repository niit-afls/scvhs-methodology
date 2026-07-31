# SCVHS Terminology Glossary

> Canonical definitions for all terms used in the SCVHS methodology.  
> When a term is used in a spec, Decision Log, sprint design, or content, its meaning is governed by this document.

---

## Agent Failure Modes (retired 2026-07-31)

Formerly: a separate, content-developer-authored list of the specific mistakes AI code
generation tools typically make for a given technology area, provided alongside the spec
in Mode 1 and Mode 2 sprint designs, tells the learner what to look for before they read
the AI output.

Retired as a standalone artifact: it duplicated work the methodology already requires.
Practice README (below) already instructs content developers to write the README's
Constraint and Acceptance Criteria pointers from their own reference-build defects, the
same pre-researched "what commonly goes wrong" knowledge an Agent Failure Modes list would
contain, delivered through the spec the learner writes instead of a second document. What
now distinguishes Mode 2 from Mode 3 is whether the README gives those pointers at all
(Mode 2: thorough; Mode 3: thin to none), not a separate checklist. See Hand-First +
Validate AI (Mode 1), Hybrid / Generate-then-Explain (Mode 2), and Practice README, below,
for the current mechanism.
Examples for CSS: !important to resolve specificity conflicts, magic numbers instead of a spacing scale, px instead of rem for font sizes.

**Cross-technology failure mode, worth including in nearly every progressive-curriculum sprint
(added 2026-07-27):** the AI tool adds functionality the spec did not ask for, typically something
genuinely good practice in general, exception handling, input validation, pagination, that happens
to be scoped to a later sprint here. This is not the AI being wrong in the usual sense, the code it
adds may work fine, it is the AI ignoring a scope boundary. Catch it by checking the artifact
against the spec's Constraints section (its scope-exclusion rules) as carefully as against
Acceptance Criteria. See Constraints for how to write the spec side of this.

---

## Acceptance Criteria

The section of a Spec file that defines pass/fail tests for the artifact. Each criterion must be:
- Binary (pass or fail — no partial credit in the criterion itself)
- Testable with a specific tool or method
- Derived from the spec constraints, not from general best practice

The Acceptance Criteria IS the VALIDATE checklist. A learner works through it construct by construct.

In standard requirements engineering terms, Acceptance Criteria are black-box: written from the
outside, the user's or tester's perspective, and checked by running the artifact, does it behave
correctly. If a rule can be verified without reading the code, it belongs here, not in Constraints.

Acceptance Criteria states what the artifact must positively do. Constraints (below) states what it
must not do, or must not do yet. Do not put a positive requirement in Constraints or a scope
boundary in Acceptance Criteria, they drive different phases and get conflated easily. See
Constraints for the distinction and for why this specifically matters in a progressive curriculum.

---

## Constraints (clarified 2026-07-27)

The section of a Spec file that states rules the artifact must follow regardless of whether it
otherwise looks or works correctly. Constraints directs CONSTRUCT; Acceptance Criteria (above)
directs VALIDATE. They are not interchangeable, and confusing them is a common content-developer
mistake.

In standard requirements engineering terms (the SRS sense, used at NASA and elsewhere),
Constraints are the limitations and parameters within which the system must operate: technology
mandates, architecture choices, implementation rules. They restrict how something is built, not
what it visibly does, and are frequently checkable only by reading the code, never by running the
program.

This is why a Decision Log checks both Constraints and Acceptance Criteria, not one or the other:
a Constraint violation is often invisible to any runtime test. Reading credentials from an
environment variable instead of hardcoding them, or using `ArrayList` internally despite a
plain-array Constraint, produces code that passes every Acceptance Criterion perfectly, `connect()`
still succeeds, `getStudents()` still returns the right rows, while still violating the spec.
Acceptance Criteria alone cannot catch either defect; that is not redundancy, it is two different
kinds of correctness, checked two different ways.

Constraints are optional, use the section only on merit. Not every artifact has a rule worth
writing down. Write a Constraint when this sprint's artifact actually needs one; do not pad the
section with a constraint invented just to fill it. An omitted Constraints section is correct more
often than a forced one.

Every constraint written must be a testable restriction, checkable pass or fail against the code,
the same standard Acceptance Criteria are already held to. "Keep it simple," "write clean code,"
and "include clear comments" are not constraints: they apply equally to every sprint, are not
specific to this artifact, and a Decision Log entry has no way to check pass or fail against them.
When a constraint like that feels necessary, the fix is to find the specific rule it is standing in
for and write that instead, for example "use a single fixed-size array; do not implement resizing
logic" rather than "keep the implementation simple."

Two kinds of constraint:
1. **How-to rules**, for what IS being built: no magic numbers, no business logic in the controller
   layer, no `!important` in any stylesheet. These shape the implementation of in-scope behavior.
2. **Scope-exclusion rules**, for what must NOT be built at all, even though a generically
   "complete" or "production-ready" version of the artifact would normally include it.

Scope-exclusion rules exist specifically because SCVHS courses teach one construct at a time across
a sequence of sprints. An AI tool asked to construct "a REST endpoint," left unconstrained, will
generate exception handling, input validation, and pagination whether or not those are this
sprint's topic, because that is what a complete endpoint looks like to a general-purpose model. If
those techniques are taught in a later sprint, their unrequested appearance now is not a bonus, it
is a defect: the learner has not built reading literacy for them yet, and the artifact no longer
matches what this sprint is teaching.

Phrase scope-exclusion constraints as explicit negative instructions, naming what to omit and why:
"Do not add exception handling. Introduced in Sprint 4." Not "keep it simple", that is not testable
and an AI tool will not reliably act on it.

Pair a scope-exclusion constraint with a matching Acceptance Criterion whenever the omission itself
needs verifying: "The endpoint contains no try/catch block. Verify by reading the controller
method." An AI tool adding untaught functionality anyway is a real, common Agent Failure Mode
(see that entry), worth naming explicitly in any progressive-curriculum sprint's failure list.

---

## Practice README (locked 2026-07-27)

The learner-facing document for one sprint's practice, separate from the spec. Written by the
content developer, read by the learner before they write their own spec.

Its job for the Specify stage: name the specific Constraints and Acceptance Criteria topics that
sprint's spec must cover, without supplying the answers. A pointer says what to decide ("where the
database credentials come from, and what happens when they are missing"); it never says the
decision itself ("read them from environment variables"). The learner still writes every line of
their own spec.

This exists to solve a real problem without removing the learning: a first-time learner facing a
blank "write your Constraints" instruction often does not know what dimensions matter, and either
gets stuck, or writes a spec that looks complete but never asks the question that would have caught
a real defect. The Practice README closes that gap by naming the dimensions. See
`Practice_README_Guidance.md` for the pattern and a worked example.

What it is not: a place to write the spec's answers, hand the AI tool a workflow narration, or list
files to commit inside the spec itself (that also belongs here, not in the spec, see the Spec
Template's note on scope).

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

Filed as `AI_Decision_Log_S0N_v1.md`. Never edited in place once committed (locked 2026-07-27): a
revision, correcting a mistake, reclassifying a finding after more testing, anything, is saved as a
new file, `_v2.md`, `_v3.md`, and so on, never overwriting a prior version. This keeps every past
finding visible in the file listing itself, rather than something only recoverable by digging
through commit history.

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

The README gives thorough Constraint and Acceptance Criteria pointers, so the learner knows in advance what to check for, already written into the spec they authored from those pointers. The Decision Log requires an explanation of every construct, not just defective ones.

The explain-every-construct requirement is the comprehension mechanism. Even a passing construct requires an entry explaining what it does. This cannot be skipped.

Distinguishing feature from Mode 3 (AI-Drafted Spec, below): who writes the spec's first draft. Construct, Validate, and the Decision Log are identical in both modes.

When to apply: the full artifact is too complex to hand-code in the available time, but the learner must comprehend every line.

---

## SCVHS

Acronym: **S**pecify, **C**onstruct, **V**alidate, **H**arden, **S**hip.

Pronounced: "sciv-us."

A five-phase, mode-adaptive engineering methodology for AI-native software development education and production software delivery. Developed by NIIT Limited, 2026.

The invariant across all modes: the engineer specifies before anything is built, can explain every construct before it ships, and has a documented record of every validation and hardening decision.

---

## SCVHS Mode

The parameter that determines who performs the Specify and Construct phases and what scaffolding is provided in the Validate phase for a given sprint. Declared in the header of every Spec file.

Three modes exist:
- Mode 1: Hand-First + Validate AI
- Mode 2: Hybrid / Generate-then-Explain
- Mode 3: AI-Drafted Spec, see below

Mode is a per-sprint decision, not a per-learner label. A learner may be in Mode 3 for one technology and Mode 1 for another in the same course. Mode 3 is reached after Mode 2 experience in that technology, the same way Mode 2 follows Mode 1; it is a normal ladder rung, not a gated exception.

---

## Scaffolding Fade

The SCVHS model for progressively withdrawing support structures as learner mastery grows. Derived from Vygotsky's Zone of Proximal Development and Wood, Bruner & Ross's scaffolding theory.

In SCVHS, scaffolding fades across two dimensions as mode advances from 1 to 3:
1. Construction support: from full hand-construction (Mode 1) to AI-construction with validation (Modes 2–3).
2. Specify authorship: from learner-authored (Modes 1–2) to AI-drafted and learner-reviewed (Mode 3).

What does not fade between Mode 2 and Mode 3: README Constraint/Acceptance-Criteria pointers stay
thorough in both, and Decision Log depth stays full-entry-per-construct in both. Only Specify
authorship changes.

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
- Structured with a Constraints section when this sprint's artifact needs one (see Constraints,
  above); not every sprint has a constraint worth writing down. Include it only on merit: a
  how-to rule the artifact must follow, or a scope-exclusion rule naming something to leave out.
  An empty or padded Constraints section is worse than an omitted one.
- Written before any code is written.

The spec is normally learner-authored. The one exception is Mode 3 (AI-Drafted Spec), where an AI
tool drafts the spec and the learner reviews and finalizes it before it directs construction; see
below.

---

## AI-Drafted Spec (Mode 3)

The third SCVHS mode. An AI tool drafts the spec from three inputs: the sprint's README, the
generic `Spec_Creation_Prompt.md`, and the raw `Sample_Spec_Template.md`. The learner reviews the
draft, edits it until it is correct, and commits it as their own spec before construction begins.
Construct, Validate, and the Decision Log then follow Mode 2 rules exactly: the AI tool constructs
from the reviewed spec, and the learner writes a full Decision Log entry for every construct,
passing and failing alike.

Mode 3 is a normal ladder rung reached after Mode 2 experience in a technology, the same way Mode 2
follows Mode 1. It is not gated behind any other mode's mastery beyond that; assigned once a
learner's Mode 2 Decision Logs show they reliably catch AI-construction defects, evidence they can
also catch the equivalent gaps in an AI-drafted spec. It is not a substitute for learners who find
spec-writing hard, it removes the writing burden, not the reviewing burden; see Practice README,
above, for why AI drafting the spec still requires the learner to review it critically.

Distinguishing feature from Mode 2: who writes the spec's first draft. Everything downstream of
Specify (Construct, Validate, Decision Log) is identical to Mode 2.

When to apply: the learner has practiced Mode 2 for this technology and their Decision Logs show
they can reliably review AI output, evidence they are ready to reliably review an AI-drafted spec
too.

---

## VALIDATE (Phase 3)

The third SCVHS phase. The engineer reads the constructed artifact against the spec, construct by construct. Every construct gets a full Decision Log entry in Mode 2 and Mode 3 alike, passing and failing constructs both; in Mode 1, entries record what the AI got wrong and what it got right against the learner's own hand-built reference.

Validation is active, not passive. It uses tools: W3C Validator, TypeScript compiler, browser DevTools, Postman, docker build, pytest, etc. "It looks right" is not a validation method.

"I cannot explain what this construct does" is itself a defect, recorded in the Decision Log as a comprehension defect. It must be resolved before HARDEN begins.

---

## Worked Example

A completed sprint example showing all five SCVHS phases for one technology, including a sample Decision Log entry with a specific defect, how it was caught, and the fix applied.

Worked Examples are found in [scvhs-examples/](../scvhs-examples/). They are not templates — they are reference artifacts showing the standard of specificity expected in a SCVHS sprint.
