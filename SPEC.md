# AI Claims Decision Card v0.1

Specification for a signed, hash-chained AI insurance claims decision record.

## Purpose

An AI Claims Decision Card documents that:
1. An AI system evaluated an insurance claim.
2. The decision was made under a specific set of underwriting rules.
3. Evidence sources are identified and content-hashed.
4. Whether a human adjuster reviewed before finalization.
5. The record is cryptographically signed and chain-linked.

## Canonical detection field

`claims_card_version: "0.1"` at root level.

## Required fields

### claim
| Field | Type | Description |
|-------|------|-------------|
| claim_id | string (UUID) | Unique claim identifier. |
| policy_id | string | Policy identifier. |
| claimant_ref | string | Opaque claimant reference. No PII. |
| claim_type | enum | property_damage, medical, auto, life, liability, or other |
| filed_at | ISO 8601 datetime | When the claim was filed. |

### decision
| Field | Type | Description |
|-------|------|-------------|
| outcome | enum | approve, deny, pend, or refer |
| reasons | string[] | Human-readable reasons. At least one required. |
| rule_refs | string[] | Underwriting rule identifiers applied. |
| coverage.covered | boolean | Whether the claim is covered. |
| coverage.amount | number or null | Approved amount. null for deny/pend/refer. |
| coverage.currency | string | ISO 4217, e.g. USD. |

### evidence_bundle
| Field | Type | Description |
|-------|------|-------------|
| sources | EvidenceItem[] | At least one required. |
| model.model_id | string | AI model identifier. |
| model.model_version | string | Model version. |
| model.provider | string | Model provider. |
| synthesis_method | string | How the model synthesized evidence. |

#### EvidenceItem
| Field | Type | Description |
|-------|------|-------------|
| source_id | string | Unique identifier. |
| source_type | enum | document, image, database_record, external_api, structured_data |
| content_hash | string | SHA-256 of evidence content at retrieval time. |
| retrieval_confidence | number | 0.0 to 1.0. |
| synthesis_role | enum | primary, supporting, or excluded |

### governance
| Field | Type | Description |
|-------|------|-------------|
| underwriting_rules_version | string | Underwriting ruleset version. |
| jurisdiction | string | ISO 3166-1 alpha-2 + optional subdivision (e.g. US-CA). |
| regulatory_refs | string[] | Applicable frameworks. |
| human_in_loop | boolean | Whether a human adjuster reviewed. |
| reviewer_ref | string or null | Opaque reviewer identifier. |

### attestation
| Field | Type | Description |
|-------|------|-------------|
| card_hash | string | SHA-256 of canonical JSON (attestation excluded). |
| signature | string | ed25519 signature of card_hash. |
| algorithm | string | Must be "ed25519". |
| signing_key_id | string | Signing key identifier. |
| signed_at | ISO 8601 datetime | Attestation timestamp. |
| chain_index | integer | Chain position. Starts at 0. |
| prev_card_hash | string or null | Preceding card hash. null for index 0. |

### disclaimer
| Field | Type | Description |
|-------|------|-------------|
| disclaimer | string | REQUIRED. Must state governance artifact, not legal advice. |

## Canonical hash procedure

Serialize with keys sorted lexicographically, no insignificant whitespace.
Exclude the attestation object. SHA-256 of UTF-8 bytes, lowercase hex.

## Chain integrity

card N: chain_index = chain_index(N-1) + 1, prev_card_hash = card_hash(N-1).

## Changelog

### v0.1 (initial)
Defines: claim, decision, evidence_bundle, governance, attestation, disclaimer.
Detection key: claims_card_version.
