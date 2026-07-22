# Category Map — the `~~category` capability vocabulary

> **What this is.** The controlled vocabulary the interview uses to talk about tools **generically**,
> so a spec stays tool-agnostic. A skill says `~~CRM`, not "HubSpot." The interview captures the
> org's *actual* named tool in each category; the Build Spec maps the required capability →
> that named tool. **This plugin ships no connectors and calls no tools** — `~~category` is a
> *prose* device for interviewing and mapping, never an MCP binding. See `CONNECTORS.md` for why.
>
> The example tools below are **illustrations to help the interviewer recognize what an operator
> names — never a menu, never a default, never a required stack.** If an org names a tool not listed
> here, that is normal; capture it and map to the nearest capability (or record a new capability).

## How to use `~~category` in a skill

- Refer to a capability as `~~<category>` in prose (e.g. "pull recent activity from the org's
  `~~CRM`").
- When the org has named its tool, the Build Spec writes the mapping: `~~CRM → Close`.
- If a play needs a capability the org has **no** tool for, that is a **data/capability gap** — flag
  it in the completeness pass (`gtm-brain-skeleton.md` invariants), never silently assume one.

## The capability catalog

| `~~category` | What the capability is | Its GTM-Brain role (signal it feeds / action it enables) | Example tools (illustrative only) |
|---|---|---|---|
| `~~CRM` | System of record for accounts, contacts, opportunities | Identity backbone + relationship/deal history (evidence + identity); write-back target for routing/notes (act) | HubSpot, Salesforce, Close, Pipedrive, Copper, Attio |
| `~~email` | Business email send/inbox | Engagement signal (opens/replies/threads); draft/send channel (act) | Gmail / Google Workspace, Microsoft 365 / Outlook |
| `~~calendar` | Meeting scheduling | Meeting-held signal; booking as an outcome (learn) | Google Calendar, Microsoft 365 |
| `~~sales engagement` | Outbound sequencing / cadence | Touch history + reply signal; sequence enrollment (act) | Outreach, Salesloft, Apollo, Groove |
| `~~web/product analytics` | Website + in-product behavior | Behavioral/product-usage evidence (the richest first-party signal for PLG) | Amplitude, Mixpanel, PostHog, Segment, GA4 |
| `~~intent` | Third-party buying-intent / research signals | In-market evidence beyond first-party | 6sense, Bombora, G2, Demandbase |
| `~~enrichment` | Firmographic / contact enrichment | Fills identity + firmographic evidence; dedup keys | Clearbit, Apollo, ZoomInfo, Cognism |
| `~~conversation intelligence` | Call/meeting recording + analysis | Conversational evidence + sentiment; outcome capture (learn) | Gong, Chorus, Fathom, Fireflies, Otter |
| `~~data warehouse` | Central analytical store | Where facts are computed + kept fresh; the brain's memory | Snowflake, BigQuery, Redshift, Databricks |
| `~~reverse-ETL / activation` | Syncs warehouse-computed facts back into operational tools | Turns facts into action across the stack (act) | Hightouch, Census |
| `~~CDP` | Customer data platform / identity resolution | Stitches a person/customer across sources (identity layer) | Segment, RudderStack, Twilio Segment |
| `~~marketing automation` | B2B nurture / lifecycle email + scoring | Nurture engagement evidence; program enrollment (act) | Marketo, Pardot, HubSpot Marketing |
| `~~email/SMS marketing` | DTC lifecycle messaging | Engagement + purchase-driving channel (act); engagement-decay signal | Klaviyo, Braze, Iterable, Attentive |
| `~~commerce/orders` | E-commerce order + customer store | Purchase evidence (orders, RFM, LTV inputs); the identity anchor for DTC | Shopify, BigCommerce, WooCommerce |
| `~~ads` | Paid acquisition platforms | Spend + conversion evidence; audience push (act — the paid feedback loop) | Meta Ads, Google Ads, LinkedIn Ads, TikTok Ads |
| `~~attribution/marketing analytics` | Spend attribution + blended performance | ROAS/efficiency facts across channels | Triple Whale, Rockerbox, Northbeam |
| `~~support / helpdesk` | Customer support / ticketing | Support-signal evidence (risk, sentiment); a channel for CS plays | Zendesk, Gorgias, Intercom, Front |
| `~~relationship intelligence` | Professional-network / relationship graph | Relationship-strength + trigger-event evidence (partner-led motions) | LinkedIn Sales Navigator, relationship-graph tools |
| `~~newsletter/content` | Owned audience / content distribution | Audience engagement evidence; nurture channel (act) | Beehiiv, Substack, ConvertKit |
| `~~workflow / automation` | Cross-tool orchestration glue | Where lightweight decision logic + syncs run when there's no warehouse | Zapier, n8n, Make, Workato |

## Notes on using categories well

- **One capability can be served by a tool that also serves another.** HubSpot can be `~~CRM` *and*
  `~~marketing automation`; Segment can be `~~web/product analytics` *and* `~~CDP`. Capture the
  overlap; don't force a 1:1.
- **Low-infrastructure orgs are normal.** A professional-services firm may have no `~~data warehouse`
  and no `~~CDP` — facts live in the `~~CRM` and a spreadsheet, and `~~workflow / automation` is the
  glue. The Build Spec's v1 notes must match the org's real infrastructure, not assume a warehouse.
- **Uncommon tools are the whole point.** The tool-agnostic promise (R10, AE3) is proven when the org
  names something not in the "example tools" column and the spec still maps its capability cleanly.
- **A named capability with no how-to is a gap, not a hand-wave.** If the interviewer cannot credibly
  say *how* to get data out of / push action into a named tool, that is an **integration-knowledge
  gap** for the completeness pass — flag it for the builder; do not paper over it with vague
  "capability" language.
