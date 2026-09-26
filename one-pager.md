# Verification Assumes Settled Residency
### Portable Continuity Passport — a blockchain identity layer for transnational workers

**Track:** Blockchain / Web3 | **Team:** [Error 404] | **Hackathon:** Google Hackathon 2026

---

**The problem.** Cross-border identity verification assumes a persistent domestic legal residency — a fixed address, a national ID anchored to it, a bank account tied to one jurisdiction. But the transnational workforce funding remittance and gig-economy corridors is transient by design: visas expire, work permits renew across shifting states, and jobs move across borders. These workers are legitimately unsettled, yet verification systems have no way to recognize that — so they get re-verified from scratch every time their situation changes.

**The insight.** Verification should check *continuity*, not *residency*. Instead of asking "where do you legally reside right now?", the right question is "can we prove this is the same accountable person across every jurisdiction they've touched?" That reframes identity from a single brittle claim into a portable, resilient chain of attestations — exactly what a blockchain is built to anchor.

**The solution.** A Portable Continuity Passport: a self-sovereign DID wallet that accumulates Verifiable Credentials from any issuer a worker encounters — employer, bank, embassy, NGO, cooperative. A Continuity Registry smart contract scores the resulting attestation trail for gaps, overlaps, and revocations. A Compliance Oracle translates a destination jurisdiction's actual legal requirement into an on-chain checkable rule. A verifier — a new bank, a remittance platform — queries sufficiency of proof via zero-knowledge disclosure, getting a yes/no and a cryptographic audit trail without seeing the worker's full history.

**Why blockchain.** No single jurisdiction owns the record, which matters precisely because no single jurisdiction claims these workers permanently. Issuance and revocation are auditable without a central arbiter. Zero-knowledge proofs protect privacy for populations often wary of surveillance. And the identity wallet is portable — it moves with the person, not with a bank account that gets frozen when they leave.

**Compliance positioning.** This is not a KYC/AML bypass. It's designed to sit alongside FATF Travel Rule compliance and feed it more continuous data, using the same risk-based tiering regulators already apply — thin proof for low-value transactions, thicker proof for higher-value or cross-border transfers. Sanctions and AML screening remain separate, layered checks.

**What we built.** DID creation and credential issuance on testnet, a deployed Continuity Registry smart contract, a verifier dashboard performing live sufficiency checks, and three mocked jurisdiction rule-sets. The zero-knowledge proof circuit is simulated for this demo — we show the interface a real proof would expose, not a hardened circuit.

**What's next.** Harden the ZK circuit, pilot with one remittance corridor, onboard real issuers, and work with a regulator sandbox on the compliance oracle.

---

*Full details, architecture diagram, and smart contract code: see README.md and the accompanying repo.*
