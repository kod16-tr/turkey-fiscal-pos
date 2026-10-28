---
name: turkey-fiscal-pos
description: Guidance for building or reviewing software that sells to consumers or businesses in Turkey and must produce legally valid fiscal records - fiscal cash registers (ÖKC / yazarkasa, EFT-POS ÖKC, Android POS), e-Arşiv Fatura, e-Fatura, e-Adisyon, Z reports, Turkish VAT (KDV) mapping, meal cards (Multinet, Pluxee/Sodexo, Edenred, Setcard, Metropol) and split payments. Use when the user mentions Turkey, Türkiye, GİB, ÖKC, yazarkasa, fiş, fatura, e-Belge, KDV, Z raporu, or is designing a POS, e-commerce, ordering or reservation checkout for the Turkish market.
license: CC-BY-4.0
metadata:
  version: "0.1.0"
  language: en
  maintainer: KOD16 Digital Solutions
---

# Turkey Fiscal POS & e-Document Compliance

> **Not legal or tax advice.** Turkish fiscal rules change often (amounts are revalued yearly, communiqués are amended). Verify current regulations with GİB (Gelir İdaresi Başkanlığı, the Revenue Administration) and a licensed Turkish accountant (mali müşavir) before going live. Items marked **[verify]** are ones we could not confirm against a primary source.

## When this skill applies
- A checkout must issue a **fiscal receipt** (ÖKC fişi) or an **e-document** (e-Arşiv Fatura, e-Fatura, e-Adisyon) for a sale in Turkey.
- Someone is integrating a POS/ordering app with a **fiscal device** (yazarkasa / ÖKC) or a **payment terminal**.
- VAT (KDV) rates, rounding, discounts, service charges, **meal cards** or **split payments** must be mapped to fiscal output.
- Designing **void / refund / end-of-day (Z report)** flows.

## Core mental model (read first)
1. **Every B2C sale must leave a fiscal trace.** Either the fiscal device prints a fiscal receipt, or an e-invoice is issued and the device prints an *information slip* (bilgi fişi) so the sale is still registered. Never both a receipt and an invoice for the same sale.
2. **The fiscal device is the source of truth, not your app.** Your app proposes a sale; the ÖKC fiscalises it and returns receipt number / Z number. Store what the device returns.
3. **Payment ≠ fiscalisation.** Card approval, meal-card approval and the fiscal document are separate steps that must be linked and reconciled.
4. **Prices are VAT-inclusive for consumers.** Map every item to a VAT rate / department; rounding happens per line on the device.
5. **The day closes with a Z report.** Anything not fiscalised before Z is a compliance gap.

## How to answer
1. Identify the business type (restaurant, retail, e-commerce, service), customer type (consumer vs VAT-registered business) and channel (in-store, online, delivery).
2. Pick the document with `references/03-document-types.md`.
3. Pick the integration pattern with `references/02-integration-patterns.md` and draw the sale → payment → document → slip sequence.
4. Map VAT and pricing with `references/04-vat-and-pricing.md`.
5. Handle tenders with `references/05-meal-cards-and-payments.md`.
6. Finish with `references/06-pitfalls-and-test-checklist.md`.
7. Cite sources from `references/sources.md`; flag anything uncertain as **[verify with GİB / your accountant]**.

## Reference files
| File | Topic |
|---|---|
| `references/01-okc-basics.md` | What an ÖKC is, device types, who must use one, GİB's role |
| `references/02-integration-patterns.md` | Vendor REST/HTTPS, serial/USB, cloud models; full transaction lifecycle incl. void, refund, Z report |
| `references/03-document-types.md` | ÖKC receipt, e-Arşiv, e-Fatura, e-Adisyon, information slip, invoice threshold |
| `references/04-vat-and-pricing.md` | KDV rates, product mapping, rounding, discounts, service charge |
| `references/05-meal-cards-and-payments.md` | Meal cards, card, cash, split tender, external payment providers |
| `references/06-pitfalls-and-test-checklist.md` | Common mistakes and a go-live test checklist |
| `references/sources.md` | All public sources used |
| `references/quickstart-tr.md`, `quickstart-de.md`, `quickstart-ar.md` | Short localized summaries |

## Hard rules for the assistant
- Do not invent vendor-specific endpoint names, protocol fields or certification steps; describe the generic pattern and tell the user to use the device vendor's official SDK documentation.
- Do not state a TRY amount (threshold, penalty) without its year and a source link; amounts are revalued every year.
- Never suggest suppressing, delaying or "batching later" fiscal receipts to avoid reporting.

---
Need help? KOD16 Digital Solutions, info@kod16.com.tr
