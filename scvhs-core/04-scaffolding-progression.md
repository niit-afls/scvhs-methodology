# Scaffolding Progression — How SCVHS Modes Map to Learner Development

> The SCVHS Scaffolding Fade model governs how mode assignments change across a course.
> Grounded in Vygotsky's Zone of Proximal Development and Wood, Bruner & Ross's scaffolding theory.

> **Changed 2026-07-31:** the former Mode 3 (independent spec-writing, no README pointers,
> defects-only Decision Log) is retired. The former Mode 4 (AI-Drafted Spec) is renumbered
> to Mode 3 and now follows Mode 2 directly in the ladder. Mode 3 no longer removes README
> scaffolding or Decision Log depth, both stay identical to Mode 2. The only thing Mode 3
> fades is who authors the spec's first draft.

---

## The Core Principle

**The invariant across all SCVHS modes is cognitive engagement. What fades is scaffolding.**

As a learner progresses through a course:
- The proportion of construction done by hand decreases from Mode 1 to Mode 2
- Who authors the spec's first draft changes from Mode 2 to Mode 3
- The learner's cognitive engagement — specification, evaluation, ownership — remains constant

The scaffold is not the AI tool. The AI tool is the production workflow. The scaffold is the support around the learner's engagement with that workflow, and it fades as mastery grows.

---

## What Fades Across Modes

| Scaffold element | Mode 1 | Mode 2 | Mode 3 |
|---|---|---|---|
| Hand-construction | Full artifact, by hand | Comprehension Primitive only | Comprehension Primitive only |
| Who writes the spec | Learner | Learner | AI tool drafts; learner reviews and finalizes |
| README Constraint/Acceptance-Criteria pointers | Thorough (AI is the subject) | Thorough (tells learner what to check for) | Same as Mode 2 |
| Decision Log depth | All AI constructs: full entry | All constructs: full entry (explain even passing ones) | Same as Mode 2 |
| Construct-by-construct guidance | Implicit in hand-building | Explicit: "explain this, explain that" | Same as Mode 2 |

**What never fades:**
- Specification is always written before construction
- Comprehension Primitive is always written before AI construction (Modes 2–3)
- Decision Log is always produced and committed with the artifact
- All defects are always fixed before SHIP

---

## Progression Within a Course

The mode assignment for a sprint is a function of:
1. How many previous sprints the learner has had in this technology area
2. Whether the learner has previously hand-built this construct type
3. Whether the concept is fundamental enough that a mental model must be earned by hand
4. Whether the learner has shown, through Mode 2 Decision Logs, that they can reliably review a spec, not just write one

A typical course follows this pattern:

### Early sprints (Mode 1)
New technology area. The learner has never written this type of construct. Hand-construction is the primary mode. The AI generates a parallel version used only as a foil for comparison. The README's Constraint and Acceptance Criteria pointers, already written into the spec the learner authored, help the learner know what to check in the AI output.

**Goal:** Build the mental model through writing. Earn the comprehension that will be used in Mode 2 and Mode 3.

### Middle sprints (Mode 2)
The learner has built the foundational mental model but the artifacts have grown too large for full hand-construction within the time budget. AI constructs; the learner explains everything. The README's Constraint and Acceptance Criteria pointers scaffold the learner's attention during Validate.

**Goal:** Extend mental model through reading and explaining at scale. Build both the explain-everything discipline and the spec-writing fluency that Mode 3's review step depends on.

### Later sprints (Mode 3)
The learner has practiced Mode 2 for this technology enough to reliably catch AI-construction defects. An AI tool drafts the spec from the same README pointers; the learner reviews and finalizes it, then directs construction and explains every construct exactly as in Mode 2.

**Goal:** Build the ability to critically review a spec someone (or something) else drafted, a distinct skill from writing one, without losing any of the construct-level ownership Mode 2 already built.

---

## Course-Level Progression: C04 Web Applications (Example)

| Sprint | Technology | Mode | Rationale |
|---|---|---|---|
| 1 | Semantic HTML5 | Mode 1 | First HTML sprint — mental model must be built by writing semantic elements by hand |
| 2 | CSS Box Model + Cascade | Mode 1 | First CSS sprint — specificity must be felt before AI manages it |
| 3 | Tailwind + ShadCN | Mode 2 | Full Tailwind layout is 200+ utility classes — hand-coding unrealistic; but every class must be explainable |
| 4 | Modern JavaScript | Mode 2 | Event loop, closures, scope must be hand-traced; ES6 boilerplate can be AI-generated with explanation |
| 5 | Array methods | Mode 2 | Pipeline methods benefit from hand-tracing one reduce; rest can be AI with explanation |
| 6 | DOM manipulation | Mode 3 | Learner has practiced Mode 2 for HTML (S1) and JavaScript (S4, S5); ready to review a drafted spec instead of writing one from scratch |
| 7 | Fetch API | Mode 3 | Learner has async/await (S4) and DOM (S6) Mode 2 practice; reviews the drafted spec against the README's async-handling pointers |
| 8 | Assessment | Mode 2 or Mode 3 | Fresh brief; whichever mode the learner most recently practiced for this technology; every line explainable on demand |

---

## The Scaffolding Fade Is Not Linear

The mode does not simply tick from 1 to 2 to 3 across all sprints simultaneously. Each technology area has its own scaffolding ladder:

- A learner may be in Mode 3 for HTML (after Sprints 1–2) and Mode 1 for TypeScript (first encounter in a new course).
- Within a sprint, some concept areas may stay at Mode 1 (hand-trace the event loop) while others move to Mode 2 (AI generates the ES6 class structure).
- An assessment sprint can apply Mode 2 or Mode 3 rules (explain every construct on demand) regardless of where other sprints are.

This is by design. The scaffold fades at different rates for different construct types based on when they were first learned and how often they have been practiced.

---

## The Scaffolding Fade for the Content Developer

### Mode 1 → Mode 2 transition: when?
When the learner has hand-built this construct type at least once and the sprint artifact has grown complex enough that hand-construction would consume the entire time budget without leaving time for Validate and Harden.

**Indicator:** The learner can explain what the core construct does without looking it up.

### Mode 2 → Mode 3 transition: when?
When the learner has practiced Mode 2 for this technology area in at least one previous sprint and their Decision Logs show they catch AI-construction defects reliably, evidence they can also catch the equivalent gaps in an AI-drafted spec.

**Indicator:** The learner's Mode 2 Decision Logs show defects caught construct by construct, not just accepted output. Readiness for Mode 3 is about reviewing critically, not about needing less README guidance, the guidance stays the same in both modes.

### Stay in Mode 2: when?
When the technology area is still new enough that the learner needs practice writing the spec themselves before reviewing one is meaningful. When the construct type introduces new security, accessibility, or correctness concerns that warrant extra attention. When the time budget allows for full Decision Log entries either way.

---

## Design Principle: Cognitive Engagement Is the Invariant

Scaffolding fade is about support, not about effort. As mode advances:
- Less hand-construction effort from Mode 1 to Mode 2
- Less spec-authoring effort from Mode 2 to Mode 3
- But: construct-level explanation responsibility never fades, Mode 2 and Mode 3 both require it in full

The cognitive engagement at Mode 3 is not less than at Mode 2. It is differently distributed. At Mode 2, the cognitive load in Specify is in writing a precise spec from README pointers. At Mode 3, the cognitive load in Specify shifts to critically reviewing a spec someone else drafted, a distinct skill, not an easier one; the Validate load (explaining every construct) is identical in both.

This is the cognitive profile of a proficient AI-native engineer: **high specification discipline, whether writing or reviewing, and high construct-level explanation skill, applied consistently regardless of who drafted the spec.**

SCVHS builds this profile through the scaffold progression. Mode 1 builds the foundational mental model. Mode 2 builds spec-writing fluency and the explain-everything discipline. Mode 3 builds the critical-review skill that discipline enables, without ever relaxing it.
