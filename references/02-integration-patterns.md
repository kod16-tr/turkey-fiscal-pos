# 02 — Integration patterns and the transaction lifecycle

> Generic patterns only. Each device vendor publishes its own SDK/API; follow the vendor's official documentation for exact calls, fields and certification. Do not reuse field names from this file as if they were a real API.

## Three integration models
| Model | How it works | Pros | Watch out for |
|---|---|---|---|
| **A. Local REST/HTTPS to the device** | POS app sends JSON over the LAN (or localhost on Android POS) to a service on the ÖKC. | Easy for web/mobile stacks; works with Android POS. | Device IP changes, TLS/self-signed certs, timeouts, one-request-at-a-time locking. |
| **B. Serial / USB (incl. GMP-3 pairing)** | POS PC talks to the ÖKC over RS-232/USB using the vendor library or the public GİB GMP-3 pairing protocol. [S6] | Mature, offline-safe. | Native drivers, COM-port management, OS support. |
| **C. Cloud / vendor-hosted** | App calls the vendor's cloud; cloud pushes the job to the paired device. | No LAN access needed; good for SaaS. | Internet dependency at the counter, latency, idempotency, device online status. |

Many vendors offer more than one model. Pick by: where your app runs (Windows PC, Android, browser, cloud), whether the counter has reliable internet, and whether the device also takes card payments.

## Canonical sale flow
```
1. BASKET     app builds lines (name, qty, unit price incl. VAT, VAT rate/department)
2. OPEN       app → device: open sale (or one-shot "sale" request)  [idempotency key!]
3. PAYMENT    for each tender:
                cash        → registered on device
                bank card   → EFT-POS on same device, or external bank POS linked to the sale
                meal card   → meal-card app/terminal, linked as tender type
4. FISCALISE  device closes sale, prints receipt (or information slip if an invoice is issued)
5. RESULT     device → app: receipt no, Z no, date/time, totals per VAT rate, payment refs
6. PERSIST    app stores result; marks order as fiscalised
7. INVOICE    (optional) e-Arşiv / e-Fatura issued and referenced to the slip
```

Example of the *shape* of a generic request (illustrative, not any vendor's API):
```json
{
  "idempotencyKey": "order-2026-000123",
  "documentType": "RECEIPT",
  "lines": [
    {"name": "Lentil soup", "qty": 1, "unitPrice": 120.00, "vatRate": 10},
    {"name": "Soft drink",  "qty": 2, "unitPrice": 60.00,  "vatRate": 20}
  ],
  "discounts": [{"type": "DOCUMENT", "amount": 20.00}],
  "payments": [
    {"tender": "MEAL_CARD", "provider": "<meal-card-brand>", "amount": 100.00},
    {"tender": "BANK_CARD", "amount": 120.00}
  ]
}
```

## Idempotency and failure handling (most bugs live here)
```
send(sale, key)
on timeout:
    status = query_device_status(key)      # never blindly resend
    if status == FISCALISED: persist(result)
    elif status == OPEN: resume or cancel the open sale on the device
    else: retry with SAME key
```
- Card approved but receipt failed → do **not** charge again; complete or void on the device using the vendor's recovery procedure.
- Paper out / cover open → device-side error; surface to cashier, then resume.
- Never print a "copy" of a fiscal receipt as a new sale.

## Void, cancel, refund
| Situation | Typical handling | [verify] |
|---|---|---|
| Line correction before payment | Line cancel inside the open sale | — |
| Cancel whole sale before close | Sale cancel on device; card reversal if already approved | — |
| After receipt printed, same day | Vendor-specific void/return procedure; card refund via bank | **[verify procedure with vendor & accountant]** |
| Return after Z report / another day | Usually a return document (e.g. *gider pusulası* or return invoice) per accounting rules, not a negative sale | **[verify with your accountant]** |

## End of day: X and Z reports
- **X report**: read-only, any time.
- **Z report**: closes the fiscal day, resets daily totals, is reported to GİB via TSM. Take it at least daily on days with sales. [S5]
- Before Z: ensure no sale is left open, all orders are fiscalised, card batch is settled (for EFT-POS the bank end-of-day may be triggered together; vendor-specific).
- After Z: store Z number, totals per VAT rate and per tender; reconcile against your order database.

Sources: S5, S6 in `sources.md`.
