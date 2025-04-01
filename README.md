# Overview Project Finances

This repository tracks all financial transactions for the [Overview](https://github.com/williamcpierce/Overview) project using [hledger](https://hledger.org/), a free and open source plain text accounting system.

For information about the project's funding policies and donation methods, see the [main project repository](https://github.com/williamcpierce/Overview).

## Current Status (as of April 1, 2025)

### Income Statement

```
Quarterly Income Statement 2024-04-01..2025-03-31, converted to cost, valued at period ends (USD)
              || 2024Q2  2024Q3   2024Q4  2025Q1    Total
==============++==========================================
 Revenues     ||
--------------++------------------------------------------
 donation     ||      0       0        0  317.50   317.50
   github     ||      0       0        0  281.94   281.94
   patreon    ||      0       0        0   35.56    35.56
--------------++------------------------------------------
              ||      0       0        0  317.50   317.50
==============++==========================================
 Expenses     ||
--------------++------------------------------------------
 development  ||  40.00   40.00    60.00  179.00   319.00
   membership ||      0       0        0   99.00    99.00
   tool:llm   ||  40.00   40.00    60.00   80.00   220.00
 fee          ||      0       0        0    5.96     5.96
   conversion ||      0       0        0    0.14     0.14
   payment    ||      0       0        0    2.72     2.72
   payout     ||      0       0        0    0.25     0.25
   platform   ||      0       0        0    2.85     2.85
 marketing    ||      0       0    45.00   29.00    74.00
   domain     ||      0       0    45.00       0    45.00
   tool:video ||      0       0        0   29.00    29.00
--------------++------------------------------------------
              ||  40.00   40.00   105.00  213.96   398.96
==============++==========================================
 Net:         || -40.00  -40.00  -105.00  103.54   -81.46
```

### Balance Sheet

```
Quarterly Balance Sheet 2024-06-30..2025-03-31, converted to cost, valued at period ends (USD)
                        || 2024-06-30  2024-09-30  2024-12-31  2025-03-31
========================++================================================
 Assets                 ||
------------------------++------------------------------------------------
 balance                ||          0           0           0      311.54
   bank                 ||          0           0           0      311.54
   github               ||          0           0           0           0
   patreon              ||          0           0           0           0
------------------------++------------------------------------------------
                        ||          0           0           0      311.54
========================++================================================
 Liabilities            ||
------------------------++------------------------------------------------
 payable:william_pierce ||      40.00       80.00      185.00      393.00
------------------------++------------------------------------------------
                        ||      40.00       80.00      185.00      393.00
========================++================================================
 Net:                   ||     -40.00      -80.00     -185.00      -81.46
```

## Understanding the Ledger

This project uses double-entry bookkeeping, where each transaction must balance to zero. The main accounts are:

-   `assets:*` - Project bank/platform account balances
-   `expenses:*` - Project expenses by category
-   `liabilities:payable:*` - Pending expense reimbursements
-   `equity:*` - Opening/closing balances between years

### Example Transaction

```
2025-03-31 * Patreon | Donations
    assets:balance:patreon                 17.40 USD
    expenses:fee:payment                    1.37 USD
    expenses:fee:platform                   1.65 USD
    expenses:fee:conversion                 0.14 USD
    income:donation:patreon               -15.00 USD
    income:donation:patreon    -8.00 CAD @@ 5.56 USD
```

Each transaction includes:

-   Date, payee, and description (first line)
-   One or more account postings that must sum to zero
-   Optional tags and comments after semicolons
-   Indentation for readability
-   Coversions to USD using `@@`, if applicable

## Generating Reports

To view the current financial status, install hledger and run:

```bash
hledger -f all.journal bal
```

For a list of all transactions:

```bash
hledger -f all.journal reg
```

To generate the above income statement and balance sheet:

```bash
hledger -f all.journal is -p "from 2024-04" -TEVBQt not:payee:equity --layout=bare --drop=1
hledger -f all.journal bs -p "from 2024-04 to today" -TEVBQt not:payee:equity --layout=bare --drop=1
```

## Repository Structure

-   `all.journal` - Main journal file that includes all yearly files
-   `2024.journal` - Transactions from 2024
-   `2025.journal` - Transactions from 2025

## Questions

For questions about project finances, contact:

-   William Pierce
-   Email: will@williampierce.io

## License

This financial data is made available under CC0-1.0. The intent is for this financial information to be public domain.
