---
name: ai-invoice-generator
description: "Turns raw, unstructured billing information - pasted text, a list of services, a quick note about what a client owes - into a complete professional invoice in clean markdown or plain text, ready to send or convert to PDF, handling single and multi line-item invoices, applying tax and discount logic, and filling in every standard invoice field even from partial input. Use when someone gives a client name plus work done, an hourly rate and hours, a flat project fee, a note like \"bill Acme for the March consulting, 10 hours at 150\", or an existing invoice to reformat, and says \"create an invoice\", \"invoice template\" or \"bill this client\"."
---

# AI Invoice Generator

## What this skill does

This skill turns raw, unstructured billing information (pasted text, a list of services, a quick note about what a client owes) into a complete, professional invoice in clean markdown or plain text that is ready to send or convert to PDF. It handles single line item invoices and multi line item invoices, applies tax and discount logic when mentioned, and fills in every standard invoice field even when the user only gives a fraction of the needed information.

## When to use this skill

Use this skill whenever the user provides any of the following and wants a formatted invoice back:
- A client name plus a list of work done or products sold
- An hourly rate and hours worked
- A flat project fee
- A rough note like "bill Acme for the March consulting, 10 hours at 150"
- An existing invoice they want reformatted or corrected

## Step by step process

1. Extract the core facts from the user's raw input: seller (issuer) name, client (bill to) name, line items with quantity, unit price, and description, currency, due date, and any tax or discount rate mentioned.
2. If the seller's business name is not given, use a placeholder like "[Your Business Name]" and flag it once at the top of the output as something the user should replace, rather than inventing a name.
3. If the client's address or contact details are missing, omit those fields rather than guessing. Never fabricate contact information.
4. Assign an invoice number. If the user supplies one, use it. If not, generate a sensible one using the pattern INV-YYYYMMDD-001 based on the invoice date, or ask the user in one line if they have a numbering convention already in use. Default to generating one so the flow is not blocked.
5. Set the invoice date to today unless the user specifies otherwise.
6. Set the due date using the user's instruction if given (for example "net 30", "due in 15 days", "due on the 1st"). If nothing is specified, default to net 30 from the invoice date and state this default explicitly.
7. Calculate line item totals (quantity times unit price), subtotal, tax amount if a tax rate is given, discount amount if a discount is given, and the final total due. Show the math clearly so the client can verify it.
8. If currency is not stated, default to USD and note the assumption.
9. Add standard payment terms language and a short "how to pay" line only if the user specified a payment method (bank transfer, PayPal, check, etc). If no method was given, leave a placeholder field instead of inventing bank details.

## Output structure

Produce the invoice with these sections in order:
1. Header: business name, invoice title, invoice number, invoice date, due date
2. Bill To: client name and any details provided
3. Line items table: description, quantity, unit price, line total
4. Totals block: subtotal, discount (if any), tax (if any), total due
5. Payment terms and instructions
6. Optional notes or thank you line

## Tone and formatting guidance

Keep the language plain, professional, and free of filler. No marketing language, no exclamation points, no emojis. Use a markdown table for line items when the output supports it, otherwise use clean aligned plain text columns. Always state any default or assumption made (currency, due date, invoice number) directly under the header so nothing is hidden from the user. When information is genuinely missing and cannot be defaulted safely (legal business name, tax ID, bank details), leave an explicit bracketed placeholder rather than guessing, since invoices carry legal and financial weight.

---

Free edition from [KissMySkills](https://kissmyskills.com), released under the MIT license as part of [free-claude-skills](https://github.com/Kreal-51/free-claude-skills). More skills for this role: https://kissmyskills.com/collections/ai-document-generators
