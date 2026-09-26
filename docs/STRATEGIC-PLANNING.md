# 🗺️ Strategic Planning Document

**Created:** 24 September 2026
**Status:** Living Document
**Last Updated:** 24 September 2026

> This document captures strategic discussions, decisions, and open questions
> for NotaPeer and the ZCP2O ecosystem.

---

## 📑 Table of Contents

1. Token Listing Strategy ($ZPRO)
2. Feature Expansion Roadmap
3. Multi-User Architecture
4. Monetization Model
5. Wave-by-Wave Execution Plan
6. Open Questions & Decisions

---

## 🪙 1. Token Listing Strategy ($ZPRO)

### Objective
Get $ZPRO listed on CoinMarketCap (CMC) and CoinGecko to establish credibility and liquidity.

### Phase 1 — DEX Listing (Week 1–2)
Target: Uniswap / PancakeSwap pool creation.

Requirements:
- Token live on mainnet (not testnet)
- Liquidity pool: $50k–$100k minimum
- Smart contract audit (optional but recommended)
- Website live + whitepaper + active social media

Actions:
1. Create liquidity pool on Uniswap V3 or PancakeSwap
2. Submit to CoinGecko (easier, 1–2 week approval)
3. Submit to CMC (2–4 week approval)
4. Target: "Listed" status, not necessarily trending

Budget: $500 for listing specialist (Fiverr/Upwork) or DIY.

### Phase 2 — CEX Listing (Month 2–3)
Target: Tier-2 exchanges (Gate.io, MEXC, KuCoin).

Requirements:
- Active DEX trading volume
- Organic community engagement (no bots)
- Listing fee: $10k–$50k (negotiable with volume)
- Market making for liquidity

Actions:
1. Build trading volume on DEX first
2. Approach exchanges with proposal
3. Negotiate listing terms
4. Launch "trending" campaign post-listing

Budget: $10k–$30k (from grants / investors).

### Execution Strategy
Parallel development: do NOT pause NotaPeer development for listing.

    Month 1    : Development (Wave 2–4) + submit CMC/CoinGecko
    Month 2–3  : NotaPeer pilot (10 warungs) + CEX listing

Key principle: listing without product = token without fundamental.
Focus on product first; the token follows.

---

## 🛠️ 2. Feature Expansion Roadmap

### Feature A — Opname Kompleks + Pro Features (Paid)
What it is:
- Stock opname (inventory management)
- P&L (Profit & Loss) reports
- Cash flow forecasting
- Multi-branch reporting
- Export to Excel/PDF

Conflict with doctrine: our manifesto says "TIDAK ADA subscription fee" —
but that promise is for small UMKM, not large warungs/enterprise.

Solution (freemium):

    ✅ Free        : basic ledger, on-chain anchor, 1 user
    💰 Pro $10/mo  : opname, P&L, multi-branch, 5 users
    💎 Ent $50/mo  : API access, white-label, unlimited users

Wave: 5 (after Wave 4 completes). Purpose: monetization layer.

### Feature B — Owner App
What it is:
- Dashboard for warung owner
- View all transactions from all cashiers
- Set permissions (cashier A can refund, cashier B cannot)
- Approve large expenses
- Daily / weekly / monthly reports

Architecture needed:

    CURRENT : 1 device = 1 user (zid)
    FUTURE  : 1 owner + N cashier devices
              → Owner zid (master)
              → Cashier zid (slave, linked to owner)
              → Optional cloud sync (not required)

Wave: 3 (alongside Riwayat Anchor). Purpose: scaling layer.

### Feature C — Kasir App
What it is:
- Quick-sale mode for cashiers
- Preset categories (coffee, rice, snack)
- Quick-amount buttons (Rp 10k, Rp 20k, Rp 50k)
- Shift management (open/close register)
- Daily report

Two implementation options:
- Option 1 (recommended): Kasir mode inside the same app — fast, simple, 1 APK; cashier login with PIN linked to owner zid. Wave 2.
- Option 2: separate "NotaPeer Kasir" app — 2 APKs, backend sync needed, +2 months. Only if enterprise demand appears.

Wave: 2 (as a mode in the same app). Purpose: daily engagement.

---

## 👥 3. Multi-User Architecture

### Current State
- Single user per device
- zid generated from Witness Gate (HOLD 3 seconds)
- All data local-first, no cloud sync

### Future State (hierarchy)

    Owner (master zid)
      ├── Cashier 1 (slave zid, linked)
      ├── Cashier 2 (slave zid, linked)
      └── Cashier 3 (slave zid, linked)

### Sync Strategy
- Local-first: each device stores its own transactions
- Optional cloud sync for real-time owner visibility
- Conflict resolution: timestamp-based (latest wins)
- Privacy: owner sees aggregated data, not individual customer details

### Implementation Phases
- Phase 1 (Wave 2–3): basic multi-user — owner creates cashier accounts (PIN), transactions tagged with cashier_id, owner views all on own device, no real-time sync.
- Phase 2 (Wave 4–5): optional encrypted cloud sync, real-time visibility, conflict resolution logic.
- Phase 3 (Wave 6+): role-based permissions, audit trails, multi-branch support.

### Technical Challenges
1. zid collision → add timestamp + random salt to zid generation.
2. Offline sync → queue transactions, sync when online.
3. Privacy → owner sees aggregates only, never customer PII.

---

## 💰 4. Monetization Model

### Doctrine vs Reality
Doctrine: zero subscription fee (small UMKM), privacy-first, offline-first.
Reality: revenue needed for sustainability; large warungs need multi-user; enterprises need cloud sync.

### Tiered Model
- Tier 1 — UMKM Kecil (free, forever): 1 user, basic features, offline-first. This is our social mission.
- Tier 2 — Warung Menengah ($10/month): 5 users, opname, P&L, export. This is our revenue stream.
- Tier 3 — Enterprise ($50/month): unlimited users, API, white-label, priority support. This is our profit engine.

### Revenue Projections (Year 1)
Assumptions: 10,000 free users; 500 paid @ $10/mo; 50 enterprise @ $50/mo.

    Tier 2 : 500 × $10 = $5,000 / month
    Tier 3 :  50 × $50 = $2,500 / month
    Total  : $7,500 / month = $90,000 / year

Break-even: ~6 months (assuming $50k initial development cost).

### Pricing Philosophy
- Free tier is sacred — never compromise it.
- Paid tiers are value-add — features that save time/money.
- Enterprise is premium — custom solutions, white-glove service.

---

## 🏗️ 5. Wave-by-Wave Execution Plan

### Wave 1 — Foundation ✅ COMPLETE (23 Sep 2026)
AppShell, i18n (ID/EN), Recharts, Profile page, footer socials.
Deliverables: private repo notapeer-app, public repo notapeer,
2 social flowcharts, animated Merkle visualization.

### Wave 2 — Daily Engagement (next 2 weeks) 🚧
- Mode Kasir (quick-sale UI, same app)
- Absensi Pekerja (proof-of-presence via HOLD)
- [PARALLEL] Submit CMC + CoinGecko (Phase 1)
Budget: $500 listing specialist. Timeline: 2 weeks.

### Wave 3 — Scaling (Month 2) 📋
- Riwayat Anchor (view all on-chain anchors)
- Owner App (multi-user Phase 1)
- Tutorial + FAQ + Donasi pages
Technical debt: zid collision prevention, offline transaction queue.

### Wave 4 — Trust & Transparency (Month 3) 📋
- Advanced Settings (profile, export, danger zone)
- Optional encrypted cloud sync
- [PARALLEL] CEX listing (Phase 2)
Budget: $10k–$30k (grants/investors).

### Wave 5 — Monetization (Month 4–5) 📋
- Opname Pro, P&L reports, Excel/PDF export
- Freemium tier implementation
Revenue target: first $1k MRR.

### Wave 6 — Enterprise (Month 6+) 📋
- White-label, API access, multi-branch, role-based permissions
Revenue target: $10k MRR.

---

## ❓ 6. Open Questions & Decisions

### Decision 1 — Token listing approach
A) Hire freelancer ($500, 3–4 weeks)  ← RECOMMENDED
B) DIY (save $500, cost 20–30 hours)
Rationale: focus development time on product, not listing ops.

### Decision 2 — Kasir app architecture
A) Kasir mode in same app (Wave 2, quick)  ← RECOMMENDED
B) Separate Kasir app (Wave 4, complex)
Rationale: faster to market; can split later if needed.

### Decision 3 — Monetization model
A) Freemium  ← RECOMMENDED
B) 100% free (grants/donations only)
C) One-time purchase
Rationale: sustainable revenue without compromising the social mission.

### Decision 4 — Cloud sync strategy
A) No cloud sync (pure local-first)
B) Optional encrypted cloud sync (user pays)  ← RECOMMENDED
C) Mandatory cloud sync (breaks offline-first doctrine)
Rationale: preserves offline-first for UMKM, adds value for enterprise.

### Open Question 1 — Pricing for paid tiers
Is $10/$50 too expensive for the Indonesian market?
Annual discount (2 months free)? Regional pricing?
Status: open.

### Open Question 2 — Token utility
Should $ZPRO give a discount on paid tiers (e.g., 10% off)?
Should staking unlock premium features? Burn tokens from subscriptions?
Status: open.

### Open Question 3 — Partnership strategy
Candidates: UMKM associations (HIMWINDO, IWAPI), fintech (GoPay, OVO, Dana),
government programs (KUR, BPUM), financial-inclusion NGOs.
Which align with our mission? What is the value exchange? How to approach?
Status: open.

---

## 📝 Meeting Notes — 23 September 2026

Attendees: Founder + AI Architect. Duration: 2 hours.

Key decisions:
1. Wave 1 complete — move to Wave 2.
2. Token listing strategy approved (Phase 1 DEX, Phase 2 CEX).
3. Multi-user architecture designed (Owner + Cashier hierarchy).
4. Monetization model agreed (freemium: free + $10 + $50 tiers).
5. Kasir app decision: mode in same app (not separate APK).

Action items:
- [ ] Execute Wave 2 (Mode Kasir + Absensi) — next 2 weeks
- [ ] Submit CMC + CoinGecko (parallel) — next week
- [ ] Research UMKM associations for partnerships — Month 2

Next review: 7 October 2026 (after Wave 2 completion).

---

## 📚 References

- [ROADMAP.md](./ROADMAP.md) — technical feature roadmap
- [WHITEPAPER.md](./WHITEPAPER.md) — ZCP2O protocol vision
- [flowcharts/](./flowcharts/) — visual architecture diagrams

---

*This is a living document. Update it as decisions are made and strategies evolve.*

**Last Modified:** 24 September 2026 by Founder