# ROOTS
### From Proof of Family to Proof of Personhood

> *"You cannot transfer your roots."*

**ROOTS** is a rural social experiment on the Kusama network. It takes the oldest anti-Sybil mechanism in human history — the oral tradition of family nicknames in a small Southern Italian village — and encodes it on-chain as a living, growing identity graph.

This repository contains the full MVP proposal, interactive presentation, and technical documentation for the **Art & Social Experiments Bounty** of the Kusama Vision Initiative.

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
A directed acyclic graph on-chain where each ROOTS token stores a `roots_parent_token_id` — linking to the ancestral family token. When a new house name is born in the village, a new node is added. The graph grows by itself, maintained by the community simply by living.

---

## Project Structure

```
roots/
├── README.md                        ← You are here
├── presentation/
│   └── roots_presentation.html      ← Interactive deck (8 slides, Three.js animation)
├── docs/
│   └── proof_of_family_MVP.docx     ← Full technical proposal (EN)
├── assets/
│   └── roots_cover.html             ← Cover page / visual identity
└── contracts/
    └── roots_nft_schema.md          ← NFT metadata schema
```

---

## The Five Phases

| # | Phase | Type | Duration | Budget |
|---|-------|------|----------|--------|
| 1 | Oral Ethnography & Book of Names | Off-chain | 4 weeks | 6,500 DOT |
| 2 | The Attestation Ceremony | Off → On bridge | 2 weeks | 8,500 DOT |
| 3 | On-Chain Registration | On-chain | 2 weeks | 6,500 DOT |
| 4 | The Social Experiment | Hybrid | 4 weeks | 7,500 DOT |
| 5 | Report & Replication Framework | Off-chain | 2 weeks | 3,333 DOT |
| — | Contingency buffer | — | — | 1,260 DOT |
| — | Italian crypto tax (26%) | — | — | 8,407 DOT |
| **TOTAL** | | | **3 months** | **42,000 DOT** |

> Rate: $1.20 / DOT · February 2025 · ~$50,400 USD total

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
  "name": "ROOTS — [House Name] · [Village]",
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
Reputation points are accumulated on-chain and stored as an additional field in the Identity Pallet. Actions that generate reputation:

| Action | Points |
|--------|--------|
| Attending the attestation ceremony | +50 |
| Attesting a new community member (witness) | +30 per attestation |
| Years of continuous on-chain presence | +10 per year |
| Participating in an OpenGov referendum | +20 |
| Spawning a new branch (new family house name) | +40 |
| Receiving attestation from a high-reputation family | +15 |

Reputation cannot be transferred, purchased, or delegated. It can only be earned through verified community participation. In the OpenGov experiment, votes are weighted by a logarithmic function of reputation: `vote_weight = 1 + log2(reputation / 50)`, so that elder families with deep roots carry more weight — mirroring the actual social dynamics of the village.

---

## The ROOTS NFT — Generative Artwork

Each NFT is a procedurally generated tree rendered as an SVG/canvas animation. The visual parameters are derived deterministically from the token's on-chain metadata:

- **Trunk width** — proportional to lineage depth
- **Branch count** — equals the number of living child tokens (`branch_count`)
- **Leaf density** — grows with reputation score
- **Color palette** — shifts from terracotta (new family) to deep amber (ancient lineage)
- **Animation speed** — slower and more majestic for high-reputation families

When a new child token is minted with this token as `roots_parent_token`, the NFT artwork is re-rendered with an additional branch. The NFT is alive. It grows.

---

## Important Disclaimers

**ROOTS tokens and NFTs have zero monetary value.** They are identity attestation records. They cannot be traded, sold, or exchanged on any market. Holding a ROOTS token or NFT confers no financial rights, no claim on any treasury, and no governance rights on Kusama at large beyond the specific local experiment described in this proposal.

**ROOTS Reputation points have zero monetary value.** They exist solely to weight participation in the local governance experiment. They cannot be transferred, delegated, or monetized.

This project operates under Italian law as a registered cultural association (APS). All crypto receipts are subject to Italian capital gains tax (26%) at the time of conversion to fiat.

---

## The Presentation

Open `presentation/roots_presentation.html` in any browser.

- **Navigate**: arrow keys, click side dots, or use Prev/Next buttons
- **Mobile**: swipe left/right
- **Background**: live Three.js animation — a generative root system that grows in real time

The presentation covers: Cover · Problem · Core Insight · Architecture · Roadmap · Budget · Why Kusama · Closing.

---

## Scalability

The replication framework produced in Phase 5 enables any village with a living oral identity tradition to run this experiment. Target regions: Southern Italy, Greece, Spain, Portugal, the Balkans, North Africa — all areas with strong oral identity traditions and significant rural depopulation challenges.

Each replication generates a new subnet of the ROOTS graph, linked to the original via a `network_parent` field. Over time, ROOTS becomes a federated global graph of rural human identity — rooted in specific places, connected across the Mediterranean.

---

## Budget Rationale

> Full breakdown in `docs/proof_of_family_MVP.docx`

The 42,000 DOT budget includes Italian crypto capital gains tax (26%) as an explicit line item. This is not absorbed into operational costs — it is reported transparently. All expenses will be documented with invoices and receipts. A financial report will accompany the Phase 5 deliverables.

If operational costs come in below projection, surplus funds will be allocated to Phase 6: replication in a second Southern Italian village.

---

## Contact & Proposal Submission

This proposal is submitted to the **Art & Social Experiments Bounty** of the Kusama Vision Initiative.

Reach the curators via the official Kusama bounty channels linked in the Web3 Foundation Referendum 498 documentation.

---

*ROOTS · Kusama Network · Art & Social Experiments Bounty · 2025*
*Built in Southern Italy. Rooted in four centuries of oral tradition.*
