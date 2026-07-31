# SCVHS Pipeline — The Five Phases

> Canonical specification of the SCVHS five-phase pipeline.  


---

## The Pipeline

```
SPECIFY → CONSTRUCT → VALIDATE → HARDEN → SHIP
```

The phases are invariant. What changes between modes is:
- Who performs SPECIFY (learner, or AI-drafted and learner-reviewed in Mode 3)
- Who performs CONSTRUCT (human, AI tool, or both)
- How deeply the Decision Log entries are written

---

## Phase 1: SPECIFY

**The engineer writes the spec before any construction begins.**

### What happens
The learner writes a `Spec_S0N_[Title].md` file that defines:
- What the artifact is and what it does
- The structure, constraints, and parameters (technology-stack specific)
- The Acceptance Criteria — a binary pass/fail checklist used in VALIDATE

**Exception, Mode 3 only:** an AI tool drafts the spec from the README, `Spec_Creation_Prompt.md`, and `Sample_Spec_Template.md`. The learner reviews and finalizes the draft before it is used to direct construction; an unreviewed draft is not a valid spec. See [01-modes.md](01-modes.md).

### The invariant
No code is written before the spec is complete. The spec is the contract. Any AI output that violates the spec is a defect, regardless of whether the output looks correct or runs without errors.

### What a good spec enables
- An AI tool can construct the artifact from the spec alone, with no additional instruction
- A different engineer (or the same engineer in a future sprint) can understand what was built and why
- VALIDATE has an objective standard — the spec — rather than relying on the learner's judgment about what "looks right"

### Common failure modes in SPECIFY
| Failure | Description | Fix |
|---|---|---|
| Intent spec | "Make it responsive" | Structure spec: "grid-cols-1 default, grid-cols-2 sm:, grid-cols-3 lg:" |
| Missing constraints | No rules, only descriptions | Add a Constraints section listing what is forbidden |
| Untestable criteria | "The page should look clean" | Binary: "Zero custom CSS — no .css file, no style= attribute" |
| Missing mode declaration | Spec header has no SCVHS Mode field | Every spec must declare mode in the header |

### Output
File: `Spec_S0N_[Short_Title].md`  
Template: [../scvhs-templates/Spec_Template.md](../scvhs-templates/Spec_Template.md)

---

## Phase 2: CONSTRUCT

**The artifact is built from the spec.**

### Who constructs
Determined by the SCVHS Mode:

| Mode | Who constructs |
|---|---|
| Mode 1: Hand-First + Validate AI | Learner by hand |
| Mode 2: Hybrid | AI tool, directed by spec |
| Mode 3: AI-Drafted Spec | AI tool, directed by the learner-reviewed AI-drafted spec |

### The invariant
Construction follows the spec, not instinct, habit, or a remembered pattern. In AI-construction modes, the spec is passed to the AI tool verbatim or near-verbatim — the learner does not guide the AI with verbal additions that are not in the spec.

### Comprehension Primitive
In Modes 2 and 3, the Comprehension Primitive is completed BEFORE directing the AI. See [02-comprehension-primitive.md](02-comprehension-primitive.md).

### AI direction
In Modes 2 and 3, the learner gives the full spec to the AI tool (in Mode 3, the spec they reviewed and finalized after the AI drafted it). The AI generates the artifact. The learner saves the AI-generated file with a name that makes it identifiable as AI output (e.g., `portfolio-ai-generated.html`, `styles-ai-generated.css`). This file is committed alongside the corrected version for comparison.

### Output
- In Mode 1: learner's hand-built artifact + AI-generated version
- In Modes 2–3: AI-generated version (corrected version produced during HARDEN)

---

## Phase 3: VALIDATE

**The engineer reads the artifact against the spec, construct by construct.**

### The unit of attention: the construct
A construct is one logical unit of the technology in use:
- HTML: one landmark section, one semantic element
- CSS: one rule set, one selector group
- JavaScript: one function, one class
- Spring Boot: one endpoint method, one service class
- Docker: one Dockerfile, one service in compose

The learner reads one construct, writes a Decision Log entry, reads the next construct, writes the next entry. The Decision Log is filled in real time, not after finishing the whole file.

### The Decision Log
Same format in every mode: one entry per Constraint and one entry per Acceptance Criterion in the spec, every one requiring a full entry, pass or fail, that explains what the code does. What differs by mode is how "Match with spec" gets determined: in Mode 1, by comparing against the learner's hand-built reference; in Mode 2 and Mode 3, by validating directly against the spec. Mode 3 follows the Mode 2 Decision Log rules exactly, since the spec being AI-drafted only changes SPECIFY, not VALIDATE.

See [03-decision-log.md](03-decision-log.md) for the full Decision Log specification.

### Validation tools
Validation is active, not passive. The learner uses tools appropriate to the technology:

| Technology | Validation tools |
|---|---|
| HTML | W3C Validator, browser DevTools Accessibility pane, keyboard navigation |
| CSS | Browser DevTools Computed panel, DevTools Accessibility colour contrast |
| Tailwind | Browser DevTools, Device Mode at each breakpoint |
| JavaScript | Browser console, DevTools debugger, deliberate error injection |
| TypeScript | TypeScript compiler (`tsc --noEmit`) |
| React | React DevTools, component rendering in browser |
| Spring Boot | Postman, Spring application logs, unit tests |
| Docker | `docker build`, `docker run`, `docker images`, `docker compose up` |
| CI/CD | Pushing to test branch, observing pipeline execution |

### The comprehension defect
If the learner cannot explain what a construct does in plain English, that is a defect. It is recorded in the Decision Log as a comprehension defect: "I cannot explain what this construct does." This defect must be resolved during HARDEN before the artifact ships.

### Output
Decision Log with all VALIDATE entries complete. Defects identified, counted, and categorized.

---

## Phase 4: HARDEN

**Every defect from VALIDATE is fixed. Edge cases, security, and robustness are addressed.**

### What HARDEN covers
1. **Defect fixes:** Every entry in the Decision Log marked "No" or "Partial" must be fixed in the code. The fix is recorded in the same Decision Log entry.
2. **Edge cases:** What happens in boundary conditions — empty arrays, null inputs, network failures, missing env vars, very narrow viewports?
3. **Security:** Are secrets in environment variables (not hardcoded)? Are inputs validated? Are dependencies up to date?
4. **Accessibility:** Does the page work with keyboard navigation? Does it meet WCAG AA contrast? Does a screen reader navigate the structure correctly?
5. **Comprehension defects:** Any construct the learner could not explain must be understood and explained before shipping.

### The invariant
Defects are fixed in the code. "Known issue" is not an acceptable HARDEN output. If a defect cannot be fixed in the available time, it is escalated — not shipped.

### Recheck
After all defects are fixed, the full Acceptance Criteria from the spec are checked again from the top. Fixing one defect can introduce another (e.g., changing a CSS rule to fix a specificity problem may affect contrast).

### Output
- Corrected artifact (defects fixed)
- Completed Decision Log (all entries have fix recorded where applicable)

---

## Phase 5: SHIP

**The corrected artifact and completed Decision Log are committed together.**

### The commit
The commit contains:
- The corrected artifact
- The AI-generated version (for comparison and audit)
- The completed Decision Log
- The spec, including the Comprehension Primitive (Modes 2/3): committed alongside everything else,
  not excluded. See `02-comprehension-primitive.md` (updated 2026-07-18) for why it is now part of
  the deliverable set rather than a discarded scratch file.

### The commit message
The commit message must be meaningful. It names what was built and what was validated, not just the change type:

Good: `feat: build semantic portfolio HTML; validate AI output and fix 5 semantic defects`  
Bad: `final version`  
Bad: `update HTML`

### CI/CD
If a pipeline is configured, it must pass before the commit is merged. The pipeline is not a substitute for the Decision Log — it tests behavior; the Decision Log records human evaluation. Both are required.

### The commit IS the evidence
A commit containing a corrected artifact, an AI-generated version, and a completed Decision Log is the evidence that the engineer:
1. Directed AI construction from a spec
2. Validated the output construct by construct
3. Hardened every defect
4. Owns the result

This is the unit of engineering work in SCVHS.
