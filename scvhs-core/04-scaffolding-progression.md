# Scaffolding Progression — How SCVHS Modes Map to Learner Development

> The SCVHS Scaffolding Fade model governs how mode assignments change across a course.  
> Grounded in Vygotsky's Zone of Proximal Development and Wood, Bruner & Ross's scaffolding theory.

---

## The Core Principle

**The invariant across all SCVHS modes is cognitive engagement. What fades is scaffolding.**

As a learner progresses through a course:
- The proportion of construction done by hand decreases
- The scaffolding provided in Validate decreases
- The depth of explanation required in the Decision Log changes
- But the learner's cognitive engagement — specification, evaluation, ownership — remains constant

The scaffold is not the AI tool. The AI tool is the production workflow. The scaffold is the support around the learner's engagement with that workflow, and it fades as mastery grows.

---

## What Fades Across Modes

| Scaffold element | Mode 1 | Mode 2 | Mode 3 |
|---|---|---|---|
| Hand-construction | Full artifact, by hand | Comprehension Primitive only | Comprehension Primitive only |
| Agent Failure Modes list | Provided (AI is the subject) | Provided (tells learner what to look for) | Not provided (learner derives independently) |
| Decision Log depth | All AI constructs: full entry | All constructs: full entry (explain even passing ones) | Defects only: full entry; passing: pass recorded |
| Construct-by-construct guidance | Implicit in hand-building | Explicit: "explain this, explain that" | Implicit: "validate against spec" |

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

A typical course follows this pattern:

### Early sprints (Mode 1)
New technology area. The learner has never written this type of construct. Hand-construction is the primary mode. The AI generates a parallel version used only as a foil for comparison. The Agent Failure Modes list helps the learner know what to check in the AI output.

**Goal:** Build the mental model through writing. Earn the comprehension that will be used in Mode 3.

### Middle sprints (Mode 2)
The learner has built the foundational mental model but the artifacts have grown too large for full hand-construction within the time budget. AI constructs; the learner explains everything. The Agent Failure Modes list scaffolds the learner's attention during Validate.

**Goal:** Extend mental model through reading and explaining at scale. Build the explain-everything discipline that Mode 3 trusts.

### Late sprints (Mode 3)
The learner has sufficient mental model and has practiced Mode 2 validation enough to independently derive what to look for. AI constructs; the learner validates against spec and owns the output.

**Goal:** Production engineering mode. Validate and own AI-constructed code without a checklist.

---

## Course-Level Progression: C04 Web Applications (Example)

| Sprint | Technology | Mode | Rationale |
|---|---|---|---|
| 1 | Semantic HTML5 | Mode 1 | First HTML sprint — mental model must be built by writing semantic elements by hand |
| 2 | CSS Box Model + Cascade | Mode 1 | First CSS sprint — specificity must be felt before AI manages it |
| 3 | Tailwind + ShadCN | Mode 2 | Full Tailwind layout is 200+ utility classes — hand-coding unrealistic; but every class must be explainable |
| 4 | Modern JavaScript | Mode 2 | Event loop, closures, scope must be hand-traced; ES6 boilerplate can be AI-generated with explanation |
| 5 | Array methods | Mode 2 | Pipeline methods benefit from hand-tracing one reduce; rest can be AI with explanation |
| 6 | DOM manipulation | Mode 3 | Learner has HTML (S1) + JavaScript (S4) mental model; can derive DOM defects independently |
| 7 | Fetch API | Mode 3 | Learner has async/await (S4) and DOM (S6) — can validate API integration independently |
| 8 | Assessment | Mode 3 variant | Fresh brief; AI as reference only; every line explainable on demand |

---

## Mode 4 Sits Outside This Ladder

Modes 1 through 3 are a single ladder: the fade happens within CONSTRUCT and VALIDATE, and every learner is expected to climb it for every technology area over the course of a program.

Mode 4 (AI-Drafted Spec) is not the next rung. It fades a different phase, SPECIFY, and it is not something every learner is expected to reach. It is available only after a learner has already earned Mode 3 independence for a technology, and only when a content developer or instructor deliberately opts a sprint into it, typically an advanced or capstone track where directing AI-assisted spec drafting is itself the skill being taught. Most learners should finish a course still in Mode 3 for most technology areas, never having used Mode 4 at all; that is not a gap, it is the expected outcome. See [01-modes.md](01-modes.md) for the full Mode 4 specification.

---

## The Scaffolding Fade Is Not Linear

The mode does not simply tick from 1 to 2 to 3 across all sprints simultaneously. Each technology area has its own scaffolding ladder:

- A learner may be in Mode 3 for HTML (after Sprints 1–2) and Mode 1 for TypeScript (first encounter in a new course).
- Within a sprint, some concept areas may stay at Mode 1 (hand-trace the event loop) while others move to Mode 2 (AI generates the ES6 class structure).
- An assessment sprint can apply Mode 3 rules (own the output, explain on demand) regardless of where other sprints are.

This is by design. The scaffold fades at different rates for different construct types based on when they were first learned and how often they have been practiced.

---

## The Scaffolding Fade for the Content Developer

### Mode 1 → Mode 2 transition: when?
When the learner has hand-built this construct type at least once and the sprint artifact has grown complex enough that hand-construction would consume the entire time budget without leaving time for Validate and Harden.

**Indicator:** The learner can explain what the core construct does without looking it up.

### Mode 2 → Mode 3 transition: when?
When the learner has practiced Mode 2 validation for this technology area in at least one previous sprint and can write a spec precise enough to direct AI without additional guidance.

**Indicator:** The learner does not need the Agent Failure Modes list to find defects — they spot them on their own during Mode 2 validation.

### Stay in Mode 2: when?
When the technology area is still new enough that the learner needs the explain-everything discipline. When the construct type introduces new security, accessibility, or correctness concerns that warrant extra attention. When the time budget allows for full Decision Log entries.

---

## Design Principle: Cognitive Engagement Is the Invariant

Scaffolding fade is about support, not about effort. As mode advances:
- Less hand-construction effort
- Less scaffolded validation
- But: more responsibility for independent specification
- More responsibility for independent defect identification
- More responsibility for production-grade hardening

The cognitive engagement at Mode 3 is not less than at Mode 1. It is differently distributed. At Mode 1, the cognitive load is in construction (writing code). At Mode 3, the cognitive load is in specification (writing a precise spec that directs AI correctly) and independent validation (catching defects without a checklist).

This is the cognitive profile of a proficient AI-native engineer: **high specification discipline, high independent validation skill, fast and accurate construction via AI direction.**

SCVHS builds this profile through the scaffold progression. Mode 1 builds the foundational mental model. Mode 2 builds the reading and explanation discipline. Mode 3 builds the independent ownership and validation skill that the profession requires.
