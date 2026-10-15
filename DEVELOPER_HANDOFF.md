# Developer handoff

Status: documentation only; no scaffold, dependency lockfile, application, or test harness exists yet. [PRD](PRD.md) defines behavior; [decisions](DECISIONS.md) records unresolved product choices; [backlog](BACKLOG.md) orders implementation.

## First deliverable

Build the synthetic ILP slice in PRD section 7. Import a text PDF and chat, show source passages, confirm a premium and allocation charge, inspect a guarantee claim, distinguish partial withdrawal from surrender, save encrypted, and reopen the same citations. A candidate model may assist selection; manual review must work independently.

The first fixture set must include a correct, clearly qualified sales pitch, as well as misleading/ambiguous claims and missing evidence. Do not optimize solely for flagging issues.

## Proposed module boundaries

| Module | Responsibility | Boundary |
| --- | --- | --- |
| `app` | Case setup, import, review, source viewer, locking | Never persists plaintext or logs case content |
| `evidence` | Source revisions, anchors, facts, claims, confirmation and invalidation | Owns shared versioned schemas |
| `import` / `workers` | Local PDF/chat extraction and later OCR | Receives bounded bytes; no vault key or remote fetch |
| `vault` / `storage` | Crypto envelope, encrypted transactional records, backup/restore | Keys remain in unlocked runtime; no persistent plaintext catalog |
| `rules` / `financial-math` | Confirmed inputs to explainable findings and integer-cent/decimal math | No provider calls; all inputs traceable |
| `models` | Candidate extraction adapter and response validation | Returns proposals; cannot write final findings or access vault keys |
| `reports` | Frozen report revisions and warned export | Validates evidence revision links; escapes exported content |
| `offline` | Verified asset setup/cache and staged updates | No customer content in HTTP caches |
| `fixtures` / `eval` | Synthetic corpus, expected outcomes, provider comparison | Explicit live-run command; no real documents or embedded credentials |

These are proposed directories, not existing source paths. The schema owner and integration reviewer should be named in the first implementation PR. Parallel work can then use fixtures of the agreed contract.

## Shared contracts to implement first

- `SourceDocument`: random ID, immutable source revision and digest, encrypted filename/bytes, document role/date/status, extraction coverage.
- `ExtractionRevision`: source revision, page or chat-line representation, quality flags, native/OCR/corrected provenance. Preserve source-to-normalized mappings.
- `EvidenceAnchor`: source/extraction revision IDs, exact quotation, UTF-16 code-unit start inclusive/end exclusive offsets into the immutable extraction text. PDF anchors also carry physical page and normalized coordinates with explicit coordinate convention; chat anchors carry line ranges. Reject invalid offsets and split-surrogate boundaries. Never silently reinterpret an anchor after normalization.
- `Fact` / `Claim`: anchor IDs, typed proposed value or exact claim, confirmation state, user correction revision. A confirmed value does not by itself confirm the relationship between a claim and a passage.
- `CandidateBatch`: schema version, input revision IDs, candidate facts/claims/relationships, supplied anchor IDs or exact spans, omitted coverage, validation errors. Unknown IDs and unsupported fields fail validation.
- `AnalysisRun`: adapter/model/provider identifiers, prompt/schema versions, input revisions, cancellation/error state, token/cost/latency metrics where available. All case-derived records stay encrypted.
- `Finding` / `Calculation`: allowed status, input/anchor IDs, rule or human adjudication provenance, caveats/questions, exact formula/units/bases where applicable. Never promote model confidence into a factual status.
- `ReportSnapshot`: source/fact/finding revisions, checked and omitted coverage, export-safe excerpts. Changed inputs invalidate dependent live findings; historical snapshots remain clearly dated revisions.

Engineers must agree schemas, coordinate conventions, revisions and error semantics before implementations diverge. These text contracts are design guidance, not validated schemas.

## Model adapter behavior

Accept only a bounded list of allowed evidence windows, the output schema version, and cancellation/budget settings. Return `CandidateBatch`; adapters do not receive the vault, an unrestricted document collection, filesystem access, or action tools.

The validation pipeline checks schema, exact source/revision/quotation, offsets, duplicates, and coverage. User confirmation and deterministic checks or human adjudication then establish findings. Out-of-context quotes remain a semantic error even when offsets validate. Test hostile instructions inside both policy text and chat.

For OpenRouter experiments, an explicit developer command loads allowlisted synthetic fixtures and environment credentials. No frontend integration or product proxy is required for this experiment. Pin the requested model/provider configuration, forbid unapproved provider fallback, record observed routing, cap input/output/retries and total spend, and stop when the budget cannot be enforced. Verify current API capabilities before implementation. Routine tests use recorded synthetic responses or mocks; live runs are deliberately invoked and excluded from CI by default.

Compare a small hosted candidate and a browser-local candidate on identical cases when feasible. Report citation validity, semantic support, finding precision/recall/abstention, manual correction effort, time per review, actual hosted cost including retries, and local model download/peak memory. No model name or benchmark result has been selected yet.

## Completion evidence for the synthetic slice

- Exact citations survive corrections, lock/reopen, and fresh-profile backup restore.
- Critical unconfirmed inputs block dependent calculations; charge bases and withdrawal/surrender distinctions are preserved.
- Wrong password, tampering, quota failures and worker errors fail safely.
- No content-bearing requests in local mode and no app-created plaintext persistence after tested flows.
- Model output with a missing/invalid quote is rejected; provider timeout and invalid output preserve manual review.
- A synthetic demo and concise measured-results note show what works and what remains untested. Do not describe full release gates as passed based on a small smoke test.

No installation/build command is published yet because no app exists. Add verified commands, pinned dependencies, and the supported runtime version with the scaffold PR.
