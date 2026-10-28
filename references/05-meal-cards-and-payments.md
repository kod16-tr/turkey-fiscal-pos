# 05 — Meal cards, card payments and split tender

> Not legal or tax advice. Payment rules for meal cards were under active discussion in 2024–2025. Verify current status with GİB, the Ministry of Trade and each provider.

## Tender types you must support
| Tender | Notes |
|---|---|
| Cash | Registered on the ÖKC; change computed by device or app (keep them consistent). |
| Bank card (credit/debit) | On EFT-POS ÖKC the card payment and receipt are linked on one device. External bank POS: link the slip reference to the sale. |
| **Meal card** (*yemek kartı*) | Employer-funded cards accepted at restaurants and some markets. Separate provider, separate approval, separate settlement. |
| Voucher / gift card / points | See `04-vat-and-pricing.md` (discount vs. tender). |
| Online/external payment (payment link, wallet, aggregator) | Payment happens outside the device; you still need a fiscal document. |

## Meal cards
Common providers in Turkey: **Multinet, Pluxee (formerly Sodexo), Edenred (Ticket), Setcard, Metropol**. Each has its own merchant agreement, terminal or app and settlement cycle.

Integration models seen in the market:
1. **Provider's own terminal (external POS)** — cashier keys the amount; the device is separate from the ÖKC. A public GİB answer reported that, under certain conditions and with written notification to GİB, meal-card providers' external POS devices could continue to be used without integration to the new-generation ÖKC; the merchant then invoices the meal-card company and keeps the slip copies. [S12] **[verify current status]**
2. **App on Android POS ÖKC** — the meal-card app runs on the fiscal device and the payment is recorded as a tender on the same receipt.
3. **QR / mobile wallet** — customer pays from the provider's app; merchant confirms; link the provider's transaction id to the sale.

GİB's draft format guide for new-generation ÖKC receipts and e-documents (Dec 2025) defines a separate meal-card payment document format, indicating closer integration is coming. [S13] **[draft – verify final version]** The Ministry of Trade also published announcements on meal-card regulation. [S14]

### Design rules
- Treat each meal-card brand as its own **tender type** for reporting and reconciliation.
- Store provider transaction id, terminal id, amount, and the fiscal receipt no together.
- Meal cards typically cannot pay for everything (e.g. alcohol, tobacco or non-food items may be excluded by provider/employer rules). Validate basket eligibility. **[verify per provider]**
- Commission and settlement: reconcile provider statements against your tender totals per Z report.

## Split (parçalı) payments
```
remaining = basketTotal
for each tender chosen by cashier:
    authorize(tender, amount ≤ remaining)   # card / meal card get approval ids
    remaining -= amount
when remaining == 0:
    fiscalise(sale, tenders[])              # ONE receipt listing all tenders
```
- One sale → one fiscal document with multiple tenders. Do not print one receipt per tender.
- If a later tender fails, offer: another tender, or reverse the earlier approvals and cancel the sale.
- Splitting a restaurant bill between guests (each pays own items) = multiple sales, each with its own receipt.

## External / online payment providers
- For e-commerce and delivery platforms, the payment provider (virtual POS, wallet, marketplace) does **not** fiscalise for you. Issue the **e-Arşiv Fatura** (or e-Fatura) yourself or via your integrator, and keep the payment reference on the invoice record.
- For pay-at-table / QR ordering inside a venue, the venue still needs a fiscal document for the sale (ÖKC receipt or invoice). Design how the online payment is reflected as a tender on the device. **[verify with device vendor]**

Sources: S12–S14 in `sources.md`.
