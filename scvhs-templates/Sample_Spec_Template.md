# Sample Spec Template - for AI-Assisted Drafting (locked 2026-07-27)

For content developers using an AI tool to draft a sprint's reference `Spec_S0N_[Title].md`, the
same authoring work a content developer would otherwise do by hand. This is not for learners
drafting their own spec, that remains the whole point of the Specify stage, see
`Practice_README_Guidance.md` for why, and for how to scaffold that without doing it for them.

Use this kit as: attach the sprint's `README.md`, paste the prompt below, then paste the template
below that. Review what comes back the same way you would review a human-drafted spec, nothing here
substitutes for that review.

---

## The prompt

```
You are drafting a CLAUDE.md/AGENTS.md-style specification file, not documentation. This file will
be handed directly to an AI coding tool as its construction instructions. Write it that way: direct,
imperative statements about what to build. Never address "the learner," "the student," or "you" as
a person. Never describe the AI in third person. Never include a section telling anyone what to
commit, committing is a human workflow action, not a construction instruction.

Read the attached README.md for this practice. It states the sprint's domain and technology, the
Comprehension Primitive requirement, and a list of points the spec must include under "Writing Your
Spec." Use those points as the source of truth for what the Constraints and Acceptance Criteria
must cover. Do not invent requirements the README doesn't ask for, and do not skip any point it
does ask for.

First, identify from the README:
- The technology and artifact type for this sprint (for example: a React component, an HTML page, a
  Dockerfile, a Spring Boot class, a CI/CD pipeline file, a properties file, a CSS stylesheet).
- The SCVHS Mode this sprint uses. If the README does not name a Comprehension Primitive
  requirement, this is Mode 1: skip section 3 below entirely. If it does, this is Mode 2 or 3: keep
  section 3.
- The one core technique this sprint is introducing for the first time (the thing the
  Comprehension Primitive is meant to build reading literacy for).

Fill in the template below. Follow its section order exactly. Do not add sections it does not have.
```

---

## The template

```markdown
# Spec_S0N_[Title].md

**Author:** [Content Dev Name]
**Sprint:** [Sprint Number] - [Sprint Title]
**Date:** [Date]
**SCVHS Mode:** [Mode 1 / Mode 2 - Hybrid / Generate-then-Explain / Mode 3 - Full SCVHS]
**Base:** [What exists before this sprint, or "None"]

---

## 1. Purpose

[One or two sentences: what is being built, and why, drawn from the README's domain description.]

---

## 2. Comprehension Primitive

*(Required for Mode 2 and Mode 3 only. Delete this entire section if the README's mode is Mode 1.)*

```[language]
[One minimal example, in the smallest meaningful unit for this technology, demonstrating the core
technique this sprint introduces for the first time. Not the full artifact. Not a full class or
component. If the real artifact must handle variable or unknown input, this primitive must
demonstrate that same handling in miniature, not a single fixed case.]
```

[One sentence naming the exact pattern this primitive establishes, and stating that the artifact in
Section 3 must follow the same pattern, without pre-solving structure, error handling, or edge
cases that belong there instead.]

---

## 3. What to Build

[Use whichever structure fits this technology: classes/methods for a backend artifact,
components/props for a UI artifact, stages/steps for a pipeline, services/resources for
infrastructure or config, keys/values for a properties file. One block per artifact named in the
README. Name every piece; do not leave any artifact from the README's domain description out.]

**[Artifact / class / component name]**

**Responsibilities:**
[What it does. What it does NOT do, boundaries matter.]

**[Methods / Props / Stages / Keys, whichever fits]:**
- [name] - [what it does]

**Dependencies:**
[What this depends on. "None" if nothing.]

*(Repeat this block for each additional artifact.)*

---

## 4. Constraints

*(One bullet per point the README's "Writing Your Spec" section lists under Constraints. State the
actual decision, do not restate the README's question back as the answer. Do not add constraints
the README never asked for.)*

- [Constraint: the actual decision, stated as a rule]
- [Constraint: the actual decision, stated as a rule]

---

## 5. Acceptance Criteria

*(One checkbox per point the README lists under Acceptance Criteria. Every criterion is binary
pass/fail and names the specific way to verify it, not just the expected behavior. "Works
correctly" is never acceptable on its own.)*

**[Concern group, e.g. Connection / Structure / Behaviour]**

- [ ] [Expected behavior, precisely stated]. Verify by [the specific action you would actually take].
- [ ] [Expected behavior, precisely stated]. Verify by [the specific action you would actually take].

**[Second concern group, if needed]**

- [ ] [Expected behavior]. Verify by [specific action].
```

---

## After the AI drafts it

Do not ship the output as-is. Check, the same review this kit's own worked example (the JDBC demo)
went through:
- Every Constraint and Acceptance Criterion traces back to something the README's "Writing Your
  Spec" section actually asked for, nothing invented, nothing missing.
- The Comprehension Primitive is genuinely minimal, one unit, not a working version of the real
  artifact.
- Every acceptance criterion names a specific, repeatable verification action, not a restated
  conclusion.
- No "Files to Commit" section, no meta-commentary about the AI or the workflow, snuck in.

Related: `Spec_Template.md` (the full, human-facing version with tutorial content, use this instead
when a learner is writing their own spec by hand), `Practice_README_Guidance.md` (how to write the
"Writing Your Spec" pointers this whole kit depends on).
