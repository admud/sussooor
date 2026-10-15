# Initial delivery backlog

Planning only; tasks are not completed. See [PRD](PRD.md) for scope and release gates, [decisions](DECISIONS.md) for working defaults, and [handoff](DEVELOPER_HANDOFF.md) for shared contracts. IDs are local task identifiers, not created GitHub issues. Owners are unassigned.

| ID | Priority | Task | Depends on | Acceptance evidence |
| --- | --- | --- | --- | --- |
| S01 | P0 | Scaffold React/TypeScript/Vite and basic checks | — | Verified setup/build commands, pinned packages, no telemetry, documented runtime |
| S02 | P0 | Define evidence and model schemas; revisions/offset convention | — | Synthetic PDF/chat citations validate, including Unicode and corrections; integration reviewer named |
| S03 | P0 | Create synthetic ILP bundle and labeled checks | S02 | Allocation, illustration, partial withdrawal/surrender, variable charges, missing fees, and non-conflict controls |
| S04 | P0 | Build interchangeable candidate-extraction interface and offline evaluation harness | S02, S03 | Mock/manual adapters, strict citation validation, invalid-output and cancellation cases |
| S05 | P0 | Run bounded synthetic OpenRouter experiment | S04; configured credentials/spend cap | Recorded model/provider configuration, quality/coverage/latency/cost report; no real documents |
| S06 | P0 | Specify vault envelope and implement crypto tests | S02 | Wrong password, tampering, IV allocation, bounded KDF input and rewrap tests; independent review before real data |
| S07 | P0 | Implement encrypted persistence and backup/restore | S01, S06 | No plaintext records; atomic/quota failure safe; restore in fresh profile |
| S08 | P0 | Prove local text-PDF/chat import with pinned workers | S01, S02, S03 | Bounded input, source mapping, no external PDF actions or customer-content requests |
| S09 | P0 | Build evidence confirmation workspace | S01, S02, S03; integrate S08 | Exact source navigation; critical inputs block calculations; separate relationship adjudication |
| S10 | P0 | Implement initial deterministic ILP checks | S02, S03 | Correct reviewed fixture outcomes, comparable bases, no invented total fees or surrender advice |
| S11 | P0 | Integrate save/lock/reopen vertical slice | S07–S10 | Same anchors survive; hidden/inactivity/resume clears unlocked UI; manual path needs no provider |
| S12 | P1 | Benchmark browser-local adapter on same corpus | S04 | Real hardware/model run, measured quality/download/memory/latency, manual fallback |
| S13 | P1 | Add scanned PDF OCR and corrections | S08, S09 | Local assets, page limits, cancel/timeouts, quality flags and dependent-finding invalidation |
| S14 | P1 | Add report, completeness questions and warned export | S10, S11 | Material claims cited; hostile Markdown escaped; omitted/unconfirmed coverage visible |
| S15 | P1 | Qualify offline updates and browser lifecycle | S11 | Cold reopen offline, cache loss fails closed, updates wait for locked sessions |
| S16 | P1 | Run blind evaluation and independent readiness reviews | S11, S13–S15 | PRD gates met before real-document pilot; scope/corpus reviewed by insurance-domain expert |
| S17 | P2 | Integrate selected model assistance into product | S05 and/or S12; resolved AI route; S16 for real-data pilot | Candidate-only output, user confirmation, mode-specific privacy tests; any cloud path has approved payload/provider/key/spend design |

Start S01–S03 together. After S02, work on vault, import, and model harness can proceed independently using shared fixtures. S05/S12 model results do not block S11 manual functionality. No live model invocation has been performed or authorized by this backlog alone.

Before public code contributions: select a license and establish private vulnerability reporting. Never attach real policies or chats to GitHub issues.
