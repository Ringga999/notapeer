# 🚪 Two Doors, One Book — Owner & Cashier Separation

> *The cashier holds the counter. The owner holds the vault. Neither key opens the other's door.*

**Status:** Specification locked · 1 October 2026
**Companion specs:** `notapeer-app/docs/SPEC-ROLES.md` (private) ·
`zcp2o-protocol/specs/employment-binding.md` (future on-chain binding)

---

## Why Separation Exists

A warung is a family of trust: the owner trusts the cashier with the counter,
and the cashier trusts the owner with their wages. Software must honor that
trust by **making overreach impossible, not merely forbidden**.

- The cashier needs a **simple, fast tool**: shift, sell, undo mistake, clock out.
- The owner needs a **safe vault**: ledger, balance, anchors, exports, staff control.
- Neither should ever see a button that tempts the other's boundary.

## The Two Doors
notapeer.app/ → OWNER APP : full shell, all rooms
notapeer.app/kasir → CASHIER APP : locked kiosk, own login, own PWA icon


- The cashier door has **no corridor** to owner rooms. Exit = logout, never "back to dashboard".
- Installable separately: home-screen icon **"NotaPeer Kasir"** on the shop tablet
  or the cashier's phone-at-work.
- One codebase, two applications — a solo founder feeds one baby; the cashier
  experiences a separate one. Physical repo split remains a documented upgrade path.

## One Device, Many Sovereign Roots

The device is a vault holding **many identities**, each fully sovereign:

- Owner root + owner PIN + owner recovery phrase
- Cashier root + cashier PIN + cashier recovery phrase (per employee)
- Login = choose profile → enter PIN. No shared passwords, ever.
- Suspension is immediate: a suspended profile cannot wake, mid-shift or not.

## Permission Matrix

| Capability | CASHIER | OWNER |
|---|:---:|:---:|
| Open/close own shift | ✅ | ✅ |
| Record sales · undo own last sale | ✅ | ✅ |
| See own shift totals & own attendance | ✅ | ✅ |
| Ledger, balance, charts, anchors | ❌ | ✅ |
| Delete/edit any record | ❌ | ✅ |
| Export data | ❌ | ✅ |
| All-staff attendance | ❌ | ✅ |
| Manage staff profiles (add/suspend) | ❌ | ✅ |
| Settings, PINs, identities | ❌ | ✅ |
| Leaving the kiosk | = logout | = dashboard |

## One Book, Many Hands

- Cashier sales flow into the **same local ledger**, each entry signed with the
  cashier's face (`actor`) — accountability without surveillance.
- Attendance is per face: the owner sees everyone; each cashier sees only themselves.
- The monthly Merkle anchor covers all hands — the book stays one truth.

## Doctrine Lines (non-negotiable)

1. A cashier cannot touch what a cashier cannot see.
2. Sessions die with the shift: cashier tokens expire at clock-out (hard cap 12h).
3. Suspension beats speed: owner suspends → every door closes instantly.
4. No guests, no shared PINs, no recovery phrases on screens after first show.
5. The employee's identity belongs to the employee — leaving the warung keeps
   their attendance history as theirs, attested by their own face.

## Future Doors (documented, not built)

- **On-chain employment binding** (`Bound` event) — see protocol spec.
- **Multi-device sync** (Wave 4) — cashier app on the cashier's own phone.