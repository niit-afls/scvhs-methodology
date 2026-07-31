# SCVHS Modes: The Four Operating Modes

> The SCVHS mode determines who performs the Construct phase and what scaffolding exists in Validate.  
> Mode is a per-sprint decision declared in the header of every Spec file.

---

## The Four Modes

| Mode | Name | Who constructs | Who specifies | Key scaffold in Validate |
|---|---|---|---|---|
| 1 | Hand-First + Validate AI | Learner by hand | Learner | AI version is the foil; instructor provides Agent Failure Modes list |
| 2 | Hybrid / Generate-then-Explain | AI tool | Learner | Instructor provides Agent Failure Modes list; learner explains every construct |
| 3 | Full SCVHS | AI tool | Learner | No Agent Failure Modes list; learner validates against spec independently |
| 4 | AI-Drafted Spec (Advanced) | AI tool | AI tool, drafted; learner reviews and finalizes | Same as Mode 3, no Agent Failure Modes list; learner validates against the spec they reviewed |

The workflow steps are **identical** in all four modes: Specify → Construct → Validate → Harden → Ship.  
The difference is not the steps; it is who does the writing at each step, the scaffolding, and the level of independence.

Modes 1 through 3 fade CONSTRUCT and VALIDATE scaffolding as the learner's mental model grows (see [04-scaffolding-progression.md](04-scaffolding-progression.md)). Mode 4 is a different, narrower exception: it fades SPECIFY itself, and only for learners who have already earned Mode 3 independence. It is not the next rung after Mode 3; see "When to apply" under Mode 4 below.

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

## Mode 4: AI-Drafted Spec (Advanced)

### Summary
An AI tool drafts the spec from three inputs: the sprint README, a spec-creation prompt, and the spec template. You review and finalize the draft. AI builds from it. You validate and log exactly as in Mode 3.

### Specify
Three inputs go to the AI tool: the sprint's `README.md`, `Spec_Creation_Prompt.md`, and `Sample_Spec_Template.md` (see [../scvhs-templates/Spec_Creation_Prompt.md](../scvhs-templates/Spec_Creation_Prompt.md)). The AI tool drafts `Spec_S0N_[Title].md` from these three inputs. The learner does not write the first draft by hand.

The learner then reviews the draft using the same checklist a content developer uses to review an AI-drafted reference spec: every Constraint and Acceptance Criterion traces back to something the README's "Writing Your Spec" section actually asked for, nothing invented, nothing missing; any scope-exclusion constraint matches an actual later-sprint topic; no "Files to Commit" section or meta-commentary. The learner edits the draft until it is correct, then commits it as their own spec. An unreviewed AI draft is not a valid Mode 4 spec.

### Construction
Same as Mode 3: the AI tool constructs the artifact from the learner-reviewed spec. The Comprehension Primitive is completed before directing the AI, at the content developer's discretion for shortening if the learner has written this exact construct type many times before (same rule as Mode 3).

### Validate activity
Identical to Mode 3. The Decision Log records a pass or fail for every construct; only defective constructs require a full entry. The spec being AI-drafted does not relax this: the learner validates against a spec they reviewed and signed off on, not against the AI's intentions.

### Scaffolding provided
None for validation criteria, same as Mode 3. What Mode 4 removes that Mode 3 keeps is the requirement that the learner author the spec's first draft by hand. This is a scaffold removal in a different phase from Modes 1→3, which fade CONSTRUCT and VALIDATE support: Mode 4 fades SPECIFY support instead.

### What ships
The reviewed and finalized spec, the Comprehension Primitive, the corrected AI-constructed artifact, and the Decision Log: the same artifact set as Mode 3.

### When to apply
Mode 4 is a narrow, instructor-gated exception, not a destination every learner reaches. It is reserved for advanced developers who have already operated in Mode 3 for this technology across multiple prior sprints and have demonstrated they can write a precise spec independently, and for tracks where directing AI-assisted spec drafting is itself the skill being taught (for example, an advanced capstone simulating a production AI-native workflow).

Mode 4 is not a fix for learners who find spec-writing hard. If a learner cannot yet write a Mode 3 spec independently, the answer is more Mode 2/3 practice, not Mode 4. See `Practice_README_Guidance.md` for why having AI draft the spec removes the skill the Specify stage exists to build, in every mode except this narrowly-scoped one.

**Characteristic questions:** "Has this learner already written independent Mode 3 specs for this technology?" and "Is AI-assisted spec drafting itself part of what this sprint or track is teaching?" If both are yes, Mode 4 may apply, at the content developer's or instructor's discretion.

**Examples:**
- An advanced or capstone sprint where the learner directs an AI tool through the full pipeline, including spec drafting, to simulate a production AI-native engineering workflow.
- A sprint explicitly designed to teach AI-assisted specification as a skill in its own right, for learners who have already mastered manual specification in Mode 3.

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

### In Practice: What the Learner's Evening Looks Like

Field feedback from content teams shows the confusion persists even after the one-line distinction, so here is the same sprint in both modes. The setup is identical in both: the learner authors the spec, hand-writes the Comprehension Primitive, and the AI tool constructs from the spec. Only the reading changes.

Think of reviewing a pull request from a junior developer (the AI tool):

- **Mode 2 is reviewing with a mentor's cheat sheet.** The Agent Failure Modes list names the mistakes to look for ("check whether it paginates in memory; check page indexing"). The learner writes a Decision Log entry for every construct, including correct ones - explaining correct code is the learning activity, and it cannot be faked.
- **Mode 3 is reviewing as the senior.** No cheat sheet; the spec is the sole reference. The learner tests the output against their own acceptance criteria ("my spec caps page size at 50 - does size=100000 fail correctly?") and logs only what was wrong and how it was fixed. Passing constructs get a recorded pass, no essay.

Mode 2 trains the learner to READ AI output in a technology. Mode 3 tests whether they can OWN it.

Two rules content developers must apply when assigning these modes:

1. **Transition signal:** move a sprint to Mode 3 only when prior Mode 2 Decision Logs show learners catching defects the failure modes list did not name.
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

Does the learner have prior validated AI output experience with this technology?
  NO  → Mode 2 (Hybrid — explain everything, provide Agent Failure Modes list)
  YES → continue...

Can the learner derive validation criteria from the spec independently?
  NO  → Mode 2 (keep the scaffold)
  YES → Mode 3 (Full SCVHS)
```

**Mode 4 is not part of this decision tree.** It is a separate, opt-in exception layered on top of Mode 3 eligibility; see "When to apply" under Mode 4 above. Never assign Mode 4 as the automatic next step once a learner reaches Mode 3; most learners should stay in Mode 3.

---

## Common Mode Assignment Errors

| Error | Description | Correct approach |
|---|---|---|
| Using Mode 3 too early | Assigning Full SCVHS before learner has hand-built this construct type even once | Ensure at least one Mode 1 sprint before Mode 3 for any technology area |
| Using Mode 1 too late | Still requiring hand-construction when learner has solid mental model and time is the constraint | Move to Mode 2; hand-construction at advanced levels has lower return than deep validation |
| Skipping Mode 2 | Going from Mode 1 directly to Mode 3 | Mode 2 is the bridge — learn to read AI code before being expected to catch defects without a checklist |
| Treating mode as permanent | Assigning a learner a "Mode 2 learner" label | Mode is per-sprint and per-technology, not a learner property |
| No mode declaration in spec | Content developer forgets to declare mode in spec header | Every spec must have SCVHS Mode in the header — see Spec_Template.md |
| Treating Mode 4 as the next rung after Mode 3 | Assigning Mode 4 to every learner who reaches Mode 3, as if it were mandatory progression | Mode 4 is a narrow, opt-in exception for advanced tracks; eligibility is prior demonstrated Mode 3 independence, not simply reaching Mode 3 |
| Using Mode 4 to skip spec-writing difficulty | Assigning Mode 4 because learners are struggling to write specs, rather than because they have mastered it | If the learner cannot write a Mode 3 spec independently, give more Mode 2/3 practice; Mode 4 is not remedial |
