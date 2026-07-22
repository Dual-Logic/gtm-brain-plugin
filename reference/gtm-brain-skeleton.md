# GTM-Brain Skeleton — the fixed architecture

> **What this is.** The *fixed* backbone every GTM-Brain spec this plugin produces is built on. The
> **structure here never changes** — three layers plus an OODA+L loop — so every output is
> recognizably a GTM Brain. What *does* change per org is the **fill**: which plays, which signals,
> which decisions, which tools. Placeholders (`«like this»`) mark where discovered, org-specific
> detail goes.
>
> Skills load this file to keep their language and structure consistent. It is the interviewer's
> mental model, not a script to read aloud to the operator.

---

## The one-sentence definition

A **GTM Brain** is a *stateful decision system* for go-to-market: it continuously turns raw signals
into resolved, trustworthy **facts**, and turns facts into **decisions** that drive **plays** — and
it improves as it sees what worked. It is not a tool that *executes* faster; it is the layer that
knows *what to do*. (Framing: warmly.ai, "GTM Brain: Own Your Decisions.")

The bottleneck it addresses: modern GTM can execute infinitely (unlimited outreach, infinite
personalized copy), so the constraint has moved from **execution** to **decision quality**. The
brain is where decision quality lives.

---

## The three layers (fixed, bottom-up)

Signals flow **up**; decisions flow **down** into plays. Every play exercises some slice of all
three layers — the completeness pass (Phase 4) exists to catch layers a chosen play left
under-specified.

### Layer 1 — Evidence (data)

The raw inputs. Everything the brain observes about the market, accounts, and people, *before* it
means anything.

- **Signal types:** firmographic, technographic, intent/research, product-usage/behavioral,
  engagement (email/site/ads), relationship/CRM history, enrichment/third-party, conversational
  (calls, tickets).
- **For each signal the brain uses, the spec records:** `«what the signal is»`, `«where it comes
  from — which capability/tool»`, `«how fresh it needs to be»`, `«how reliable it is»`.
- **Failure mode to avoid:** treating evidence as truth. Raw evidence is noisy, duplicated, and
  stale until the next two layers do their work.

### Layer 2 — Identity

Resolution. Evidence is meaningless until it is attached to a **canonical entity** — this *person*,
this *account*, this *opportunity*. The identity layer dedupes, merges, and stitches signals from
many sources onto one resolved record, so a fact is about *someone* rather than about a stray row.

- **What it resolves:** person ↔ account ↔ opportunity; multiple emails/domains/records → one
  entity; anonymous behavior → known entity when possible.
- **For each play, the spec records:** `«what entity the play acts on»` and `«what has to be
  resolved/stitched for evidence to attach to it»`.
- **Why it is its own layer:** the same evidence resolved to the wrong entity produces a confident,
  wrong decision. Identity is where precision is won or lost.

### Layer 3 — Fact / Decision

Meaning and judgment. This layer turns resolved evidence into **facts**, and facts into
**decisions**.

- **The precision primitive — a fact.** A fact is the atomic unit the brain acts on: a **typed,
  sourced, dated assertion** about a resolved entity. Good facts are:
  - *Atomic* — one claim (`account is in active evaluation`), not a paragraph.
  - *Typed* — boolean / enum / number / date, not free text.
  - *Sourced* — traceable to the evidence + identity that produced it.
  - *Fresh* — carries a timestamp + a decay/confidence, so a stale fact stops driving decisions.
  - **Template:** `«FACT_NAME» = «type/value» · derived from «evidence» on «entity» · as of «date»
    · confidence «high/med/low»`.
- **Decision policies.** The rules that read facts and choose an action: `IF «facts hold» THEN
  «decision/route/priority»`. A decision is an explicit, inspectable choice — *which* play fires,
  on *whom*, *when*, with *what treatment* — not a black box.
- **For each play, the spec records:** the facts it consumes, the decision policy that fires it, and
  the action it hands off.

---

## The loop (fixed) — OODA + L

The three layers are the anatomy; the loop is the physiology. The brain runs a continuous
**Observe → Orient → Decide → Act → Learn** cycle. Every play is an instance of this loop.

| Stage | What happens | Lives in |
|---|---|---|
| **Observe** | Ingest new signals | Evidence layer |
| **Orient** | Resolve signals to entities; derive/refresh facts | Identity + Fact layers |
| **Decide** | Apply decision policies to current facts | Fact/Decision layer |
| **Act** | Fire the play (route, prioritize, personalize, alert, enrich) | Play surface |
| **Learn** | Feed outcomes back as new evidence; tune the policies and fact thresholds | Evidence → Fact |

**Learn is the difference between a workflow and a brain.** A workflow runs the same rule forever; a
brain updates its facts and policies from what the last cycle's actions produced. For each play, the
spec records `«what outcome signal closes the loop»` (reply, meeting booked, stage change, churn,
conversion) and `«how that feeds back»`.

---

## Plays sit on top of the skeleton

A **play** is a repeatable GTM motion the brain automates a decision for — e.g. "revive a stalled
opportunity," "route an inbound lead," "flag an expansion-ready account," "trigger outreach on an
intent spike." Plays are **discovered per org** (never picked from a menu — see the interview
skills). Each discovered play is specified *against this skeleton*:

```
Play: «name»
  Goal / decision automated: «the judgment the operator wants the brain to own»
  Observe  — evidence it needs:      «signals» (Layer 1)
  Orient   — entity + resolution:    «entity acted on + what must be stitched» (Layer 2)
  Decide   — facts + policy:         «facts consumed» → «IF/THEN decision policy» (Layer 3)
  Act      — the action:             «what fires and where»
  Learn    — outcome + feedback:     «outcome signal» → «what it updates»
```

This per-play template is the bridge between the **Strategy Readout** (which names the play and the
decision in business language) and the **Build Spec** (which fills every line above with the org's
real signals, facts, policies, and named tools).

---

## How the tiers use this skeleton

- **Strategy Readout** speaks the *top* of the skeleton in business language: the brain's purpose,
  the priority plays, and the decisions it makes — no layer jargon.
- **Build Spec** fills the *whole* skeleton per play: the evidence/identity/fact detail, the decision
  policies, the loop closure, and the capability→tool mapping (see `category-map.md`).
- **Completeness pass** walks this skeleton play-by-play and flags any layer left blank — a data gap
  (evidence the org has not described) or an integration-knowledge gap (a named tool whose how-to the
  interviewer cannot credibly specify). Gaps are **flagged, never silently omitted**.

## Invariants (do not violate)

1. All three layers appear in every spec; a play may lean on one, but none of the three is deleted.
2. Facts are typed, sourced, and dated — never free-text opinions.
3. The loop always closes: every play names an outcome signal and a feedback path (no fire-and-forget).
4. No fixed play catalog is ever surfaced to the operator; plays are discovered.
5. Capabilities are named generically (`~~category`) and mapped to the org's real tools — never
   hard-wired to a specific vendor.
