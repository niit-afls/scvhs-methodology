# AI Decision Log — Template

**Learner Name:**
**Sprint Number:**
**Sprint Title:**
**Date:**
**Spec file referenced:** `Spec_S0N_Short_Title.md`
**AI-generated file reviewed:** `[filename]`

---

## How to Use This Log

This log is your record of the VALIDATE and HARDEN phases. You fill it in **as you read the AI-generated code** — not after.

**The process:**

1. Open the AI-generated file and your spec side by side.
2. Read the AI output **one construct at a time** (a construct is one section, one component, one rule set, one function, one class, one service definition — whatever is a logical unit in this sprint's technology).
3. For each construct, fill in one entry below.
4. If you find a defect, record it now (VALIDATE). Fix it in the code, then come back and record your fix (HARDEN).
5. Commit the corrected code and this completed log together.

**Mode 2 (Hybrid) note:** Fill an entry for EVERY construct — passing and failing alike. The explaining of correct constructs is the comprehension activity. Do not skip entries for constructs that pass.

**Mode 3 (Full SCVHS) note:** Defective constructs get a full entry. Passing constructs: record "Yes" in "Does it match the spec?" and a brief description. Full explanation is not required for passing constructs in Mode 3.

**Standards:**
- Be specific. "AI used div instead of article" — not "AI was wrong."
- Reference the spec. "Spec required exactly one h1 — AI generated two."
- State how you caught it. "Found with W3C Validator" or "Compared line-by-line with spec" or "Checked in DevTools Computed panel."
- Record what AI got right — this is not only a defect list.

---

## Entries

---

### Entry 1: [Construct Name]

**What this construct does (plain English):**
Write one or two sentences describing what this construct does. If you cannot explain it, that is itself a defect — flag it as a comprehension defect.

**Does it match the spec?**
`Yes` / `Partial` / `No`

**Defect found:**
Describe the defect specifically. What did the AI do? What does the spec require?
*(Leave blank if no defect.)*

**How I caught it:**
Describe the method — W3C Validator, DevTools, line-by-line comparison with spec, running in browser, Postman, TypeScript compiler, etc.
*(Leave blank if no defect.)*

**Fix applied:**
Describe the exact change you made in the code.
*(Leave blank if no defect.)*

---

### Entry 2: [Construct Name]

**What this construct does (plain English):**

**Does it match the spec?**
`Yes` / `Partial` / `No`

**Defect found:**

**How I caught it:**

**Fix applied:**

---

### Entry 3: [Construct Name]

**What this construct does (plain English):**

**Does it match the spec?**
`Yes` / `Partial` / `No`

**Defect found:**

**How I caught it:**

**Fix applied:**

---

*(Copy the entry above for each construct you review)*

---

## Summary

**Total constructs reviewed:**
**Total defects found:**
**Defects fixed:**

**What the AI got right:**
List the constructs or decisions where the AI output was correct and matched the spec. Be specific — this trains you to recognise good AI output, not just bad.

**Patterns in the defects:**
Were the defects random, or did the AI make the same type of mistake repeatedly? Name the pattern if you see one.

---

## Reflection

*(Answer in 2–4 sentences)*

Where did the AI diverge most from your spec — and how did you know it was wrong?
