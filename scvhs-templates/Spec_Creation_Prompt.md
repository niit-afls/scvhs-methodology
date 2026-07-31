# Spec Creation Prompt (locked 2026-07-27)

For a content developer using an AI tool to draft a sprint's reference `Spec_S0N_[Title].md`, the
same authoring work a content developer would otherwise do by hand. Not for learners drafting their
own spec, that remains the whole point of the Specify stage, see `Practice_README_Guidance.md` for
why, and for how to scaffold that without doing it for them.

Subject-agnostic: works the same way for React, HTML, CSS, Docker, Spring Boot, a properties file,
a CI/CD script, or any other sprint technology, since it derives every technology-specific detail
from the sprint's own README rather than assuming one.

**How to use:** attach the sprint's `README.md`, paste the prompt below, then paste the raw
contents of `Sample_Spec_Template.md` after it. Review what comes back the same way you would
review a human-drafted spec, the checklist below is not optional.

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

## After the AI drafts the spec

Do not ship the output as-is. Check:
- Every Constraint and Acceptance Criterion traces back to something the README's "Writing Your
  Spec" section actually asked for, nothing invented, nothing missing.
- The Comprehension Primitive is genuinely minimal, one unit, not a working version of the real
  artifact.
- Every acceptance criterion names a specific, repeatable verification action, not a restated
  conclusion.
- No "Files to Commit" section, no meta-commentary about the AI or the workflow, snuck in.

Related: `Sample_Spec_Template.md` (the placeholder template this prompt fills in),
`Practice_README_Guidance.md` (how to write the "Writing Your Spec" pointers this prompt depends
on), `Spec_Template.md` (the full, human-facing version, for when a learner writes their own spec).
