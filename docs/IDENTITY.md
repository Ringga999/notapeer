# 🔐 Sovereign Identity — Root, Faces, and the Right to Own Your Name

> *One human. One secret. Many faces. Zero servers.*

**Status:** Specification locked · 26 September 2026
**Implements:** Hukum 1 (Witness wajib, login opsional) · Hukum 3 (privasi dulu)

---

## Why Identity Exists

Early NotaPeer builds issued a **fresh identity on every visit** — seven visits,
seven identities. A ledger without a persistent owner cannot grow a credit
score, cannot sign attendance, cannot be trusted across time. Identity is not
a feature; it is the spine of trust.

## The Model: One Root, Many Faces
ROOT SECRET S (128-bit · born at register · NEVER leaves the device)
│
├─ H(S ‖ 'merchant') → merchant face ← books, anchors, credit score [live]
├─ H(S ‖ 'worker') → worker face ← attendance, shifts [Wave 4]
└─ H(S ‖ 'witness') → witness face ← third-party attestation [future]

- **On-chain only ever sees faces.** The root never touches storage, network,
  or chain — it lives encrypted (AES-GCM, PIN-derived key) in the device.
- **Faces are unlinkable to each other** without the root: an auditor seeing a
  merchant face cannot find the worker face of the same human.
- **Recovery = 12 words.** The root is encoded as a BIP-39-style phrase, shown
  once at register, written on paper by the merchant. Lose the device + lose
  the words = lose the identity. That is the price of sovereignty; we say it
  out loud.

## Register (once per human)

1. **zcp2o-captcha** — hold + micro-jitter sampling → `traceCommitment`
2. Root `S` generated locally; recovery phrase shown once
3. PIN set → encrypts `S` at rest (WebCrypto, PBKDF2-SHA256)
4. Merchant face derived → session begins
5. **Attestation queued offline-first** → when online + wallet available:
   `WitnessRegistry.attest(face, commitment)` on Sepolia
6. Badge honesty: ⏳ *pending* until the chain event exists → ✅ *validated*

## Login (every return)

- PIN decrypts the root → faces re-derived deterministically
- Optional **"trust this device"** = 30-day session token
- No email. No phone. No KYC. No server to breach.

## Doctrine Lines (non-negotiable)

- **No guest mode.** Public curiosity is served by the public docs site, not by
  an unauthenticated app session — guest paths are attack surface.
- **No identity without humanity.** Every root is born from a captcha trace.
- **No face without consent.** Attestation publishes a pseudonym the merchant
  chose to activate; nothing else.
- **No silence about status.** The UI must show ⏳ until the chain says ✅.

## Open Decisions (deliberately deferred)

- Token listing policy ($ZPRO) — frozen until post-mainnet
- PRO tier boundary & pricing — after pilot demand is proven
- Multi-device sync — Wave 4 (Supabase candidate, Google login optional)

---

*Companion documents:*
- Technical spec: `notapeer-app/docs/SPEC-IDENTITY.md` (private)
- Contract spec: `zcp2o-protocol/specs/witness-registry.md`
- Visual flow: `zcp2o-protocol/docs/flowcharts/identity-attestation.md`