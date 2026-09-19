# NotaPeer — Flowcharts

Three views of the system: the merchant journey, the partner (Anchor API)
journey, and the verifier journey. Diagrams use Mermaid and render natively
on GitHub.

## 1 · Merchant Journey (core loop)

```mermaid
flowchart TD
    A[Download / open app] --> B{Witness gate<br/>hold 3s}
    B -- rejected: too still --> B
    B -- passed --> C[zid issued<br/>sovereign identity]
    C --> D[Dashboard]
    D --> E[Input transaction<br/>income / expense]
    E --> F[(Local encrypted DB<br/>offline-first)]
    F -- connectivity --> G[Sync Supabase]
    G --> H{End of period?}
    H -- no --> D
    H -- yes --> I[Tap: Verify period]
    I --> J[Merkle tree built<br/>leaves = tx hashes]
    J --> K[ERC-4337 gasless relay]
    K --> L[UMKMAnchor.anchorReport]
    L --> M[anchors row:<br/>merkle_root, tx_hash, block]
    M --> N[Badge: Verified on-chain]
    N --> D
```

## 2 · Partner Journey (Anchor API)

```mermaid
sequenceDiagram
    participant P as Partner POS / SaaS
    participant A as Anchor API
    participant W as Witness
    participant C as UMKMAnchor (L2)
    P->>A: POST /anchor {txHash, meta}
    A->>W: request human attestation
    W-->>A: witness signature (zid, policy v1)
    A->>C: anchorReport(root, period)
    C-->>A: tx_hash, block_number
    A-->>P: 200 {anchorId, txHash, explorerUrl}
    Note over P,C: Partner badge: "Notarized by NotaPeer"
```

## 3 · Verifier Journey (lender / auditor)

```mermaid
flowchart LR
    V[Verifier] --> Q[GET /verify?anchor=...]
    Q --> R[Read merkle_root from chain]
    R --> S{Merkle proof<br/>matches leaf?}
    S -- yes --> T[Record authentic]
    S -- no --> U[Tampered or unknown]
    T --> W2[Feed credit-score layer]
```

## 4 · ASCII Fallback (for tools without Mermaid)

```
[MERCHANT]
 open app -> WITNESS(hold 3s) -> zid -> dashboard
   -> input tx -> local DB -> sync -> [end of period?]
       -> merkle tree -> gasless relay -> ANCHOR(L2)
       -> badge: verified -> dashboard

[PARTNER]
 POS -> Anchor API -> Witness sig -> ANCHOR(L2) -> badge

[VERIFIER]
 lender -> read root on-chain -> merkle proof? -> authentic / tampered
```

## Design Notes

- **Gate the door, not every coin:** Witness cadence is a policy parameter
  (session budget, idle re-gate). The jam-era build gated every spin;
  production gates sessions.
- **Rules change, history does not:** anchor policy is versioned per
  attestation; old anchors stay verifiable forever.
- **Privacy by construction:** only Merkle roots cross the chain boundary.
- **Peers over oracles:** high-value records gain weight from counter-party
  witness holds, not from paid data feeds.