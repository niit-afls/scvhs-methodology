# Guidance for the Practice README (locked 2026-07-27)

Every sprint's practice README must give learners detailed, sprint-specific pointers for what their
spec needs to cover, without writing the spec's decisions for them. This document explains why, and
gives a reusable pattern for content developers writing that section.

---

## The problem this solves

Learners write their own spec before construction begins, that is the whole point of the Specify
stage. But a learner on their first pass through a technology, faced with a blank "write your
Constraints and Acceptance Criteria" instruction, often does not know what dimensions even matter.
Left unscaffolded, this produces two bad outcomes:

1. **Overwhelm.** The learner does not know where to start, and the exercise feels harder than the
   sprint's actual technical content.
2. **Silent gaps.** The learner writes a spec that looks complete but never addresses the exact
   question that would have caught a real defect, because they did not know to ask it.

The instinct to fix this by having an AI tool write the spec from the README is understandable but
wrong: it removes the one skill this stage exists to build, and downstream steps stop meaning
anything. Validate against a spec you did not write is not validation, it is proofreading someone
else's, or something else's, decisions. See the Decision Log and Comprehension Primitive
specifications for why ownership at each stage matters, the same reasoning applies here.

**The fix that keeps ownership with the learner: scaffold the structure, not the decisions.** The
README names the specific things the spec must address. The learner still decides, and still
writes, the actual answer.

---

## The pattern

For each sprint that requires learners to write Constraints and Acceptance Criteria (Modes 1-3, any
sprint with a spec), the README includes a section, typically titled "Writing Your Spec," with two
lists:

### Constraints your spec must include

One bullet per topic the spec needs to address, phrased as a pointer, not an answer. Each bullet
names a decision the learner has to make and write down, it does not make the decision for them.

**Weak (do not do this):** "How should the database URL, username, and password reach the code?
Hardcoded in the class, or read from somewhere else?"
This is a question, not a pointer. It invites the learner to think out loud instead of committing
to something written in the spec.

**Right:** "Where the database URL, username, and password come from. Name the source (for example,
environment variables), and name what the code does when they are not set."
This names the topic and tells the learner what a complete answer looks like, but the learner still
supplies the actual source and the actual fallback behaviour.

Every topic named must be capable of becoming a testable constraint once the learner answers it,
checkable pass or fail by reading the code. Never point at generic project hygiene the learner
would apply on every sprint regardless, "keep it simple," "write clean code," "add clear comments,"
these are not decisions to write down, and no answer to them can be checked. If a real concern feels
like that, the fix is to find the specific rule underneath it: not "keep the array handling simple"
but "state what your chosen structure does when it needs to hold more than you expected."

### Acceptance criteria your spec must include

Same pattern: name the behaviour that needs a criterion, and require the criterion to name its own
verification method. Do not supply the verification method yourself, that is the learner's decision
too.

**Right:** "A criterion for `getStudents()` returning every row in the table, naming how you will
confirm the count is correct, for example, by comparing it against a row count you already know
from the database."

---

## How to write these pointers for a new sprint

1. Build (or review) the sprint's own reference solution first. The real defects that reference
   solution's construction surfaces are exactly the pointers this section needs, if a fixed-size
   array silently drops rows past a limit in your own build, that is the pointer: "state what your
   chosen structure does when it needs to hold more than you expected."
2. Write one pointer per topic that a first-time learner would not think to ask about unaided.
   Do not pad the list with things a learner would obviously include anyway.
3. Never write the answer into the pointer. If you catch yourself writing "should return 201," you
   have written an acceptance criterion, not a pointer, move it out of the README and into your own
   reference spec instead.
4. Keep the list short enough to read in under a minute. If it is longer than five or six bullets
   per section, the sprint's spec is probably too broad for its time box, that is a scoping problem
   to fix at the sprint level, not something to solve by trimming the pointers below what is needed.

---

## Worked example (from a JDBC/PostgreSQL sprint)

```markdown
## Writing Your Spec

You write the spec yourself, before you give anything to the AI tool. Your spec must include the
points below, add each one as its own Constraint or Acceptance Criterion, in your own words.

### Constraints your spec must include

- Where the database URL, username, and password come from. Name the source, and name what the
  code does when they are not set.
- Which Java type holds the records: a plain array, or a custom list you build yourself.
- A rule that this type must hold every row the query returns. It must not be capped at a fixed
  number.
- What the code does when the database cannot be reached. Name the exact behaviour.

### Acceptance criteria your spec must include

- A criterion for the connection succeeding, naming exactly what confirms it.
- A criterion for the connection failing when the database is unreachable, naming exactly what
  confirms the failure was handled the way your Constraint above says.
- A criterion for the query returning every row, naming how you will confirm the count is correct.
```

This example is deliberately built from a real sprint where the fixed-array-size pointer and the
unreachable-database pointer both trace back to defects a reference solution actually shipped with,
before the README named them explicitly. That is the intended way to write this section: let real
defects from your own reference build tell you what the pointers need to say.
