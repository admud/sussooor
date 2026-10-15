# Product decisions and working defaults

15 October 2026. This register distinguishes confirmed direction from proposals. Pending decisions do not imply approval to spend money, send real documents to a provider, or deploy a public application.

## Confirmed direction

- Product: Sussooor; intended public repository: `admud/sussooor`.
- Review one insurance product/proposal and associated material; replacement comparison is not the core workflow.
- ILPs are a primary supported product category.
- Explain costs, guarantees, exit conditions, and conflicts between sales claims and supplied documents, with evidence links.
- Local/private browser models and inexpensive OpenRouter models are both candidates for discussion and evaluation; neither has been selected or benchmarked.
- Prepare a PRD and developer handoff for collaborative implementation.

## Choices for the product owner

| Decision | Proposed starting point | When needed |
| --- | --- | --- |
| First user-facing AI route | Local-first with optional cloud assistance; compare both using synthetic fixtures before choosing | Before integrating real-document cloud analysis or committing privacy messaging |
| Open-source license | Apache-2.0 for permissive reuse with an explicit patent grant; MIT is a simpler alternative | Before inviting code contributions under a defined license; no license applied yet |
| First market | Singapore, English, SGD, based on the supplied plan | Before market-specific rules and a real-document pilot |
| Experiment budget | Prepare the harness without live calls; owner supplies credentials and explicit spend cap | Before any paid model invocation |

The first two choices have been requested in the project conversation. All remain pending unless recorded as resolved here. Marketing, pricing, visual branding, subscriptions, and exact model names can wait; they do not block the prototype.

## Engineering defaults

- React, TypeScript, Vite; desktop Chrome/Edge initially.
- Local text-PDF extraction and pasted/WhatsApp text first; local OCR next.
- One encrypted local vault, multiple cases, no account or cloud sync.
- A shared candidate-extraction interface with manual, browser-local, and synthetic OpenRouter adapters.
- No automated misconduct verdict or scam score. Findings identify supported statements, direct conflicts, qualifications, and missing evidence.
- A small synthetic vertical slice first; broad model/provider choice follows measured quality, cost, and latency.
- PR-based contributions after initial repository bootstrap; task IDs and dependencies in the backlog. Repository existence, branch protections, or contributor access must not be assumed from this document.

## AI paths and privacy

| Path | Data destination | Failure behavior | Current status |
| --- | --- | --- | --- |
| Manual/local model | This device; software/model assets downloaded during setup | Keep manual review available | Planned baseline |
| OpenRouter development experiment | Selected synthetic fixture text to OpenRouter and selected provider | Bounded failure; report no result; no unapproved provider fallback | Harness proposed; no provider calls made |
| User-facing cloud assistance | User-approved excerpts through a documented credential/network path to selected providers | Preserve local case; show failure and any known incurred charge | Open product decision |

A cloud path requires an accurate list of recipients, payload preview, provider/routing/retention review, credential protection, a hard spend budget and retry policy, and mode-specific privacy tests. Those details must be checked against current provider documentation during implementation. Provider data-handling guarantees are not assumed. A shared application API key must never ship in browser code. Local encryption protects saved records, not transmitted excerpts.

## Prototype versus release

Developers can build with synthetic data now after agreeing shared interfaces. The synthetic demo should prove extraction, citation navigation, narrow ILP checks, and encrypted save/restore. Independent security/legal/domain review and the full evaluation gates apply before real-document pilots and release; they are not prerequisites for writing synthetic prototype code.

No private insurance material belongs in Git, issues, PRs, CI, coding-agent prompts, or public screenshots. Use visibly synthetic labels in fixtures and demos.
