# SCVHS in Practice — Cross-Course Examples

> Reference document for Content Development team.  
> Shows how Specify, Construct, Validate, Harden, Ship applies across every course in the program — with concrete worked examples sprint by sprint.

For the full worked examples, see [C04-Web-Applications/](C04-Web-Applications/). This document provides the cross-course summary and representative examples for C05–C09.

---

## Course Summary Table

| Course | Technology stack | Mode progression | What "Validate" looks like |
|---|---|---|---|
| C04: Web Applications | HTML, CSS, Tailwind, JavaScript | Mode 1 (S1–2) → Mode 2 (S3–5) → Mode 3 (S6–8) | W3C Validator, DevTools, browser resize, keyboard nav |
| C05: React + TypeScript | React, TypeScript, Hooks, Context | Mode 1 (S1–2) → Mode 3 (S3–8) | TypeScript compiler, React DevTools, browser rendering |
| C06: Spring Boot | Java, Spring MVC, Security, JPA | Mode 1 (S1–2) → Mode 2 (S3–5) → Mode 3 (S6–8) | Postman, Spring application logs, unit tests |
| C07: Distributed Systems | Microservices, Kafka, Resilience4j | Mode 2 (S1–4) → Mode 3 (S5–8) | Service logs, Postman, Kafka CLI, DB inspection |
| C08: Cloud-Native (Elective) | Docker, CI/CD, Kubernetes | Mode 2 (S1–3) → Mode 3 (S4–8) | docker build/run, docker compose up, pipeline trigger |
| C09: Agentic AI (Elective) | LangChain, RAG, Multi-agent | Mode 2 (S1–4) → Mode 3 (S5–8) | LLM output inspection, test queries, iteration logs |

**The pattern holds across every course:**
Early sprints use Mode 1 or Hybrid because learners are building mental models for the first time.
Later sprints use Full SCVHS because learners now have enough understanding to direct an agent and own the output.
The Decision Log is always the same format — construct by construct, spec is the contract, defects are specific.

---

## C04 — Building Interactive and Responsive Web Applications

Full specs and worked examples in [C04-Web-Applications/](C04-Web-Applications/).

### Example C04-1: Semantic HTML Portfolio (Mode: Hand-First + Validate AI)

**Specify:**
Learner writes `Spec_S01_Portfolio_Structure.md`. Defines every landmark element (`header`, `nav`, `main`, `section`, `article`, `footer`), heading hierarchy (exactly one `h1`), and acceptance criteria (W3C valid, no div soup, `lang` attribute declared).

**Construct:**
Learner hand-codes `portfolio.html`. Then gives the same spec to an AI tool: `portfolio-ai-generated.html`.

**Validate:**
W3C Validator on both files. Reads AI output construct by construct.

*Sample Decision Log entry:*
> Construct: Projects section.
> What it does: Groups three project entries.
> Match spec? No.
> Defect: Spec required each project as `<article>`. AI used `<div class="project">`. Div has no semantic meaning — screen readers cannot identify project entries as independent content.
> How caught: Compared AI output line by line against spec. Spec said "article element."
> Fix: Replaced each `<div class="project">` with `<article>`.

**Harden:**
Disable CSS in browser. Keyboard Tab navigation. DevTools Accessibility pane for landmark roles.

**Ship:**
`portfolio.html`, `portfolio-ai-generated.html`, `AI_Decision_Log_S01.md` committed. Commit message: `feat: build semantic portfolio; validate AI output and fix 4 semantic defects`.

---

### Example C04-3: Fetch API (Mode: Full SCVHS)

**Specify:**
Learner writes `Spec_S07_API_Integration.md`. Defines the endpoint, data shape, three UI states (loading, success, error), how each state renders, and error handling for network failure, non-ok status, and empty data.

**Comprehension Primitive:**
Hand-write one `fetch` + `await` + `try/catch` that calls one endpoint and logs the response. Scratch file only.

**Construct:**
AI generates the full data-fetching feature from the spec.

**Validate:**
Network tab in DevTools. Tests all three error states deliberately (throttle network, bad URL, mock empty response).

*Sample Decision Log entry:*
> Construct: Error handling block.
> What it does: Catches fetch errors and displays a message.
> Match spec? No.
> Defect: AI checked for network failure (catch block) but did not check `response.ok`. A 404 or 500 response passes silently.
> How caught: Called a URL returning 404. Page showed empty instead of an error message. Spec said "handle non-ok status."
> Fix: Added `if (!response.ok) throw new Error(response.status)` before calling `response.json()`.

---

## C05 — React with TypeScript

### Example C05-1: React Component with Props (Mode: Hand-First + Validate AI)

**Specify:**
Learner writes `Spec_S01_ProjectCard_Component.md`. Defines the TypeScript props interface (`title: string`, `description: string`, `tags: string[]`, `link: string`), what the component renders, and what happens when `tags` is an empty array.

**Construct:**
Learner hand-writes `ProjectCard.tsx`. Then gives spec to AI: `ProjectCard-ai.tsx`.

**Validate:**
TypeScript compiler first (`tsc --noEmit`). Then render in browser with React DevTools.

*Sample Decision Log entry:*
> Construct: Props interface.
> What it does: Defines the shape of data the component accepts.
> Match spec? No.
> Defect: Spec required `tags: string[]`. AI used `tags: any[]`. This defeats TypeScript — no type safety on the tags array.
> How caught: Checked the interface in the AI file. Saw `any`. Spec was explicit about `string[]`.
> Fix: Changed `tags: any[]` to `tags: string[]`.

---

### Example C05-3: React Context (Mode: Full SCVHS)

**Specify:**
Learner writes `Spec_S06_ThemeContext.md`. Defines context shape (`theme: 'light' | 'dark'`, `toggleTheme: () => void`), provider component, which components consume context, and default value.

**Comprehension Primitive:**
Hand-write a minimal React Context with one value and one consumer. Scratch file only.

*Sample Decision Log entry:*
> Construct: Default context value.
> What it does: Provides a fallback value when no Provider wraps a consumer.
> Match spec? No.
> Defect: AI set `createContext(undefined)`. Any consumer outside a provider will receive `undefined` and crash on `toggleTheme()`. Spec required a defined default value.
> How caught: Rendered a consumer without a Provider wrapper. It crashed with `toggleTheme is not a function`.
> Fix: Set default to `{ theme: 'light', toggleTheme: () => {} }`.

---

## C06 — Spring Boot

### Example C06-1: Dependency Injection (Mode: Hand-First + Validate AI)

**Specify:**
Learner writes `Spec_S02_UserService_DI.md`. Defines `UserService` interface (two methods), `UserServiceImpl`, `UserController` depending on `UserService` via constructor injection, and expected response for `/users/{id}`.

**Construct:**
Learner hand-writes all three files. Constructor injection, `@Service`, `@RestController` — foundational Spring concepts must be earned by writing.

*Sample Decision Log entry:*
> Construct: Dependency injection in UserController.
> What it does: Injects UserService into the controller.
> Match spec? No.
> Defect: Spec required constructor injection. AI used field injection (`@Autowired` directly on the field). Field injection hides dependencies and makes the class harder to test.
> How caught: Read the controller class. Saw `@Autowired` above the field, not in the constructor.
> Fix: Removed `@Autowired` from field. Added a constructor with `UserService` parameter.

---

### Example C06-2: REST API with Validation (Mode: Hybrid)

*Sample Decision Log entry:*
> Construct: POST /products endpoint.
> What it does: Creates a new product and returns 201 with the created resource.
> Match spec? No.
> Defect: AI returned 200 on successful creation. Spec required 201 Created. This violates REST conventions — 200 means "here is an existing resource"; 201 means "I created something new."
> How caught: Called POST /products in Postman. Saw 200. Spec said 201.
> Fix: Changed `return ResponseEntity.ok(product)` to `return ResponseEntity.status(HttpStatus.CREATED).body(product)`.

---

## C07 — Distributed Systems and Microservices

### Example C07-2: Kafka Event-Driven Communication (Mode: Full SCVHS)

**Specify:**
Learner writes `Spec_S05_OrderPlaced_Event.md`. Defines topic name, event schema, producer behavior (publish after order saved), consumer behavior (send email on receipt), and what happens when a malformed message arrives.

**Comprehension Primitive:**
Hand-write a minimal Kafka producer that sends a string to a topic and a consumer that logs it.

*Sample Decision Log entry:*
> Construct: Kafka consumer error handler.
> What it does: Handles messages that cannot be deserialized or processed.
> Match spec? No.
> Defect: AI had no error handler. A malformed message caused an unhandled deserialization exception — Kafka retried it indefinitely, blocking all subsequent messages on that partition.
> How caught: Published a malformed message directly to the topic using the Kafka CLI. Repeated retry errors in the logs. No new messages processed.
> Fix: Added a `DefaultErrorHandler` with a `DeadLetterPublishingRecoverer` — failed messages routed to `order-placed.DLT` after 3 retries.

---

## C08 — Cloud-Native Systems

### Example C08-1: Dockerfile (Mode: Hybrid)

*Sample Decision Log entry:*
> Construct: User configuration.
> What it does: Sets the user the container process runs as.
> Match spec? No.
> Defect: AI ran the application as root. Spec required a non-root user. Running as root means a container escape vulnerability gives the attacker root access on the host.
> How caught: Ran `docker run myapp whoami` — returned `root`. Spec said non-root.
> Fix: Added `RUN addgroup -S appgroup && adduser -S appuser -G appgroup` and `USER appuser` before the CMD instruction.

---

## C09 — Agentic AI Systems

### Example C09-2: RAG Pipeline (Mode: Full SCVHS)

**Specify:**
Learner writes `Spec_S04_DocumentQA_RAG.md`. Defines document source, chunking strategy (512 tokens, 50-token overlap), embedding model, vector store (Chroma), retrieval top-k (5 chunks), generation prompt template (answer only from retrieved context), and expected behavior when no relevant document is found.

*Sample Decision Log entry:*
> Construct: Out-of-scope handling.
> What it does: Responds when no relevant context is retrieved.
> Match spec? No.
> Defect: When asked a question outside the documents, the model answered from its training knowledge instead of returning the defined fallback. Spec required the model to answer only from retrieved context.
> How caught: Asked "What is the capital of France?" — not in the docs. Model answered "Paris." Spec was explicit: answer only from retrieved context.
> Fix: Added to the system prompt: "If the retrieved context does not contain the answer, respond with: I could not find this information in the provided documents. Do not use knowledge outside the retrieved context."

### Example C09-3: Multi-Agent System (Mode: Full SCVHS)

*Sample Decision Log entry:*
> Construct: Termination condition.
> What it does: Stops the agent loop.
> Match spec? No.
> Defect: AI only checked for test success as a termination condition. No maximum iteration check. Agent looped indefinitely when tests kept failing — 47 iterations, consumed the entire token budget.
> How caught: Ran the agent with a task where the test could never pass. Observed loop running indefinitely. Spec said maximum 3 iterations.
> Fix: Added `iteration_count` variable incremented each loop. Added check: `if iteration_count >= 3: return "Agent could not solve the task in 3 iterations."` before the next tool call.
