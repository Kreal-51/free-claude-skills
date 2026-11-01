# Worked Example: AI Invoice Generator

Below are two complete outputs produced for two real-shaped requests, printed exactly as they would be handed back to the user. Every business, person, address, rate and figure is fictional and is used only to make the arithmetic and the handling of gaps visible end to end.

---

## Scenario 1: Mixed studio work, notes dictated in a hurry

### Raw request as it arrived

> ok so i need to bill Harborline Dental Group for the august stuff. there was the brand refresh, that was the flat 3,200 we agreed on in the SOW. then Priya did 18.5 hrs of photo retouching at 65 and i did 6 hours of press checks at 110. also we fronted 284.50 for the printer proofs, pass that straight through at cost dont mark it up. no tax on this one, our accountant says these services arent taxed where we invoice from. they always pay slow so put net 21 on it instead of the usual. we're Tidewater Studio. their AP contact is Marcus Vela, marcus.vela@harborlinedental.example, and i think their office is somewhere on Dunmore Street but dont quote me on that

### Gaps resolved before the invoice was written

| Gap in the request | How it was resolved |
|---|---|
| No currency named | Defaulted to USD and stated as an assumption in the header block |
| No invoice number given | Generated as INV-20260923-001 from the invoice date |
| "net 21" is not one of the usual terms | Taken literally: 21 calendar days from the invoice date |
| Client street address uncertain ("dont quote me on that") | Omitted entirely; only the confirmed AP contact is printed |
| No payment method named | Left as a bracketed placeholder instead of inventing bank details |
| "they always pay slow" | Not converted into a late fee; no late fee was authorised, so none was added |

### Generated invoice

---

Tidewater Studio

INVOICE

Invoice Number: INV-20260923-001
Invoice Date: September 23, 2026
Due Date: October 14, 2026 (Net 21)

Assumptions made, please correct anything that is wrong before sending:
- Currency defaulted to USD because none was stated.
- Invoice number generated as INV-20260923-001 because no numbering convention was supplied.
- Invoice date set to today, September 23, 2026, because no other issue date was given.
- Due date calculated as 21 calendar days from the invoice date, per the instruction "net 21". September 23 plus 21 days lands on October 14, 2026.
- Tax shown as 0.00 because the request stated these services are not taxed. That statement was taken as given and was not independently checked.
- The printer proofs are billed at the stated cost of 284.50 with no markup, as instructed.
- The client street address was described as uncertain and has therefore been left off.
- No late fee or interest charge has been added, because none was authorised.

Bill To:
Harborline Dental Group
Attn: Marcus Vela, Accounts Payable
marcus.vela@harborlinedental.example

| Description | Quantity | Unit Price | Line Total |
|---|---|---|---|
| Brand refresh, fixed fee per signed SOW | 1 | $3,200.00 | $3,200.00 |
| Photo retouching (P. Priya) | 18.5 hours | $65.00 | $1,202.50 |
| Press check attendance, on-site | 6 hours | $110.00 | $660.00 |
| Printer proofs, reimbursable pass-through at cost | 1 | $284.50 | $284.50 |

How each line total was reached:
- Brand refresh: fixed fee, no quantity multiplier. 1 x $3,200.00 = $3,200.00
- Photo retouching: 18.5 x $65.00 = $1,202.50
- Press check attendance: 6 x $110.00 = $660.00
- Printer proofs: 1 x $284.50 = $284.50

Totals:

Subtotal: $5,347.00
Discount: $0.00 (none requested)
Tax: $0.00 (stated as not applicable by the issuer)
Total Due: $5,347.00 USD

Subtotal check: $3,200.00 + $1,202.50 + $660.00 + $284.50 = $5,347.00
Total check: $5,347.00 - $0.00 + $0.00 = $5,347.00

Payment Terms: Net 21. Full payment of $5,347.00 is due by October 14, 2026.

Payment Instructions: [Add your payment method here, for example bank name, account number, routing number, or the email address tied to your payment processor. Nothing has been filled in because no payment method was provided.]

Notes:
The brand refresh line is the fixed fee agreed in the signed scope of work and is not an estimate. The printer proofs line is a reimbursable expense passed through at cost with no markup. Hours shown for retouching and press checks are billable hours recorded against the August 2026 engagement. Questions about this invoice can go to Tidewater Studio.

---

### Verification a client can repeat by hand

| Check | Working | Result |
|---|---|---|
| Line 1 | 1 x 3,200.00 | 3,200.00 |
| Line 2 | 18.5 x 65.00 | 1,202.50 |
| Line 3 | 6 x 110.00 | 660.00 |
| Line 4 | 1 x 284.50 | 284.50 |
| Subtotal | 3,200.00 + 1,202.50 + 660.00 + 284.50 | 5,347.00 |
| Discount | none requested | 0.00 |
| Tax | stated as not applicable | 0.00 |
| Total due | 5,347.00 - 0.00 + 0.00 | 5,347.00 |

Half-hour rounding note for line 2: 18.5 hours is billed as stated. Half an hour at $65.00 contributes $32.50, which is why the line ends in .50 rather than a whole dollar.

---

## Scenario 2: Two rate types, a discount and a tax rate, a foreign currency, and a company name the user does not have to hand

This second request is the harder one. It stacks four things that commonly go wrong at once: a fixed fee sitting next to two different hourly rates, a percentage discount that has to be applied before tax rather than after, a currency that is not USD, and a legal entity name the user cannot supply. It also carries a payment instruction that is not "net" anything.

### Raw request as it arrived

> Invoice Kestrel Analytics Ltd, they're in Manchester. This one is in pounds, GBP, not dollars. Work was: the Q3 dashboard build, that was a fixed 4,500 quote, signed off. Then 27 hours of ad hoc data cleanup at 78 an hour and 9.25 hours of training sessions at 95 an hour. Knock 7.5 percent off the whole lot, they referred two clients to us this quarter and I promised them something. Then VAT at 20 percent on top of that, that's the rate my bookkeeper told me to charge. Do NOT put my old trading name on the invoice. I registered the limited company three weeks ago and I do not have the exact registered wording in front of me, leave me a gap to fill in. Their finance team pays everything on the last working day of the month after the invoice month, so date it accordingly. Payment is bank transfer, they already have our details on file from the deposit.

### Gaps and traps resolved before the invoice was written

| Item | How it was resolved |
|---|---|
| Legal business name not available | Left as the bracketed placeholder [Your Registered Company Name] in the header. No name was invented and the old trading name was not reused. |
| Currency | GBP, as stated by the user. Written as "GBP" in plain text so the figures survive any encoding. |
| Discount and tax order | Discount applied to the subtotal first, then tax calculated on the discounted amount. Both steps are printed. |
| Tax rate | 20 percent, applied because the issuer supplied that rate. It is printed as an issuer-supplied rate, not as a legal determination. |
| Due date instruction | "Last working day of the month after the invoice month". Invoice month is September 2026, so the month after is October 2026. October 31, 2026 falls on a Saturday, so the due date resolves to Friday, October 30, 2026. |
| Company registration number and tax registration number | Not supplied, so both are left as bracketed placeholders. These usually have to appear on a tax invoice, and guessing them is not safe. |
| Payment method | Bank transfer was named, so the method is stated. The account details themselves were not supplied and are left as a placeholder rather than reused from memory. |

### Generated invoice

---

[Your Registered Company Name]

INVOICE

Invoice Number: INV-20260923-002
Invoice Date: September 23, 2026
Due Date: October 30, 2026

Assumptions made, please correct anything that is wrong before sending:
- The legal business name is missing. [Your Registered Company Name] must be replaced with the exact registered wording of the company before this invoice is sent. The previous trading name was deliberately not used.
- Currency is GBP, as stated in the request. All figures below are GBP.
- Invoice number generated as INV-20260923-002 because no numbering convention was supplied. It follows INV-20260923-001 issued the same day.
- The 7.5 percent discount is applied to the subtotal first. The 20 percent tax is then calculated on the discounted amount, not on the original subtotal. Applying them in the other order would produce a different total, so the order is shown explicitly below.
- The 20 percent tax rate is the rate supplied by the issuer for this invoice. It is reproduced as instructed and has not been independently verified against any rule or schedule.
- Due date derived from the instruction "last working day of the month after the invoice month". The invoice month is September 2026; the following month is October 2026; October 31, 2026 is a Saturday, so the last working day is Friday, October 30, 2026. Working days are assumed to be Monday through Friday. Public holidays were not supplied and have not been taken into account.
- Company registration number and tax registration number were not supplied and are left as placeholders.
- Bank transfer was named as the payment method, but no account details were supplied, so they are left as a placeholder rather than filled in from anywhere else.

Bill To:
Kestrel Analytics Ltd
Manchester, United Kingdom

| Description | Quantity | Unit Price | Line Total |
|---|---|---|---|
| Q3 analytics dashboard build, fixed fee per signed quote | 1 | GBP 4,500.00 | GBP 4,500.00 |
| Ad hoc data cleanup, hourly | 27 hours | GBP 78.00 | GBP 2,106.00 |
| Training sessions, hourly | 9.25 hours | GBP 95.00 | GBP 878.75 |

How each line total was reached:
- Dashboard build: fixed fee, no hourly component. 1 x GBP 4,500.00 = GBP 4,500.00
- Data cleanup: 27 x GBP 78.00 = GBP 2,106.00
- Training: 9.25 x GBP 95.00 = GBP 878.75. The quarter hour contributes GBP 23.75, which is why this line does not end in a round figure.

Totals:

Subtotal: GBP 7,484.75
Discount (7.5% referral discount): -GBP 561.36
Amount after discount: GBP 6,923.39
Tax (20% on the discounted amount, rate supplied by issuer): GBP 1,384.68
Total Due: GBP 8,308.07

Order of operations, shown in full so the client can repeat it:
1. Subtotal: 4,500.00 + 2,106.00 + 878.75 = 7,484.75
2. Discount: 7,484.75 x 0.075 = 561.35625, rounded to the nearest penny = 561.36
3. Amount after discount: 7,484.75 - 561.36 = 6,923.39
4. Tax: 6,923.39 x 0.20 = 1,384.678, rounded to the nearest penny = 1,384.68
5. Total due: 6,923.39 + 1,384.68 = 8,308.07

Why the order matters on this invoice: taxing the full subtotal first and only then applying the discount would give 7,484.75 x 0.20 = 1,496.95 in tax and a total of 8,420.34, which is GBP 112.27 higher than the figure above. The discount was applied first, which is the order the request described.

Payment Terms: Payment in full of GBP 8,308.07 is due by Friday, October 30, 2026, being the last working day of the month following the invoice month.

Payment Instructions: Bank transfer. [Add the account name, sort code, account number and IBAN here. No account details were supplied with this request, so nothing has been filled in. Please reference invoice INV-20260923-002 on the transfer.]

Notes:
Company registration number: [Add registered company number]
Tax registration number: [Add tax registration number]
The dashboard build line is a fixed fee per the signed quote and does not vary with hours worked. The cleanup and training lines are billed at the hourly rates given, including part hours. The referral discount of 7.5 percent is a one-off applied to this invoice only and does not carry forward.

---

### Verification a client can repeat by hand

| Check | Working | Result |
|---|---|---|
| Line 1 | 1 x 4,500.00 | 4,500.00 |
| Line 2 | 27 x 78.00 | 2,106.00 |
| Line 3 | 9.25 x 95.00 | 878.75 |
| Subtotal | 4,500.00 + 2,106.00 + 878.75 | 7,484.75 |
| Discount at 7.5% | 7,484.75 x 0.075 = 561.35625 | 561.36 |
| Net of discount | 7,484.75 - 561.36 | 6,923.39 |
| Tax at 20% of net | 6,923.39 x 0.20 = 1,384.678 | 1,384.68 |
| Total due | 6,923.39 + 1,384.68 | 8,308.07 |
| Contrast, wrong order | tax on the gross subtotal: 7,484.75 x 0.20 = 1,496.95, then 6,923.39 + 1,496.95 | 8,420.34, which is 112.27 too high |

Rounding rule used throughout: each of the discount and the tax is rounded to two decimal places at the moment it is calculated, and the rounded figures are the ones carried into the next step. This is why the printed lines add up exactly rather than differing by a penny from an unrounded calculation.

---

## Assumptions used in this example

Every figure in both invoices above comes from the request it belongs to or from an explicit default. Nothing here is drawn from an outside source.

Scenario 1:
- Issuer name Tidewater Studio, as given. No legal suffix was supplied and none was added.
- Client Harborline Dental Group, with AP contact Marcus Vela, as given. Street address omitted because the user said it was uncertain.
- Fixed fee of $3,200.00 for the brand refresh, as given.
- 18.5 hours at $65.00 per hour for retouching, as given.
- 6 hours at $110.00 per hour for press checks, as given.
- $284.50 reimbursable expense at cost with no markup, as given.
- Currency USD: a default, not stated by the user.
- Invoice number INV-20260923-001: generated, not supplied.
- Invoice date September 23, 2026: today's date by default, not supplied.
- Due date October 14, 2026: calculated as 21 calendar days from the invoice date, from the instruction "net 21".
- Tax 0.00: the issuer stated these services are not taxed where they invoice from. That statement is reproduced as the issuer's own, and no rule or rate has been asserted here.
- Discount 0.00: none was requested.
- Payment method: none supplied, left as a bracketed placeholder.

Scenario 2:
- Issuer legal name: not available. Left as [Your Registered Company Name] and must be replaced before sending.
- Client Kestrel Analytics Ltd, Manchester, as given. No street address was supplied and none was invented.
- Fixed fee of GBP 4,500.00 for the dashboard build, as given.
- 27 hours at GBP 78.00 per hour, as given.
- 9.25 hours at GBP 95.00 per hour, as given.
- Currency GBP: stated by the user, not a default.
- Discount 7.5 percent: stated by the user, applied to the subtotal before tax.
- Tax 20 percent: the rate the issuer supplied for this invoice. It appears here because the issuer asked for it, not as a statement of what any rule requires.
- Tax base: the discounted amount, not the gross subtotal.
- Rounding: two decimal places, applied at each step, standard half-up rounding.
- Invoice number INV-20260923-002: generated, not supplied.
- Invoice date September 23, 2026: today's date by default.
- Due date October 30, 2026: derived from "last working day of the month after the invoice month", with working days assumed to be Monday through Friday and no public holiday calendar available.
- Company registration number and tax registration number: not supplied, left as bracketed placeholders.
- Bank details: not supplied, left as a bracketed placeholder even though bank transfer was named as the method.

All businesses, people, email addresses, rates and amounts in this document are fictional and are used for illustration only. Any tax rate shown is a rate the requesting user supplied for their own invoice; nothing here states or implies what rate applies to any real transaction.
