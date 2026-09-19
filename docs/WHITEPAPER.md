# NotaPeer Whitepaper

**Verifiable Books for the World's Unbanked Businesses**

*Version 1.0 · September 2026*

---

## Executive Summary

**64 million micro-businesses in Indonesia** (and 400+ million globally) keep
their financial records on paper or in editable spreadsheets. Editable books
are untrustworthy books — banks cannot underwrite what can be rewritten
overnight. Existing SaaS bookkeeping tools charge subscriptions and keep data
in private silos; the merchant never *owns* their trust. Web3 alternatives
demand KYC, gas money, and stable internet — luxuries our users do not have.

**NotaPeer** is a cashier-simple app that turns everyday bookkeeping into
tamper-proof, on-chain evidence. A merchant records daily income and expenses
in a private, offline-first app; each reporting period is compressed into a
Merkle root and anchored to an L2 (Base / Polygon); from that anchor trail,
an **on-chain credit score** grows — readable by any lender, verifiable by
anyone, forgeable by no one.

The name says how it works: **peer**. Every book is witnessed by peers — the
human who keeps it (via on-device human proof), and the counterparties who
trade with it (via counter-party attestation for high-value transactions).

**Target:** 100,000 UMKM onboarded in Year 1 · First DeFi lending integration
in Year 2 · Sustainable revenue via Anchor API licensing.

---

## 1. The Problem

### 1.1 The Trust Gap

| Metric | Value | Source |
|---|---|---|
| UMKM di Indonesia | 64 million | Kementerian Koperasi & UKM (2024) |
| UMKM tanpa laporan keuangan terverifikasi | 70%+ | World Bank Findex |
| UMKM yang akses kredit bank formal | <20% | OJK Financial Inclusion Survey |
| Average loan rejection rate (UMKM) | 65% | Bank Indonesia |

**Root cause:** Banks require **auditable financial history** to underwrite
loans. Paper books and editable spreadsheets fail this test — they can be
rewritten overnight to inflate revenue or hide losses. Existing SaaS tools
(Majoo, BukuWarung, Moka) solve bookkeeping but not **trust**.

### 1.2 Why Existing Solutions Fail

**Traditional SaaS (Majoo / BukuWarung / Moka):**
- ✅ Good UX, offline-first
- ❌ Data lives in vendor silo — merchant does not own trust
- ❌ Subscription fees (Rp 99k–499k/month) burden thin-margin businesses
- ❌ No path to capital — books stay private, never become credit history

**Web3 Existing (Centrifuge, Goldfinch, etc.):**
- ✅ On-chain trust, DeFi lending integration
- ❌ Require KYC (excludes unbanked)
- ❌ Require gas fees (excludes zero-capital users)
- ❌ Require stable internet (excludes offline communities)
- ❌ Complex UX (designed for crypto-natives, not warung owners)

**The gap:** A solution that is **free, offline-capable, no-KYC, and
produces on-chain credit history** — without demanding crypto literacy from
the merchant.

---

## 2. The Solution: NotaPeer

### 2.1 Three Layers of Trust

```
┌─────────────────────────────────────────────────────────┐
│  Layer 3 · TRUST                                        │
│  Merkle root anchored on L2 (Base / Polygon)            │
│  Only hashes go on-chain; history becomes immutable     │
├─────────────────────────────────────────────────────────┤
│  Layer 2 · PRIVACY                                      │
│  Local-first encrypted DB + Supabase sync               │
│  Raw transactions never leave merchant's control        │
├─────────────────────────────────────────────────────────┤
│  Layer 1 · IDENTITY                                     │
│  ZCP2O Witness (on-device human proof)                  │
│  Real human opens the books — no KYC, no email, no phone│
└─────────────────────────────────────────────────────────┘
```

### 2.2 How It Works (Merchant Journey)

1. **Onboarding:** Merchant opens app → holds circle 3 seconds (Witness gate
   samples micro-jitter) → sovereign identity (`zid`) issued.
2. **Daily Use:** Record income/expense → stored in local encrypted DB
   (offline-first via PowerSync) → syncs to Supabase when online.
3. **Monthly Anchor:** Merchant taps "Verify Period" → backend builds Merkle
   tree of transactions → sends only root hash to smart contract via ERC-4337
   gasless relay → anchor stored on-chain with `tx_hash` + `block_number`.
4. **Credit Score:** Anchor trail + consistency signals feed credit-score
   layer → public, permissionless score readable by DeFi lenders.

### 2.3 The Peer Layer (Differentiator)

Trust is not only cryptographic — it is **social**. Large transactions
(> Rp 1,000,000) can carry a **counter-party witness**: the supplier or
customer confirms the record with their own Witness hold. Peer-attested
records carry higher weight in the credit-score layer.

**Example:** Warung Kopi A buys 50kg beras @ Rp 12,000 from Toko Sembako B.
- Warung Kopi A records transaction + holds Witness (3s).
- System sends link to Toko Sembako B → B confirms via Witness hold.
- Transaction anchored with **2x trust weight** in credit score.

This creates a **network effect**: the more merchants use NotaPeer, the more
accurate the credit scores become.

---

## 3. Technical Architecture

### 3.1 Smart Contract: UMKMAnchor (Solidity ^0.8.20)

```solidity
contract UMKMAnchor {
    struct Report {
        address submitter;
        bytes32 merkleRoot;
        uint256 periodStart;
        uint256 periodEnd;
        uint256 timestamp;
        bool exists;
    }

    mapping(address => mapping(bytes32 => Report)) public reports;
    mapping(address => bytes32[]) public reportKeys;

    event ReportAnchored(
        address indexed submitter,
        bytes32 indexed periodKey,
        bytes32 merkleRoot,
        uint256 periodStart,
        uint256 periodEnd,
        uint256 timestamp
    );

    function anchorReport(
        bytes32 _merkleRoot,
        uint256 _periodStart,
        uint256 _periodEnd
    ) public returns (bytes32 periodKey) {
        // ... validation + storage + emit event
    }

    function verifyTransaction(
        bytes32 _periodKey,
        bytes32 _leaf,
        bytes32[] calldata _proof
    ) public view returns (bool) {
        // ... Merkle proof verification
    }
}
```

**Key functions:**
- `anchorReport()` — anchor Merkle root for a period (gasless via ERC-4337)
- `verifyTransaction()` — verify a transaction belongs to an anchored report
- `getReportKeys()` — list all anchored periods for an address
- `getReport()` — retrieve anchor details

**Gas optimization:** 1000 transactions → 1 Merkle root → 1 on-chain tx.
Cost per anchor: ~$0.01 on Base, ~$0.001 on Polygon.

### 3.2 Witness Gate (Proof-of-Human)

**Mechanism:** User holds a circle for 3 seconds while pointer micro-jitter
is sampled. Perfectly still holds are rejected (bots do not tremble; humans do).

**Session-scoped:** One hold opens a proof budget (e.g., 10 spins/anchors).
Cadence is a policy parameter, not a hard rule. This balances security and UX.

**Offline-capable:** Witness attestation is signed locally and cached; syncs
when connectivity returns.

### 3.3 Merkle Tree Construction

Each reporting period (e.g., "August 2026") is hashed into a Merkle tree:
```
Leaves: hash(transaction_id, amount, timestamp, counterparty_zid)
Tree: binary Merkle tree (OpenZeppelin standard)
Root: single bytes32 sent to chain
```

**Verification:** Lender queries "Is transaction X in August 2026 report?" →
backend returns Merkle proof → smart contract verifies against anchored root.

### 3.4 Offline-First Architecture

- **Local DB:** Encrypted SQLite (or WatermelonDB) on device
- **Sync:** PowerSync or Supabase Realtime when online
- **Conflict resolution:** Last-write-wins with timestamp; user prompted for
  manual merge if conflict detected

---

## 4. Business Model

### 4.1 Revenue Streams (Ranked by Speed-to-Revenue)

**Priority 1: B2B API Licensing (6–9 months)**
- **Target:** Payment gateways (Midtrans, Xendit, DOKU) + Fintech lending
  (KoinWorks, Investree, Akseleran)
- **Product:** Anchor API as white-label "Verified Merchant" badge
- **Revenue:** API call fee (Rp 500–2,000 per anchor) + revenue share (0.5–1%
  of loans facilitated via NotaPeer credit scores)
- **Example:** 1000 merchants × 1 anchor/month × Rp 1,000 = Rp 1M/month

**Priority 2: Grants (3–6 months)**
- **Target:** Polygon Village, Arbitrum Foundation, Gitcoin, Optimism RetroPGF
- **Revenue:** $10k–100k per grant (typically 2–3 grants in Year 1)
- **Use:** Fund pilot phase + hire 1–2 engineers

**Priority 3: Freemium + Premium (12+ months)**
- **Free tier:** Core bookkeeping + monthly anchor (forever free)
- **Pro tier (Rp 49k/month):** Export PDF, multi-user, advanced analytics
- **Enterprise tier (Rp 199k/month):** API access, white-label, priority support
- **Conversion rate:** 3–5% (industry standard)

**Priority 4: White-Label for Koperasi/BPR (9–12 months)**
- **Target:** 10,000+ koperasi and BPR in Indonesia
- **Revenue:** Subscription (Rp 500k–2M/month per koperasi) + setup fee
  (Rp 5–20M)

### 4.2 Unit Economics (Year 1 Projection)

**Optimistic scenario:**
- Grants: $50k (Rp 750M)
- B2B API: Rp 300M/year
- **Total: Rp 1.05 Miliar**

**Realistic scenario:**
- Grants: $20k (Rp 300M)
- B2B API: Rp 100M/year
- **Total: Rp 400M**

**Break-even:** ~Rp 500M/year for minimal operations (2 engineers + infra + legal).

### 4.3 Why Merchants Don't Pay (and Why That's Good)

Merchants are **users, not customers**. Charging them subscription fees puts
us in direct competition with Majoo/BukuWarung (who have 100x our resources).

Instead, we make merchants **free forever** and monetize the **parties who
benefit from trustworthy data**: payment gateways (lower churn), fintech
lenders (lower NPL), and cooperatives (better underwriting).

---

## 5. Roadmap

### Phase 0 — Doctrine (September 2026) ✅
- [x] README + Flowcharts + Whitepaper
- [x] GitHub repo public
- [x] Jitter Jackpot hackathon entry (proof of execution capability)

### Phase 1 — MVP (October–December 2026)
- [ ] Witness onboarding (ZCP2O integration)
- [ ] Transaction ledger (local-first + Supabase sync)
- [ ] Monthly anchor (Base Sepolia testnet)
- [ ] Basic dashboard (income/expense summary)
- [ ] Demo video 2 minutes

### Phase 2 — Pilot (January–March 2027)
- [ ] Recruit 10–100 real merchants (1 city: Jakarta Selatan warung kopi)
- [ ] 3-month pilot: daily usage, monthly anchors, feedback loops
- [ ] Iterate UX based on merchant interviews
- [ ] Collect testimonials + photos

### Phase 3 — Partners (April–June 2027)
- [ ] First Anchor API integration (1 payment gateway or fintech lender)
- [ ] First grant awarded (target: $20–50k)
- [ ] Hire 1 engineer (part-time)
- [ ] Scale pilot to 1,000 merchants

### Phase 4 — Credit (July–December 2027)
- [ ] Credit score layer live (reads anchor trails + consistency signals)
- [ ] First DeFi lending integration (Aave, Morpho, or local protocol)
- [ ] Launch freemium tiers (Pro + Enterprise)
- [ ] Revenue: Rp 50M+/month

### Phase 5 — Scale (2028+)
- [ ] ZCP2O mainnet launch (NotaPeer migrates to native chain)
- [ ] Token economics (if regulatory environment allows)
- [ ] Expand to other emerging markets (Philippines, Vietnam, India)
- [ ] Target: 1M merchants onboarded

---

## 6. Team

**Solo Founder: Ringga999**
- Full-stack Web3 developer
- Built Jitter Jackpot (casino game) for Chain Jam Vol. 1 hackathon
- Shipped on-chain smart contract + standalone web app + public deployment
- Zero-capital philosophy: bootstrapped with free tiers + open source

**Advisors:** (seeking — open to ZCP2O core team, Web3 grant committees,
fintech veterans)

**Hiring Plan:**
- Month 6: 1 part-time engineer (smart contract + backend)
- Month 12: 1 sales/BD (B2B partnerships)
- Month 18: 1 designer (mobile app polish)

---

## 7. Ask

**For Hackathons:**
- Prize money to fund pilot phase (target: $10–50k)
- Visibility + network (meet potential partners, advisors, hires)

**For Grants:**
- $20–100k to fund 12-month runway (2 engineers + infra + pilot costs)
- Technical mentorship + ecosystem introductions

**For Investors:**
- Pre-seed round: $200–500k for 15% equity (or token allocation if token launches)
- Use of funds: engineering (60%), sales/BD (20%), legal/compliance (10%), ops (10%)

**For Partners (Payment Gateways / Fintech Lenders):**
- Free pilot: 50 merchants × 3 months × zero cost
- We provide: verified merchant badge + credit score API
- You provide: merchant access + feedback
- Post-pilot: commercial terms negotiable (API fee, revenue share, white-label)

---

## 8. Contact

**GitHub:** https://github.com/Ringga999/notapeer  
**ZCP2O Protocol:** https://github.com/Ringga999/zcp2o-protocol  
**Email:** (coming soon)  
**Twitter/X:** (coming soon)  

---

*Built in public. Solo founder. Rp 0 capital. Verifiable books for the unbanked.*