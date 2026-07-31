# AI Decision Log Templates

Use the template for your sprint's SCVHS Mode, declared in your spec's header:

- **Mode 1 (Hand-First + Validate AI):** [AI_Decision_Log_Template_Mode1.md](AI_Decision_Log_Template_Mode1.md)
- **Mode 2 (Hybrid / Generate-then-Explain):** [AI_Decision_Log_Template_Mode2.md](AI_Decision_Log_Template_Mode2.md)
- **Mode 3 (Full SCVHS) and Mode 4 (AI-Drafted Spec, Advanced):** [AI_Decision_Log_Template_Mode3.md](AI_Decision_Log_Template_Mode3.md)

The rules differ per mode (Mode 1 compares your hand-built version against a discarded AI
foil; Mode 2 explains every construct; Mode 3 and Mode 4 log defects only), but the basis
for every entry, in every mode, is the same: check the construct against a specific
Constraint or Acceptance Criterion named in your own spec, nothing else, no separate
checklist. If an entry can't name which line of the spec it's checking against, it isn't
a valid entry.
