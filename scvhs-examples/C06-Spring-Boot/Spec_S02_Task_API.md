# Spec_S02_Task_API.md

**Author:** [Learner name]
**Sprint:** 2 — Build REST APIs with Spring Boot (C06)
**Date:** [Date]
**SCVHS Mode:** Mode 2 - Hybrid / Generate-then-Explain. The AI tool constructs the API from this spec; I hand-write one @GetMapping first as my Comprehension Primitive, then explain every generated construct in my Decision Log, fix every defect, and ship the corrected output.
**Base:** Sprint 1 bean-wiring project (`eventhub-core`, constructor-injected service graph). This sprint converts it into a Spring Boot web application.

---

## 1. Purpose

Build the first REST API for EventHub: a layered Spring Boot application exposing CRUD endpoints for `Event` resources, persisting to an in-memory H2 database. This becomes the base artifact every later sprint extends.

## 2. What to Build

**Class or module name:** `eventhub-api`

**Responsibilities:**
Controller layer handles HTTP concerns only. Service layer owns business rules (title uniqueness). Repository layer owns persistence. The controller does NOT touch the repository directly.

**Methods or endpoints:**

| Verb | Path | Request body | Success response | Status |
|---|---|---|---|---|
| GET | /api/events | none | JSON array of events | 200 |
| GET | /api/events/{id} | none | single event JSON | 200; 404 if id unknown |
| POST | /api/events | `{ "title": string, "venue": string, "date": ISO-8601 }` | created event with generated id | 201 with Location header |
| PUT | /api/events/{id} | same as POST | updated event | 200; 404 if id unknown |
| DELETE | /api/events/{id} | none | empty body | 204; 404 if id unknown |

Event JSON shape: `{ "id": number, "title": string, "venue": string, "date": "YYYY-MM-DD" }`.

**Dependencies:** Spring Web, Spring Data JPA, H2. No security, no validation annotations yet (Sprint 3 adds them).

## 3. Constraints

- No business logic in the controller layer; the service owns the title-uniqueness rule.
- Constructor injection only; no field injection.
- All imports are `jakarta.*`; any `javax.*` import is a defect.
- POST returns 201 with a `Location: /api/events/{id}` header, never 200.
- No endpoints beyond the five specified; anything extra the AI invents is a defect.

## 4. Comprehension Primitive

Before giving this spec to the AI tool, hand-write ONE `@GetMapping` method returning a hardcoded `Event` as JSON.

**File:** `scratch_first_endpoint.java`. Committed alongside this spec, 10-20 minutes to write.

## 5. Acceptance Criteria

**Structure**
- [ ] Controller, Service and Repository are separate classes in separate packages
- [ ] Controller constructor-injects the service; service constructor-injects the repository
- [ ] No `javax.*` imports anywhere

**Behaviour**
- [ ] POST /api/events returns 201 with Location header and the created resource
- [ ] GET /api/events/{id} with an unknown id returns 404
- [ ] DELETE returns 204 and a subsequent GET for that id returns 404
- [ ] Creating two events with the same title returns an error from the service rule, not a database exception
- [ ] All five endpoints pass the provided Postman collection

**Quality**
- [ ] Service layer has no Spring Web imports (no HTTP types below the controller)
- [ ] Every handler method uses the correct mapping annotation (no bare @RequestMapping on methods)

