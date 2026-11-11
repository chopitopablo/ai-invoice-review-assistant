# Example invoices

All invoices here are **fictional**, created to demonstrate the kind of issue each prompt catches. No real or confidential company data is included. Supplier and recipient names, tax IDs and amounts are invented.

| File | What it demonstrates |
|---|---|
| `01_missing_supplier_vat.pdf` | Supplier tax ID is missing. The assistant flags it and drafts a request to the supplier. |
| `02_miscalculated_vat.pdf` | VAT is declared as 231.00 when 21% of 1,000.00 is 210.00. The mathematical check catches the mismatch. |
| `03_foreign_language.pdf` | Invoice fully in Italian, data correct. The assistant extracts it and can prepare the supplier email in English or Spanish for internal control. |
| `04_missing_date.pdf` | Invoice date is missing. Flagged as a critical field for posting. |
| `05_missing_number.pdf` | Invoice number is missing. Flagged as a critical field for posting. |
| `06_wrong_entity.pdf` | Invoice is addressed to a different entity than the active session. Raises the critical entity alert. |

To try one: set the variables at the top of a prompt, paste the prompt into your LLM, and attach one of these files.
