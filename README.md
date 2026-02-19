# ROOTS
### From Proof of Family to Proof of Personhood

> *"The roots of a dead tree feed the surrounding earth — not only the branches that were closest to it."*

**ROOTS** is a rural social experiment on the Kusama network. It takes the oldest anti-Sybil system in human history — the oral tradition of family nicknames in a small Southern Italian village — and encodes it on-chain as a living, growing identity graph.

Submitted to the **KSM Art & Social Experiments Initiative** of the Kusama Vision Initiative.

---

## Two Assets, Two Functions

Every attested family receives two distinct on-chain assets. They must not be confused.

### Asset 1 — The ROOTS NFT (Identity)

The NFT is the **identity and lineage instrument**. Every ROOTS NFT is a generative artwork computed from the family's position in the lineage graph. The artwork **evolves over time**: every time a sub-family branches off, the parent NFT acquires a new visual element.

Key metadata fields:

- `roots_parent_nft_id` — which family this descends from (null for founding families)
- `lineage_depth` — generations from the graph root
- `branch_count` — direct sub-families branched
- `total_descendants` — total families in the subtree
- `succession_address` — designated successor wallet (null until set)
- `status` — active / dormant / succeeded
- `token_allocation` — computed by the indexer, updated on every graph change

**Rarity is structural.** It emerges from the real size and seniority of the family in the village — not from arbitrary assignment.

### Asset 2 — The ROOTS Token (Governance)

The ROOTS Token is the **governance instrument**. Fungible token minted via Kusama Asset Hub with `transfer: None` at protocol level. Cannot be sold, sent, or traded. **Zero monetary value.**

The token is **not static**: allocation changes as the family grows, using a diminishing-returns formula that ensures no single family can dominate alone.

---

## Token Redistribution Mechanism

```
nodes = 1 + branch_count + total_descendants

token_allocation = floor( sqrt(nodes) × 10 )
```

The square root ensures diminishing returns without any artificial cap.

### Simulation — village of 60 families

| Family | Nodes | Tokens | % of supply |
|--------|-------|--------|-------------|
| Founders A (largest) | 54 | 73 | 8.4% |
| Founders B | 39 | 62 | 7.2% |
| Founders C | 28 | 52 | 6.0% |
| Average family | 10 | 31 | 3.6% |
| New family (alone) | 1 | 10 | 1.2% |
| **Top 3 combined** | — | **187** | **21.6% — not enough** |

No family exceeds ~8% of total supply. The top 3 combined cannot reach 22%. Winning a referendum requires a genuine village coalition.

### Redistribution triggers

Recalculated every time a sub-family links to a parent, a family enters dormancy, a succession event changes the holding wallet, or a referendum snapshot is taken.

---

## Dual Quorum

A referendum is valid only if it satisfies **both** quorums simultaneously:

```
Quorum A (token weight):   >50% of expressed tokens in favour
Quorum B (participation):  >33% of registered families have voted
```

Quorum B is the popular legitimacy floor. Even the family with 73 tokens (8.4%) cannot govern alone without persuading at least 20 of 60 families to show up.

---

## The Death of the Capostipite

**This is the question nobody asks. It should be the first.**

Every capostipite will die. When it happens: the private key is lost, the token is locked, the NFT becomes orphaned. Families with the most tokens — the oldest, most branched — are also the most likely to be led by elderly patriarchs.

### What happens at death

Tokens are **burned** — not inherited. What remains is the family NFT: the memory of the lineage, the node from which children continue to branch.

**The protocol:**

1. **Tokens burned.** The patriarch's political weight does not transfer.
2. **+1 token to each directly registered child** — symbolic inheritance.
3. **NFT stays at the top of the graph.** The family does not disappear.
4. **The new capostipite** is designated by the community and receives tokens computed from the existing graph.

**Succession Address — the ideal case:**

At the ceremony, every capostipite has 2 minutes to sign their successor's wallet on-chain. If done, transfer at death is immediate with no limbo. If not done, the community has 30 days to co-sign a successor (3 token-holders from different village quarters — family members cannot attest their own kin).

**At the ceremony, every capostipite hears three things:**
1. Your tokens vanish with you — they are not inherited.
2. Your NFT remains: it is the memory of your family.
3. Every registered child receives 1 token in your memory.

---

## Technical Clarifications

### Timeline: 14 weeks = 3.5 months

| Phase | Description | Weeks |
|-------|-------------|-------|
| 1 | Oral Ethnography & Book of Names | 1–4 |
| 2 | The Attestation Ceremony | 5–6 |
| 3 | On-Chain Registration | 7–8 |
| 4 | The Social Experiment (OpenGov) | 9–12 |
| 5 | Report & Replication Framework | 13–14 |

### Gating via OpenSquare

```
Platform:    OpenSquare (opensquare.network)
Gate:        ROOTS Token balance >= 1
Quorum A:    >50% expressed tokens in favour
Quorum B:    >33% registered families have voted
Snapshot:    block at referendum launch (end Phase 3)
```

---

## Project Structure

```
roots/
├── README.md            ← This file
├── index.html           ← Navigation landing page
├── roots_cover.html     ← Cover page / interactive tree
├── presentation.html    ← Interactive deck (12 slides)
└── roots_proposal.pdf   ← Full technical proposal
```

---

## Budget

| # | Phase | Weeks | Net DOT | Crypto Tax Italy (33%) | Gross DOT |
|---|-------|-------|---------|------------------------|-----------|
| 1 | Oral Ethnography & Book of Names | 1–4 | 7,500 | 3,694 | 11,194 |
| 2 | The Attestation Ceremony | 5–6 | 10,000 | 4,925 | 14,925 |
| 3 | On-Chain Registration | 7–8 | 7,500 | 3,694 | 11,194 |
| 4 | The Social Experiment (OpenGov) | 9–12 | 9,200 | 4,531 | 13,731 |
| 5 | Report & Replication Framework | 13–14 | 4,200 | 2,069 | 6,269 |
| — | Contingency buffer | — | 3,300 | 1,626 | 4,926 |
| **TOTAL** | **14 weeks / 3.5 months** | | **41,700** | **20,539** | **62,239** |

---

## Payment Milestones

| Milestone | Deliverable | Phases | Net DOT | Tax | Gross DOT | Release |
|-----------|-------------|--------|---------|-----|-----------|---------|
| **M1 — START** | Signed agreement. On-chain identity verified. Field coordinator engaged. Phase 1 underway. | Phase 1 | 7,500 | 3,694 | 11,194 | Week 1 |
| **M2 — 100+ TOKENS** | 100+ NFTs + tokens on-chain. Indexer live. Book of Names deposited. Ceremony documented. Referendum launched. | Phases 2–3 | 17,500 | 8,619 | 26,119 | End wk 8 |
| **M3 — FINAL** | Referendum closed. Result to Municipal office. Documentary. Mirror.xyz report. Handbook. | Phases 4–5 + Cont. | 16,700 | 8,226 | 24,926 | End wk 14 |
| | **TOTAL** | | **41,700** | **20,539** | **62,239** | |

---

## Technical Architecture

### Off-Chain Layer
- Oral collection sessions (bars, homes, village squares)
- Book of Names: physical archive, 100 copies, deposited with the Municipal office
- Lineage graph indexer: reads NFT metadata from IPFS, computes token allocations, calls Asset Hub
- Succession event log: off-chain record of all claims and outcomes
- Video documentation of all phases

### On-Chain Layer (Kusama Asset Hub)
- **Kusama Identity Pallet** — `house_name`, `village_quarter`, `attestation_hash`, `lineage_parent`
- **ROOTS NFT** — non-fungible, generative, lineage on IPFS, evolves with the graph
- **ROOTS Token** — fungible, `transfer: None`, dynamically allocated with sqrt formula
- **OpenSquare space** — referendum with dual quorum (token weight + family participation)

### ROOTS NFT Metadata Schema (IPFS)

```json
{
  "name": "ROOTS [House Name] / [Village]",
  "attributes": [
    { "trait_type": "roots_parent_nft_id",  "value": "nft_id | null" },
    { "trait_type": "lineage_depth",        "value": "integer" },
    { "trait_type": "branch_count",         "value": "integer" },
    { "trait_type": "total_descendants",    "value": "integer" },
    { "trait_type": "token_allocation",     "value": "integer (computed)" },
    { "trait_type": "succession_address",   "value": "ss58 | null" },
    { "trait_type": "status",               "value": "active | dormant | succeeded" },
    { "trait_type": "attestation_ipfs_cid", "value": "CID" }
  ],
  "properties": { "transferable": false, "monetary_value": false }
}
```

---

## Open Questions

- **Quorum B on OpenSquare**: does the platform natively support a participant-count quorum? Fallback: off-chain check via indexer.
- **Indexer trust model**: trusted operation in MVP; production version would use a Substrate pallet with direct IPFS reading.
- **Quarter identification**: `village_quarter` must be encoded in every NFT at registration and verifiable on-chain.
- **Proof of life for elderly patriarchs**: annual `remark` requires sustained wallet access; local assistance protocol needed.

---

## Disclaimer

**ROOTS tokens and NFTs have zero monetary value.** They cannot be traded, sold, or transferred. The redistribution mechanism creates governance weight, not financial value. The project operates under Italian law. All crypto proceeds are subject to Crypto Tax Italy (33%) at EUR conversion.

---

*ROOTS · Kusama Network · KSM Art & Social Experiments Initiative · 2026*
*Built in Southern Italy. Rooted in four centuries of oral tradition.*
