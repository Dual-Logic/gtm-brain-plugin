<!--
============================================================================
GTM-BRAIN WORKING DOC — TEMPLATE
============================================================================
This single file is BOTH:
  (1) the in-progress state the interview reads/appends across sittings, and
  (2) the final deliverable (Strategy Readout over Build Spec).

The interview skills COPY this template into the operator's project as
`gtm-brain-spec.md` on first run, then read-then-append it every phase.
Placeholders read «like this». HTML comments are authoring guidance — the
final deliverable keeps the PHASE-PROGRESS block (small, at top) and drops the
remaining guidance comments once a section is filled.

How to use this file (for the interviewer):
  - Read the PHASE-PROGRESS block first, every session. It is the resume marker.
  - Fill sections top-to-bottom as phases complete; append per sub-section, not
    only at phase boundaries, so a mid-phase interruption resumes cleanly.
  - Keep RAW CAPTURE current — it holds the operator's actual answers, so a
    resume can re-synthesize without re-asking.
  - Never delete a captured answer to "clean up"; supersede it in place.
============================================================================
-->

<!-- PHASE-PROGRESS:START — the resume marker. Every skill reads this first and rewrites it as it works. Keep it accurate. -->
```yaml
# RESUME MARKER — read this first, always.
org_name: «Org»
created: «YYYY-MM-DD»
last_updated: «YYYY-MM-DD»
current_phase: profile-and-plays   # profile-and-plays | strategy-readout | architecture-and-stack | build-spec | complete
last_completed_step: none          # free text: the last step finished within current_phase
status: in_progress                # in_progress | phase_complete | complete
resonance_confirmed: false         # set true only after the operator confirms the Strategy Readout (gate for build-tier phases)
phases:
  profile-and-plays:      not_started   # not_started | in_progress | complete
  strategy-readout:       not_started
  architecture-and-stack: not_started
  build-spec:             not_started
next_action: "Run the gtm-brain entry skill, or the profile-and-plays skill to begin Phase 1."
```
<!-- PHASE-PROGRESS:END -->

---

# GTM Brain — «Org Name»

> Draft spec produced through the GTM-Brain interview. Two linked tiers:
> the **Strategy Readout** (for the operator — is this your business?) sits above the fold;
> the **Build Spec** (for the builder — can you stand up a v1?) sits below it.

<!-- ======================= RAW CAPTURE (internal) ======================= -->
<!--
This section holds the operator's ACTUAL answers, verbatim-ish, as captured per phase.
It is the source the tiers are synthesized from and what makes a mid-phase resume lossless.
It stays in the working doc but is NOT part of what the operator/builder reads as the deliverable
(fold it under a collapsed heading or move to an appendix when finalizing).
-->

## Raw capture

### Org profile (Phase 1)
- Industry / business model: «captured»
- Motion (PLG / sales-led / hybrid; inbound vs outbound weight): «captured»
- Who they sell to (segments, ICP in their words): «captured»
- GTM team shape & who runs plays: «captured»
- Stated GTM goals (this quarter / this year), in the operator's words: «captured»
- The decisions they most wish were automatic / made better: «captured»

### Discovered plays (Phase 1) — no menu was shown; these emerged from the conversation
- Play «1»: «name» — why it matters to them: «captured»
- Play «2»: «name» — «captured»
- Play «3»: «name» — «captured»
- (Priority order the operator gave): «captured»

### Architecture inputs per play (Phase 3)
- For each play: evidence discussed, entity acted on, facts/decisions the operator described. «captured»

### Named tool stack (Phase 3)
- «~~category» → «actual named tool» (+ notes: edition/tier, who owns it, confidence). «captured»
- Tools mentioned that don't map cleanly to a category: «captured»

<!-- =============================================================================
     STRATEGY READOUT  (above the fold — operator-facing, business language)
     Fills in Phase 2. Gate: operator confirms this before any build-tier phase.
============================================================================= -->

## Strategy Readout

*Read this and tell me: is this your business?*

### What your GTM Brain is for
«2–4 sentences, in the operator's own framing: the purpose of this brain — the go-to-market
decisions it will own for «Org», and why that matters given their stated goals. No architecture
jargon. It should sound unmistakably like their business, not generic AI copy.»

### The priority plays it runs
<!-- One block per discovered play. Business language only. The decision is the star. -->
1. **«Play name»** — «one line: what motion this is, in their words».
   - *The decision it makes for you:* «the judgment the brain owns — e.g. "which stalled deals are
     worth re-opening this week, and with what angle" — not the mechanics».
   - *Why it's a priority:* «tie to a stated goal».
2. **«Play name»** — «…»
3. **«Play name»** — «…»

### What it will feel like when it's working
«2–3 sentences of the observable difference: what the operator/team stops doing manually, what gets
decided faster or better, what stops slipping. Concrete to «Org», not aspirational boilerplate.»

### The shape underneath (one paragraph, plain-English)
«A single accessible paragraph naming that the brain watches signals, resolves them to the right
accounts/people, turns them into trustworthy facts, decides which play to run, and learns from what
worked — so the operator knows there's a real architecture below without needing the Build Spec. This
is the only place the three-layer/loop idea surfaces to the operator, and it stays plain-English.»

> **Resonance checkpoint.** Operator confirms: ☐ *"Yes, this is my business."*  |  ☐ *Needs correction:*
> «notes». Build-tier phases do not proceed until this is confirmed (`resonance_confirmed: true`).

<!-- =============================================================================
     — — — — — — — — — — — —  FOLD  — — — — — — — — — — — —
     BUILD SPEC  (below the fold — technical-team-facing)
     Fills in Phase 4 (architecture captured in Phase 3). Credible enough that a
     builder stands up a v1 without returning with basic questions.
============================================================================= -->

## Build Spec

*For the eng team / technical marketer standing up v1. Every play below is specified against the
fixed GTM-Brain skeleton (evidence → identity → fact/decision + OODA+L loop). See
`gtm-brain-skeleton.md` for the model; `category-map.md` for the capability vocabulary.*

### System overview
- **Brain purpose (technical restatement):** «what the system decides, end to end».
- **The fixed skeleton, instantiated for «Org»:**
  - *Evidence layer:* «the signal sources this brain draws on, across all plays».
  - *Identity layer:* «the entities resolved (person/account/opportunity) and what must be stitched».
  - *Fact/Decision layer:* «the core facts this brain maintains + the decision policies that read them».
  - *Loop:* «how Observe→Orient→Decide→Act→Learn runs — batch/scheduled, event-triggered, or on-demand».

### The tool stack (capability → named tool)
<!-- Verbatim from RAW CAPTURE, resolved. This is what makes the spec org-specific + tool-agnostic. -->
| Capability (`~~category`) | «Org»'s tool | Tier/notes | Confidence |
|---|---|---|---|
| «~~CRM» | «e.g. Close» | «» | «high/med/low» |
| «~~email» | «» | «» | «» |
| «~~web/product analytics» | «» | «» | «» |
| «…» | «» | «» | «» |

### Plays — the "how", one per play
<!-- Repeat this block for every priority play. This is the heart of the Build Spec. -->

#### Play: «name»
- **Capability contract**
  - *Inputs:* «typed inputs the play consumes».
  - *Outputs:* «what it emits — a fact, a routed record, a drafted action, an alert».
  - *Trigger:* «what fires it — schedule, event, threshold, on-demand».
- **Observe — evidence needed:** «signals» → from «~~category → named tool».
- **Orient — entity + resolution:** acts on «entity»; must resolve «what stitching».
- **Decide — facts + policy:**
  - Facts consumed: `«FACT» = «type» · from «evidence» · as of «date» · confidence «…»` (repeat).
  - Decision policy: `IF «facts hold» THEN «action/route/priority»`.
- **Act — the action:** «what the play does, and where it writes/sends (which named tool)».
- **Learn — outcome + feedback:** outcome signal = «reply/meeting/stage-change/…»; feeds back into «which fact/policy».
- **Build notes for v1:** «concrete how — where the logic runs (workflow tool / warehouse / script / agent), what to build first, sequencing, any known integration specifics for the named tool».

### Completeness pass — gaps (flag, never omit)
<!-- Filled by the build-spec skill's completeness pass. Two gap classes. Empty is a valid result only if genuinely none. -->
**Data gaps** — a chosen play needs evidence the org has not described:
- ⚠️ Play «name» needs «signal» but «Org» did not describe a source for it. Required: «what to acquire/instrument».

**Integration-knowledge gaps** — a named tool whose how-to the interviewer cannot credibly specify:
- ⚠️ «~~category → tool» is named, but the concrete integration path (API/export/native automation) is
  not specified here. Builder should confirm: «the open question». *(Flagged rather than hand-waved as
  vague "capability" talk.)*

### Sequencing recommendation
«Which play to build first (usually the highest-priority one whose evidence + tools are already in
place with no gaps), and the rough order for the rest. One short paragraph.»
