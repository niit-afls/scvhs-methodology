# AI Decision Log — Worked Example (C06 Sprint 2)

**Learner Name:** [Example — for content developer reference]
**Sprint Number:** 2
**Sprint Title:** Build REST APIs with Spring Boot
**Date:** [Date]
**Spec file referenced:** `Spec_S02_Task_API.md`
**AI-generated file reviewed:** `EventController.java`, `EventService.java`, `EventRepository.java`, `Event.java`

Mode 2 rules apply: one entry per construct, passing and failing alike. Construct granularity for this sprint: one endpoint method, one layer class, or one annotation cluster.

---

### Entry 1: EventController class wiring

**What this construct does (plain English):**
Declares the REST controller and injects EventService through the constructor so HTTP handling is separated from business rules.

**Does it match the spec?**
`Yes`

**Defect found:** —
**How I caught it:** —
**Fix applied:** —

(Correct constructs still get an entry in Mode 2 — writing this is the comprehension activity.)

---

### Entry 2: POST /api/events handler

**What this construct does (plain English):**
Accepts an Event JSON body, delegates creation to the service, and returns the created event.

**Does it match the spec?**
`No`

**Defect found:**
AI returned `ResponseEntity.ok(created)` — status 200 with no Location header. Spec requires 201 with `Location: /api/events/{id}`.

**How I caught it:**
Ran the provided Postman collection; the POST assertion failed on status. Cross-checked spec section 2 table.

**Fix applied:**
`return ResponseEntity.created(URI.create("/api/events/" + created.getId())).body(created);`

---

### Entry 3: Import statements in Event.java

**What this construct does (plain English):**
Entity annotations marking the class for JPA persistence.

**Does it match the spec?**
`No`

**Defect found:**
AI generated `import javax.persistence.Entity;` — the pre-Spring-Boot-3 namespace. Project uses Jakarta; this does not compile. Spec constraint: all imports `jakarta.*`.

**How I caught it:**
Compiler error on first build. Confirmed against the spec's Constraints section, which requires `jakarta.*` imports.

**Fix applied:**
Replaced all `javax.persistence.*` imports with `jakarta.persistence.*`.

---

### Entry 4: Title-uniqueness rule placement

**What this construct does (plain English):**
Rejects a new event whose title already exists.

**Does it match the spec?**
`Partial`

**Defect found:**
The rule works, but AI placed the duplicate check inside `EventController` before calling the service. Spec constraint: no business logic in the controller; the service owns this rule.

**How I caught it:**
Read the controller construct by construct against the constraints section. The check reads the repository from the controller — two layer violations at once.

**Fix applied:**
Moved the check into `EventService.create()`; controller now only translates the service's exception into an HTTP response.

---

### Entry 5: GET /api/events/{id} not-found path

**What this construct does (plain English):**
Returns the event for a known id and 404 for an unknown one.

**Does it match the spec?**
`Yes`

**Defect found:** —
**How I caught it:** — (verified via Postman: unknown id returns 404)
**Fix applied:** —

---

## Summary

**Total constructs reviewed:** 9 (5 shown here for brevity in this example)
**Total defects found:** 3
**Defects fixed:** 3

**What the AI got right:**
Constructor injection throughout; clean layer separation for GET/DELETE paths; correct `@RestController` and mapping annotations; DELETE returning 204.

**Patterns in the defects:**
All three defects (200-for-create, javax imports, logic in controller) were caught by reading construct-by-construct against the spec's own Acceptance Criteria and Constraints sections, not a separate checklist, which is why both sections must be explicit and complete in every spec.

## Reflection

The AI's output looked complete and compiled after one import fix, which is exactly why construct-by-construct reading matters: the 200-vs-201 defect and the layering violation produce no errors and would have shipped silently. The spec's constraints section, not the happy-path table, is where both were caught.
