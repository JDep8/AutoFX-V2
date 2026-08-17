# Security and Secrets Rules

## Absolute rules

- Never expose or commit credentials, tokens, API keys, account identifiers,
  connection strings, or private data — in documents, logs, commit messages,
  chat output, or research artefacts.
- Never read secrets into output. Never copy `.env` files, `.rdp` files, or
  connection details from V1 or anywhere else.
- `.gitignore` blocks common secret patterns; that is a backstop, not a
  licence to keep secrets in the working tree.
- Verify no secrets or unintended files before every commit.
- Never push without Jacob's explicit instruction.

## V1 inspection

- Repository inspection is read-only via the authenticated GitHub CLI. Do not
  clone V1 into this workspace; do not copy V1 code into V2.
- Known flag: V1 commits an `.rdp` file at its repo root
  (`101005649.rdp`). Treat as a security finding in `V1_AUDIT.md`; never open
  or echo its contents.

## Database access (when configured)

- A dedicated **read-only** PostgreSQL account, provided through a secure
  configuration path (never pasted into chat or committed).
- Begin with schema/catalogue inspection; bounded queries, statement timeouts,
  sampling. Never write to or lock production data.
- Connection configuration lives outside the repository.

## Provider and automation boundaries

- Headless automation of paid consumer AI UIs (ChatGPT, Claude apps) is
  `BLOCKED` unless provider terms and Jacob's legal/security review explicitly
  permit it. Do not assume permission, stability, or scalability.
- For user-supplied videos (e.g. YouTube), access only what platform terms
  lawfully allow; never evade platform controls. Compliant fallback:
  user-supplied notes/transcripts or authorised access.

## Future-facing

Environments, secrets management, identity/RBAC, least privilege, encryption,
audit, supply-chain and dependency policy, and the threat model are specified
in `docs/03-architecture/SECURITY_AND_THREAT_MODEL.md` before implementation.
