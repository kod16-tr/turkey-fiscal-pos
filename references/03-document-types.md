# 03 — Which document, when?

> Not legal or tax advice. Thresholds are revalued yearly. Verify with GİB / your accountant.

## The documents
| Document | Issued by | Typical buyer | Notes |
|---|---|---|---|
| **ÖKC fişi** (fiscal receipt) | ÖKC | Consumer, in person | Default for counter retail and restaurants. [S1] |
| **e-Arşiv Fatura** | Seller's e-Arşiv system (own, integrator, or GİB portal) | Consumers and buyers **not** registered for e-Fatura | Mandatory for e-commerce/distance sales; delivered as PDF/e-mail/SMS link. [S7][S9] |
| **e-Fatura** | e-Fatura system (UBL-TR) | Buyers **registered** in GİB's e-Fatura user list | B2B between e-Fatura users must be e-Fatura. Check the buyer's registration (by VKN/TCKN) before issuing. [S7] |
| **e-Adisyon** | e-Adisyon system | Restaurant table service | Electronic version of the order/bill (*adisyon*) introduced by VUK 509; obligation applies to taxpayers **designated by GİB**, with at least 3 months' notice. [S10] **[verify whether you are designated]** |
| **Bilgi fişi** (information slip) | ÖKC | — | Printed when an invoice is issued for a sale registered on the ÖKC, so the device still records it. [S1] **[verify exact use cases with vendor/accountant]** |

## Decision table
```
Is the buyer a VAT-registered business that wants an invoice?
 ├─ yes → Is the buyer an e-Fatura user? → yes: e-Fatura   no: e-Arşiv Fatura
 │        (in-store: ÖKC prints an information slip, not a receipt)
 └─ no (consumer)
      ├─ In-store / counter sale       → ÖKC receipt
      │     └─ total ≥ invoice threshold OR customer asks → invoice (e-Arşiv) + information slip
      ├─ Online / delivered to address → e-Arşiv Fatura
      └─ Restaurant table service      → ÖKC receipt (+ e-Adisyon if you are designated)
```

## Invoice threshold (fatura düzenleme sınırı)
- Under VUK Art. 232 an invoice is mandatory when the sale amount exceeds a yearly revalued limit. **For 2026 the limit is TRY 12,000** (VUK General Communiqué No. 588). Below the limit an invoice is still mandatory **if the customer asks for one**. [S8]
- 2025 was TRY 9,900 [S8]. Always look up the current year.

## e-Arşiv scope (recent changes)
- Thresholds for mandatory e-Arşiv have been lowered step by step (VUK 509 as amended). For balance-sheet taxpayers sources indicate **all invoices must be e-Arşiv or e-Fatura from 1 Jan 2026**; for simple-method and business-account taxpayers secondary sources disagree on whether the "regardless of amount" rule starts 2026 or 2027 (amended by VUK 589). **[verify with GİB / your accountant]** [S9]
- Practical rule for software vendors: build e-Arşiv as a first-class output; do not design around paper invoices.

## e-Fatura vs e-Arşiv in practice
| Check | e-Fatura | e-Arşiv |
|---|---|---|
| Buyer lookup | Required: buyer must be in GİB e-Fatura user list | Not required |
| Delivery | Via GİB to buyer's mailbox | Seller delivers (e-mail/PDF/print) |
| Format | UBL-TR XML | UBL-TR XML (+ human-readable copy) |
| Cancel/return | Return invoice / rejection flows | Cancellation within the allowed period, or return document **[verify current rules]** |

Sources: S1, S7–S10 in `sources.md`.
