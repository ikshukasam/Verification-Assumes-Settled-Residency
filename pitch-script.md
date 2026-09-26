# Pitch Script — Verification Assumes Settled Residency

## 60-Second Version

"Every KYC system in the world assumes you have one settled home — a fixed address, an ID anchored to it, a bank account tied to a single jurisdiction. But the people who actually fund cross-border money corridors — gig workers, seasonal migrants, remittance senders — don't have that. Their visas expire, their permits renew across different countries, their jobs move. They're not undocumented, they're just *not persistent* — and verification systems have no category for that.

Our insight: stop verifying residency, start verifying continuity. We built a Portable Continuity Passport — a self-sovereign identity wallet that accumulates verifiable credentials from any employer, bank, or NGO a worker encounters, anchored on-chain in a Continuity Registry smart contract. When they need to open a new account or send money home, a verifier checks sufficiency of that history via zero-knowledge proof — not a single residency document they'll never have.

This isn't a KYC bypass — it's built to sit alongside FATF compliance, using the same risk-based tiering regulators already trust. We've deployed the registry contract on testnet and have a working verifier dashboard live right now. Let me show you."

*(→ transition into demo)*

---

## 3-Minute Version

**[Open — 20s]**
"Raise your hand if you've ever moved apartments, changed banks, or switched jobs across a border. Now imagine every time that happened, you had to prove your entire identity from scratch, because the system verifying you assumes you live in exactly one place, permanently.

That's the reality for the workforce that actually funds most cross-border money corridors: gig workers, seasonal migrant labor, remittance senders. They're not undocumented — they're just transient by design. And identity verification has no category for 'legitimately unsettled.'

**[Problem — 30s]**
KYC and AML checks require persistent domestic legal residency: a fixed address, a national ID anchored to it, a bank account tied to one jurisdiction. But visas expire. Work permits renew across different states. A gig worker might earn in three countries in a single year. Every transition resets their verification status, even though they're the same accountable person the whole time.

**[Insight — 20s]**
Our reframe: don't verify *where someone lives*. Verify *that it's continuously the same person, accountable across every jurisdiction they've touched*. That turns identity from one brittle claim into a portable chain of attestations — which is exactly the kind of thing a blockchain is built to anchor, because no single jurisdiction has to own or arbitrate it.

**[Solution — 45s]**
We built the Portable Continuity Passport. A worker holds a self-sovereign DID wallet. As they move through jobs, banks, and visa renewals, each entity — an employer, a bank, an NGO, a cooperative — issues them a Verifiable Credential, hash-anchored in our Continuity Registry smart contract. When they apply somewhere new, that verifier doesn't ask for a residency document. They query the registry through a Compliance Oracle that translates their jurisdiction's actual legal requirement into an on-chain check, and get back a zero-knowledge sufficiency proof — yes or no, with a cryptographic audit trail, without ever seeing the worker's full history.

**[Why blockchain — 20s]**
This only works decentralized. No single country owns the record — which matters, because the whole problem is that no country claims these workers permanently. Revocation is auditable without a central arbiter. And zero-knowledge proofs protect people who are often, understandably, wary of surveillance.

**[Compliance — 15s]**
To be clear: this is not a bypass. It's designed to sit alongside FATF Travel Rule compliance and existing AML screening, using the same risk-based tiering regulators already apply.

**[Demo — 30s]**
Here's what's actually working: [demo the DID wallet, credential issuance, and verifier dashboard live]

**[Close — 10s]**
We're looking for a pilot corridor partner, ZK cryptography mentorship, and regulatory feedback. Thank you."

---

## Anticipated Judge Questions & Prepared Answers

**"Isn't this just a way to dodge KYC?"**
No — it decomposes the residency requirement into jurisdiction-flexible proof components, but sanctions screening and AML checks remain fully intact as separate layers. We're making the *continuity* half of KYC work for people it currently fails, not removing the compliance half.

**"What stops a bad actor from getting fraudulent attestations?"**
Only recognized issuers (vetted employers, banks, NGOs) can write to the registry — this mirrors how trust works in the real world today, just made portable and auditable. Revocation lets any issuer retract a bad attestation, and continuity scoring naturally penalizes thin or single-source histories.

**"Why not just use a database instead of a blockchain?"**
Because the core problem is that no single institution or jurisdiction can be trusted to own this record — a database implies a single owner making unilateral decisions about someone else's cross-border identity. A blockchain lets attestation and revocation be publicly auditable without recreating that same central-authority problem in software.

**"Is the ZK proof actually implemented?"**
Not yet — for this hackathon we simulated the interface a real zk-SNARK circuit would expose. The registry, issuance flow, and verifier dashboard are real and deployed on testnet; hardening the ZK circuit is our next milestone.
