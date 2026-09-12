# Why We Built This

**ai-claims-decision-card-spec** started from a recurring problem in InsurTech: an AI system evaluates a claim, reaches a decision, and the trail that explains why stops at a log line nobody outside engineering can read. That gap between a decision being made and a decision being defensible kept showing up under regulatory pressure.

The recurring pressure in this space showed up around AI-assisted claims adjudication with no standard, auditable record of what evidence the model saw, what rules it applied, and who signed off. In practice, that meant an insurer could point to a model version and a rule-engine ruleset and still not have a good answer to the questions a regulator, a claimant's attorney, or an internal auditor actually asks: what evidence supported this outcome, which underwriting rules were applied, was a human in the loop, and can the record be proven unaltered after the fact? Once a system reaches that point, the problem is no longer only technical. It becomes evidentiary.

That is why **ai-claims-decision-card-spec** was built the way it was. The repo is a deliberate attempt to model a real operating layer for claims, underwriting, and compliance teams. It is not just trying to log a decision, it is trying to show what happens when evidence provenance, rule references, and cryptographic tamper-evidence are treated as first-class parts of the record.

Existing tools helped with adjacent workflows. Claims management systems, rule engines, and model-monitoring platforms covered storage, execution, or drift detection in pieces. What they still missed was a single, portable, signed record that ties a claim to its evidence, its decision reasons, its regulatory context, and a hash chain proving the record has not been altered since it was signed. That left compliance teams reconstructing the story manually at exactly the moment a regulator asked for it.

That shaped the design philosophy:

- **evidence-first** so the sources behind a decision (documents, images, model, synthesis method) are part of the record, not a separate log
- **regulator-legible** so jurisdiction, applicable rules, and human-in-loop status are explicit fields, not inferred
- **tamper-evident** so a full ed25519 hash chain (chain_index, prev_card_hash, signature) proves a record was not backdated or altered
- **CI-native** so every example in this repo is validated against the schema on every push

This repo also avoids trying to be a vague platform for everything. Its value comes from being opinionated about a real problem: AI Claims Decision Card v0.1 draft. A signed, hash-chained record documenting that an AI system evaluated an insurance claim and reached a decision, with full evidence provenance and governance context.

What comes next is practical. The roadmap is about wider adoption across claim types, deeper integration with the audit-stream hash-chain used elsewhere in the Kinetic Gain Protocol Suite, and reconciling this spec's attestation shape with the AI Procurement Decision Card's. The long-term value of **ai-claims-decision-card-spec** is that it makes that evidentiary record concrete enough to review, improve, and trust.
