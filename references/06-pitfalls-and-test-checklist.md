# 06 — Common mistakes and go-live test checklist

## Common mistakes
| # | Mistake | Consequence | Fix |
|---|---|---|---|
| 1 | Treating card approval as "sale done" | Paid but unfiscalised sales | Mark order complete only after the device returns a receipt number |
| 2 | Blind retry on timeout | Double receipts / double charges | Idempotency key + status query before retry |
| 3 | Issuing both receipt and invoice for one sale | Double-reported revenue | Invoice → information slip, not receipt |
| 4 | Product with no department / wrong VAT | Wrong VAT reported | Startup validation of mapping; change rates on device and catalogue together |
| 5 | App and device round differently | 0.01 TRY differences, rejected sales | Compute VAT per VAT group like the device |
| 6 | Document discount not allocated per VAT rate | Wrong VAT base | Pro-rata allocation |
| 7 | Using a "copy" print as a new receipt | Fiscal irregularity | Use the device's official copy function only |
| 8 | Open sale left on device at closing | Z report blocked or missing sale | Check for open sales before Z |
| 9 | No Z report on a trading day | Reporting gap visible to GİB | Daily Z, alert if missing |
| 10 | e-commerce order with an ÖKC receipt instead of e-Arşiv | Wrong document | Channel-based document decision (`03-document-types.md`) |
| 11 | Not checking whether a B2B buyer is an e-Fatura user | e-Arşiv sent to an e-Fatura user | Lookup by tax id before issuing |
| 12 | Hard-coding yearly TRY thresholds | Wrong after 1 January | Store thresholds as dated configuration |
| 13 | Meal card tender merged into "card" | Reconciliation impossible | One tender type per provider |
| 14 | Storing card data | PCI-DSS scope | Store only masked PAN / approval refs returned by the terminal |

## Go-live test checklist
### Setup
- [ ] Device model is GİB-approved and registered to the taxpayer; vendor SDK version recorded
- [ ] Department/VAT mapping matches catalogue (20 / 10 / 1 %) and is reviewed by the accountant
- [ ] Yearly thresholds (invoice limit, e-Arşiv scope) stored as dated config with source

### Sales
- [ ] Single item, cash, exact amount
- [ ] Cash with change
- [ ] Bank card approved; bank card declined; card approved + device error (recovery)
- [ ] Each meal-card brand you accept; meal card + card split; meal card partial decline
- [ ] Mixed VAT basket (20 % + 10 % + 1 %) — totals per VAT group match app
- [ ] Line discount, document discount, 100 % comp
- [ ] Weighed item with 3-decimal quantity
- [ ] Service/cover charge line (if used)
- [ ] Sale above the current invoice threshold → invoice + information slip
- [ ] Customer requests invoice below the threshold
- [ ] B2B buyer: e-Fatura user vs. non-user

### Failures
- [ ] Network drop between app and device mid-sale (REST/cloud)
- [ ] Device off / paper out / cover open
- [ ] App crash after payment, before receipt → recovery on restart
- [ ] Duplicate submit (double click) → only one receipt

### Corrections and closing
- [ ] Line cancel, whole-sale cancel before close
- [ ] Same-day return / void per vendor procedure
- [ ] Return on a later day per accountant's procedure
- [ ] X report mid-day; Z report end of day; Z number stored
- [ ] Z totals per VAT rate and per tender reconcile with app and provider statements

### Online channel
- [ ] e-Arşiv issued for each online order; PDF/e-mail delivered
- [ ] Cancelled online order → e-Arşiv cancellation/return handled **[verify current rules]**

Sign-off: developer, store manager, accountant.
