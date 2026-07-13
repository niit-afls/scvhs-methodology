# SCVHS: A Specification-Driven Methodology for AI-Assisted Professional Work

**Authors:** Simanta Sarma, NIIT Limited - AI Futures and Learning Systems
**Institution:** NIIT Limited
**Date:** June 2026
**Version:** 1.0 (Pre-Registration Draft)
**Contact:** NIIT Limited, Instructional Design

---

## Abstract

The adoption of AI tools capable of generating professional-grade artifacts - software code, video content, written copy, visual design outputs, data analyses - has created a structural problem across disciplines: practitioners who delegate construction to AI without a structured re-engagement protocol show measurably lower comprehension, retention, and ownership of the resulting artifacts than practitioners who construct by hand. This problem is domain-independent. It applies wherever an AI tool generates an artifact that a human practitioner is expected to own, be accountable for, and modify under conditions of review or failure. This paper introduces **SCVHS** (Specify, Construct, Validate, Harden, Ship), a five-phase, mode-adaptive methodology for AI-assisted professional work in any domain where human ownership of AI-constructed artifacts is required. SCVHS is presented here in a software engineering education context, which constitutes its primary empirical deployment. The five phases, three operating modes, and two core artifacts are domain-agnostic and are intended for generalization beyond engineering. SCVHS addresses the comprehension gap through three mechanisms: specification-first design discipline, the **Comprehension Primitive** (a pre-construction hand-produced minimal example that establishes reading literacy before validation begins), and the **Decision Log** (a construct-by-construct validation and hardening record that constitutes durable evidence of ownership). The methodology is grounded in cognitive load theory, Vygotskian scaffolding, mastery learning, and the generation effect in memory research. This paper additionally provides a structured comparative analysis of SCVHS against the AWS AI-Driven Life Cycle (AI-DLC), identifying capability gaps, the rationale for each gap, and a development roadmap for closing the gaps that warrant closure.

**Keywords:** AI-assisted professional work, specification-driven methodology, scaffolding fade, comprehension primitive, decision log, AI-native education, mastery learning, human-AI collaboration, domain-agnostic methodology

---

## 1. Introduction

### 1.1 The Problem

In 2023, GitHub reported that developers using GitHub Copilot completed tasks 55% faster than those working without AI assistance [1]. McKinsey's 2023 developer productivity study found productivity gains of 30-45% across code generation tasks [2]. These productivity findings are not in dispute. What is disputed - and largely unmeasured - is what happens to comprehension, diagnostic skill, and artifact ownership when AI tools perform most of the construction work.

The problem is not specific to software development. In any professional domain where AI generates artifacts that a practitioner is accountable for - software code, architectural drawings, legal drafts, video production, written analysis, data pipelines - the same structural issue arises: the practitioner receives an artifact they did not build, is expected to validate and own it, and frequently lacks the conceptual schema required to do so reliably.

The present paper focuses on software engineering education as its primary empirical context because AI-assisted coding tools have been widely deployed since 2021, making this the domain with the strongest available evidence base. Section 8.2 addresses generalization to other professional domains.

Within software engineering, empirical evidence consistently shows that practitioners who receive AI-generated artifacts without a structured re-engagement protocol demonstrate significantly lower comprehension than those who construct by hand. Prather et al. (2023) found that novice programmers using AI code assistants without structured guidance were less able to explain their code in subsequent interviews than those who wrote code by hand, despite producing functionally similar outputs [18]. Vaithilingam et al. (2022) found that while AI code generation tools significantly increased task completion rates, they did not improve practitioners' ability to write similar code independently in post-task assessments [19]. The critical variable is not whether AI was used. It is whether a structured re-engagement procedure was present or absent.

SCVHS operationalizes that procedure.

### 1.2 The Inadequacy of Existing Responses

Responses to AI tool adoption in professional training have followed two patterns, both inadequate.

The first is prohibition: several engineering programs in 2024-2025 responded to AI adoption by prohibiting AI tools in coursework. The 2025 Stack Overflow Developer Survey found that 76% of professional developers were using or planning to use AI coding tools [3]. Training practitioners without AI tool fluency produces graduates who enter a professional context in which AI-assisted construction is the norm, without the skills to direct, validate, or own AI-generated work.

The second is unrestricted permission: allowing AI tool use without specifying what the practitioner must do with the AI output. This produces the comprehension gap described above. The practitioner submits artifacts they cannot fully explain. The gap becomes visible when they are asked to modify or defend the work.

Neither approach provides a structured answer to the central question: how does a practitioner maintain comprehension and ownership of artifacts that an AI tool constructs on their behalf?

### 1.3 The SCVHS Response

SCVHS does not prescribe whether construction is performed by hand or by an AI tool. It treats both as legitimate professional acts and recognizes that the practitioner's role shifts depending on mastery level and task context. The methodology requires three properties regardless of who performs construction:

1. The practitioner specifies before anything is constructed.
2. The practitioner can explain every construct in the artifact before it is delivered.
3. The practitioner has a documented record of every validation and hardening decision.

These three properties constitute ownership of an AI-assisted artifact. They apply whether the artifact is a Spring Boot endpoint, a 60-second brand film, a market analysis report, or an architectural design document.

### 1.4 Scope and Contributions

This paper makes the following contributions:

1. Formal specification of the SCVHS five-phase pipeline and three operating modes, with domain-agnostic definitions.
2. Introduction and theoretical grounding of the **Comprehension Primitive** as a pedagogical device applicable across AI-assisted professional domains.
3. Introduction and specification of the **Decision Log** as a cross-phase validation and hardening artifact.
4. A **Scaffolding Fade** model mapping SCVHS modes to practitioner progression stages.
5. A structured comparative analysis of SCVHS against AWS AI-DLC, including a capability gap analysis and a development roadmap.
6. A cross-technology application model spanning six courses and 40+ sprints in software engineering, with a generalization framework for other domains.

---

## 2. Background and Related Work

### 2.1 Specification-Driven Development

Specification-Driven Development (SDD) is an approach to software engineering in which a formal, machine-readable or human-readable specification precedes and governs all implementation. Its roots include:

- **Design by Contract (Meyer, 1992):** Bertrand Meyer's introduction of preconditions, postconditions, and class invariants as first-class language constructs in Eiffel [4]. The core principle - specify the contract before writing the body - is directly inherited by SCVHS's SPECIFY phase.
- **Test-Driven Development (Beck, 2002):** Kent Beck's formalization of writing a failing test before writing the implementation [5]. TDD is a specification discipline: the test is the spec. SCVHS shares this spec-first orientation but extends it to AI-directed construction.
- **API-First Design (OpenAPI Initiative, 2015-present):** The OpenAPI Specification (formerly Swagger) established the industry practice of specifying API contracts before implementation [6]. This practice is now standard at organizations including Google, Stripe, and Twilio.
- **Behavior-Driven Development (North, 2006):** Dan North's extension of TDD into natural-language specifications (Given/When/Then) [7]. BDD made specification accessible to non-engineers. SCVHS makes specification a practitioner-produced artifact, not just a team artifact.

The SCVHS SPECIFY phase inherits from all four traditions. A SCVHS spec is:
- Precise enough to direct an AI tool (Meyer's contract)
- Testable as a binary pass/fail checklist (Beck's test)
- Technology-stack-aware (OpenAPI's schema orientation)
- Written before construction (all four traditions)

### 2.2 AWS AI-Driven Life Cycle (AI-DLC)

Amazon Web Services introduced the AI-Driven Life Cycle (AI-DLC) in 2025 as a framework for governing AI agents in production software delivery. The AI-DLC defines three adaptive phases: Inception (requirements analysis, user story creation, risk assessment), Construction (component design, code generation, quality validation), and Operations (deployment automation, production readiness) [8].

AI-DLC is a team-level, delivery-pipeline framework. It answers: how should an engineering team structure its workflow when AI agents are active participants? It does not answer: how does an individual practitioner build the mastery to direct those agents effectively, validate their output, and own the result?

SCVHS answers the second question. The two frameworks are complementary:

| Dimension | AWS AI-DLC | SCVHS |
|---|---|---|
| Scope | Team delivery pipeline | Individual mastery and sprint-level practice |
| Primary user | Engineering team, delivery lead | Individual practitioner, content developer |
| AI role | Active workflow participant governed by rules | Construction agent directed by practitioner spec |
| Validation actor | Pipeline quality gates | Individual practitioner, construct by construct |
| Artifact of record | Verified deliverable | Decision Log + corrected artifact |
| Learning objective | Delivery efficiency and auditability | Comprehension and ownership of AI-constructed artifacts |

A practitioner who has completed SCVHS training is prepared to operate as a high-quality participant in an AI-DLC workflow. See the SCVHS-AWS AI-DLC mapping document (supplementary material) for the detailed phase mapping.

### 2.3 Cognitive Load Theory

Cognitive Load Theory (CLT), introduced by John Sweller in 1988, proposes that working memory has a limited capacity and that instructional design must manage the cognitive load imposed on learners [9]. Sweller distinguishes three types of cognitive load:

- **Intrinsic load:** the inherent complexity of the learning material.
- **Extraneous load:** cognitive effort caused by poor instructional design (irrelevant information, confusing presentation).
- **Germane load:** cognitive effort that directly contributes to schema formation - the "good" load.

In the context of AI-assisted learning, an unstructured AI generation task imposes high extraneous load: the practitioner must simultaneously parse unfamiliar code, evaluate its correctness, understand its structure, and make editorial decisions - all without a prior schema for what correct looks like.

SCVHS manages cognitive load by:
1. **Separating specification from construction** - SPECIFY phase builds schema before construction begins.
2. **The Comprehension Primitive** - reduces intrinsic load in VALIDATE by ensuring the practitioner has a working model of the core construct before reading the AI's version.
3. **Construct-by-construct reading** - reduces extraneous load in VALIDATE by making the unit of attention explicit.
4. **The Decision Log** - externalizes working memory, freeing capacity for evaluation.

### 2.4 Scaffolding Theory and the Zone of Proximal Development

Lev Vygotsky's Zone of Proximal Development (ZPD) defines the space between what a learner can do independently and what they can do with guidance [10]. Effective instruction operates in this zone - neither too easy (no learning) nor too hard (failure without progress).

Wood, Bruner, and Ross (1976) operationalized ZPD as scaffolding: temporary support structures that enable a learner to perform tasks they could not perform unaided, with the expectation that support is progressively withdrawn as competence grows [11].

The SCVHS Scaffolding Fade model applies this directly:

| Stage | SCVHS Mode | Scaffolding provided | Scaffolding withdrawn |
|---|---|---|---|
| Early sprints | Hand-First + Validate AI | Full hand-construction; AI as comparison foil | None yet |
| Mid sprints | Hybrid / Generate-then-Explain | AI constructs; instructor provides Agent Failure Modes list | Hand-construction |
| Late sprints | Full SCVHS | AI constructs; no failure modes list provided | Instructor checklist |

The mode is not a fixed property of a practitioner. It is a per-sprint decision based on whether the practitioner has sufficient mental model to direct the AI and own the output without guidance. The scaffolding does not disappear suddenly - it fades construct by construct, sprint by sprint.

Collins, Brown, and Newman's (1989) cognitive apprenticeship model is directly instantiated in SCVHS: the Comprehension Primitive is the "modeling" phase, the Decision Log is the "coaching and scaffolding" phase, and Full SCVHS is the "fading" phase [12].

### 2.5 Mastery Learning

Benjamin Bloom (1968) introduced Mastery Learning as a model in which instructional time is the variable and achievement is the constant: all learners can achieve mastery if given sufficient time and appropriate instruction [13]. Bloom's model requires:

1. Clear specification of mastery criteria before instruction.
2. Formative assessment that identifies gaps.
3. Corrective instruction targeted at those gaps.
4. Re-assessment until mastery is demonstrated.

SCVHS operationalizes all four requirements:
1. The SPECIFY phase produces the mastery criteria (the Acceptance Criteria section of the spec).
2. The VALIDATE phase is formative assessment (construct by construct against the spec).
3. The HARDEN phase is corrective instruction (fix every flagged defect).
4. The SHIP phase is the demonstration of mastery (corrected artifact + completed Decision Log).

Bloom's revised taxonomy (Anderson & Krathwohl, 2001) maps to SCVHS phases as follows [14]:

| Bloom Level | SCVHS phase where this is exercised |
|---|---|
| Remember / Understand | SPECIFY (recall of domain concepts to write the spec) |
| Apply | CONSTRUCT (direct AI to apply concepts) |
| Analyze | VALIDATE (decompose AI output against spec) |
| Evaluate | VALIDATE + HARDEN (judge correctness, identify defects) |
| Create | SPECIFY + HARDEN (original specification, original fixes) |

### 2.6 The Generation Effect

The generation effect, first described by Slamecka and Graf (1978), is the well-replicated finding that information is better remembered when it is generated by the learner than when it is read passively [15]. The effect holds across modalities, ages, and content types.

For engineering education, the generation effect has a direct corollary: code that a practitioner writes is better retained than code a practitioner reads. This is the empirical foundation for the traditional hand-construction model.

SCVHS preserves the generation effect in AI-construction modes through two mechanisms:

**The Comprehension Primitive:** The practitioner generates a minimal version of the core construct before reading the AI's full version. This small act of generation primes the schema needed to read the AI output with comprehension rather than recognition.

**The Decision Log:** Writing a plain-English explanation of what a construct does is itself a generation task. The practitioner generates the explanation, not retrieves it. The generation effect applies to verbal generation as well as code generation (McDaniel & Donnelly, 1996) [16].

Kapur's (2016) work on productive failure shows that even failed generation attempts - attempts that do not produce correct code - improve subsequent learning when followed by instruction [17]. The Comprehension Primitive intentionally uses this: the practitioner's minimal hand-written construct does not need to be complete or production-grade. It needs to have been generated.

### 2.7 AI-Assisted Learning: Empirical Evidence

The empirical literature on AI-assisted coding and its effects on learning is nascent but growing:

**Comprehension studies:**
- Prather et al. (2023) found that novice programmers who used AI code assistants without structured guidance were less able to explain their code in subsequent interviews than those who wrote code by hand, despite producing functionally similar outputs [18].

**Productivity vs. mastery divergence:**
- Vaithilingam et al. (2022) showed that while GitHub Copilot significantly increased task completion rate for novice programmers, it did not improve their ability to write similar code independently in post-task assessments [19].
- Imai (2022) found that Copilot-assisted developers completed more code faster but produced more security vulnerabilities per line of code than unassisted developers, suggesting that speed gains came at a correctness cost [20].

**Spec quality as a predictor of AI output quality:**
- Jiang et al. (2022) demonstrated that the quality of a natural language prompt to a code-generation model strongly predicts the correctness and completeness of the output - and that the ability to write a high-quality prompt requires domain expertise [21]. This is the empirical basis for SCVHS's SPECIFY phase: a practitioner who cannot specify cannot direct AI effectively.

**The assessment challenge:**
- Becker et al. (2023) surveyed CS educators and found that 67% believed AI tools would fundamentally change what constitutes evidence of learning, but fewer than 20% had modified their assessments to account for AI-generated work [22]. SCVHS addresses this directly: the Decision Log is an AI-proof assessment artifact. It cannot be generated by an AI tool because it requires the practitioner to document what the AI got wrong and how the practitioner caught it.

---

## 3. The Problem Formalized

### 3.1 The Comprehension Gap

Let C(h) be comprehension when a practitioner constructs by hand, and C(ai) be comprehension when a practitioner delegates construction to an AI tool. The available literature consistently shows:

> C(h) >> C(ai, no protocol)

The conventional response is to mandate C(h) - require hand-construction. SCVHS argues this is wrong: the goal is not hand-construction; the goal is comprehension and ownership. The question is whether C(ai, with protocol) can approach C(h).

SCVHS proposes:

> C(ai, SCVHS protocol) >> C(ai, no protocol) via:
> - Comprehension Primitive (generation before reading)
> - Decision Log (explanation as generation task)
> - Spec-first design (schema before construction)

### 3.2 The Validation Problem

The secondary problem is that comprehension without verification is insufficient. A practitioner who believes they understand AI-generated code but has not tested that understanding against a specification may have **false confidence** - the Dunning-Kruger risk in AI-assisted work.

SCVHS addresses this through the **binary acceptance criterion**: every item in the Acceptance Criteria section of the spec is a pass/fail test. If the practitioner cannot run the test, the criterion is invalid and must be rewritten. This discipline forces the practitioner's claimed understanding to confront observable evidence.

### 3.3 The Ownership Problem

The third problem is attribution. When a defect is found in production, the practitioner responsible must be able to explain:
1. What the artifact does.
2. Why that approach was chosen.
3. What alternatives were considered.
4. What defects were caught and fixed before ship.

The Decision Log is SCVHS's answer to the ownership problem. It is a durable, commit-linked record of these four questions, produced at the time of construction - not reconstructed after the fact.

---

## 4. The SCVHS Methodology: Formal Specification

### 4.1 Overview

SCVHS is a five-phase workflow with three operating modes. The phases are invariant - every sprint runs all five. The mode determines who performs the Construct phase and what scaffolding is provided in the Validate phase.

**The Five Phases:**

```
SPECIFY -> CONSTRUCT -> VALIDATE -> HARDEN -> SHIP
```

**The Three Modes:**

```
Mode 1: Hand-First + Validate AI
Mode 2: Hybrid / Generate-then-Explain
Mode 3: Full SCVHS
```

**The Two Critical Artifacts:**

```
Spec file          - produced in SPECIFY; governs CONSTRUCT and VALIDATE
Decision Log       - produced in VALIDATE; completed in HARDEN; shipped with the artifact
```

### 4.2 The Five Phases in Detail

#### Phase 1: SPECIFY

**Definition:** The practitioner writes a complete, testable specification of the artifact to be constructed before any construction begins.

**Invariants:**
- No code is written before the spec is complete.
- The spec must be precise enough to direct an AI tool to construct the artifact with no additional instruction.
- The Acceptance Criteria section must contain only binary pass/fail checks - items that can be verified with a tool, in a browser, in a terminal, or by reading the code.
- The spec is the contract. Any deviation from the spec by the AI output is a defect.

**Outputs:** A `Spec_S0N_[Title].md` file. See the SCVHS Spec Template (supplementary material).

**What good looks like:** A spec from which a content developer, a practitioner, or an AI tool can derive the same artifact with no ambiguity.

**Common failure:** Specs that describe intent rather than structure ("make a responsive layout" rather than "grid with 1 column at default, 2 at sm:, 3 at lg:, using Tailwind grid-cols-* classes").

#### Phase 2: CONSTRUCT

**Definition:** The artifact is built from the spec. Who builds it depends on the SCVHS Mode (see Section 4.3).

**Invariants:**
- Construction follows the spec, not instinct, habit, or a remembered pattern.
- In AI-construction modes, the spec is passed to the AI tool verbatim or near-verbatim. The practitioner does not guide the AI verbally.
- The Comprehension Primitive (Section 4.4) is completed before AI construction begins in Modes 2 and 3.

**Outputs:** The constructed artifact. In AI modes, two files: the AI-generated version and (eventually) the corrected version.

#### Phase 3: VALIDATE

**Definition:** The practitioner reads the constructed artifact against the spec, construct by construct. Every construct gets an entry in the Decision Log.

**Invariants:**
- Reading is construct by construct, not file-level. A construct is one logical unit of the technology: one HTML section, one CSS rule set, one function, one class, one service definition.
- Every construct gets a Decision Log entry - pass and fail alike.
- "I cannot explain what this construct does" is itself a defect, flagged as a comprehension defect.
- Validation tools (W3C Validator, TypeScript compiler, Postman, browser DevTools, docker build) are used actively, not optionally.

**Outputs:** Decision Log with VALIDATE entries complete. Defects identified and flagged.

**The cognitive act required:** Analysis (Bloom Level 4) - decomposing the AI output against the spec criteria.

#### Phase 4: HARDEN

**Definition:** Every defect flagged in the Decision Log is fixed. The fix is recorded in the same Decision Log entry.

**Invariants:**
- Defects are fixed in the code, not documented as "known issues."
- The fix is recorded in the Decision Log in the same entry as the defect, so the log tells the full story: what was wrong, how it was caught, what was done.
- After all defects are fixed, the Acceptance Criteria from the spec are checked again in full.
- Hardening addresses not just correctness but robustness: edge cases, security, accessibility, performance where specified.

**Outputs:** Corrected artifact. Completed Decision Log (all entries have fix recorded where applicable).

#### Phase 5: SHIP

**Definition:** The corrected artifact and the completed Decision Log are committed to the repository together, with a meaningful commit message.

**Invariants:**
- The Decision Log must be committed in the same commit as the artifact, not as a separate afterthought.
- The commit message must be meaningful: it names what was built, not just "final" or "update."
- In CI/CD contexts, the pipeline must pass before the commit is merged.

**Outputs:** A git commit containing: corrected artifact, AI-generated artifact (for comparison), completed Decision Log, commit message.

### 4.3 The Three Modes

The SCVHS mode determines who constructs and what scaffolding exists in Validate. The mode is declared in the header of every Spec file.

#### Mode 1: Hand-First + Validate AI

**Construction:** The practitioner constructs the artifact by hand, without AI assistance.

**AI role:** After hand-construction is complete, the same spec is given to an AI tool. The AI constructs a parallel version. The practitioner validates the AI version against the spec - not to improve it (it is discarded) but to identify the failure patterns the AI exhibits for this technology. The AI version is the **foil**: it shows what AI gets wrong so the practitioner can recognize it when directing AI in later sprints.

**Validate activity:** Construct-by-construct comparison of AI output against spec. Decision Log records all AI defects and what the AI got right. The practitioner's own hand-built version is already the known-correct reference.

**Agent Failure Modes list:** Provided by the content developer in the sprint design. This is a pre-researched list of the specific mistakes AI tools typically make for this technology (e.g., for HTML: multiple h1s, div soup, missing lang attribute, non-descriptive link text).

**When to apply:** First encounter with a fundamental concept. The mental model must be earned through hand-construction before it can be used to evaluate AI output.

**Examples:** First CSS stylesheet, first React component, first Spring Boot controller, first Dockerfile.

#### Mode 2: Hybrid / Generate-then-Explain

**Construction:** The AI tool constructs the artifact, directed by the practitioner's spec. The practitioner does NOT hand-build first.

**AI role:** Primary constructor.

**Comprehension Primitive:** Required. The practitioner hand-writes ONE minimal example of the core construct type before giving the spec to the AI tool (see Section 4.4). This is not the full artifact; it is reading insurance.

**Validate activity:** The Decision Log is filled in real time as the practitioner reads the AI output. Every construct gets an entry: what it does, why that choice, does it match spec. Correct constructs are explained as well as defective ones. The explaining IS the comprehension activity - not a reporting step after comprehension has occurred.

**Agent Failure Modes list:** Provided by the content developer. The practitioner is told in advance what defects to look for. This is the primary scaffold that distinguishes Mode 2 from Mode 3.

**When to apply:** The time budget makes hand-coding the full artifact unrealistic, but the practitioner must still comprehend every construct. Complex tooling with many moving parts, where the scaffold of reading-and-explaining provides sufficient protection.

**Examples:** Full Tailwind responsive layout (Sprint 3), complex Java class hierarchy (Spring Boot), multi-service Docker Compose, LangChain chain assembly.

#### Mode 3: Full SCVHS

**Construction:** The AI tool constructs the artifact, directed by the practitioner's spec.

**AI role:** Primary constructor.

**Comprehension Primitive:** Required. Same as Mode 2.

**Validate activity:** The Decision Log is filled construct by construct. The difference from Mode 2: **correct constructs do not require a full explanation entry**. The practitioner records what the construct does and a pass/fail - but only defective constructs require the full analysis. The assumption is that the practitioner now has sufficient mental model to recognize correct output without laboriously explaining it. The cognitive work shifts from "explain everything" (Mode 2) to "validate against spec and flag failures" (Mode 3).

**Agent Failure Modes list:** NOT provided. The practitioner is expected to derive their own validation criteria from the spec. This is the primary scaffold removal that distinguishes Mode 3 from Mode 2.

**When to apply:** The practitioner has built sufficient mental model in previous sprints to direct AI with a precise spec and to independently identify defects without a pre-supplied checklist. This is the production work mode.

**Examples:** DOM manipulation features (after Mode 1 HTML/JS), Fetch API integration (after Mode 1 async/await), REST API endpoints (after Mode 2 Spring Boot), CI/CD pipeline (after Mode 2 Docker).

**Assessment variant of Mode 3:** In assessment sprints, AI is permitted as a reference tool only. Construction is by hand. The practitioner must be able to explain and modify every line on demand during the review session.

#### Scaffolding Comparison

| | Mode 1 | Mode 2 | Mode 3 |
|---|---|---|---|
| Who constructs | Practitioner by hand | AI tool | AI tool |
| Comprehension Primitive | No (practitioner IS constructing) | Yes - required | Yes - required |
| Agent Failure Modes list | Yes (to guide AI validation) | Yes (to guide AI validation) | No (practitioner derives independently) |
| Decision Log entries | All AI constructs: pass/fail + defect | All constructs: what it does + pass/fail + defect | Defects only (passing constructs: pass recorded, no full entry) |
| What ships | Practitioner's hand-built artifact | Corrected AI output | Corrected AI output |
| Primary cognitive activity | Construction + analysis of foil | Explanation of every construct | Validation against spec |

### 4.4 The Comprehension Primitive

#### Definition

A Comprehension Primitive is a short, hand-written minimal example of the core construct type used in a sprint, produced by the practitioner BEFORE giving the spec to an AI tool.

#### Purpose

The Comprehension Primitive solves the bootstrap problem of AI-construction modes: a practitioner who has never written a CSS Grid layout cannot validate whether the AI's Grid layout is correct. They lack the schema to distinguish correct from plausible-but-wrong.

The Comprehension Primitive does not make the practitioner an expert. It gives them **reading literacy** - the minimum mental model required to evaluate AI output rather than trusting it on appearance.

#### Specification

- It is ONE minimal construct - not the full artifact.
- It is written in a scratch file, not committed to the repo.
- It takes 10-20 minutes.
- It does not need to be production-grade or complete.
- Its only purpose is to fire the schema that will be needed during Validate.
- After it is written, it is discarded (the scratch file is deleted or left uncommitted).

#### Theoretical Basis

The Comprehension Primitive is grounded in three bodies of research:

1. **The generation effect (Slamecka & Graf, 1978):** Generating a minimal example activates deeper encoding than reading an example. Even a failed generation attempt improves subsequent reading comprehension of a correct example [15].

2. **Schema theory (Bartlett, 1932; Rumelhart, 1980):** Comprehension requires a pre-existing schema - a mental framework into which new information is organized [23]. The Comprehension Primitive creates a minimal schema for the technology construct, enabling the practitioner to organize the AI's output into a meaningful structure rather than processing it as a sequence of unfamiliar tokens.

3. **Kapur's productive failure (2016):** Struggling with a problem before receiving instruction produces better learning outcomes than receiving instruction before struggling [17]. The Comprehension Primitive is a structured, bounded struggle.

#### Examples by Technology

| Technology | Comprehension Primitive | What it enables |
|---|---|---|
| HTML | Write one `<article>` with heading, paragraph, and link | Read AI's semantic structure |
| CSS | Write one selector with box model properties | Read specificity and cascade |
| Tailwind | Write one 3-column Grid container with 3 items | Read responsive prefixes (sm:, lg:) |
| JavaScript | Write one closure-based counter function | Read lexical scope in AI code |
| TypeScript | Write one generic function with a type parameter | Read type constraints in AI interfaces |
| React | Write one functional component with one prop | Read JSX and component structure |
| Java | Write one sealed interface with one permitted type | Read pattern matching in AI code |
| Spring Boot | Write one `@GetMapping` returning a hardcoded response | Read controller layer annotations |
| Kafka | Write one producer sending a string, one consumer logging it | Read topic configuration and listener annotations |
| Docker | Write one `FROM` + `COPY` + `CMD` Dockerfile | Read multi-stage build instructions |
| LangChain | Write one chain with one prompt template and one model call | Read chain composition in AI code |
| RAG Pipeline | Write one document loader printing chunk count | Read document splitting and embedding configuration |

### 4.5 The Decision Log

#### Definition

The Decision Log is a durable, construct-by-construct record of the VALIDATE and HARDEN phases. It is produced in real time as the practitioner reads the AI output, not written after reading is complete. It is committed to the repository alongside the artifact.

#### Structure

Each entry covers one construct and records:
1. What the construct does (in plain English).
2. Whether it matches the spec (Yes / Partial / No).
3. If Partial or No: the specific defect, with reference to the spec requirement violated.
4. How the defect was caught (tool used, method used).
5. The fix applied (exact change made in the code).

#### Why the Decision Log Is Not Replaceable

The Decision Log serves several functions simultaneously that no other artifact serves:

**As a learning artifact:** Writing "what this construct does" in plain English is a generation task that deepens encoding. It cannot be skipped without losing the comprehension benefit.

**As an assessment artifact:** The Decision Log cannot be generated by an AI tool, because it requires the practitioner to document what the AI got wrong. An AI tool cannot document its own defects as observed by the practitioner. This makes it an AI-proof assessment: a practitioner who submits a completed Decision Log with specific defects and fixes has demonstrably validated the AI output themselves.

**As an ownership artifact:** In a production context, the Decision Log is the practitioner's record of due diligence. It answers: "Did you review this AI-generated artifact before shipping it?" with specific, traceable evidence.

**As a pattern-recognition tool:** Across multiple sprints, the practitioner's Decision Logs reveal patterns in AI failure modes for specific technologies. This builds the meta-skill of anticipatory validation - knowing before reading where AI is likely to fail.

#### The Decision Log is not:
- A code comment (comments are in the code; the log is in a separate file).
- A test file (tests verify behavior; the log records human evaluation).
- A code review document (code reviews are team-facing; the log is the practitioner's own record).
- An after-the-fact summary (it is written in real time, construct by construct).

### 4.6 Scaffolding Progression

The SCVHS Scaffolding Fade model governs how mode assignments change across a course. The model has three principles:

**Principle 1: Mode is per-sprint, not per-practitioner.**
A sprint is assigned a mode based on where that sprint sits in the practitioner's mental model progression, not on a fixed assessment of the practitioner's general ability. A practitioner may be in Mode 3 for HTML and Mode 1 for Kafka in the same week.

**Principle 2: Mode progresses from 1 to 3, never backwards within a topic.**
Once a practitioner has demonstrated Mode 3 capability for a construct type, subsequent sprints in that construct type remain at Mode 3. Regression to Mode 1 within a topic is a curriculum design error.

**Principle 3: The invariant is cognitive engagement, not hand-construction share.**
What does not change as mode advances is the requirement for the practitioner to think: to specify, to explain, to validate, to own. What changes is the proportion of construction done by hand versus by AI, and the degree of scaffolding provided in Validate.

**Typical progression in a course (C04 example):**

| Sprint | Technology | Mode | Rationale |
|---|---|---|---|
| 1 | Semantic HTML | Mode 1 | First encounter with HTML semantics - mental model must be earned by writing |
| 2 | CSS Box Model | Mode 1 | First encounter with CSS cascade - specificity must be felt before AI manages it |
| 3 | Tailwind + ShadCN | Mode 2 | Full Tailwind layout is 200+ utility classes - hand-coding unrealistic; but every class must be explainable |
| 4 | Modern JavaScript | Mode 2 | Event loop, closures, and scope must be hand-traced; ES6 boilerplate can be AI-generated |
| 5 | Array methods | Mode 2 | Pipeline methods (map, filter, reduce) benefit from hand-tracing one reduce; rest can be AI |
| 6 | DOM manipulation | Mode 3 | Practitioner has HTML + JS mental model from Sprints 1-2 and 4 |
| 7 | Fetch API | Mode 3 | Practitioner has async/await and DOM mental model |
| 8 | Assessment | Mode 3 (assessment variant) | Fresh brief, AI as reference only, every line explainable on demand |

---

## 5. Theoretical Synthesis: Why SCVHS Works

### 5.1 The Spec-First Discipline

Writing a spec before constructing is not bureaucracy - it is cognition. The act of specifying forces the practitioner to:
1. Retrieve and organize domain knowledge (Bloom: Remember + Understand).
2. Anticipate the artifact structure (schema activation).
3. Define the validation contract in advance (preventing post-hoc rationalization).

Research on analogical reasoning shows that learners who anticipate the structure of a problem before receiving a solution develop stronger problem-solving schemas than learners who receive the solution first (Schwartz & Bransford, 1998) [24]. The SPECIFY phase is this anticipatory reasoning, made visible and durable.

### 5.2 Why Specifying Before AI Construction Matters

When a practitioner gives an AI tool a vague prompt ("build me a portfolio page"), the AI's output is essentially a random sample from the space of possible implementations. The practitioner has no basis to evaluate it except visual appearance.

When a practitioner gives the AI a precise spec ("exactly one h1, article elements for each project, no div soup, W3C valid"), the AI's output is constrained and the practitioner has a precise evaluation framework. The spec transforms AI output from "a plausible answer" to "an answer to my specific question, measurable against my specific criteria."

This is why spec quality is the most important factor in AI-assisted work: not because it improves the AI's output (though it does), but because it equips the practitioner to evaluate that output.

### 5.3 Why the Comprehension Primitive Works

The empirical basis is the generation effect: generating is better than reading for retention. But the Comprehension Primitive does more than activate the generation effect. It:

1. **Creates the schema** for reading the AI's output (schema theory).
2. **Reduces intrinsic cognitive load** during Validate - the practitioner is not processing an entirely unfamiliar construct, they are comparing a familiar shape to a potentially different AI version.
3. **Surfaces the practitioner's misconceptions** before validation - if the practitioner's Comprehension Primitive is wrong, they discover this when comparing it to the AI's output or when the spec check fails. A discovered misconception before Validate is better than one discovered after Ship.

The Comprehension Primitive is the minimum viable generation act. It is not designed to be the final form of the construct. It is designed to be the reading key.

### 5.4 Why the Decision Log Works

The Decision Log works because **explanation is not a proxy for understanding - it is understanding**. The research tradition from Chi et al. (1989) on self-explanation shows that learners who explain material to themselves while studying learn more than learners who reread the material [25]. The effect is robust across domains, ages, and materials.

The Decision Log mandates self-explanation at the moment of encounter - not as an optional review strategy but as a required artifact. It externalizes the self-explanation so that:
1. The practitioner cannot skip it (it is a deliverable).
2. The explanation can be assessed for accuracy.
3. The explanation creates a durable record of what was understood.

The construct-by-construct structure is deliberate. A summary log ("I reviewed the artifact and found three problems") does not produce the self-explanation effect. A construct-by-construct log - where every construct requires a sentence explaining what it does - does.

### 5.5 Why Scaffolding Fade Applies

Van Leusen (1998) and Wood et al. (1976) both identify the key risk of scaffolding: if support is not withdrawn, learners become dependent on it and fail to develop independent capability [26]. This is the failure mode of AI-assisted work without a scaffolding model - the AI is always available, always scaffolding, and the practitioner never needs to develop the independent judgment that the scaffold is temporarily replacing.

SCVHS's scaffolding fade is built into the mode progression: the Agent Failure Modes list is provided in Mode 2, removed in Mode 3. The Decision Log entry format loosens from "explain every construct" to "validate against spec, document failures." The Comprehension Primitive remains but shortens as the practitioner's prior schema grows.

The scaffold is not the AI tool. The AI tool is the production workflow. The scaffold is the support around the practitioner's engagement with that workflow, and it fades as mastery grows.

---

## 6. SCVHS and AWS AI-DLC: A Complementary Mapping

### 6.1 The Relationship

AWS AI-DLC and SCVHS are not competing frameworks. They operate at different levels of the professional ecosystem:

- **AWS AI-DLC** is a production delivery framework: it governs how AI agents participate in team-level software development workflows, with rules for quality gates, human-in-the-loop checkpoints, and audit trails.
- **SCVHS** is a mastery methodology: it governs how individual practitioners build the competence to direct AI agents with precision, validate their output with expertise, and own the result.

A practitioner who has trained through SCVHS is a better participant in an AWS AI-DLC workflow. SCVHS is the preparation; AI-DLC is the destination.

### 6.2 Phase Mapping

| SCVHS Phase | AWS AI-DLC Analog | Notes |
|---|---|---|
| SPECIFY | Inception: Requirements analysis, user story creation | SCVHS SPECIFY is the individual-level equivalent of AI-DLC's team-level requirements phase |
| CONSTRUCT | Construction: Code generation | AI-DLC governs agents generating code; SCVHS governs how the individual directs and receives that generation |
| VALIDATE | Construction: Quality validation | AI-DLC uses automated quality gates; SCVHS uses human construct-by-construct validation |
| HARDEN | Construction: Quality validation + Operations: Production readiness | AI-DLC's production readiness checks; SCVHS's edge case and robustness hardening |
| SHIP | Operations: Deployment automation | AI-DLC deploys; SCVHS commits - the unit of ship differs by context |

### 6.3 Positioning Statement

SCVHS is not a replacement for AWS AI-DLC. Organizations adopting AI-DLC for their delivery pipelines will benefit from practitioners who have trained through SCVHS, because those practitioners:
1. Write precise specs before directing AI - improving the quality of AI-DLC's Inception outputs.
2. Validate AI output construct by construct - improving the quality of AI-DLC's Construction phase quality gates.
3. Harden systematically against edge cases - improving AI-DLC's Operations readiness.
4. Maintain a Decision Log - providing the audit trail AI-DLC requires.

The training methodology and the delivery framework are designed for the same world. They are built to coexist.

---

## 7. Implementation: Application Across Courses

SCVHS has been designed and applied across six courses in NIIT's AI-Native Engineering program:

| Course | Technology stack | Mode progression | Typical sprint count |
|---|---|---|---|
| C04: Web Applications | HTML, CSS, Tailwind, JavaScript | Mode 1 (S1-2) -> Mode 2 (S3-5) -> Mode 3 (S6-8) | 8 |
| C05: React with TypeScript | React, TypeScript, Hooks, Context | Mode 1 (S1-2) -> Mode 3 (S3-8) | 8 |
| C06: Spring Boot | Java, Spring MVC, Security, JPA | Mode 1 (S1-2) -> Mode 2 (S3-5) -> Mode 3 (S6-8) | 8 |
| C07: Distributed Systems | Microservices, Kafka, Resilience4j | Mode 2 (S1-4) -> Mode 3 (S5-8) | 8 |
| C08: Cloud-Native (Elective) | Docker, CI/CD, Kubernetes | Mode 2 (S1-3) -> Mode 3 (S4-8) | 8 |
| C09: Agentic AI (Elective) | LangChain, RAG, Multi-agent | Mode 2 (S1-4) -> Mode 3 (S5-8) | 8 |

Cross-course worked examples for all six courses are documented in the cross-course worked examples (supplementary material).

The continuous portfolio thread in C04 illustrates how SCVHS creates coherence across sprints: the same artifact (a developer portfolio) is built in Sprint 1 (HTML only, Mode 1), styled in Sprint 2 (CSS, Mode 1), made responsive in Sprint 3 (Tailwind, Mode 2), enhanced with JavaScript in Sprints 4-5 (Mode 2), and fully agent-driven in Sprints 6-7 (Mode 3). The Decision Log from Sprint 1 informs what the practitioner watches for in Sprint 6.

---

## 8. Discussion

### 8.1 Limitations

**SCVHS is a design methodology, not a verified experimental intervention.** No controlled study comparing SCVHS-trained and non-SCVHS-trained practitioners on comprehension metrics, production defect rates, or artifact ownership assessments has yet been conducted. Such a study would measure comprehension depth - not just task completion - across cohorts using and not using the SCVHS protocol. This is an identified priority for future empirical work.

**Mode assignment requires instructor judgment.** SCVHS does not specify an algorithmic method for determining when a practitioner has sufficient mental model to advance from Mode 2 to Mode 3 for a given technology. Content developers currently apply the model based on curriculum design judgment. A diagnostic assessment tool for mode readiness is an open research question.

**The Comprehension Primitive duration is approximate.** The 10-20 minute estimate is based on curriculum design experience, not empirical measurement. Some construct types (e.g., a minimal LangChain chain) may require longer; others (e.g., a single HTML article element) may require much less.

### 8.2 Generalizability

SCVHS was designed within a software engineering education context, but the three structural conditions that make the methodology applicable are not unique to that domain:

1. An AI tool can construct a meaningful artifact in the domain.
2. The practitioner is expected to own, be accountable for, and modify that artifact.
3. There is a substantive difference between "this artifact was accepted" and "I understand why this artifact is correct."

The third condition is the most important and the most frequently overlooked. In domains where practitioners are evaluated on outcomes alone (did the artifact pass review?), the comprehension gap is invisible until a failure or audit occurs. SCVHS makes the third condition a first-class requirement: the Decision Log is the evidence of understanding, not the artifact itself.

The following table illustrates domain generalization, mapping SCVHS elements to non-engineering professional contexts:

| Domain | SPECIFY | CONSTRUCT (AI) | Comprehension Primitive | VALIDATE | Decision Log entry example |
|---|---|---|---|---|---|
| Video production | Shot list, script, color grade spec, pacing requirements | AI generates rough cut, color grade, transitions | Hand-edit one 30-second segment | Review cut against shot list and pacing spec, frame by frame at key transitions | "Scene 3 cut: spec required a 2-second dissolve at timestamp 01:14. AI used a jump cut. Caught by scrubbing through at 0.5x speed. Fixed by inserting dissolve transition." |
| Marketing copy | Brief: tone, structure, claim hierarchy, prohibited phrases, word count | AI drafts body copy, headlines, CTAs | Hand-write one paragraph in the required tone | Review each section against brief | "CTA section: spec said no urgency language. AI wrote 'Act now before it's too late.' Caught by searching for urgency phrases. Replaced with 'Start when you're ready.'" |
| Data analysis | Analysis requirements, output format, statistical method, interpretation constraints | AI generates analysis code and narrative | Hand-write one summary statistic calculation | Review each claim in the narrative against the underlying data | "Trend claim in paragraph 2: spec required 95% CI on all trend statements. AI stated 'sales increased 12%' without confidence interval. Added CI using stored standard error." |
| Legal drafting | Clause requirements, jurisdiction, defined terms, prohibited boilerplate | AI generates clause drafts | Hand-draft one clause of each type | Review each clause against requirements | "Limitation of liability clause: spec required a mutual cap. AI drafted a unilateral cap favoring one party. Caught by comparing clause direction against spec. Rewritten to mutual." |
| Infrastructure (IaC) | Resource spec: network topology, security groups, IAM constraints, cost ceiling | AI generates Terraform plan | Hand-write one resource block | Review each resource against spec and security baseline | "S3 bucket: spec required server-side encryption and block-public-access. AI generated bucket without encryption setting. Caught with tfsec scan. Added encryption and public access block." |

The Comprehension Primitive principle generalizes directly: before directing AI to construct any complex artifact, the practitioner hand-produces a minimal version of the core unit to establish the schema required to evaluate AI output. The minimum viable generation act differs by domain but the function is identical.

The Decision Log generalizes directly: construct-by-construct self-explanation at the time of review, with spec reference for defects, constitutes the same evidence of ownership regardless of domain.

Mode progression also generalizes: Mode 1 (hand-first) applies to the first encounter with any construct type; Mode 2 (explain everything) applies when the practitioner has basic schema but not independent validation capability; Mode 3 (validate against spec, document failures) applies when independent validation capability is established.

### 8.3 Trademark and Registration Basis

The following elements constitute the registerable proprietary methodology:

1. **The SCVHS name and acronym** as applied to this specific five-phase pipeline.
2. **The Comprehension Primitive** - a novel pedagogical device not described in the prior literature under this name or in this specific application to AI-assisted professional work.
3. **The Decision Log** as defined in SCVHS - a specific artifact format and filing discipline that differs from code review, test files, and code comments in defined ways.
4. **The three-mode structure** with the specific scaffold differentiator (Agent Failure Modes list provided in Mode 2, absent in Mode 3).
5. **The Scaffolding Fade model** as applied to AI construction modes.
6. **Ship-Backward Design** as a curriculum design methodology derived from SCVHS principles.

This document, dated June 2026, constitutes the earliest known published record of these terms in combination as a named methodology.

---

## 9. Comparative Analysis: SCVHS and AWS AI-DLC

### 9.1 Basis for Comparison

AWS AI-DLC (AI-Driven Life Cycle) is the most structurally similar publicly documented framework to SCVHS. Both define a phased workflow for AI-assisted professional work, both require human oversight at defined points, and both treat AI as a construction agent whose output must be reviewed before delivery. The comparison is therefore substantive rather than incidental.

The comparison data for this section is drawn from the AI-DLC public repository [8], specifically the README, the WORKING-WITH-AIDLC guide, the DEVELOPERS_GUIDE, and the repository directory structure as of June 2026.

### 9.2 Structural Comparison

| Dimension | AWS AI-DLC | SCVHS | Nature of difference |
|---|---|---|---|
| Primary purpose | Govern AI agents in team delivery pipelines | Build individual practitioner mastery and ownership of AI-constructed artifacts | Different level of the stack: AI-DLC governs the agent; SCVHS governs the human |
| Primary user | Engineering team, delivery lead | Individual practitioner, content developer | Team vs individual |
| Scope | Software engineering production delivery | Any domain where AI constructs owned artifacts | SCVHS is domain-agnostic by design |
| AI role | Active, governed workflow participant | Construction agent directed by practitioner spec | AI-DLC steers the AI; SCVHS steers the human |
| Validation | Automated quality gates (pipeline, scanners) | Human construct-by-construct review against spec | Complementary: automated tests verify behavior; Decision Log verifies understanding |
| Artifact of record | Verified, auditable deliverable | Decision Log plus corrected artifact | Both constitute audit trails; different purposes |
| Comprehension requirement | Not addressed | Central requirement (Comprehension Primitive, Decision Log) | Core design difference |
| Scaffolding model | Not present | Three-mode scaffolding fade | SCVHS-specific |
| License | MIT-0 (open source) | Proprietary | Different IP strategy |

### 9.3 Capabilities AI-DLC Has That SCVHS Lacks

The following capabilities are present in AI-DLC and absent in SCVHS v1.0. For each, the analysis identifies why the gap exists and whether SCVHS should close it.

---

**9.3.1 Machine-readable agent rule files**

AI-DLC provides markdown rule files read by AI coding agents as operational instructions. These live in platform-specific directories: `.amazonq/rules/`, `.cursor/rules/`, `.clinerules/`, `.claude/`, `.github/copilot-instructions.md`. When a practitioner uses an AI coding tool integrated with AI-DLC, the tool reads these rules and follows them automatically. The methodology is embedded in the agent's operating context.

SCVHS v1.0 is entirely human-readable documentation. No mechanism exists for an AI agent to read the SCVHS rules and apply them during construction.

*Why the gap exists.* SCVHS was initially designed as an educational methodology targeting human practitioners. Machine-readable rule files were not in scope.

*Should SCVHS close this gap?* Yes, partially. A `.scvhs/` directory with agent-readable rule files would improve the quality of AI-constructed output by making the AI tool aware of: the spec contract, the Acceptance Criteria, and the Comprehension Primitive requirement. This would reduce defects before validation begins, compressing the VALIDATE-HARDEN cycle.

*Development plan.* Add a `scvhs-agent-rules/` directory. First integration: Claude Code via a SCVHS-specific `CLAUDE.md` that enforces SPECIFY-phase discipline and references the spec file. Subsequent integrations: Cursor rules, Amazon Q rules. Priority: high.

---

**9.3.2 Adaptive execution based on complexity and risk**

AI-DLC analyzes project complexity and adjusts its execution accordingly: simple changes receive lightweight treatment; complex or high-risk changes receive comprehensive review. The system executes only stages that add value for a given change context.

SCVHS v1.0 applies the same five-phase process to all sprints. Mode selection provides some adaptability, but it is made by the content developer at sprint design time, not dynamically at execution time based on observable project signals.

*Why the gap exists.* SCVHS mode selection is pedagogically motivated: the mode is chosen based on what the practitioner needs to develop mastery, not on what the artifact requires. This is a different optimization criterion from AI-DLC's risk-based execution.

*Should SCVHS close this gap?* Partially. SCVHS should formalize its mode selection as a documented decision algorithm and should add a sprint-start diagnostic protocol that allows mode adjustment based on observed practitioner readiness, rather than fixing mode at design time. This preserves the pedagogical motivation while adding adaptability.

*Development plan.* Add a sprint-start mode diagnostic checklist. Not automated execution adjustment, but a structured 5-minute assessment at the start of each sprint that can trigger mode upgrade or downgrade. Priority: medium.

---

**9.3.3 Automated evaluator tooling**

AI-DLC includes an evaluator script that automates testing of workflow execution. It provides programmatic verification that the methodology was followed.

SCVHS v1.0 has no tooling. All evaluation is human-conducted through the Decision Log.

*Why the gap exists.* SCVHS evaluation is intentionally human: the Decision Log is the evaluation artifact, and its value derives precisely from being human-produced. Automating evaluation would defeat the comprehension purpose. The act of writing the Decision Log is not separable from the comprehension benefit it provides.

*Should SCVHS close this gap?* Selectively. SCVHS should not automate Decision Log production or evaluation. However, a spec quality linter - a tool that checks whether a Spec file has a declared mode, binary acceptance criteria, a Constraints section, and a Comprehension Primitive section - would improve content developer practice without compromising practitioner evaluation. The linter checks the input to the methodology (the spec), not the output (the Decision Log).

*Development plan.* Add a `scvhs-tools/` directory with a spec linter specification and reference implementation. The linter reports: missing mode declaration, acceptance criteria that are not binary, missing Constraints section, missing Comprehension Primitive for Modes 2-3. Priority: medium.

---

**9.3.4 Extension system**

AI-DLC supports a formal directory-based extension mechanism. Organizations add custom rules for security baseline requirements, property-based testing, resiliency patterns, and compliance constraints by placing markdown files in an extensions/ directory.

SCVHS v1.0 has no extension mechanism. Domain-specific guidance is embedded in the core documents.

*Why the gap exists.* SCVHS was designed for a single organizational context (NIIT's AI-Native Engineering program). Extension requirements only became apparent when considering domain generalization.

*Should SCVHS close this gap?* Yes. If SCVHS is to be applied to video production, marketing, legal, data analysis, and other domains, domain-specific extension packs are required. The core methodology documents remain domain-agnostic; domain-specific Comprehension Primitive examples, Acceptance Criteria patterns, and Agent Failure Modes lists are packaged as extensions.

*Development plan.* Add `scvhs-extensions/` directory. Initial extensions: software-engineering/ (migrated from existing core examples), video-production/, marketing-copy/, data-analysis/. Each extension provides: domain-specific Comprehension Primitive examples, domain-specific Decision Log entry examples, domain-specific Acceptance Criteria patterns. Priority: high for trademark scope; medium for immediate use.

---

**9.3.5 Brownfield and existing-system support**

AI-DLC explicitly addresses brownfield scenarios in which practitioners work with existing codebases. Its WORKING-WITH-AIDLC guide recommends preparing a Technical Environment Document that includes current system state, prohibited libraries with documented reasons, and representative code examples before initiating the workflow.

SCVHS v1.0 has a Base field in the spec header but no formal treatment of existing-system constraints or a dedicated brownfield spec template.

*Why the gap exists.* SCVHS sprints are primarily greenfield: each sprint starts from a clearly defined previous output. Professional practitioners using SCVHS outside an educational program will frequently work with existing, partially undocumented systems.

*Should SCVHS close this gap?* Yes. A brownfield variant of the Spec Template is needed for professional deployment of SCVHS. It should include sections for: existing system constraints, prohibited patterns, integration points that cannot be changed, and the technical environment at the start of the sprint.

*Development plan.* Add `Spec_Template_Brownfield.md` to `scvhs-templates/`. Priority: medium for educational use; high for professional deployment.

---

**9.3.6 Multi-platform integration (7 platforms)**

AI-DLC provides configuration files for seven AI coding environments: Kiro IDE, Amazon Q Developer, Cursor IDE, Cline, Claude Code, GitHub Copilot, and OpenAI Codex. A practitioner using any of these tools can activate AI-DLC by including its rule files in their project.

SCVHS v1.0 has no platform integrations. It is methodology documentation that the practitioner must consciously apply.

*Why the gap exists.* Platform integration requires engineering work on top of methodology specification. This was not in scope for v1.0.

*Should SCVHS close this gap?* Yes, progressively. Platform integration embeds the methodology in the practitioner's workflow rather than requiring deliberate recall.

*Development plan.* Phase 1: Claude Code integration via `.claude/` directory with a SCVHS `CLAUDE.md` that references the spec file, enforces SPECIFY-before-CONSTRUCT, and prompts the Comprehension Primitive before AI construction begins. Phase 2: Cursor rules and Amazon Q rules. Phase 3: remaining platforms. Priority: high for Phase 1.

---

**9.3.7 Team-level workflow governance**

AI-DLC governs how a team collectively structures its AI-assisted development process. It includes structured question capture, shared quality gates, and an explicit anti-vibe-coding principle: update design first, then regenerate code, even for quick fixes.

SCVHS v1.0 is an individual methodology. It does not specify how teams should coordinate mode assignments, share Decision Logs as the basis for code review, or conduct team-level spec review.

*Why the gap exists.* SCVHS was designed for individual practitioners in an educational program. Team application was not in scope for v1.0.

*Should SCVHS close this gap?* Yes, in limited form. A team practice supplement is needed for professional deployment. It should address: using Decision Logs as the primary artifact for code review, team-level mode assignment conversations, and the principle that spec updates precede regeneration.

*Development plan.* Add `scvhs-team-practice/` directory with a team application guide. Priority: medium for current scope; high for professional deployment.

---

**9.3.8 Design decision capture in SPECIFY**

AI-DLC captures design decisions during the Inception phase by writing questions into markdown files that team members answer collaboratively, creating a permanent record of the rationale behind requirements decisions.

SCVHS v1.0 specs capture what was decided but do not formally capture why key specification choices were made or what alternatives were rejected.

*Why the gap exists.* The SCVHS spec is intended to be the practitioner's own specification, written for their own use. The rationale is implicit in the practitioner's understanding.

*Should SCVHS close this gap?* Partially. An optional Design Decisions section in the Spec Template would allow practitioners to record key specification choices and rejected alternatives. This is optional in individual use but recommended in team and professional use.

*Development plan.* Add an optional `## Design Decisions` section to the Spec Template. Priority: low for educational use; medium for professional use.

### 9.4 Capabilities SCVHS Has That AI-DLC Lacks

The following capabilities are present in SCVHS and absent in AI-DLC. These represent the primary differentiation of SCVHS as a methodology.

| Capability | Description | Why AI-DLC lacks it |
|---|---|---|
| Comprehension requirement | The practitioner must be able to explain every construct before delivery | AI-DLC optimizes for delivery efficiency, not practitioner comprehension |
| Comprehension Primitive | A pre-construction generation act to establish reading literacy | No educational mechanism in AI-DLC |
| Scaffolding Fade model | Structured progression of support from Mode 1 to Mode 3 | AI-DLC does not address practitioner mastery development |
| Decision Log as a learning artifact | Construct-by-construct self-explanation as an owned deliverable | AI-DLC uses automated quality gates, not human self-explanation |
| Mode-based adaptive scaffolding | Support level adapts based on practitioner mastery, not artifact complexity | AI-DLC adapts based on risk and complexity, not practitioner state |
| Domain-agnostic applicability | The methodology applies to any domain where AI constructs owned artifacts | AI-DLC is scoped to software engineering |
| Educational framework | The methodology is explicitly designed to build professional mastery over time | AI-DLC is a delivery tool, not a training methodology |

### 9.5 Intentional Gaps: What SCVHS Should Not Replicate

Two AI-DLC capabilities are intentionally absent from SCVHS and should not be added:

**Open-source community model.** AI-DLC operates as an MIT-0 open-source project with 3,000+ GitHub stars as of June 2026. SCVHS is proprietary by design. Open source would expose the methodology to unattributed use and dilute the trademark basis. The IP value of SCVHS depends on its remaining attributable to NIIT.

**Automated Decision Log production.** AI-DLC uses automated quality gates as its primary validation mechanism. An AI-assisted or automated Decision Log would undermine the mechanism by which SCVHS achieves comprehension. The Decision Log's value is inseparable from the cognitive act of producing it.

### 9.6 Summary Gap Table

| Capability | AI-DLC | SCVHS v1.0 | SCVHS Roadmap |
|---|---|---|---|
| Machine-readable agent rules | Yes | No | v1.1 - Claude Code integration |
| Risk/complexity-adaptive execution | Yes | Mode selection only | v1.2 - sprint-start diagnostic |
| Automated evaluator | Yes | No | v1.1 - spec linter |
| Extension system | Yes | No | v1.1 - domain extension packs |
| Brownfield/existing-system template | Yes | Partial (Base field) | v1.2 - brownfield spec template |
| Multi-platform integrations | 7 platforms | None | v1.1 (Claude Code), v1.3 (others) |
| Team-level governance | Yes | No | v1.2 - team practice guide |
| Design decision capture | Yes | No | v1.2 - optional spec section |
| Comprehension requirement | No | Yes | Not applicable |
| Scaffolding Fade model | No | Yes | Not applicable |
| Comprehension Primitive | No | Yes | Not applicable |
| Decision Log as learning artifact | No | Yes | Not applicable |
| Domain-agnostic scope | No | Yes | Not applicable |

---

## 10. Conclusion

SCVHS addresses a structural problem in AI-assisted professional work: practitioners who receive AI-generated artifacts without a structured re-engagement protocol lack the comprehension required to diagnose failures, make modifications, or be meaningfully accountable for outcomes. The problem is not solved by prohibiting AI tools or by accepting comprehension loss as an inevitable trade-off for productivity gain.

The methodology proposes three invariants that constitute ownership of an AI-constructed artifact:
1. The practitioner specifies before anything is built.
2. The practitioner can explain every construct before it is delivered.
3. The practitioner maintains a documented record of every validation and hardening decision.

These invariants are domain-independent. They apply to software code, video content, written analysis, infrastructure configuration, and any other artifact domain where AI tools can construct and practitioners must own.

The comparative analysis in Section 9 identifies eight capability gaps relative to AWS AI-DLC. Four are designated for near-term closure (machine-readable agent rules, spec linter, extension system, Claude Code integration). Three are designated for medium-term closure (sprint-start diagnostic, brownfield template, team practice guide). One (design decision capture) is designated for optional addition. Two are intentionally absent (open-source model, automated Decision Log) for structural reasons internal to the methodology.

SCVHS v1.0 constitutes the specification document for these capabilities. The development roadmap above constitutes the scope for v1.1 and v1.2 releases. The methodology is designed to be extended as AI tool capabilities evolve and as new professional domains adopt AI-assisted construction workflows.

What remains constant across versions is the three-invariant principle. Specification, explanation, and documentation of decisions are the properties that distinguish ownership from mere receipt of AI output. They are the properties that SCVHS exists to enforce.

---

## References

[1] GitHub. (2023). *The economic impact of the AI coding assistant era*. GitHub Blog. https://github.blog/2023-06-27-the-economic-impact-of-the-ai-coding-assistant-era/

[2] Chui, M., Hazan, E., Roberts, R., Singla, A., Smaje, K., Sukharevsky, A., Yee, L., & Zemmel, R. (2023). *The economic potential of generative AI: The next productivity frontier*. McKinsey & Company. https://www.mckinsey.com/capabilities/mckinsey-digital/our-insights/the-economic-potential-of-generative-ai-the-next-productivity-frontier

[3] Stack Overflow. (2025). *2025 Developer Survey*. Stack Overflow. https://survey.stackoverflow.co/2025/

[4] Meyer, B. (1992). Applying design by contract. *IEEE Computer*, 25(10), 40-51. https://doi.org/10.1109/2.161279

[5] Beck, K. (2002). *Test-Driven Development: By Example*. Addison-Wesley Professional.

[6] OpenAPI Initiative. (2015-present). *OpenAPI Specification*. https://www.openapis.org/

[7] North, D. (2006). *Introducing BDD*. Better Software Magazine. https://dannorth.net/introducing-bdd/

[8] Amazon Web Services. (2025). *AI-DLC Workflows*. GitHub Repository. https://github.com/awslabs/aidlc-workflows

[9] Sweller, J. (1988). Cognitive load during problem solving: Effects on learning. *Cognitive Science*, 12(2), 257-285. https://doi.org/10.1207/s15516709cog1202_4

[10] Vygotsky, L. S. (1978). *Mind in Society: The Development of Higher Psychological Processes*. Harvard University Press.

[11] Wood, D., Bruner, J. S., & Ross, G. (1976). The role of tutoring in problem solving. *Journal of Child Psychology and Psychiatry*, 17(2), 89-100. https://doi.org/10.1111/j.1469-7610.1976.tb00381.x

[12] Collins, A., Brown, J. S., & Newman, S. E. (1989). Cognitive apprenticeship: Teaching the craft of reading, writing, and mathematics. In L. B. Resnick (Ed.), *Knowing, Learning, and Instruction: Essays in Honor of Robert Glaser* (pp. 453-494). Lawrence Erlbaum Associates.

[13] Bloom, B. S. (1968). Learning for mastery. *Evaluation Comment*, 1(2), 1-12.

[14] Anderson, L. W., & Krathwohl, D. R. (Eds.). (2001). *A Taxonomy for Learning, Teaching, and Assessing: A Revision of Bloom's Taxonomy of Educational Objectives*. Longman.

[15] Slamecka, N. J., & Graf, P. (1978). The generation effect: Delineation of a phenomenon. *Journal of Experimental Psychology: Human Learning and Memory*, 4(6), 592-604. https://doi.org/10.1037/0278-7393.4.6.592

[16] McDaniel, M. A., & Donnelly, C. M. (1996). Learning with analogy and elaborative interrogation. *Journal of Educational Psychology*, 88(3), 508-519. https://doi.org/10.1037/0022-0663.88.3.508

[17] Kapur, M. (2016). Examining productive failure, productive success, unproductive failure, and unproductive success in learning. *Educational Psychologist*, 51(2), 289-299. https://doi.org/10.1080/00461520.2016.1155457

[18] Prather, J., Reeves, B. N., Denny, P., Becker, B. A., Leinonen, J., Luxton-Reilly, A., Powell, G., & Finnie-Ansley, J. (2023). "It's weird that it knows what I want": Usability and interactions with copilot for novice programmers. *ACM Transactions on Computer-Human Interaction*, 31(1), 1-31. https://doi.org/10.1145/3617367

[19] Vaithilingam, P., Zhang, T., & Glassman, E. L. (2022). Expectation vs. experience: Evaluating the usability of code generation tools powered by large language models. In *CHI Conference on Human Factors in Computing Systems Extended Abstracts*. https://doi.org/10.1145/3491101.3519665

[20] Imai, S. (2022). Is GitHub Copilot a threat to your code security? In *Proceedings of the 2022 IEEE/ACM 44th International Conference on Software Engineering: New Ideas and Emerging Results* (pp. 106-110). https://doi.org/10.1145/3510454.3516678

[21] Jiang, E., Hartmann, B., Riedl, M., & Canny, J. (2022). Discovering the syntax and strategies of natural language programming with generative language models. In *Proceedings of the 2022 CHI Conference on Human Factors in Computing Systems*. https://doi.org/10.1145/3491102.3501870

[22] Becker, B. A., Denny, P., Finnie-Ansley, J., Luxton-Reilly, A., Prather, J., & Santos, E. A. (2023). Programming is hard - or at least it used to be: Educational opportunities and challenges of AI code generation. In *Proceedings of the 54th ACM Technical Symposium on Computer Science Education V. 1* (pp. 500-506). https://doi.org/10.1145/3545945.3569759

[23] Rumelhart, D. E. (1980). Schemata: The building blocks of cognition. In R. J. Spiro, B. C. Bruce, & W. F. Brewer (Eds.), *Theoretical Issues in Reading Comprehension* (pp. 33-58). Lawrence Erlbaum Associates.

[24] Schwartz, D. L., & Bransford, J. D. (1998). A time for telling. *Cognition and Instruction*, 16(4), 475-522. https://doi.org/10.1207/s1532690xci1604_4

[25] Chi, M. T. H., Bassok, M., Lewis, M. W., Reimann, P., & Glaser, R. (1989). Self-explanations: How students study and use examples in learning to solve problems. *Cognitive Science*, 13(2), 145-182. https://doi.org/10.1207/s15516709cog1302_1

[26] Van Leusen, P. H. M. (1998). Scaffolding withdrawal and the Zone of Proximal Development. In P. Vedder (Ed.), *Measuring the Quality of Education* (pp. 43-57). Swets & Zeitlinger.

---

## Appendix A: SCVHS Terminology Reference

See the SCVHS Terminology Glossary (supplementary material) for canonical definitions of all SCVHS terms.

## Appendix B: Template Library

See the SCVHS template library (supplementary material) for:
- Spec Template (generic, all technology stacks)
- Decision Log Template (generic, all technology stacks)
- Sprint Design Checklist (for content developers)

## Appendix C: Worked Examples

See the SCVHS worked examples (supplementary material) for complete worked examples across all six courses.
