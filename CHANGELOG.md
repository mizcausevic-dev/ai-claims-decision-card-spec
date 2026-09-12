# Changelog

## [Unreleased] — 2026-09-12

Brought the repo up to the Kinetic Gain Protocol Suite template, confirming
this as the Suite's 12th spec:

- Schema moved to repo root (`ai-claims-decision-card.schema.json`, was
  `schemas/`); `$id` updated to match.
- `fixtures/` renamed to `examples/`, matching every other spec repo.
- Added `docs/ORIGIN.md`.
- Added `.github/workflows/validate.yml` (kg-validate-action) and
  `.github/dependabot.yml`.
- License consolidated to a single MIT `LICENSE`, replacing the dual
  `LICENSE-APACHE` + `LICENSE-CC-BY`, matching the other 11 specs.

No change to the schema, the detection key, or the example data.

## [0.1.0] — 2026-06-29

Initial release of the AI Claims Decision Card specification.

Defines: claim, decision, evidence_bundle, governance, attestation, disclaimer.
Detection key: claims_card_version. Algorithm: ed25519.
