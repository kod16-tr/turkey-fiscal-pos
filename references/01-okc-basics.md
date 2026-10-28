# 01 — ÖKC basics: what it is and who must use one

> Not legal or tax advice. Verify with GİB / your accountant.

## What is an ÖKC?
**ÖKC (Ödeme Kaydedici Cihaz)**, colloquially *yazarkasa*, is a GİB-approved fiscal device that registers retail sales, prints fiscal receipts and keeps tamper-resistant fiscal memory. The legal basis is Law No. 3100 on the use of payment-recording devices and the Tax Procedure Law (VUK) general communiqués issued under it. [S1][S2]

### Device generations and families
| Family | What it is | Typical use |
|---|---|---|
| **Yeni nesil ÖKC** (new-generation ÖKC) | Fiscal register with secure element and permanent connection to GİB via a **TSM** (trusted service manager) operated for the vendor. | Retail counters, restaurants |
| **EFT-POS ÖKC** | New-generation ÖKC with a built-in bank card terminal; card payment and fiscal receipt on one device. | Most counter sales today |
| **Android / smart POS ÖKC** | EFT-POS ÖKC running Android; third-party apps can run on the device or talk to it. | Restaurants, mobile/table-side sales |
| Old-generation ÖKC | Pre-2013 devices without online reporting. | Being phased out; replacement rules in VUK 557 [S4] |

Since 2013 the new-generation devices report sales and Z reports electronically to GİB; VUK General Communiqué No. 566 (Resmî Gazete 25.09.2024) further regulates electronic reporting of Z reports via the TSM and puts responsibility for continuity of reporting on the user. [S3][S5]

## Who must use one?
- In general, taxpayers selling goods/services **directly to final consumers** (retail, restaurants, cafés, many services) must register those sales on an ÖKC, unless they are exempt or issue invoices instead. [S1][S2]
- Some activities are required to use **EFT-POS ÖKC** specifically (e.g. mobile/itinerant card acceptance). [S2]
- Exemptions exist based on activity type and size thresholds; VUK 566 updated the revenue/asset thresholds for exemption. **[verify current exemption list with GİB]** [S5]
- **E-commerce** sales delivered to a consumer's address are normally documented with an **e-Arşiv Fatura**, not an ÖKC receipt. See `03-document-types.md`. **[verify for your business model]**

## GİB's role
| GİB does | Means for you |
|---|---|
| Approves device models and vendors | Only use certified devices; your software is *not* certified by GİB, the device is. |
| Publishes technical documents for new-generation ÖKC (incl. the public **GMP-3** protocol for pairing an ÖKC with external devices/apps) on the YN ÖKC portal | Read the public docs, then the vendor's SDK. [S6] |
| Receives sales and Z report data electronically via TSM | Missing Z reports or offline devices become visible to the tax office. |
| Runs the e-Belge (e-invoice) systems | e-Arşiv, e-Fatura, e-Adisyon live under ebelge.gib.gov.tr. [S7] |

## Key vocabulary
| Turkish | English | Notes |
|---|---|---|
| Mali fiş / ÖKC fişi | Fiscal receipt | Proof of sale for consumers |
| Bilgi fişi | Information slip | Printed by ÖKC when an invoice is issued instead of a receipt |
| Z raporu | Z report | End-of-day fiscal closing, resets daily counters |
| X raporu | X report | Read-only interim report, no reset |
| Kısım / departman | Department | Maps items to a VAT rate on the device |
| Mali müşavir | Licensed accountant | Your final authority on bookkeeping |
| TSM | Trusted service manager | Connects devices to GİB |

Sources: see `sources.md` (S1–S7).
