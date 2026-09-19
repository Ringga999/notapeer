# NotaPeer Glossary

**A plain-language dictionary for humans, not cryptographers.**
If any word here still confuses you after reading, open an issue —
we will fix the word, not the reader.

Every entry has three lines:
*what it is* · *warung-world analogy* · *where it lives in NotaPeer*.

---

## 1 · Money & Books (why we exist)

- **UMKM** — Indonesia's micro, small, and medium businesses: the warung,
  the kopi stall, the sembako shop, the home bakery.
  *Warung-world:* you, reading this, or your neighbor.
  *In NotaPeer:* the entire reason the protocol exists.

- **Books / bookkeeping** — the record of money in and money out.
  *Warung-world:* the notebook behind the cashier, or the Excel file on the
  shop's old laptop.
  *In NotaPeer:* the private ledger each merchant keeps on their phone.

- **Underwriting** — a lender's homework before saying "yes" to a loan.
  *Warung-world:* the bank officer asking "show me your last year of sales"
  before approving a mesin-espresso loan.
  *In NotaPeer:* the homework becomes reading your anchor trail instead of
  doubting your notebook.

- **NPL (non-performing loan)** — a loan that stopped being repaid.
  *Warung-world:* the reason banks say "no" 65 times out of 100.
  *In NotaPeer:* the number our credit-score layer exists to lower.

- **KYC (Know Your Customer)** — paperwork identity: ID card, selfie, forms.
  *Warung-world:* the queue at the bank branch with photocopies.
  *In NotaPeer:* replaced by **Witness** — three seconds of being human.

- **Credit score** — one number summarizing how trustworthy your money
  history is.
  *Warung-world:* the reputation you have with your supplier, but readable
  by any bank in seconds.
  *In NotaPeer:* grown from your anchor trail, owned by you, readable by all.

---

## 2 · Chain Words

- **Blockchain** — a ledger copied to thousands of keepers, where past pages
  cannot be rewritten.
  *Warung-world:* your buku kas photocopied to 10,000 notaries; burn your
  original and the truth survives.
  *In NotaPeer:* the permanent shelf where anchors live.

- **L2 (Layer 2)** — a cheaper, faster settlement layer sitting on top of
  Ethereum (e.g., Base, Polygon).
  *Warung-world:* the district notary office instead of the national archive
  — same legal force, shorter queue, smaller fee.
  *In NotaPeer:* where `anchorReport()` is called.

- **Gas fee** — the postage cost for any work done on-chain.
  *Warung-world:* the stamp you must buy for every letter.
  *In NotaPeer:* merchants never buy stamps — see *gasless*.

- **Gasless transaction** — a transaction whose postage is paid by a sponsor
  or relay, not the sender.
  *Warung-world:* the partner post office that pre-pays your stamps because
  your letters bring them business.
  *In NotaPeer:* ERC-4337 relays (Gelato/Biconomy) carry every anchor.

- **Smart contract** — rules that live on-chain and run exactly as written,
  with no operator behind the curtain.
  *Warung-world:* a vending machine: no shopkeeper to argue with, no
  shopkeeper to bribe.
  *In NotaPeer:* `UMKMAnchor`, the notary that never sleeps.

- **Address** — an account number on-chain.
  *Warung-world:* your shop's PO box, but nobody can open it without your key.
  *In NotaPeer:* tied to your `zid`, not your email.

- **Tx hash** — the receipt number of one on-chain transaction.
  *Warung-world:* the numbered slip the notary hands you; quote it and anyone
  can find your file.
  *In NotaPeer:* shown on the dashboard next to "Verified on-chain".

- **Block / block number** — a page of the ledger and its page number.
  *Warung-world:* "recorded on page 12,345,678 of the national book."
  *In NotaPeer:* stored in the `anchors` table as proof of when.

- **Testnet / mainnet** — the rehearsal stage / the real stage.
  *Warung-world:* practicing the recipe at home vs. serving paying customers.
  *In NotaPeer:* Phase 1 lives on Base Sepolia (testnet).

- **Explorer** — a search engine for the chain.
  *Warung-world:* the public reading room of the national archive.
  *In NotaPeer:* where any lender can look up your anchors.

---

## 3 · Secret-Math Words

- **Hash** — a fingerprint of data: same input, same fingerprint; one grain
  of rice changed, entirely new fingerprint.
  *Warung-world:* press your thumb in ink — the print proves the thumb
  without carrying the thumb.
  *In NotaPeer:* every transaction becomes a leaf hash.

- **Merkle tree** — a folder of fingerprints, folded pairwise until one
  fingerprint remains.
  *Warung-world:* 1,000 notes → 500 seals → 250 seals → … → 1 seal.
  *In NotaPeer:* built locally each period from your transactions.

- **Merkle root** — that final single fingerprint summarizing the whole folder.
  *Warung-world:* the one notary seal on the sealed box of 1,000 notes.
  *In NotaPeer:* the **only** bytes that cross onto the chain.

- **Merkle proof** — the minimal trail of sibling fingerprints proving one
  document belongs inside the sealed box.
  *Warung-world:* the notary opens only 10 drawers to prove your note was in
  the box — not all 1,000.
  *In NotaPeer:* what `verifyTransaction()` checks for lenders.

- **Encryption vs hashing** — encryption is a locked box (openable with the
  key); hashing is a fingerprint (never openable back).
  *Warung-world:* a brankas vs. a stempel — one hides, the other testifies.
  *In NotaPeer:* your raw books stay encrypted at home; only hashes travel.

- **Digital signature** — a stamp only your key can make, that anyone can
  verify is yours.
  *Warung-world:* your personal seal (cap stempel toko), impossible to forge
  without stealing the stamp itself.
  *In NotaPeer:* Witness attestations are signed by your device key.

---

## 4 · NotaPeer Words

- **Witness / Witness gate** — a 3-second hold during which your pointer's
  micro-jitter is sampled; perfectly still holds are rejected.
  *Warung-world:* signing with your hand, not your name — bots do not tremble,
  humans do.
  *In NotaPeer:* Layer 1 identity; the phrase on every gate: *"Hold to witness."*

- **zid** — sovereign identity issued after passing Witness.
  *Warung-world:* a membership card earned by being alive, not by paperwork.
  *In NotaPeer:* the key that ties books, anchors, and score to one human.

- **Anchor / anchoring** — writing a Merkle root on-chain so a period's books
  become tamper-evident forever.
  *Warung-world:* the monthly visit to the notary: from that stamp onward,
  the page cannot be quietly rewritten.
  *In NotaPeer:* one tap: "Verify period".

- **Anchor API** — a one-call door for partners:
  `POST /anchor {txHash, meta}` → notarized on-chain.
  *Warung-world:* handing your existing notebook to the notary without
  changing how you write in it.
  *In NotaPeer:* how Majoo-likes adopt us without rebuilding anything.

- **UMKMAnchor** — the Solidity notary contract (`anchorReport`,
  `verifyTransaction`, events `ReportAnchored` / `ReportRevoked`).
  *Warung-world:* the notary office itself — open 24/7, no queue, no bribes.
  *In NotaPeer:* deployed on Base / Polygon.

- **Proof budget / session** — one Witness hold opens a budget of actions
  (e.g., 10 anchors); cadence is policy, not punishment.
  *Warung-world:* the notary knows your face for the whole visit; you don't
  re-sign every page.
  *In NotaPeer:* "gate the door, not every coin."

- **Counter-party attestation (peer witness)** — the other side of a big
  trade co-confirms it with their own Witness hold.
  *Warung-world:* the supplier signing your purchase note: "yes, I sold him
  50kg of beras that day."
  *In NotaPeer:* peer-attested records carry higher credit weight.

- **Local-first / offline-first** — books live on your device first; the
  cloud is a copy, not the owner.
  *Warung-world:* your notebook stays in your drawer even when the internet
  (and the electricity) leaves.
  *In NotaPeer:* encrypted on-device DB + sync when connectivity returns.

- **Sync** — the moment connectivity returns and local changes meet the cloud.
  *Warung-world:* the courier finally reaching your village road.
  *In NotaPeer:* PowerSync/Supabase reconciliation, conflict-safe.

- **Credit-score layer** — reads anchor trails + consistency signals and
  publishes a permissionless score.
  *Warung-world:* your reputation, computed from stamped pages instead of
  gossip.
  *In NotaPeer:* Phase 4; the bridge to DeFi lending.

- **ERC-4337** — the Ethereum standard that lets relays pay gas and lets
  smart wallets exist without seed-phrase gymnastics.
  *Warung-world:* the regulation that allows a trusted courier to mail
  letters on your behalf, postage included.
  *In NotaPeer:* the machinery behind "gasless for merchants".

---

## 5 · Money-Model Words

- **B2B** — selling to businesses, not to end users.
  *In NotaPeer:* our customers are gateways and lenders; merchants stay free.

- **API licensing** — charging partners per call to our notarization door.
  *In NotaPeer:* Priority-1 revenue stream.

- **Freemium** — core free forever; comfort features paid.
  *In NotaPeer:* Pro/Enterprise tiers from Phase 4.

- **Revenue share** — taking a small slice of value we helped create.
  *In NotaPeer:* 0.5–1% of loans facilitated via our scores.

- **Grant** — non-dilutive funding from foundations that want the ecosystem
  to grow.
  *In NotaPeer:* the bootstrap fuel of Year 1.

- **Pilot** — a small, real, measured deployment before scale.
  *In NotaPeer:* 10–100 warung kopi, one city, three months.

---

*Rule of this glossary: if a term needs a fourth line, the feature is too
complicated — simplify the feature.*