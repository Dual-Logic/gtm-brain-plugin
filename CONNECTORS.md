# Connectors

## This plugin ships **no connectors** — on purpose.

The GTM Brain plugin **interviews** you about your go-to-market and **writes a spec**. It never
connects to, authenticates against, or calls any of your tools. So it ships:

- **No `.mcp.json`** and no `mcpServers` declaration in `plugin.json`.
- **No vendor defaults** — it does not assume HubSpot, Salesforce, Shopify, or any other stack.
- **No API keys, no OAuth, nothing to authenticate at install.**

This is a requirement, not an omission (Product Contract R10): the output must be *tool-agnostic* —
it names the **capabilities** a GTM Brain needs and maps them to **your actual named tools**, whatever
they are. A plugin that shipped connectors would quietly bake in a preferred stack and break that
promise.

> If a future Cowork manifest ever *requires* an MCP file to exist, it ships **empty** — never with
> vendor defaults — and this section is updated to say so.

## How tool references work instead — the `~~category` convention

Because the plugin talks *about* tools rather than *to* them, it uses a generic capability vocabulary
in prose. A skill writes `~~CRM`, not "HubSpot." During the interview:

1. Skills describe workflows in terms of **capabilities** — `~~CRM`, `~~email`,
   `~~web/product analytics`, `~~ads`, `~~data warehouse`, `~~enrichment`, and the rest.
2. The **stack-discovery step** (Phase 3) captures your **actual named tools** into the working doc.
3. The **Build Spec** maps each required capability to your named tool — `~~CRM → Close`,
   `~~ads → Meta Ads` — so the output is stack-neutral in structure yet specific to your environment.

The full capability list, with illustrative (never required) example tools per category, is in
[`reference/category-map.md`](reference/category-map.md).

## What "building it" means (for your team)

The Build Spec names capabilities and maps them to your tools; **wiring the actual integrations is
your build team's job, not this plugin's.** Where the interviewer cannot credibly describe *how* to
get data out of or push action into a named tool, the completeness pass **flags an
integration-knowledge gap** for your builder rather than hand-waving — so the spec never pretends to
know an integration it doesn't.

## Contrast with connector-based plugins

Some Dual Logic plugins (e.g. the PicassoMD BD ExecOS) *do* ship a `.mcp.json` and wire live
connectors, because those skills **act on** your CRM/email/calendar in real time. This plugin is the
opposite kind of tool: it is a **guided authoring interview**, so it stays read-only on your business
and connector-free by design.
