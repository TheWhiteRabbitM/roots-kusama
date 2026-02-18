# ROOTS
### From Proof of Family to Proof of Personhood

> *"You cannot transfer your roots."*

**ROOTS** is a rural social experiment on the Kusama network. It takes the oldest anti-Sybil mechanism in human history — the oral tradition of family nicknames in a small Southern Italian village — and encodes it on-chain as a living, growing identity graph.

This repository contains the full MVP proposal, interactive presentation, and technical documentation for the **KSM Art & Social Experiments Initiative** of the Kusama Vision Initiative.

---

## What is this?

In villages across Southern Italy, every family carries a *'u nomme 'e casa* — a house name, passed down orally for generations. Invisible to official registries. Unknown to outsiders. Impossible for any AI to fake.

This project asks: what happens when you put 400 years of community trust on a blockchain?

The answer is **ROOTS** — a three-month experiment combining oral ethnography, a public attestation ceremony, on-chain identity registration, generative NFTs, a family reputation system, and a gated governance experiment using Kusama's OpenGov.

---

## Core Concepts

### ROOTS Token
A non-transferable identity token issued to each attested family. **No monetary value. No tradeable utility.** It is the on-chain equivalent of a community certificate — proof that a specific person belongs here, attested by their peers.

Transfer permissions are set to `None` at the Kusama native assets pallet level. Non-transferability is a protocol constraint, not a social convention.

### ROOTS NFT
Each family receives a **generative NFT** — a unique visual artwork procedurally rendered from the family's position in the lineage graph. The artwork evolves: when a new branch is born from a family, the parent NFT gains a new visual element. The NFT is a living portrait of a family's place in the community graph.

### ROOTS Reputation
An on-chain reputation score accumulated by families through verifiable community actions: attending ceremonies, attesting new members, years of presence in the graph, participation in governance. Reputation is public, non-transferable, and weights votes in the OpenGov experiment.

### The Lineage Graph
A directed acyclic graph on-chain where each ROOTS token stores a `roots_parent_token_id` linking to the ancestral family token. When a new house name is born in the village, a new node is added. The graph grows by itself, maintained by the community simply by living.

---

## Project Structure

```
roots/
├── README.md                        ← You are here
├── presentation/
│   └── index.html                   ← Interactive deck (11 slides, Three.js animation)
├── docs/
│   └── roots_proposal.pdf           ← Full technical proposal (EN)
├── assets/
│   └── roots_cover.html             ← Cover page / visual identity
```

---

## The Five Phases

| # | Phase Description | Duration | Net DOT | Tax (33%) | Gross DOT |
|---|-------------------|----------|---------|-----------|-----------|
| 1 | Oral Ethnography & Book of Names | 4 weeks | 7,500 | 3,694 | 11,194 |
| 2 | The Attestation Ceremony | 2 weeks | 10,000 | 4,925 | 14,925 |
| 3 | On-Chain Registration | 2 weeks | 7,500 | 3,694 | 11,194 |
| 4 | The Social Experiment | 4 weeks | 9,200 | 4,531 | 13,731 |
| 5 | Report & Replication Framework | 2 weeks | 4,200 | 2,069 | 6,269 |
| | Contingency buffer | | 3,300 | 1,626 | 4,926 |
| **TOTAL** | | **3 months** | **41,700** | **20,539** | **62,239** |

> Requested funding: **62,239 DOT gross** (net operational: 41,700 DOT / crypto capital gains tax: 20,539 DOT)

---

## Payment Milestones

| Milestone | Deliverables | Phases | Net DOT | Tax (33%) | Gross DOT | Release |
|-----------|--------------|--------|---------|-----------|-----------|---------| 
| **M1 — PROJECT START** | Signed agreement. On-chain identity verified. Field coordinator engaged. Phase 1 oral collection underway. | Phase 1 | 7,500 | 3,694 | 11,194 | Immediate |
| **M2 — 100+ ROOTS TOKENS** | 100+ ROOTS tokens live on-chain. Book of Names printed/deposited. Attestation ceremony documented. OpenGov referendum launched. | Phases 2–3 | 17,500 | 8,619 | 26,119 | Month 2 |
| **M3 — FINAL DELIVERY** | OpenGov result to municipality. Documentary film. 30-page report on Mirror.xyz. Facilitator handbook. Financial statement. | Phases 4–5 + Contingency | 16,700 | 8,226 | 24,926 | Month 3 |
| | **TOTAL** | | **41,700** | **20,539** | **62,239** | |

---

## Technical Architecture

### Off-Chain Layer
- Oral collection sessions (bars, homes, piazzas)
- Book of Names: printed archive, 100 copies, deposited with municipality
- Lineage graph: visual DAG of how names branch over time
- Video documentation of all phases

### On-Chain Layer (Kusama)
- **Kusama Identity Pallet** — `house_name`, `village_quarter`, `attestation_hash`, `lineage_parent`
- **ROOTS Token** — native assets pallet, `transfer: None`, metadata on IPFS
- **ROOTS NFT** — generative artwork, evolves with the lineage graph
- **ROOTS Reputation** — on-chain score, weights OpenGov votes
- **OpenGov Referendum** — gated to attested identities, real community question

### ROOTS NFT Metadata Schema
```json
{
  "name": "ROOTS [House Name] · [Village]",
  "description": "A living generative portrait of a family's place in the community identity graph.",
  "image": "ipfs://[CID]",
  "attributes": [
    { "trait_type": "house_name",           "value": "string (dialect)" },
    { "trait_type": "family_surname",       "value": "string" },
    { "trait_type": "village_quarter",      "value": "string" },
    { "trait_type": "num_witnesses",        "value": "integer" },
    { "trait_type": "ceremony_date",        "value": "ISO 8601" },
    { "trait_type": "roots_parent_token",   "value": "token_id | null" },
    { "trait_type": "lineage_depth",        "value": "integer" },
    { "trait_type": "branch_count",         "value": "integer (living children)" },
    { "trait_type": "reputation_score",     "value": "integer" },
    { "trait_type": "attestation_ipfs_cid", "value": "CID" }
  ],
  "animation_url": "ipfs://[CID]/nft_render.html",
  "properties": {
    "transferable": false,
    "monetary_value": false,
    "category": "identity_attestation"
  }
}
```

### ROOTS Reputation Score

| Action | Points |
|--------|--------|
| Attending the attestation ceremony | +50 |
| Attesting a new community member (witness) | +30 per attestation |
| Years of continuous on-chain presence | +10 per year |
| Participating in an OpenGov referendum | +20 |
| Spawning a new branch (new family house name) | +40 |
| Receiving attestation from a high-reputation family | +15 |

Vote weight formula: `vote_weight = 1 + log2(reputation / 50)`

---

## Important Disclaimers

**ROOTS tokens and NFTs have zero monetary value.** They cannot be traded, sold, or exchanged. This project operates under Italian law. All crypto receipts are subject to Italian crypto capital gains tax (33%) at the time of conversion to fiat.

---

## Contact & Proposal Submission

Submitted to the **KSM Art & Social Experiments Initiative** of the Kusama Vision Initiative via official governance channels.

---

*ROOTS · Kusama Network · KSM Art & Social Experiments Initiative · 2026*
*Built in Southern Italy. Rooted in four centuries of oral tradition.*
