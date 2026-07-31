# Spec Creation Prompt (locked 2026-07-27)

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
  requirement, this is Mode 1: skip section 3 below entirely. If it does, this is Mode 2 or 3:
  keep section 3.
- The one core technique this sprint is introducing for the first time (the thing the
  Comprehension Primitive is meant to build reading literacy for).
- Whether the README's "Writing Your Spec" section lists any Constraints at all. Constraints are
  optional: if the README lists none, delete the Constraints section entirely rather than inventing
  one to fill it.
- If the README does list Constraints, check whether any of them are scope-exclusion rules: things
  a generically "complete" version of this artifact would normally include, but that belong to a
  later sprint in this course (for example, exception handling, input validation, pagination,
  authentication). Phrase each as an explicit negative naming what to omit and why: "Do not add
  [X]. Introduced in Sprint [N]." Where the omission itself needs verifying, add a matching
  Acceptance Criterion, for example: "The endpoint contains no try/catch block. Verify by reading
  the controller method." Do not invent scope-exclusion constraints for techniques the README never
  mentions as a later-sprint topic.
- Every Constraint you write must be a testable restriction, checkable pass or fail by reading the
  code, the same bar Acceptance Criteria are held to. Never write generic statements like "keep the
  implementation simple," "write clean code," or "include clear comments," they apply equally to
  every sprint and cannot be checked. If the README's pointer gestures at something like that, find
  the specific, checkable rule underneath it instead, for example "use a single fixed-size array; do
  not implement resizing logic" rather than "keep the implementation simple."

Fill in the provided template markdown file. Follow its section order exactly. Do not add sections it does not have.
```

---

