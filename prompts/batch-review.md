# Invoice Batch Review Prompt

A first-pass control prompt that scans a batch of Accounts Payable invoices and flags anomalies before posting. Paste it into your LLM of choice together with an AP batch report.

---

## Variables to set before use

- `[HIGH_VALUE_THRESHOLD]` = amount above which an invoice without a purchase order is flagged (default: 10,000)
- `[CURRENCY]` = expected currency (default: EUR)
- `[AGING_DAYS]` = how many days old an unprocessed invoice must be to count as aged (default: 90)

---

## Prompt

Act as a Senior Accounts Payable accountant specialized in reviewing AP batch reports. I will share an Accounts Payable invoice report. Analyze the full document and return a structured report with the following anomaly categories.

### 1. DUPLICATE INVOICES
Detect any invoice that appears more than once (same invoice number and supplier). Indicate on which page/batch each appears and whether it is already processed (Y) or pending.

| Supplier | Invoice No. | Gross Amount | Batch / Status | Action |
|---|---|---|---|---|

### 2. DATE ANOMALIES
Detect invoices where the invoice date is LATER than the due date. This is a critical error.

| Supplier | Invoice No. | Invoice Date | Due Date | Days difference |
|---|---|---|---|---|

### 3. INVOICES WITH WRONG OR INCONSISTENT STATUS
Detect invoices marked as DUPLICATE but with differing amounts, marked with status "E" (error), or with contradictory statuses (e.g. DUPLICATE and posted at the same time).

### 4. INVOICES WITH NO CURRENCY OR NO DEFINED STATUS
Detect invoices where the currency or status field is blank, a dash "-", or empty.

### 5. HIGH AMOUNTS WITHOUT A PURCHASE ORDER
List invoices with no purchase order, sorted from highest to lowest amount. Flag any exceeding [HIGH_VALUE_THRESHOLD] [CURRENCY] (or the threshold the user specifies).

| Supplier | Invoice No. | Gross Amount | Due Date |
|---|---|---|---|

### 6. AGED PENDING INVOICES
Detect invoices with an invoice date more than [AGING_DAYS] days before the report date that are still unprocessed.

### 7. OTHER ANOMALIES DETECTED
Any other relevant inconsistency: corrupt characters, negative amounts that are not declared credit notes, currencies other than [CURRENCY] without justification, etc.

---

### FORMAT RULES
- Use tables for structured data.
- Use CAPITALS for critical alerts.
- No emojis.
- If a category has no issues, write "No issues detected." and continue.
- At the end, include an EXECUTIVE SUMMARY with the total number of anomalies per category and the total amount at risk (sum of invoices with an anomaly).

**Purpose:** automate the audit and quality control of AP batch reports, ensuring early detection of errors before final posting or batch close.
