# Sprint Design Checklist — For Content Developers

> Use this checklist before finalizing any sprint design that follows SCVHS.  
> A sprint that fails any item must be revised before it is delivered.

---

## Step 1: Ship-Backward Design

Before doing anything else, define the Ship artifact.

- [ ] **Ship artifact defined:** What exactly will the learner commit, deploy, and show? Name it specifically (e.g., "responsive portfolio page styled with Tailwind utility classes, deployed on GitHub Pages").
- [ ] **Ship artifact is observable:** Can a reviewer confirm the artifact was produced? Can it be committed? Deployed? Demonstrated?
- [ ] **Acceptance criteria derived from Ship artifact:** Every acceptance criterion in the spec can be traced back to a property of the Ship artifact.

---

## Step 2: SCVHS Mode Selection

- [ ] **Mode declared in spec header:** The spec file has a SCVHS Mode field in the header, written in plain English (not just "Mode 2" — say what Mode 2 means for THIS sprint).
- [ ] **Mode is correct for this sprint:** Use the decision guide:
  - Is this the learner's first encounter with this construct type? → Mode 1
  - Is hand-coding the full artifact unrealistic in the time budget? → Mode 2
  - Has the learner practiced Mode 2 for this technology, with Decision Logs showing they reliably catch AI-construction defects? → Mode 3
- [ ] **Mode progression is coherent:** This sprint's mode is consistent with the previous sprint's mode for the same technology area. (Mode never regresses: once Mode 3 for a technology, stays Mode 3.)
- [ ] **If Mode 3 is being assigned:** confirm the learner's Mode 2 Decision Logs for this technology
      show them reliably catching AI-construction defects, evidence they can also catch the
      equivalent gaps in an AI-drafted spec. Mode 3 is not assigned to learners who are struggling
      to write specs; that calls for more Mode 2 practice, not Mode 3, since Mode 3 removes the
      writing burden, not the reviewing burden. See `01-modes.md`.

---

## Step 3: Spec Quality

- [ ] **Spec is precise enough to direct an AI tool:** Could a content developer give this spec verbatim to an AI tool and receive the intended artifact? If not, add specificity.
- [ ] **No intent-only spec sections:** Every section describes structure and constraints, not just goals. Not "make it responsive" — "grid-cols-1 default, sm:grid-cols-2, lg:grid-cols-3."
- [ ] **Acceptance criteria are binary pass/fail:** Every criterion can be verified with a tool, in a browser, in a terminal, or by reading the code. Remove any criterion that requires subjective judgment.
- [ ] **Constraints, where present, are testable restrictions:** Every constraint can be checked
      pass or fail by reading the code or running a tool, the same bar as Acceptance Criteria (no
      !important; no hardcoded secrets; all inputs validated; etc.). Reject generic statements like
      "keep it simple" or "write clean code," they apply to every sprint and cannot be checked;
      find the specific rule underneath and write that instead.
- [ ] **Technology constructs are named:** Spec uses the correct technology-specific terms for constructs (section vs div; article vs div; constructor injection vs field injection; etc.).
- [ ] **Mode 3 only, spec was reviewed, not just accepted:** The learner drafted the spec with an AI
      tool from the README, `Spec_Creation_Prompt.md`, and `Sample_Spec_Template.md`, then reviewed
      and edited it against the "After the AI drafts the spec" checklist in
      `Spec_Creation_Prompt.md` before committing it. An unreviewed AI draft does not satisfy this
      item.

---

## Step 4: Comprehension Primitive

*(Required for Mode 2 and Mode 3 sprints. Skip this section for Mode 1.)*

- [ ] **Comprehension Primitive defined in spec:** Section 4 of the spec describes exactly what the learner should hand-write and in what file.
- [ ] **Comprehension Primitive is minimal:** It is one construct, not a full feature. It fits in 10–20 minutes.
- [ ] **File naming specified:** The spec says to name the file `scratch_[name].[ext]` (or embed it
      inline) and to commit it alongside the spec, not to discard it.
- [ ] **Comprehension Primitive matches the core construct type:** The hand-written piece maps to the technology construct that will be most unfamiliar to the learner in this sprint.
- [ ] **Practice README scaffolds the spec, without writing it.** The README names the specific
      Constraints and Acceptance Criteria topics this sprint's spec must cover (see
      `Practice_README_Guidance.md`). Pointers name what to decide, they never supply the decision.
      A learner reading only the README should never be staring at a blank page, and should never
      be able to copy an answer straight out of it either.

---

## Step 5: README Constraint/Acceptance-Criteria Pointers

*(Thorough pointers required in all three modes. These do not fade between Mode 2 and*
*Mode 3, only who writes the spec's first draft changes.)*

- [ ] **README's "Writing Your Spec" section is thorough:** the README names the specific Constraints and Acceptance Criteria topics this sprint's spec must cover, written from the content developer's own reference-build defects (see `Practice_README_Guidance.md`).
- [ ] **Pointers are specific:** Not "handle errors well", but "What the code does when the database cannot be reached. Name the exact behaviour."
- [ ] **Pointers name a topic, not the answer:** The learner still supplies the actual decision; the pointer only names what must be decided and what a complete answer looks like.
- [ ] **Same pointers serve Mode 3:** Mode 3's AI-drafted spec is generated from this same README section (via `Spec_Creation_Prompt.md`). If the pointers are too thin for a learner to write from, they are too thin for the AI draft to be reviewable against either.

---

## Step 6: Decision Log Alignment

- [ ] **Decision Log instructions match the mode:**
  - Mode 2: "Fill an entry for EVERY construct — passing and failing alike."
  - Mode 3: same as Mode 2. Mode 3 changes who drafts the spec, not the Decision Log rules.
- [ ] **Every entry is grounded in the spec:** Each entry checks its construct against a specific
      Constraint or Acceptance Criterion from that sprint's own spec, named explicitly, not the
      reviewer's outside technology knowledge and not an external checklist. If an entry can't name
      which line of the spec it's checking against, it isn't a valid entry.
- [ ] **Construct granularity specified:** The sprint brief makes clear what counts as "one construct" for this technology (e.g., "one rule set" for CSS; "one endpoint method" for Spring Boot).
- [ ] **Decision Log file named and versioned:** Sprint materials specify the Decision Log filename:
      `AI_Decision_Log_S[NN]_v1.md`, `_v2.md` for any later revision, never edited in place.

---

## Step 7: Time Budget

- [ ] **SPECIFY time allocated:** Time is allocated for writing the spec, not just for construction. Rule of thumb: SPECIFY ≥ 15 minutes for a complex sprint.
- [ ] **VALIDATE + HARDEN time sufficient:** Time allocation allows for construct-by-construct reading, Decision Log entry writing, and defect fixing. Rule of thumb: VALIDATE + HARDEN ≥ 40% of total sprint time.
- [ ] **Comprehension Primitive time allocated:** 10–20 minutes for the Comprehension Primitive scratch file.
- [ ] **SHIP time allocated:** 5–10 minutes minimum for commit message writing and final check.

---

## Step 8: SCVHS Terminology Compliance

- [ ] **Phase headers use SCVHS terms:** Practice_Notes phase headers say SPECIFY, CONSTRUCT, VALIDATE, HARDEN, SHIP. Not "MODIFY AND VERIFY", "AI GENERATES BOILERPLATE", "REFLECT AND COMMIT", or similar.
- [ ] **No AI tool names:** Content uses "AI tool" or "an AI tool" — not "ChatGPT", "Claude", "Copilot", or any specific tool name. Tool is decided at delivery, not at design.
- [ ] **No em-dashes in new content:** New content (BLUE text in CTKS) uses hyphens, not em-dashes.
- [ ] **No bullets:** Items in cells are delimited by semicolons, not bullets.
- [ ] **"Construct" not "block":** The unit of review is always called a "construct." "Block" is not used (ambiguous across technologies).

---

## Step 9: Continuous Portfolio Thread

*(Applies to C04 sprints 1–7)*

- [ ] **Thread continuity confirmed:** Does this sprint build on the portfolio artifact from the previous sprint? If yes, the Base field in the spec header names the previous artifact.
- [ ] **Thread not forced:** If the sprint topic does not naturally extend the portfolio (e.g., a standalone JavaScript algorithm sprint), the thread is not forced. A new artifact is acceptable.

---

## Final Gate

Before releasing this sprint design to learners:

- [ ] The spec file header has: Author, Sprint number, Date, SCVHS Mode (written out), Base.
- [ ] The Acceptance Criteria section has at least 5 binary pass/fail items.
- [ ] A worked Decision Log example exists for at least one similar sprint in this technology area.
- [ ] The sprint has been reviewed against the SCVHS Application examples in [../scvhs-examples/cross-course-examples.md](../scvhs-examples/cross-course-examples.md).
