# SPEC — Roles Wave (R6–R8): Owner App & Cashier App

Locked 1 October 2026 · Doctrine: notapeer/docs/ROLES.md · Protocol reserve: zcp2o-protocol/specs/employment-binding.md

## 1. Locked Decisions

| # | Decision | Value |
|---|----------|-------|
| 1 | Architecture | One codebase, two route trees: `/` (owner) & `/kasir` (cashier, PWA-installable "NotaPeer Kasir") |
| 2 | Identity | Multi-profile vault: array of sovereign roots per device (owner + cashiers) |
| 3 | Employment binding | Local record now (`boundTo`); on-chain `Bound` event reserved for v2 |
| 4 | Ledger accountability | Transaction v2 adds `actor` (face hex of creator); legacy rows = undefined → owner |
| 5 | Sessions | Owner: optional 30-day trust token · Cashier: dies at clock-out, hard cap 12h, no long trust |
| 6 | Exit semantics | Cashier kiosk exit = logout (never "back to dashboard"); owner exit = dashboard |

## 2. Storage Schema

`notapeer.identities.v1` (replaces single-identity key; migration wraps the old root as the owner profile):

    [{
      "id": "p1",
      "name": "Bu Sari",
      "role": "owner",              // owner | cashier
      "salt": "…", "iv": "…", "ct": "…",   // AES-GCM(root) keyed by that profile's PIN
      "status": "active",           // active | suspended
      "boundTo": null,              // cashier: merchantFace bytes32 of the owner
      "createdAt": "…"
    }]

`notapeer.session.v1`:

    { "profileId": "p2", "role": "cashier", "token": "…", "expiresAt": 1790900000000 }

`notapeer.transactions` v2: existing fields + `actor?: string` (face hex; written by CashierMode & Dashboard form from the active session).

Migration rules:
- Old `notapeer.identity.v1` → becomes profiles[0] with role=owner, name="Owner".
- Old `notapeer.session.v1` (zid-based) → invalidated once; owner re-logins with PIN.
- Old shift rows keep their legacy zid string; new rows store the acting face.

## 3. Route Trees & Guards

- `app/kasir/page.tsx` → `CashierGate`: lists profiles where role=cashier AND status=active → PIN → locked shell.
- Locked shell contents: kiosk (reuse CashierMode), "My Shift" summary, own attendance rows, Logout. NO owner imports in this tree (bundle-level separation).
- `lib/session.ts`: `currentSession()`, `requireRole(role)`, `endSession()`.
  - `/` with cashier session → redirect to `/kasir`.
  - `/kasir` with owner session → offer switch (logout owner first) — never implicit.
  - Guard re-checks `status` on every wake: suspended profile = instant lockout, mid-shift or not.
- PWA: second manifest `public/site-kasir.webmanifest` (name "NotaPeer Kasir", cart icon, start_url `/kasir`).

## 4. Owner Staff Management (Settings → Staff)

- Add: enter name → hand device → employee sets own PIN + sees recovery words ONCE → profile created with role=cashier, boundTo=merchantFace, status=active.
- Suspend / reactivate: flips `status`; every live session of that profile dies on next guard check.
- Remove: deletes profile keys; attendance & actor history preserved by face (history belongs to the book, identity belongs to the human).

## 5. Build Steps & Acceptance

- R6 — multi-profile identity store + migration + profile-picker login (separate owner & cashier lists).
  AC: existing single identity wakes as owner profile without re-register; cashier list empty initially.
- R7 — `/kasir` route + CashierGate + locked shell + kasir manifest.
  AC: cashier session cannot reach `/` rooms (redirect on render); exit = logout; reload mid-shift resumes kiosk only.
- R8 — staff management UI + `actor` field on new transactions + per-face attendance views.
  AC: cashier sale shows cashier face in owner attendance; cashier sees only own rows; suspended profile cannot wake.

## 6. Threat Model (must be impossible for a cashier)

1. Read/modify any record outside own shift.
2. See balance, charts, anchors, exports — even briefly.
3. Change another profile's PIN or view its recovery words.
4. Use any session after suspension (guard checks status on every wake).
5. Reach owner routes by URL crafting (role guard on render, not just hidden links).
6. Stay logged in past clock-out (token expiry enforced on mount; hard cap 12h).
7. Re-register the device as owner without the owner PIN (registration requires owner session).

## 7. i18n Keys (new)

kasirApp.title, kasirApp.subtitle, kasirApp.myShift, kasirApp.logout, kasirApp.suspended, kasirApp.switchHint
staf.title, staf.add, staf.name, staf.handDevice, staf.suspend, staf.reactivate, staf.remove, staf.empty
login.chooseProfile, login.ownerProfiles, login.cashierProfiles, login.wrongPin, login.suspendedProfile

## 8. Seeds for Future Waves (ide tertanam, tidak dibangun sekarang)

- Shift handover signature: outgoing cashier signs closing total; incoming confirms on wake.
- Daily closure receipt: shareable image of shift summary (WhatsApp-ready).
- Cashier-of-the-month: attendance + sales consistency stats derived from faces.
- On-chain employment binding flush (mirror of the attestation queue) when `Bound` event ships.