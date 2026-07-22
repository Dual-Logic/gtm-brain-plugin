# Working-Doc & Resume Convention

> **What this is.** The operational contract every skill in this plugin follows for reading, writing,
> and resuming the single working doc. Cowork has **no built-in cross-session resume** — this
> convention *is* the resume mechanism. All five skills (`gtm-brain`, `profile-and-plays`,
> `strategy-readout`, `architecture-and-stack`, `build-spec`) read this file and obey it exactly.

---

## 1. Where the working doc lives

One file, in the **operator's project** (not inside the plugin, so it survives plugin updates and is
the operator's to keep):

```
${CLAUDE_PROJECT_DIR}/gtm-brain-spec.md
```

- `${CLAUDE_PROJECT_DIR}` is the operator's current project root (a Cowork/Claude Code variable).
- If `${CLAUDE_PROJECT_DIR}` is unavailable in the runtime, use the current working directory and
  tell the operator where the file was created.
- The plugin's own `reference/working-doc-template.md` is the **read-only source** the entry skill
  copies from — never edited in place, never the working copy.

## 2. The read-then-append contract

Every phase skill, on every run, does this in order:

1. **Read** `${CLAUDE_PROJECT_DIR}/gtm-brain-spec.md` in full (it is small enough to load whole).
2. **Read the PHASE-PROGRESS marker first** (see §3) to know where things stand.
3. **Append / fill** its own sections — it writes into the sections it owns and updates RAW CAPTURE;
   it does **not** rewrite sections owned by other phases.
4. **Update the PHASE-PROGRESS marker** to reflect exactly what just happened (phase, last step,
   status, phase states) — this is the single most important write; do it before ending the turn.

Never start a phase's work from a blank doc if the file already exists. Never delete a captured
answer to "tidy up" — supersede it in place and note the change in RAW CAPTURE.

## 3. The PHASE-PROGRESS marker — read it first, keep it true

At the top of the working doc, between `<!-- PHASE-PROGRESS:START -->` and
`<!-- PHASE-PROGRESS:END -->`, is a YAML block (see the template). It is the resume state. Fields:

| Field | Meaning | Who writes it |
|---|---|---|
| `current_phase` | The phase in progress or next to run | Each phase skill as it starts/ends |
| `last_completed_step` | Free-text label of the last finished step *within* `current_phase` | The running phase skill, after each sub-step |
| `status` | `in_progress` \| `phase_complete` \| `complete` | The running phase skill |
| `resonance_confirmed` | `true` only after the operator confirms the Strategy Readout | `strategy-readout` only |
| `phases.<name>` | `not_started` \| `in_progress` \| `complete` per phase | Each phase skill |
| `next_action` | Plain-English pointer to what to do next | Whichever skill just ran |

**Cadence rule (this is what enables mid-phase resume — AE5).** Update `last_completed_step` and
append the just-captured RAW CAPTURE **after each sub-step**, not only at phase boundaries. A phase
is a sequence of steps; if the session ends or compacts mid-phase, the next run reads
`last_completed_step` and continues at the next step — captured answers are already persisted, so
nothing is re-asked and nothing is lost.

## 4. Resume orientation (what a skill does when the doc already exists)

1. Read the marker. Determine `current_phase`, `last_completed_step`, and each `phases.<name>` state.
2. **Report** to the operator, briefly: what's captured so far and what's next (e.g. "You've finished
   the play discovery and confirmed the Strategy Readout. Next is architecture + stack capture. Pick
   up there?").
3. **Route** to the correct phase — resuming **mid-phase** at the step after `last_completed_step`
   when the phase is `in_progress`, or at the start of the next phase when the current one is
   `phase_complete`.
4. Never restart from the top when a working doc exists.

## 5. The out-of-order guard (every phase skill)

Cowork may auto-trigger a skill by description match at the wrong time. So **each phase skill checks
the marker before doing its work** and declines to run out of sequence:

- If an **earlier** phase is not yet `complete`, the skill says so and points to the right phase
  instead of running. Example: `build-spec` invoked while `architecture-and-stack` is `not_started`
  → it declines and routes back.
- **The resonance gate (AE4).** No build-tier phase (`architecture-and-stack`, `build-spec`) proceeds
  unless `resonance_confirmed: true`. If it's false, the skill routes back to `strategy-readout` for
  the operator's confirmation first.
- The guard defers to the marker, not to how the skill was invoked — the marker is the source of
  truth for sequence.

## 6. Phase order (canonical)

```
profile-and-plays  →  strategy-readout  →  [resonance gate]  →  architecture-and-stack  →  build-spec  →  complete
```

The `gtm-brain` entry skill owns doc creation and routing; it does not do phase work itself. Each
phase skill owns its sections of the doc and its slice of the marker, reads the shared `reference/`
docs it needs, and hands the marker forward on completion.

## 7. Failure / edge handling

- **No working doc, phase skill invoked directly:** route the operator to the `gtm-brain` entry skill
  (which creates the doc), or create it from the template and start Phase 1 if the operator confirms.
- **Marker missing or malformed** (hand-edited): reconstruct `current_phase` from which sections are
  filled, tell the operator what you inferred, and rewrite a clean marker.
- **Operator jumps ahead** ("just write the build spec"): honor intent only if the gate + prerequisite
  phases allow; otherwise explain what's needed first. Don't silently skip the resonance gate.
