# Verification Assumes Settled Residency

**Track:** Blockchain / Web3 — Google Hackathon
**Team:** [Your Team Name]

> Cross-border identity verification requires persistent domestic legal residency, yet the transnational workforces funding these corridors hold transient status across shifting jurisdictions.

## Problem Statement

Identity verification systems — KYC, AML onboarding, remittance corridor checks — assume every person has one settled legal home: a fixed address, a national ID anchored to that address, a bank account tied to a single jurisdiction.

The people who actually fund cross-border corridors (remittance senders, gig workers, seasonal migrant labor, platform freelancers) don't have that. Their status is transient by design — visas expire, work permits renew across different states, jobs move across borders. Verification systems have no category for "legitimately unsettled," so these workers get re-verified from scratch every time their situation changes, even though they are the same accountable person throughout.

## Our Solution: Portable Continuity Passport

Instead of asking **"where do you legally reside right now?"**, we ask **"can we prove this is the same accountable person across every jurisdiction they've touched?"**

This reframes identity from a single, brittle residency claim into a portable, resilient **chain of attestations** — which is exactly what blockchain is suited to anchor: no single jurisdiction owns the record, issuance and revocation are auditable without a central arbiter, and zero-knowledge proofs let a worker prove sufficiency of history without exposing every employer or visa detail.

## Architecture

```
Worker DID Wallet
      │
      ▼
Verifiable Credentials  (issued by employers, banks, embassies, NGOs, cooperatives)
      │
      ▼
Continuity Registry  (smart contract — scores gaps, overlaps, revocations)
      │
      ▼
Compliance Oracle  (translates a destination jurisdiction's legal rule into an on-chain checkable condition)
      │
      ▼
Verifier Dashboard  (bank / remittance platform — receives a sufficiency proof, not raw history)
```

See `architecture-diagram.svg` for the visual version.

**Layers:**

| Layer | Function |
|---|---|
| **Identity Layer** | Self-sovereign DID (W3C DID standard) — the worker controls their own identity wallet, not tied to any one state |
| **Attestation Layer** | Verifiable Credentials issued by any recognized issuer, each stamped with jurisdiction + validity window |
| **Continuity Engine** | Smart contract logic scoring "identity continuity" — no gap longer than X, overlapping attestations across transitions, revocation checks |
| **Compliance Oracle** | Off-chain oracle translating a destination jurisdiction's actual legal requirement into an on-chain checkable rule |
| **Verifier Interface** | Queries proof of sufficiency (via zero-knowledge proof or selective disclosure) without seeing the worker's full history |

## Tech Stack

- **Identity/Credentials:** W3C DID + Verifiable Credentials (`veramo` / `did-jwt-vc`)
- **Chain:** Polygon testnet (EVM-compatible, low gas, fast for demo) — or Ethereum Attestation Service (EAS) as an alternative attestation backbone
- **Smart Contracts:** Solidity, deployed on testnet — see `contracts/ContinuityRegistry.sol`
- **ZK Layer:** circom (zk-SNARK) proving "credential count ≥ N within time window" — **simulated for this demo**, see below
- **Off-chain Oracle:** Node/Express service returning mocked jurisdiction rule-sets (JSON)
- **Frontend:** React — worker credential wallet UI + verifier sufficiency-check dashboard

## How to Run

```bash
# 1. Clone the repo
git clone [your-repo-url]
cd [repo-name]

# 2. Install dependencies
npm install

# 3. Deploy contracts to testnet (e.g. Polygon Amoy)
cd contracts
npx hardhat run scripts/deploy.js --network amoy
# → note the deployed Continuity Registry address, add to .env

# 4. Start the mock compliance oracle
cd ../oracle
npm run start

# 5. Run the frontend
cd ../frontend
npm run dev
```

**Testnet contract address:** `[fill in after deployment]`
**Explorer link:** `[Polygonscan/Etherscan link]`

## Smart Contract Overview

`ContinuityRegistry.sol` — core functions:

- `issueAttestation(didHash, credentialHash, jurisdiction, validUntil)` — recognized issuers anchor a credential hash on-chain
- `revoke(didHash, index)` — issuer revokes a previously issued attestation
- `checkContinuity(didHash, maxGap, minCount)` — returns whether the identity's attestation history satisfies a continuity threshold (no gap larger than `maxGap`, at least `minCount` valid, non-revoked attestations)

Only credential **hashes** are stored on-chain; personally identifiable information stays off-chain with the worker, in line with data-minimization principles.

## What's Real vs. Simulated (Demo Scope)

We're upfront about this — it matters for judging and for anyone building on this later.

**Working / deployed:**
- DID creation and credential issuance flow, tested on testnet
- Continuity Registry smart contract, deployed and verified
- Verifier dashboard performing live sufficiency checks against the deployed contract
- Three mocked jurisdiction rule-sets (JSON) standing in for real regulatory requirements

**Simulated / roadmap:**
- Zero-knowledge proof circuit — the demo shows the *interface* a real ZK proof would expose (a yes/no sufficiency result); the underlying circuit is not yet implemented
- Live compliance oracle feeds — real jurisdictions' regulatory requirements aren't publicly available as structured data, so we hand-authored representative rule-sets
- Production-grade biometric onboarding
- Real issuer partnerships (actual banks, embassies, NGOs)

## Compliance Positioning

This is **not** a KYC/AML bypass. It's designed to sit alongside existing compliance frameworks:

- **Complementary to FATF Travel Rule compliance** — feeds it more continuous, better-attested data rather than routing around it
- **Risk-based tiering**, mirroring how regulators already treat KYC: low-value transactions need thin continuity proof, high-value or cross-border transfers need thicker proof
- **Sanctions and AML screening remain separate, layered checks** — this system proves continuity of identity, not clean legal status

## Roadmap

| Timeframe | Milestone |
|---|---|
| 0–3 months | Harden the ZK continuity circuit; pilot with one remittance corridor |
| 3–6 months | Onboard 2–3 real issuers (employer, cooperative, NGO) in a single corridor |
| 6–12 months | Multi-corridor rollout; work with a regulator sandbox on the compliance oracle |

## Team

- [Ikshu] — [Product & Problem Lead]
- [Jayanth] — [Solution & Architecture Lead]
- [vanshika] — [Blockchain & Smart Contract Lead]
- [Bharadwaj] — [Demo & Compliance Lead] 
## Demo Video

[Link to 2–3 minute demo video]

## License

[Choose a license, e.g. MIT]
