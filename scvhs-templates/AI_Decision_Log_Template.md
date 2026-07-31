# AI Decision Log Template

One template, one format, used in every SCVHS mode. What differs by mode is not the
template, it is how you arrive at each answer (see "How this differs by mode" below).

**Learner:**
**Sprint:** [Number], [Title]
**Date:**
**Spec file referenced:** `Spec_S0N_[Title].md`
**AI-generated files reviewed:**

Name this file `AI_Decision_Log_S0N_v1.md`. Never edit it in place; a later pass gets a new `_v2.md`, `_v3.md`, with a one-line "what changed and why" at the top.

One entry per Constraint and one entry per Acceptance Criterion in your spec, copied word for word from the spec, not summarized. List Constraint entries first, then Acceptance Criterion entries, in the same order they appear in your spec.

---

## Constraint Entries

### Constraint-Entry 1: [copy the Constraint text here, word for word]
**What the code does (plain English):** [describe the actual construct being checked; if you cannot explain it, that is itself a defect]
**Match with spec:** Yes | No | Not reviewed
**Issue:** None | [describe the specific defect]
**Check:** n/a | [how you confirmed it, e.g. read the code, ran a specific test]
**Fix:** No change | [the exact change you made]

*(repeat for every Constraint in your spec)*

---

## Acceptance Criterion Entries

### Acceptance-Criterion-Entry 1: [copy the Acceptance Criterion text here, word for word]
**What the code does (plain English):** [describe the actual construct being checked]
**Match with spec:** Yes | No | Not reviewed
**Issue:** None | [describe the specific defect]
**Check:** n/a | [how you confirmed it, e.g. ran the program and observed X]
**Fix:** No change | [the exact change you made]

*(repeat for every Acceptance Criterion in your spec)*

---

## Summary

**Total checked:**
**Issues found:**

**Correct:**
- [what passed]

**Main issue:**
- [each defect, referencing its entry, e.g. Constraint-Entry 2]

---

## Reflection

*(2-3 sentences: what did you learn from this validation pass?)*

---

## How this differs by mode

The template and fields above are identical in every mode. What changes is how you fill "What the code does" and "Check":

- **Mode 1 (Hand-First + Validate AI):** you already built a known-correct reference by hand. "What the code does" describes the AI's version; "Check" means comparing it against your own hand-built version, not against the spec in the abstract. If the AI's version differs from yours, that is the Issue. Your hand-built version ships; the AI version stays committed for comparison only.
- **Mode 2 (Hybrid) and Mode 3 (AI-Drafted Spec):** the AI tool constructed the artifact directly. "What the code does" is the comprehension activity, write it for every entry, passing or failing, not just the ones with an Issue. "Check" means validating against the spec itself (Mode 2 and Mode 3 behave identically here; Mode 3 only changes who drafted the spec, not how you validate it).
