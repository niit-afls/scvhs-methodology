# Spec_S0N_[Short_Title].md

**Author:** [Your name]
**Sprint:** [Number] — [Sprint Title]
**Date:** [Date]
**SCVHS Mode:** [Choose one — see SCVHS Mode Reference below]
**Base:** [What exists before this sprint — previous output file, existing codebase, Figma file, API contract, or "none"]

---

## How to Use This Template

This spec is written in the SPECIFY phase, before you construct anything.
It serves two purposes at once:

1. **Instruction to the AI tool**: Precise enough that the AI can construct the artifact from this spec alone.
2. **Your VALIDATE checklist**: The Acceptance Criteria section IS the list you check the AI output against, construct by construct.

If your spec is vague, the AI output will be unpredictable and hard to validate.
If your acceptance criteria are not testable, you cannot validate objectively.

**If you are new to writing specs and do not know where to start:** check the practice's README
first. It should point you at the specific things this sprint's Constraints and Acceptance Criteria
need to cover, without answering them for you. If the README leaves you staring at a blank page, ask
your content team to add pointers, that is a gap in the practice materials, not something you are
expected to guess. See "Guidance for the practice README" in `Practice_README_Guidance.md` if you
are the one writing that README.

**Standards:**
- Name the technology construct, not just the content. Not "a projects section" — "a `<section>` element containing three `<article>` elements."
- Every acceptance criterion must be a binary pass/fail check, something you can verify with a tool, in a browser, in a terminal, or by reading the code.
- The spec does not need to be long. It needs to be precise.

---

## SCVHS Mode Reference

SCVHS stands for Specify, Construct, Validate, Harden, Ship — the engineering workflow this program runs on. The **mode** tells you who does the Construct phase and what your role is in Validate.

For the full mode specification, see [../scvhs-core/01-modes.md](../scvhs-core/01-modes.md).

---

### Mode 1: Hand-First + Validate AI

**What it means:**
You construct the entire artifact by hand first. Then you give this spec to an AI tool and let it construct the same artifact. You validate the AI output against your spec, document defects in your Decision Log, and discard the AI version. Your hand-built version is what gets shipped.

**Your role in Validate:**
Compare the AI output against your spec construct by construct. The AI version is a foil that shows you what an AI gets wrong so you can recognise it when you direct AI later in the program.

**When it applies:**
New fundamental concept where the mental model must be built by writing. Examples: first time writing semantic HTML, first time writing CSS cascade rules, first time writing a closure.

---

### Mode 2: Hybrid / Generate-then-Explain

**What it means:**
You write this spec. An AI tool constructs the artifact from it. You do NOT hand-build the artifact first. Instead, you read the AI output construct by construct, add an entry to your Decision Log for EVERY construct — passing and failing alike (what it does, why that choice, does it match spec), fix every defect, and ship the corrected AI output.

**Your role in Validate:**
The Decision Log is filled in real time as you read. You own every line before it ships. If you cannot explain a construct, that is a defect. Correct constructs require an explanation entry too — the explaining IS the comprehension activity.

**Comprehension Primitive (required in this mode):**
Before giving the spec to an AI tool, hand-write ONE minimal example of the core construct. This is not the full artifact; it is one small piece that proves you can read the AI output before you validate it. See Section 4.

**When it applies:**
The time budget makes hand-coding the full artifact unrealistic, but the learner must comprehend every line. Examples: full Tailwind responsive layout, complex array pipeline, multi-file Java class hierarchy.

---

### Mode 3: Full SCVHS

**What it means:**
You specify, the AI constructs, you validate, harden, and ship. A Comprehension Primitive still applies — you hand-write one minimal construct before directing the AI, to ensure you can read what it produces.

**Your role in Validate:**
Decision Log filled construct by construct. Defective constructs get a full entry. Passing constructs get a pass recorded without a full explanation. The difference from Mode 2: you are now expected to direct the AI with precision and catch defects without an instructor-provided Agent Failure Modes list.

**When it applies:**
Sprints where the learner has enough mental model to direct an agent and own the output fully. Examples: DOM interaction features, HTTP Fetch integration, REST API endpoints, Docker service definitions.

**Assessment variant:**
In assessment sprints, AI is permitted as a reference tool only. Every line must be explainable and modifiable on demand during the review.

---

## Comprehension Primitive — What It Is

A Comprehension Primitive is a short hand-written piece of code you produce BEFORE giving this spec to an AI tool.

**Why it exists:**
If you have never written a sealed interface, you cannot validate whether the AI's sealed interface is correct. If you have never written a Grid layout, you cannot spot when the AI uses desktop-first breakpoints instead of mobile-first. The Comprehension Primitive closes that gap — not by making you hand-code the entire artifact, but by making you write just enough to read the AI's version with understanding.

**Rules:**
- It is ONE minimal construct, not the full artifact.
- It is written in its own file, or inline in this spec, and committed alongside the spec.
- It takes 10-20 minutes, not more.
- It is a reading aid and a 1-2 shot example for the AI tool, not a graded deliverable on its own,
  but it is still committed code, not a private scratch file.

For the full Comprehension Primitive specification and technology-specific examples, see [../scvhs-core/02-comprehension-primitive.md](../scvhs-core/02-comprehension-primitive.md).

**Quick reference examples by technology:**

| Technology | What to hand-write |
|---|---|
| HTML | One `<article>` with heading, paragraph, and link |
| CSS | One selector with box model properties |
| Tailwind | One 3-column Grid block |
| JavaScript | One closure-based counter |
| TypeScript | One generic function with a type parameter |
| React | One functional component with one prop |
| Java | One sealed interface with one permitted type and one switch arm |
| Spring Boot | One `@GetMapping` method returning a hardcoded response |
| Kafka | One producer sending a string, one consumer logging it |
| Docker | One `FROM` + `COPY` + `CMD` Dockerfile |
| LangChain | One chain with one prompt template and one model call |

---

## 1. Purpose

*One or two sentences. What are you building, and what problem does it solve or what outcome does it produce?*

---

## 2. What to Build

*Describe the artifact in enough detail for an AI tool to construct it from this section alone.*
*Use the sub-section pattern that fits your technology. Delete the ones that do not apply.*

---

### For a UI artifact (HTML / CSS / React / Tailwind / Svelte)

**Sections and layout:**
List each section or component, the element or component type, and its content.

**Visual design values:**
List spacing scale, type scale, colour palette, breakpoints — with specific values.

**Components:**
List named components and their required props or slots.

---

### For a backend artifact (Java class / Spring Boot controller / REST API / SQL schema)

**Class or module name:**

**Responsibilities:**
What this class or module does. What it does NOT do (boundaries matter).

**Methods or endpoints:**
List each method or endpoint — name, input, output, HTTP verb if applicable.

**Dependencies:**
What this construct depends on (other classes, interfaces, databases, APIs).

---

### For infrastructure or config (Dockerfile / docker-compose / CI pipeline / YAML config)

**Service or stage name:**

**What it configures:**
What this file sets up, starts, or defines.

**Key parameters:**
List each parameter — name, type, expected value or range.

**Dependencies:**
What this config depends on (other services, environment variables, secrets).

---

### For an AI or agentic construct (LangChain chain / RAG pipeline / prompt template / agent tool)

**Construct name:**

**What it does:**
Input, processing steps, output.

**Parameters and constraints:**
Model, temperature, max tokens, retrieval top-k, or other tunable values.

**Expected output format:**
What a correct response looks like — structure, type, length.

---

## 3. Constraints

*Rules that apply regardless of whether the output looks or works correctly.*
*These are often where AI fails — it produces something that runs but violates a constraint.*

Examples:
- No magic numbers: all values from the defined scale
- No business logic in the controller layer
- No direct database access from the UI layer
- No `!important` in any stylesheet
- All inputs validated before processing
- All API responses include an error shape for failure cases

*List the constraints that apply to this sprint's technology:*

---

## 4. Comprehension Primitive
*(Required for Hybrid and Full SCVHS modes. Delete this section for Hand-First sprints.)*

Before giving this spec to an AI tool, hand-write ONE minimal example of the core construct in this sprint.

**What to hand-write:**
[Describe the one minimal construct. See the Comprehension Primitive table above for examples by technology]

**File:** `scratch_[name].[ext]`, or inline in this section. Committed alongside this spec, not a
private scratch file, since it also serves as a 1-2 shot example for the AI tool.

---

## 5. Acceptance Criteria
*(This section IS your VALIDATE checklist — use it construct by construct in your Decision Log)*

*Group criteria by concern. Every item must be a binary pass/fail check.*

**[Concern 1 — e.g. Structure / Schema / Configuration]**
- [ ] Criterion one
- [ ] Criterion two

**[Concern 2 — e.g. Behaviour / Output / Response]**
- [ ] Criterion one
- [ ] Criterion two

**[Concern 3 — e.g. Quality / Security / Accessibility / Performance]**
- [ ] Criterion one
- [ ] Criterion two

---

## A note on scope (not a numbered section, delete before shipping)

This document, Sections 1 through 5 above, is what you hand to the AI tool. It should read like a
CLAUDE.md or AGENTS.md: direct instructions to whoever is constructing the code, never a
description of the AI or the workflow in third person, and never a list of what to commit. A "Files
to Commit" checklist belongs in the practice's README (or your own submission notes), not in the
spec itself, since committing is a workflow action a human takes, not a construction instruction
the AI needs.
