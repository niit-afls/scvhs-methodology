# SCVHS Modes — The Three Operating Modes

> The SCVHS mode determines who performs the Construct phase and what scaffolding exists in Validate.  
> Mode is a per-sprint decision declared in the header of every Spec file.

---

## The Three Modes

| Mode | Name | Who constructs | Key scaffold in Validate |
|---|---|---|---|
| 1 | Hand-First + Validate AI | Learner by hand | AI version is the foil; instructor provides Agent Failure Modes list |
| 2 | Hybrid / Generate-then-Explain | AI tool | Instructor provides Agent Failure Modes list; learner explains every construct |
| 3 | Full SCVHS | AI tool | No Agent Failure Modes list; learner validates against spec independently |

The workflow steps are **identical** in all three modes: Specify → Construct → Validate → Harden → Ship.  
The difference is not the steps — it is the scaffolding and the level of independence.

---

## Mode 1: Hand-First + Validate AI

### Summary
You build it first. Then AI builds the same thing. You compare and document what AI got wrong.

### Construction
The learner constructs the full artifact by hand, from the spec, without AI assistance. This is the primary construction. The hand-built version is the known-correct reference.

After hand-construction is complete, the same spec is given to an AI tool. The AI constructs a parallel version. The AI version is the **foil** — it is used only for comparison and is discarded after validation.

### Validate activity
The learner validates the AI output against the spec, construct by construct. Because the learner has already built the correct version themselves, they have an independent standard. They are not asking "is this correct?" — they know the correct answer. They are asking "what did the AI do differently, and why is that a defect?"

The Decision Log records:
- What the AI got wrong (with spec reference)
- How the learner caught it
- What the correct version looks like (no fix needed in the code — learner's hand-built version is already correct)
- What the AI got right (equally important — builds awareness of AI strengths)

### Scaffolding provided
The content developer provides an **Agent Failure Modes list** in the sprint design — a pre-researched list of mistakes AI tools typically make for this technology. This tells the learner what to look for before they read the AI output.

### What ships
The learner's hand-built artifact. The AI version is committed for comparison only.

### When to apply
- First encounter with a fundamental concept
- The mental model must be earned through writing before it can be used to evaluate AI output
- The learner has never written this type of construct before

**Characteristic questions:** "Have they ever written this by hand?" If no, Mode 1.

**Examples:**
- Sprint 1: Semantic HTML (first time writing landmark elements)
- Sprint 2: CSS cascade (first time managing specificity)
- First React component (first time writing JSX + props)
- First Spring Boot controller (first time writing REST endpoint annotations)

---

## Mode 2: Hybrid / Generate-then-Explain

### Summary
AI builds it from your spec. You explain every construct — correct ones AND defective ones. The explained-and-corrected AI output ships.

### Construction
The AI tool constructs the artifact, directed by the learner's spec. The learner does NOT hand-build first. The Comprehension Primitive is completed before directing the AI (see [02-comprehension-primitive.md](02-comprehension-primitive.md)).

### Validate activity
The learner reads the AI output one construct at a time and writes a Decision Log entry for **every construct** — not just defective ones. For each construct, the entry records:
- What this construct does (plain English)
- Whether it matches the spec
- If defective: the specific defect, how it was caught, and the fix

**The explaining IS the learning.** Even a passing construct requires an explanation of what it does. This cannot be skipped. A learner who writes "looks correct" for a passing construct has not completed a Mode 2 entry.

### Scaffolding provided
The content developer provides an **Agent Failure Modes list** in the sprint design. The learner knows before reading what types of defects to look for. This is the primary scaffold that distinguishes Mode 2 from Mode 3.

### What ships
The corrected AI output. Defects fixed. All constructs explained in the Decision Log.

### When to apply
- The full artifact is too complex or large to hand-code in the available time
- But the learner must comprehend every construct before it ships
- The concept is complex enough that a pre-supplied failure modes list is genuinely useful

**Characteristic questions:** "Is hand-coding the full artifact realistic in the time budget?" and "Does the learner have enough mental model to catch defects without a checklist?" If the first is No and the second is also No, Mode 2.

**Examples:**
- Sprint 3: Full Tailwind responsive layout with ShadCN components (200+ utility classes)
- Spring Boot REST API with validation, error handling, and status codes across 4 endpoints
- Docker Compose with 3 services, health checks, volumes, and env var management
- LangChain chain with prompt template, model, and output parser

---

## Mode 3: Full SCVHS

### Summary
AI builds it from your spec. You validate against the spec, document defects, and ship. No checklist of what to look for — you know.

### Construction
Same as Mode 2: the AI tool constructs the artifact from the learner's spec. The Comprehension Primitive is completed before directing the AI.

### Validate activity
The learner validates construct by construct. The Decision Log records a pass or fail for every construct, but **only defective constructs require a full entry** (what the defect is, how caught, fix applied). Passing constructs are marked as passed without a full explanation — the assumption is that the learner's mental model is sufficient to recognize correct output.

The learner derives their own validation criteria from the spec. They do not need to be told what to look for — they know from prior sprints in this technology area.

### Scaffolding provided
None for validation criteria. The spec is the only input. This is the primary scaffold removal: in Mode 2, the content developer tells the learner what to look for. In Mode 3, the learner generates their own criteria from the spec.

The Comprehension Primitive remains (unless the learner has written this exact construct type many times before, in which case it can be shortened or skipped at the content developer's discretion).

### What ships
The corrected AI output. All defects fixed. Decision Log records defects and fixes; passing constructs are recorded as passed.

### When to apply
- The learner has built sufficient mental model from previous sprints in this technology area
- The learner can write a precise spec independently
- The learner can identify defects without a pre-supplied checklist
- This is the production engineering mode — it mirrors how a proficient AI-native engineer works

**Characteristic questions:** "Have they validated AI output for this technology type before?" and "Can they derive their own validation criteria from the spec?" If both are Yes, Mode 3.

**Examples:**
- Sprint 6: DOM manipulation (learner has HTML + JavaScript from Sprints 1, 2, 4)
- Sprint 7: Fetch API (learner has async/await and DOM from Sprints 4, 6)
- Spring Security JWT (learner has validated Spring Boot output in 3 previous sprints)
- CI/CD pipeline (learner has validated Docker output in previous sprints)

---

## The One-Line Distinction: Mode 2 vs Mode 3

This is the most common source of confusion.

> **Mode 2:** AI builds. You explain everything — correct constructs AND defects.  
> **Mode 3:** AI builds. You validate against spec — document defects, pass the rest.

The workflow is identical. The cognitive activity in Validate is different:
- Mode 2 Validate: "Explain every construct" (comprehension activity)
- Mode 3 Validate: "Check every construct against spec, flag failures" (validation activity)

The scaffolding is different:
- Mode 2: Instructor tells you what types of defects to look for (Agent Failure Modes list)
- Mode 3: You derive your own validation criteria from the spec you wrote

A learner moves from Mode 2 to Mode 3 for a technology area when they no longer need to explain every line to know it is correct — they can read it fluently and only need to flag what breaks the spec contract.

---

## Mode Decision Guide for Content Developers

```
Is this the learner's first encounter with this construct type?
  YES → Mode 1 (Hand-First + Validate AI)
  NO  → continue...

Is hand-coding the full artifact realistic in the time budget?
  YES → consider Mode 1 (generate AI foil for comparison)
  NO  → continue...

Does the learner have prior validated AI output experience with this technology?
  NO  → Mode 2 (Hybrid — explain everything, provide Agent Failure Modes list)
  YES → continue...

Can the learner derive validation criteria from the spec independently?
  NO  → Mode 2 (keep the scaffold)
  YES → Mode 3 (Full SCVHS)
```

---

## Common Mode Assignment Errors

| Error | Description | Correct approach |
|---|---|---|
| Using Mode 3 too early | Assigning Full SCVHS before learner has hand-built this construct type even once | Ensure at least one Mode 1 sprint before Mode 3 for any technology area |
| Using Mode 1 too late | Still requiring hand-construction when learner has solid mental model and time is the constraint | Move to Mode 2; hand-construction at advanced levels has lower return than deep validation |
| Skipping Mode 2 | Going from Mode 1 directly to Mode 3 | Mode 2 is the bridge — learn to read AI code before being expected to catch defects without a checklist |
| Treating mode as permanent | Assigning a learner a "Mode 2 learner" label | Mode is per-sprint and per-technology, not a learner property |
| No mode declaration in spec | Content developer forgets to declare mode in spec header | Every spec must have SCVHS Mode in the header — see Spec_Template.md |
