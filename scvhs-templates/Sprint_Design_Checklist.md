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
  - Is hand-coding the full artifact unrealistic in the time budget, AND is this the learner's first time validating AI output for this technology? → Mode 2
  - Has the learner previously validated AI output for this technology AND can they derive validation criteria independently? → Mode 3
- [ ] **Mode progression is coherent:** This sprint's mode is consistent with the previous sprint's mode for the same technology area. (Mode never regresses: once Mode 3 for a technology, stays Mode 3.)

---

## Step 3: Spec Quality

- [ ] **Spec is precise enough to direct an AI tool:** Could a content developer give this spec verbatim to an AI tool and receive the intended artifact? If not, add specificity.
- [ ] **No intent-only spec sections:** Every section describes structure and constraints, not just goals. Not "make it responsive" — "grid-cols-1 default, sm:grid-cols-2, lg:grid-cols-3."
- [ ] **Acceptance criteria are binary pass/fail:** Every criterion can be verified with a tool, in a browser, in a terminal, or by reading the code. Remove any criterion that requires subjective judgment.
- [ ] **Constraints section present:** Rules that apply regardless of whether the output looks correct (no !important; no hardcoded secrets; all inputs validated; etc.).
- [ ] **Technology constructs are named:** Spec uses the correct technology-specific terms for constructs (section vs div; article vs div; constructor injection vs field injection; etc.).

---

## Step 4: Comprehension Primitive

*(Required for Mode 2 and Mode 3 sprints. Skip this section for Mode 1.)*

- [ ] **Comprehension Primitive defined in spec:** Section 4 of the spec describes exactly what the learner should hand-write and in what file.
- [ ] **Comprehension Primitive is minimal:** It is one construct, not a full feature. It fits in 10–20 minutes.
- [ ] **File naming specified:** The spec says to name the file `scratch_[name].[ext]` (or embed it
      inline) and to commit it alongside the spec, not to discard it.
- [ ] **Comprehension Primitive matches the core construct type:** The hand-written piece maps to the technology construct that will be most unfamiliar to the learner in this sprint.

---

## Step 5: Agent Failure Modes

*(Required for Mode 1 and Mode 2 sprints. Not provided for Mode 3.)*

- [ ] **Agent Failure Modes list included:** The sprint design (CTKS Practice_Notes or sprint brief) includes a pre-researched list of the specific mistakes AI tools make for this technology.
- [ ] **Failure modes are specific:** Not "AI makes CSS errors" — "AI uses !important to resolve specificity conflicts; AI uses px instead of rem for font sizes; AI uses desktop-first breakpoints instead of mobile-first."
- [ ] **Failure modes are observable:** Each failure mode describes something the learner can check with a tool or by reading the code.
- [ ] **Mode 3 has NO failure modes list:** If the sprint is Mode 3, the Agent Failure Modes list is intentionally absent. This is not an oversight — it is the scaffold removal.

---

## Step 6: Decision Log Alignment

- [ ] **Decision Log instructions match the mode:**
  - Mode 2: "Fill an entry for EVERY construct — passing and failing alike."
  - Mode 3: "Fill a full entry for defective constructs. Record a pass for correct ones."
- [ ] **Construct granularity specified:** The sprint brief makes clear what counts as "one construct" for this technology (e.g., "one rule set" for CSS; "one endpoint method" for Spring Boot).
- [ ] **Decision Log file named:** Sprint materials specify the Decision Log filename: `AI_Decision_Log_S[NN].md`.

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
