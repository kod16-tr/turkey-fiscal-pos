# 04 — VAT (KDV), product mapping, rounding, discounts, service charge

> Not tax advice. Rates per product are set by Presidential Decision lists and change; confirm each product category with your accountant.

## Current rate structure
Since **10 July 2023** (Presidential Decision No. 7346, Resmî Gazete 07.07.2023): general rate **20%**, reduced rates **10%** and **1%**. [S11]

| Rate | Typical examples (illustrative) | Status |
|---|---|---|
| 20% | General goods, alcoholic drinks, cleaning/paper products | [S11] |
| 10% | Many food & beverage services in restaurants/cafés, many foodstuffs | **[verify per item]** |
| 1%  | Certain basic foodstuffs (e.g. some bread/grain products) | **[verify per item]** |
| 0% / exempt | Exports and specific exemptions | Out of scope for ÖKC counter sales |

The same product can carry different rates depending on how it is sold (e.g. take-away vs. served). Keep the rate on the **sold item**, not the ingredient.

## Mapping products to the device
- The ÖKC uses **departments (kısım)** or VAT groups. Each department is bound to one VAT rate.
- Keep a mapping table in your app: `product → department/VAT group`. Validate on startup that every active product maps to a department that exists on the device.
- When rates change, the change must be applied on **both** the device (vendor/TSM procedure) and your product catalogue on the same day.

```json
{ "productId": "SKU-1001", "name": "Ayran", "price": 45.00, "vatRate": 10, "department": 2 }
```

## Prices and rounding
- Consumer prices are **VAT-inclusive**. Store the gross unit price; derive net and VAT.
- TRY has 2 decimals (kuruş). Device computes VAT **per VAT group** on the receipt; your app should compute the same way to avoid 0.01 differences:
```
for each vatRate group:
    gross = round2(sum(line.qty * line.unitGross) - groupDiscount)
    vat   = round2(gross * rate / (100 + rate))
    net   = gross - vat
```
- Quantities: weighed goods with 3 decimals are common; round the **line total**, not the unit price.
- For e-Arşiv/e-Fatura (UBL-TR) VAT is per line and per document; check that receipt totals and invoice totals agree.

## Discounts
| Type | How to handle |
|---|---|
| Line discount | Reduce that line's gross; VAT follows the line's rate |
| Document discount (e.g. 10% off bill) | Allocate **pro rata** across VAT groups; send as a document discount if the device supports it, otherwise as line discounts |
| Free item / comp | Sell at 0 or apply 100% line discount, per accountant's preference **[verify]** |
| Loyalty points / vouchers | Decide: discount (reduces VAT base) vs. tender (payment method). Usually a voucher sold earlier is a tender. **[verify with accountant]** |

Never let a discount make a VAT group negative.

## Service charge, cover, tips
- If you charge a **service charge** or **cover charge**, it is part of the sale and must appear on the fiscal document with a VAT rate (commonly the rate of the underlying service). **[verify]**
- Consumer-protection rules on price display (menus, price tags) may restrict charging amounts not shown in advance; see the Ministry of Trade price-tag regulation. **[verify with current regulation]**
- **Tips** paid to staff (voluntary) are usually not part of the sale; if collected by card on the POS, agree the treatment with your accountant. **[verify]**

Sources: S11 in `sources.md`.
