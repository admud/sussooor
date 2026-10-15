# Contributing to Sussooor

Start with the [PRD](docs/PRD.md), [decision register](docs/DECISIONS.md), and [developer handoff](docs/DEVELOPER_HANDOFF.md). This is a planning repository; the application has not been built.

## Coordination

Choose a backlog task, identify its dependencies, and state your intended scope in an issue or draft PR before substantial overlapping work. Agree shared evidence/model interfaces first. Use focused branches and pull requests; describe resulting user behavior, validation evidence, and remaining limits. Record material product/architecture decisions in the relevant document.

An integration maintainer should review cross-module changes. Branch protections and contributor permissions are repository settings to establish; this document does not configure them. External developers may use forks and PRs once a license/contribution policy is selected. No individuals have been invited or granted write access.

## Data and credentials

Use synthetic fixtures only. Never attach real insurance files, chat exports, NRICs, policy numbers, medical data, vault backups, or credentials to repository files, issues, screenshots, logs, or CI artifacts. Clearly label synthetic documents. Check staged changes before committing; `.gitignore` is not a data-leak prevention system.

Keep API keys in local environment configuration excluded from Git. Never ship a shared OpenRouter key in browser code. Live provider experiments require explicitly configured credentials and spend caps, and must remain outside routine CI. Do not send real-document excerpts through development experiments.

## Validation

Include appropriate evidence for your change: schema/anchor and financial-math tests, crypto/storage recovery tests, production-build browser flows, or synthetic provider evaluations as applicable. Do not claim an automated test suite or security review exists until it does. Documentation-only changes need link/consistency/whitespace checks, not application tests.

## License and security reports

License selection is pending. Public repository visibility does not grant an open-source license or define inbound contribution terms. Resolve the license before accepting outside code contributions.

No private vulnerability-reporting channel is configured yet. Establish one before the pilot. Do not put exploitable details or private documents in public issues; use a maintainer-provided private channel when available.
