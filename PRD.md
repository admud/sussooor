# Sussooor product requirements

Version 0.4 · 15 October 2026 · Draft for product and engineering review

Developer starting points: [decisions](DECISIONS.md), [handoff](DEVELOPER_HANDOFF.md), and [backlog](BACKLOG.md). Requirements below are planned behavior; none are implemented or validated yet.

## 1. Product decision

Sussooor gives someone considering or holding insurance a private, evidence-based second look at what they have been sold. The motivating question is: “Is this agent trying to rip me off?” The product answers with disclosed costs, conditions, contradictory statements, missing information, and questions to ask. It cannot establish an agent's intent or misconduct from documents alone.

**Promise:** Understand what you’re being sold. Check the costs, catch conflicting claims, and ask better questions—privately.

This PRD supersedes the replacement-policy framing and the exclusion of ILPs in the earlier Browser-first Insurance Review MVP plan v0.2. Its applicable security and evidence requirements remain design inputs, subject to the decisions below. The first release reviews one product and its associated sales material; an old/new policy comparison is not required.

## 2. Audience and problem

Working launch assumption, inherited from the supplied plan and to confirm before jurisdiction-specific release: adults in Singapore reviewing their own, or explicitly authorized, English-language, SGD individual life-insurance material. Primary product: investment-linked policies. Term life is a simpler secondary supported path. Whole-life and endowment documents may be reviewed for explicit charges, guarantees, illustrations, and conditions; specialist interpretation remains out of scope.

Users struggle to distinguish premiums from amounts invested, projected values from guarantees, and flexible-sounding pitches from actual exit conditions. Charges can be spread across illustrations, product summaries, schedules, and fund documents. A chat may make a claim the contract qualifies, or the supplied documents may simply be insufficient.

The job: “Before I commit—or when I have doubts—help me understand my obligations and the evidence behind the sales pitch, so I can ask informed questions.”

## 3. Outcomes and non-goals

A useful review lets a user explain their payment commitment, identify material disclosed costs and exit conditions, distinguish guarantees from illustrations, and follow each finding to its source. It should say which documents and pages were not checked.

The MVP does not rank agents, assign scam/fraud scores, declare a product good or bad, recommend buying/keeping/cancelling/surrendering, or infer that a high fee is misconduct. No personalized suitability assessment, alternative-product recommendation, investment forecast, IRR, actuarial valuation, tax/CPF advice, medical underwriting interpretation, or automatic complaint submission.

No replacement workflow, accounts, cloud sync, shared cases, integrations, analytics, billing, or payments. No audio/video or screenshot-chat interpretation. No cloud OCR or automatic cloud inference fallback. A synthetic-only OpenRouter development experiment is in scope; user-facing cloud assistance remains an open product decision under section 10. Non-English, universal life, Integrated Shield/riders, and complex critical-illness definitions are unsupported specialist areas; show scope limits and abstain on those conclusions.

## 4. Core experience

1. **Understand the boundary.** Explain local processing, device storage, supported materials, and limits. Confirm ownership or permission without collecting an NRIC or policyholder name.
2. **Set up or unlock.** Create an encrypted vault with a confirmed long passphrase, explain no provider reset, and check browser capability/storage. Use neutral case labels.
3. **Add material.** Import PDFs, WhatsApp text exports, or pasted text. Although users may say “upload,” explain that processing is intended to happen on this device. Label document type, issued/proposed/generic status, version/date, and chat salesperson. Preview ambiguous chat dates and incomplete context.
4. **Check completeness.** List supplied sources and suggest missing product summary, personalized illustration, policy schedule, charge tables, fund information, or written clarification. Missing material never becomes an invented conclusion.
5. **Confirm evidence.** Show extracted passages beside proposed facts and claims. Users confirm amounts, currencies, dates, frequencies, charge bases, and guarantee labels before dependent calculations. Manual selection works without AI.
6. **Read the review.** Show plain-language summary, costs/commitments, guarantees/illustrations, claim checks, exit conditions, unanswered questions, and review coverage. Clicking a factual statement opens the source page or chat lines.
7. **Keep or take away.** Save encrypted, lock/reopen, create encrypted backup, or deliberately export a warned plaintext Markdown report. Export should minimize identifiers by default.

A policy without a sales chat still supports a document explanation and questions. A chat without a contract supports claim collection and missing-evidence questions, not verified contract conclusions.

## 5. Review requirements

| Area | MVP behavior | Required restraint |
| --- | --- | --- |
| Payment commitment | Extract premium, frequency, payment term, coverage term, and relevant conditions | Never treat payment and coverage periods as interchangeable |
| ILP money flow | Explain premium allocation and disclosed deductions with exact bases and timing | Premium paid is not automatically the amount invested |
| Charges | Surface allocation/distribution, policy/admin, insurance, fund-management, rider, switching, withdrawal and surrender charges where supplied | Missing charge is unknown, not zero; do not double-count charges embedded in fund values |
| Charge mechanics | Preserve rate/amount, base, period, effective date, tier, and whether fixed or variable | Do not add percentages with different bases or extrapolate age-based charges |
| Guarantees | Separate explicit guarantees from conditions and non-guaranteed illustrations | Illustrated return assumptions are not promised investor returns |
| Benefits and risk | Explain stated death benefit basis and explicit investment/lapse risks | No benefit valuation or prediction of future fund performance |
| Exiting or pausing | Quote surrender/withdrawal terms, premium holidays, lock-in language, and stated consequences | Do not infer that “can withdraw” means free withdrawal or unchanged coverage |
| Cancellation window | Surface an explicitly stated free-look period and its conditions | No generic deadline presented as the user's verified deadline; request missing delivery dates |
| Sales claims | Compare selected exact claims to relevant passages from supplied material | No chat means no salesperson-claim verdict; conflicts between documents need clarification |
| Compensation | Show commissions/distribution costs only where explicitly disclosed | Do not infer the agent's personal earnings or equate distribution cost with commission received |

The cost view is a disclosed-charge inventory, not a complete total-cost model. A fee calculator must be deferred when bases, fund balance, units, time, or future rates are unknown. At most show deterministic calculations on confirmed comparable inputs, with formula, anchors, period, and assumptions. Never label premiums paid minus surrender value as a calculated financial loss.

## 6. Findings and evidence contract

Allowed internal statuses:

- `supported_in_supplied_material`: the supplied passages support the specific statement, within stated scope.
- `documented_mismatch`: a direct, comparable conflict between an exact claim and supplied evidence.
- `qualification_to_check`: conditions materially limit a claim, or supplied sources conflict.
- `cannot_verify`: missing, unreadable, unsupported, or ambiguous evidence.

UI wording should use “Matches supplied material,” “Conflicts with supplied material,” “Condition to clarify,” and “Not enough evidence.” No numeric trust score or generalized “safe” label. Prioritize by potential consequence, with a short rationale; uncertainty must remain visible. An unprocessed page is not evidence of absence.

Each finding contains the exact claim where applicable, bounded explanation, status, relevant source excerpts, caveats, and a neutral question. Every material factual statement must have a validated anchor. Anchors identify immutable document/extraction revision, physical page (separate from printed page label) and bounding box/text offsets, or chat lines/timestamp, plus exact quotation. Unicode offset convention must be specified and tested. Corrections create revisions and invalidate dependent findings/reports.

Documents and chats are untrusted input. Never execute embedded links, scripts, instructions, or model-suggested actions. Quote existence is necessary but does not by itself prove semantic support.

## 7. Example first vertical slice

Use entirely synthetic ILP documents and chat:

- Product illustration states S$300 monthly premium, a disclosed allocation charge with an explicit year/base, non-guaranteed illustrated values, and a year-one surrender charge.
- Chat states “all S$300 goes into your investments,” “the illustrated return is guaranteed,” and “withdraw anytime with no charges.”
- User imports, labels, and confirms the source passages and claim spans.
- Review identifies the precise allocation conflict, qualifies the guarantee claim using the supplied illustration wording, and checks withdrawal wording against the supplied surrender terms. Distinguish partial withdrawal from full surrender; abstain if only one is documented.
- A missing fund document generates a question about fund charges, not a made-up fee.
- A simple calculation is permitted only if the confirmed charge is explicitly 5% of each S$300 premium: S$15 for that premium. This is not an annual or lifetime cost estimate.
- Save, lock, reopen, and navigate to the same evidence; restore an encrypted backup in a fresh browser profile.

Expected question examples: “Which document guarantees this return?”, “What deductions apply before my premium purchases units?”, “What charges and coverage changes apply to partial withdrawal versus full surrender?”, and “Can insurance charges increase, and where is that schedule?”

## 8. Import and coverage

Initial engineering caps, to be validated: 12 files, 100 combined PDF pages, 100 MiB per case; 25 MiB per PDF and 5 MiB per chat. Validate signatures, sizes, and page counts. Preserve immutable originals and local hashes. Reject safely before expensive work where possible.

Start with text PDFs and pasted/exported text. Add scanned PDF OCR as the next milestone and require it before claiming scanned-document support. Flag low-quality extraction, hidden-text discrepancies, reading-order uncertainty, omitted attachments, and incomplete excerpts. Users can correct text with original and corrected revisions retained encrypted.

Process sequentially with cancellation and page-level error states. Proposed limits: 12 megapixels/render, 30 seconds/page parsing, 120 seconds/page OCR. Measure and revise before release; these are not achieved benchmarks. Timeout or worker failure must preserve the case and mark pages unprocessed.

The report identifies supplied material, pages checked, unavailable pages, confirmed versus unconfirmed inputs, unsupported areas, and rules performed. “No detected conflict” never implies a complete review or suitable product.

## 9. Privacy, security, and local storage

Target architecture: React + TypeScript + Vite static app; pinned local PDF.js worker/custom viewer; pinned local Tesseract.js/WASM/English OCR assets; Web Crypto; encrypted IndexedDB; deterministic evidence/rules. Optional PWA after offline behavior is verified. Initial supported browser matrix: current desktop Chrome and Edge on Windows/macOS; other browsers/devices require qualification.

Local mode has no document-content backend or remote inference/OCR. No mode may include remote fonts, third-party embeds, analytics, or content-bearing crash reporting. Setup downloads verified release assets before unlocking. Missing local runtime assets fail closed; lock and return to setup. Cache software assets only, never plaintext case content. Local/manual review must work offline after setup, including cold reopen; any future cloud assistance needs connectivity. Stage updates until vault sessions are locked; no surprise reloads or forced activation.

Encrypt originals, filenames, labels, text, chats, evidence, facts, reports, and indexes. Envelope candidate: random AES-256 data key wrapped with a PBKDF2-HMAC-SHA-256 passphrase key, fresh >=128-bit salt, initially 600,000 iterations subject to benchmark/review. AES-GCM uses fresh random 96-bit IVs and 128-bit tags for every object revision; authenticated canonical metadata binds IDs, types, revisions and envelope parameters. Bound/validate header fields and KDF costs before crypto. No persisted passphrase, unwrapped key, plaintext catalog, or recovery secret. Independent crypto review is a release gate.

Encrypt before short transactional IndexedDB writes; commit ciphertext/catalog atomically. Enforce a single writer across tabs. Handle quota failures without false save success. Explain and request persistent storage, show whether granted, and warn that browser clearing/device loss can remove the vault. Request permission for durable storage at an understandable point; never equate it with backup.

Lock explicitly, after five minutes of inactivity, and on hidden document by default. Recheck elapsed time on return and back/forward-cache restore. Cancel workers, clear viewers/object URLs, and discard runtime key/index references. Do not claim reliable OS-lock detection or complete memory erasure.

Encrypted backup includes validated committed ciphertext and wrapped-key header. Restore validates size/schema/authentication into a new vault without overwriting the current vault. Passphrase change rewraps the data key with fresh salt/IV after current-passphrase verification; older backups retain the old passphrase. Plaintext export warns that vault protection no longer applies, escapes hostile Markdown/HTML/link/image syntax, and disables automatic linkification.

Use a dedicated origin and tested restrictive CSP for page and workers, with active PDF features/external fetching disabled. Browser-delivered code, extensions, an unlocked session, and compromised devices remain trust boundaries. Static hosting sees normal asset-request metadata; service-worker update checks may contact the origin. Do not promise enforced network isolation, permanent erasure, or “100% secure.”

Before production claims, inspect real storage and request traces with unique synthetic canaries during import, OCR, failure, save, lock, reopen, export, and restore. No app-created plaintext persistence is acceptable. Local mode must send no document-content requests. Synthetic development experiments may send only the selected synthetic fixture payload. A future cloud mode needs separate transmission tests against its approved payload and provider boundary.

## 10. Automation and AI

The first useful version is manual-assisted: extraction, evidence selection, confirmation, deterministic checks, and report generation. The consumer experience should eventually propose relevant passages automatically, but every critical input remains human-confirmed.

Develop the manual evidence workflow and a replaceable model interface together. Run an early, explicit OpenRouter experiment on synthetic fixtures to measure whether a lower-cost hosted model can propose useful facts, claims, and quotations. No live provider calls belong in routine CI; credentials stay outside the repository and browser bundle. Experiments do not authorize transmission of real policy documents or chats. Exact models, providers, spend limits, and retention/routing settings must be selected and documented before paid runs.

Evaluate browser inference through a local adapter using pinned assets, bounded context, strict schemas, exact citation checks, hardware measurements, and no tools or remote fallback. Compare candidates on the same held-out fixtures. Measure supported findings, citation validity, omissions, latency, failure/retry rates, and actual cost per completed review; token price alone is insufficient. Publish local download/memory costs as well. Unsupported hardware returns to manual review.

Model output proposes candidate facts, claim relationships, and explanations. A validated rule on confirmed comparable facts, or explicit human adjudication of the evidence relationship, establishes the final finding. A model's self-reported confidence and a valid quotation alone do not establish support. Code performs financial math. Record the model, provider, prompt/schema versions, input revision IDs, and validation outcome in the encrypted analysis record.

**Open release decision:** local-only, local-first with opt-in cloud assistance, or cloud-assisted first with local inference later. Until decided, the default product path remains local/manual and the OpenRouter adapter is a synthetic development tool. If cloud assistance is selected, require an explicit payload preview, mode/provider disclosure, reapproval for changed payloads, reviewed provider data handling, bounded spend/retries, and a secure credential approach. Never embed a shared API key in frontend code or silently switch providers or modes. Redaction is risk reduction, not guaranteed anonymization. Local encryption does not protect text after transmission; local-only privacy wording cannot describe cloud-assisted reviews.

## 11. Report

A five-minute report contains:

1. What was supplied and what was checked.
2. Product and payment facts, with confirmed status.
3. Disclosed costs, guarantees versus illustrations, and exit conditions.
4. Evidence-backed claim findings, where chat/claims were supplied.
5. Missing information and unsupported/unreadable areas.
6. Three to five prioritized neutral questions.

Every material statement has a source link. Exports cite filename, physical page/printed label or chat lines, and short exact excerpts without internal paths. Educational material is labeled separately from contract-specific evidence and includes dated official references.

## 12. Release gates and evaluation

All targets below are proposed, not achieved. Use at least 60 synthetic cases and 300 labeled checks, reserving at least 20 cases/100 checks by template family for blind holdout. Include ILP charge bases, embedded versus additional fees, variable insurance charges, guarantee traps, partial withdrawal versus surrender, conflicting versions, missing funds/schedules, OCR/tables/footnotes, and scope abstentions. Two reviewers and an insurance-domain adjudicator assess findings; publish raw counts, confidence intervals, coverage, and abstention.

| Gate | Required outcome |
| --- | --- |
| Citation integrity | 100% valid material anchors and correct revisions |
| Semantic support | >=98% supported material statements; zero critical unsupported guarantee/value claims |
| Direct conflict precision | >=95%, with <=5% false positives on non-conflict checks |
| Supported-check recall | >=85%, with coverage and abstention reported |
| Critical inputs | 100% block dependent calculations/conclusions until confirmed |
| Arithmetic | 100% golden integer-cent/decimal cases; no mixing of bases or unsupported forecasts |
| Behavior | No personalized transaction recommendations, intent accusations, or fabricated fees |
| Privacy | No app-created plaintext persistence; no document-content requests in local mode; synthetic development egress limited to selected fixtures; separately test any approved future cloud mode |
| Recovery | Wrong passphrase/tampering fail safely; fresh-profile restore and offline cold reopen pass |
| Resilience | Quota, crash, stale-tab, worker timeout, hidden/resumed page and update/migration cases pass |
| Usability | At least 4 of 5 consented users find evidence and explain a material qualification unaided |

Measure parsing/OCR on 8 GB and 16 GB desktop baselines before latency promises. Proposed interaction goals: cancellation acknowledgement within one second and lexical search within 500 ms at the case cap.

Before real-document pilots: independent security review, Singapore legal/compliance review of actual behavior/marketing/privacy/consent, license review, and insurance-domain review of ILP rules/fixtures. Disclaimers and local processing do not establish a financial-advice exemption. Consult current MAS advisory-service guidance and MoneySense education; educational sources do not establish a particular policy's terms. Do not collect private policy files for support or evaluation.

Stop or narrow scope for leakage, unreliable recovery, broken citations, critical unsupported claims, unworkable hardware, or a legal requirement to change the operating model.

## 13. Milestones

- **M0 — Product and technical proof:** Synthetic ILP fixture set, shared evidence/model schemas, offline/browser/privacy spike, cryptographic tests before persistence, and optional bounded synthetic OpenRouter experiment.
- **M1 — Manual vertical slice:** Import text material, label documents, select/confirm facts and claims, apply initial ILP rules, navigate citations, encrypt/save/lock/reopen, encrypted backup/restore.
- **M2 — Scanned documents and richer coverage:** Local OCR, coordinate mappings/corrections, completeness checks, expanded charge/exit/illustration rules, report/export.
- **M3 — Readiness:** Lifecycle/storage/update failure testing, blind evaluation, hardware measurements, independent reviews, then a 5–10 adult consented pilot on their own computers.
- **M4 — Qualified assistance:** Integrate a benchmarked model adapter only if it improves supported claim/fact selection without weakening the release gates. The release mode decision determines browser-local and/or explicitly selected cloud assistance.

Public repository scope is product documentation, code, synthetic fixtures, and tests. Public launch, real-data collection, monetization, and deployment are separate future decisions.

## 14. Open decisions

- Which exact Singapore ILP product structures and charge schedules can be supported with reviewed rules? General ILP branding alone does not establish coverage.
- Which minimum document bundle gives a useful first review, and how much manual confirmation can users tolerate?
- Which user-facing AI route should ship first, and which benchmarked model/provider materially reduces effort at an acceptable cost? What developer experiment spend cap should apply?
- Which passphrase policy, KDF performance target, reviewed envelope specification, backup format, and migration policy should ship?
- What license, private security-reporting channel, hosting/log-retention policy, and independent reviewers should be selected?
- Is there willingness to pay after useful evidence reviews? Pricing and billing remain deferred.

These questions do not block synthetic fixtures, manual prototype work, or the offline evaluation harness. License selection is needed for a clear public contribution/reuse policy; provider credentials and spend limits are needed before paid experiments. Product-specific coverage, security/legal readiness, and tested privacy promises block real-data release. See [decisions](DECISIONS.md) for ownership and defaults.
