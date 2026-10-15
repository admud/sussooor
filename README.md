# Sussooor

Understand what you’re being sold. Check the costs, catch conflicting claims, and ask better questions—privately.

Sussooor is a planned local-first tool for reviewing insurance proposals, policies, benefit illustrations, and written sales conversations, starting with Singapore investment-linked policies (ILPs) and individual life insurance.

It helps people understand disclosed fees, guarantees, risks, and exit conditions, and compare sales claims against source passages. It does not determine fraud or recommend buying, cancelling, or surrendering a policy.

**Status:** Product planning. No application has been implemented, deployed, security-audited, or approved for real-policy use. Local processing, encryption, and offline operation below are requirements, not delivered features.

- [Product requirements](docs/PRD.md)
- [Initial delivery backlog](docs/BACKLOG.md)
- [Decisions and AI strategy](docs/DECISIONS.md)
- [Developer handoff](docs/DEVELOPER_HANDOFF.md)
- [Contributing](CONTRIBUTING.md)

## Intended privacy model

The local mode processes document contents on the user's device and saves an encrypted local vault. Development may evaluate inexpensive models through OpenRouter using synthetic fixtures only. The first user-facing AI route is still an open decision: cloud assistance would transmit selected content to external providers and requires distinct, accurate privacy messaging. Verify implemented behavior before making production privacy claims. A browser app still trusts delivered code, browser extensions, and the device.

## Contributing safely

Use synthetic documents and conversations only in issues, pull requests, fixtures, screenshots, and logs. Never submit personal policies, chat exports, identity details, credentials, or vault backups. Report a suspected vulnerability without attaching private documents; a private reporting channel must be established before a pilot.

## License

A license has not yet been selected. Public visibility alone does not grant an open-source license.
