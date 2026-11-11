**AI Invoice Review Assistant
**
A prompt-based tool that assists Accounts Payable teams in reviewing supplier invoices. It extracts key data, runs a sequential mathematical audit, flags inconsistencies, and drafts supplier emails when information is missing or incorrect. Built around a human-in-the-loop approach: every output is a draft for a person to review, never an automated action.

The problem

Manual invoice review is repetitive and error-prone. The same issues recur daily: missing tax IDs, miscalculated VAT, invoices in unfamiliar languages, missing dates or numbers, and documents posted to the wrong entity. Catching these by hand is slow and inconsistent, especially at volume.

What it does
Extracts invoice data into a clean, structured format ready for review
Runs a sequential check: line items, subtotal, VAT, withholding, total
Flags critical issues (missing tax ID, wrong entity, invalid document, math errors)
Drafts a supplier email, in the appropriate language, when something needs correcting
Leaves the final decision to a human. It does not post or send anything on its own
How it works

The tool is built from two prompts that work as modules of the same workflow:

1. Batch Review. A first pass over a batch of invoices to detect anomalies early: duplicates, date inconsistencies, invalid statuses, high-value items without a purchase order, and aged open items. Useful for quality control before posting.

2. Deep Analysis and Supplier Communication. A detailed audit of a single invoice. It runs in two phases, an initialization phase that sets the mandatory context, and a processing phase that extracts the data, verifies the maths in cascade (line items, subtotal, VAT, withholding, total), raises alerts, and conditionally drafts a correction email to the supplier in the right language.

An anti-fabrication rule anchors every output: if a value is not visible in the document, it is marked as “not found” rather than guessed. In Accounts Payable, a fabricated value is a serious error; a blank is not.

Repository structure
/prompts — the two structured prompts (batch review and deep analysis)
/examples — sample (fictional) invoices demonstrating each use case: missing VAT, miscalculated VAT, foreign language, missing date, missing number, wrong entity
What I learned

Building this taught me how to structure complex, rule-based prompts for a real financial workflow: designing strict output formats, sequencing validation logic, handling multilingual communication, and keeping a human in control of every decision. It combines an understanding of the Accounts Payable process with hands-on experimentation in applied AI.

Note

All example invoices are fictional. This project is a personal initiative and contains no real or confidential company data.
