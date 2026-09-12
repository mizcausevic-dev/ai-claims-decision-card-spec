# ai-claims-decision-card-spec

AI Claims Decision Card v0.1 — open JSON specification for signed,
hash-chained insurance claims decision records.

Part of the [Kinetic Gain Protocol Suite](https://kineticgain.com).

## What it is

The AI Claims Decision Card documents that an AI system evaluated an insurance
claim and reached a decision. Every decision gets a signed, hash-chained evidence
bundle with full provenance: claim type, evidence sources, model identity,
underwriting rules applied, and whether a human adjuster was in the loop.

## Detection

```json
{ "claims_card_version": "0.1" }
```

Note: uses claims_card_version, not decision_card_version (which belongs to
the AI Procurement Decision Card).

## Files

- [SPEC.md](./SPEC.md)
- [ai-claims-decision-card.schema.json](./ai-claims-decision-card.schema.json)
- [examples/sample-claims-decision-card.json](./examples/sample-claims-decision-card.json)
- [docs/ORIGIN.md](./docs/ORIGIN.md)

## Relationship to the Protocol Suite

- Evidence sources: AI Evidence Format spec.
- Disputed decisions: AI Incident Card spec.
- PII vault contracts: AI Procurement Decision Card data_vault_targets[].
- Attestation: same ed25519 signing model as the audit-stream.

## InsurTech 6-pack cluster

This spec feeds the following downstream repos:
- insurance-decision-record-audit-stream-reference (reference implementation)
- insurance-decision-record-audit-stream (working implementation)
- state-insurance-ai-disclosure-tracker
- naic-ai-bulletin-readiness-evidence-bundle
- insurance-applicant-bias-coverage-lab
- unfair-discrimination-incident-card-profile
- policyholder-data-vault-contract-profile

## License

MIT, matching the other specs in the Kinetic Gain Protocol Suite.

## Disclaimer

This specification defines a governance artifact format. Implementing it does not
constitute legal advice, regulatory certification, or a guarantee of claims
adjudication compliance. Organizations are responsible for ensuring their AI
claims workflows meet applicable insurance regulations, state insurance codes,
and jurisdiction-specific requirements.
