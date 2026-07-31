# SCVHS Modes: The Three Operating Modes

> The SCVHS mode determines who performs the Specify and Construct phases and what
> scaffolding exists in Validate.
> Mode is a per-sprint decision declared in the header of every Spec file.

---

## The Three Modes

> **Changed 2026-07-31:** the former Mode 3 (Full SCVHS, independent spec-writing, no
> README pointers, defects-only Decision Log) is retired. The former Mode 4
> (AI-Drafted Spec) is renumbered to Mode 3 and is now a normal ladder rung reached after
> Mode 2, not a gated exception. Mode 1 and Mode 2 are unchanged.

| Mode | Name | Who constructs | Who specifies | Key scaffold in Validate |
|---|---|---|---|---|
| 1 | Hand-First + Validate AI | Learner by hand | Learner | AI version is the foil; README gives thorough Constraint/Acceptance-Criteria pointers |
| 2 | Hybrid / Generate-then-Explain | AI tool | Learner | README gives thorough Constraint/Acceptance-Criteria pointers; learner explains every construct |
| 3 | AI-Drafted Spec | AI tool | AI tool, drafted; learner reviews and finalizes | Same README pointers as Mode 2; learner explains every construct |

The workflow steps are **identical** in all three modes: Specify → Construct → Validate → Harden → Ship.
The difference is not the steps; it is who does the writing at each step, the scaffolding, and the level of independence.

Modes 1 and 2 fade CONSTRUCT scaffolding as the learner's mental model grows (see [04-scaffolding-progression.md](04-scaffolding-progression.md)). Mode 3 fades a different phase, SPECIFY: the learner no longer writes the spec's first draft by hand, an AI tool drafts it from the same README pointers Mode 1 and 2 use, and the learner reviews it instead. Construct, Validate, and the Decision Log behave the same in Mode 3 as in Mode 2; the only thing that changes is who authors the spec.

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
The sprint's README gives thorough Constraint and Acceptance Criteria pointers (see `Practice_README_Guidance.md`), written from the content developer's own reference-build defects: a pre-researched account of what commonly goes wrong for this technology, delivered through the spec the learner writes rather than a separate checklist. This tells the learner what to check for before they compare the AI output.

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
The sprint's README gives thorough Constraint and Acceptance Criteria pointers (see `Practice_README_Guidance.md`). The learner knows before reading what to check for, because it is already written into the spec they authored from those pointers.

### What ships
The corrected AI output. Defects fixed. All constructs explained in the Decision Log.

### When to apply
- The full artifact is too complex or large to hand-code in the available time
- But the learner must comprehend every construct before it ships
- The learner has not yet demonstrated they can reliably review a spec someone (or something) else wrote

**Characteristic questions:** "Is hand-coding the full artifact realistic in the time budget?" If No, Mode 2.

**Examples:**
- Sprint 3: Full Tailwind responsive layout with ShadCN components (200+ utility classes)
- Spring Boot REST API with validation, error handling, and status codes across 4 endpoints
- Docker Compose with 3 services, health checks, volumes, and env var management
- LangChain chain with prompt template, model, and output parser

---

## Mode 3: AI-Drafted Spec

### Summary
An AI tool drafts the spec from the same README pointers Mode 2 uses. You review and finalize the draft. AI builds from it. You explain every construct, exactly as in Mode 2.

### Specify
Three inputs go to the AI tool: the sprint's `README.md`, `Spec_Creation_Prompt.md`, and `Sample_Spec_Template.md` (see [../scvhs-templates/Spec_Creation_Prompt.md](../scvhs-templates/Spec_Creation_Prompt.md)). The AI tool drafts `Spec_S0N_[Title].md` from these three inputs. The learner does not write the first draft by hand.

The learner then reviews the draft using the same checklist a content developer uses to review an AI-drafted reference spec: every Constraint and Acceptance Criterion traces back to something the README's "Writing Your Spec" section actually asked for, nothing invented, nothing missing; any scope-exclusion constraint matches an actual later-sprint topic; no "Files to Commit" section or meta-commentary. The learner edits the draft until it is correct, then commits it as their own spec. An unreviewed AI draft is not a valid Mode 3 spec.

### Construction
Same as Mode 2: the AI tool constructs the artifact from the learner-reviewed spec. The Comprehension Primitive is completed before directing the AI.

### Validate activity
Identical to Mode 2. The learner writes a Decision Log entry for every construct, passing and failing alike, explaining what each one does and whether it matches the spec. The spec being AI-drafted does not relax this: the learner validates against a spec they reviewed and signed off on, not against the AI's intentions.

### Scaffolding provided
The same thorough README Constraint and Acceptance Criteria pointers as Mode 2. What Mode 3 removes is the requirement that the learner author the spec's first draft by hand; everything else, including how much the README helps, is unchanged from Mode 2.

### What ships
The reviewed and finalized spec, the Comprehension Primitive, the corrected AI-constructed artifact, and the Decision Log with a full entry for every construct: the same artifact set as Mode 2.

### When to apply
A normal ladder rung reached after enough Mode 2 experience in a technology area, the same way Mode 2 follows Mode 1. Apply it when:
- The learner has practiced reading and explaining AI-constructed output in Mode 2 for this technology
- The learner can reliably review an AI-drafted spec against the README's pointers and catch what it got wrong or missed, the same skill a content developer uses to review a Sample Spec draft
- Directing AI-assisted spec drafting is itself a skill worth building for this sprint or track

Mode 3 is not a fix for learners who find spec-writing hard, it is a fix for the *writing* burden, not the *reviewing* burden. A learner who cannot review a spec critically should not be in Mode 3 yet regardless of how much Mode 2 practice they have had.

**Characteristic questions:** "Has this learner practiced Mode 2 for this technology?" and "Can they reliably review a spec draft, not just accept it?" If both are yes, Mode 3.

**Examples:**
- A sprint following several Mode 2 sprints in the same technology, where the learner has shown they can catch defects reliably and is ready to review rather than author the spec.
- A sprint explicitly designed to teach AI-assisted specification as a skill in its own right.

---

## The One-Line Distinction: Mode 2 vs Mode 3

This is the most common source of confusion, because Construct, Validate, and the Decision Log are identical in both modes.

> **Mode 2:** You write the spec. AI builds from it. You explain everything.
> **Mode 3:** An AI tool drafts the spec. You review and finalize it. AI builds from it. You explain everything, exactly as in Mode 2.

The only thing that changes is who produces the spec's first draft. Everything downstream, the README pointers, the Comprehension Primitive, the Decision Log's explain-every-construct rule, is the same.

### In Practice: What the Learner's Evening Looks Like

Field feedback from content teams shows the confusion persists even after the one-line distinction, so here is the same sprint in both modes.

- **Mode 2:** the learner reads the README's pointers, writes the spec from scratch in their own words, gives it to an AI tool, and explains every construct the AI produces against that spec.
- **Mode 3:** the learner reads the same README pointers, gives them to an AI tool along with `Spec_Creation_Prompt.md`, receives a drafted spec, checks it line by line against the README's pointers the same way a content developer checks an AI-drafted reference spec, corrects what's wrong or missing, then gives the finalized spec to an AI tool and explains every construct it produces, exactly as in Mode 2.

Mode 2 trains the learner to write a precise spec from a set of pointers. Mode 3 trains the learner to critically review one instead, a distinct, equally real skill, not a shortcut around it.

Two rules content developers must apply when assigning these modes:

1. **Transition signal:** move a sprint to Mode 3 only when prior Mode 2 Decision Logs show the learner reliably catching AI-construction defects, evidence they can also catch the equivalent gaps in an AI-drafted spec.
2. **Reset rule:** the ladder is per technology, not per learner. A cohort in Mode 3 for REST endpoints correctly returns to Mode 2 the sprint a new technology (for example, containerization) appears - scaffolding follows the mental model, not seniority.

---

## Mode Decision Guide for Content Developers

```
Is this the learner's first encounter with this construct type?
  YES → Mode 1 (Hand-First + Validate AI)
  NO  → continue...

Is hand-coding the full artifact realistic in the time budget?
  YES → consider Mode 1 (generate AI foil for comparison)
  NO  → continue...

Has the learner practiced Mode 2 for this technology and shown they
reliably catch defects, not just accept AI output?
  NO  → Mode 2 (Hybrid: write the spec yourself, explain everything)
  YES → Mode 3 (AI drafts the spec; you review it; explain everything)
```

---

## Common Mode Assignment Errors

| Error | Description | Correct approach |
|---|---|---|
| Using Mode 3 too early | Assigning AI-Drafted Spec before the learner has practiced Mode 2 for this technology at least once | Ensure at least one Mode 2 sprint before Mode 3 for any technology area |
| Using Mode 1 too late | Still requiring hand-construction when learner has solid mental model and time is the constraint | Move to Mode 2; hand-construction at advanced levels has lower return than deep validation |
| Skipping Mode 2 | Going from Mode 1 directly to Mode 3 | Mode 2 is the bridge: learn to write and validate a spec by hand before reviewing one someone else drafted |
| Treating mode as permanent | Assigning a learner a "Mode 2 learner" label | Mode is per-sprint and per-technology, not a learner property |
| No mode declaration in spec | Content developer forgets to declare mode in spec header | Every spec must have SCVHS Mode in the header — see Spec_Template.md |
| Using Mode 3 to skip spec-writing difficulty | Assigning Mode 3 because learners are struggling to write specs, rather than because they have mastered writing and are ready to review | Mode 3 removes the writing burden, not the reviewing burden; if the learner can't critically review a spec, give more Mode 2 practice instead |
