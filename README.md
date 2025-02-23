# Overview Project Finances

This repository tracks all financial transactions for the [Overview](https://github.com/williamcpierce/Overview) project using [hledger](https://hledger.org/), a free and open source plain text accounting system.

For information about the project's funding policies and donation methods, see the [main project repository](https://github.com/williamcpierce/Overview).

## Current Status (as of January 31, 2025)

### Income Statement

Current revenues total 280.00 USD, representing GitHub Sponsors and Patreon donations.

Current expenses total 324.00 USD, representing approved project expenses.

```
                        || 2024Q2  2024Q3   2024Q4  2025Q1    Total
========================++==========================================
 Revenues               ||
------------------------++------------------------------------------
 donation:github        ||      0       0        0  275.00   275.00
 donation:patreon       ||      0       0        0    5.00     5.00
------------------------++------------------------------------------
                        ||      0       0        0  280.00   280.00
========================++==========================================
 Expenses               ||
------------------------++------------------------------------------
 development:membership ||      0       0        0   99.00    99.00
 development:tool:llm   ||  40.00   40.00    60.00   40.00   180.00
 marketing:domain       ||      0       0    45.00       0    45.00
------------------------++------------------------------------------
                        ||  40.00   40.00   105.00  139.00   324.00
========================++==========================================
 Net:                   || -40.00  -40.00  -105.00  141.00   -44.00
```

### Balance Sheet

Current assets total 280.00 USD, representing GitHub Sponsors and Patreon balances pending payout.

Current liabilities total 324.00 USD, representing pending reimbursements for approved expenses.

```
                        || 2024-06-30  2024-09-30  2024-12-31  2025-03-31
========================++================================================
 Assets                 ||
------------------------++------------------------------------------------
 balance:github         ||          0           0           0      275.00
 balance:patreon        ||          0           0           0        5.00
 cash:bank              ||          0           0           0           0
------------------------++------------------------------------------------
                        ||          0           0           0      280.00
========================++================================================
 Liabilities            ||
------------------------++------------------------------------------------
 payable:william_pierce ||      40.00       80.00      185.00      324.00
------------------------++------------------------------------------------
                        ||      40.00       80.00      185.00      324.00
========================++================================================
 Net:                   ||     -40.00      -80.00     -185.00      -44.00
```

## Repository Structure

-   `all.journal` - Main journal file that includes all yearly files
-   `2024.journal` - Transactions from 2024
-   `2025.journal` - Transactions from 2025

## Understanding the Ledger

This project uses double-entry bookkeeping, where each transaction must balance to zero. The main accounts are:

-   `assets:*` - Project bank/platform account balances
-   `expenses:*` - Project expenses by category
-   `liabilities:payable:*` - Pending expense reimbursements
-   `equity:*` - Opening/closing balances between years

### Example Transaction

```
2025-01-17 * Apple | Apple Developer Program
    expenses:development:membership          99.00 USD
    expenses:development:membership           8.54 USD  ; tax:sales
    liabilities:payable:william_pierce     -107.54 USD
```

Each transaction includes:

-   Date, payee, and description (first line)
-   One or more account postings that must sum to zero
-   Optional tags and comments after semicolons
-   Indentation for readability

## Generating Reports

To view the current financial status, install hledger and run:

```bash
hledger -f all.journal bal
```

For a list of all transactions:

```bash
hledger -f all.journal reg
```

## Questions

For questions about project finances, contact:

-   William Pierce
-   Email: will@williampierce.io

## License

This financial data is made available under CC0-1.0. The intent is for this financial information to be public domain.
