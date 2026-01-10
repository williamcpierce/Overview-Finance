# Overview Project Finances

This repository tracks all financial transactions for the [Overview](https://github.com/williamcpierce/Overview) project using [hledger](https://hledger.org/), a free and open source plain text accounting system.

For information about the project's funding policies and donation methods, see the [main project repository](https://github.com/williamcpierce/Overview).

## Current Status (as of January 9, 2026)

### Forecast

`hledger -f budget.journal is --forecast "(expenses|income)" -YVBETt --layout=bare --drop=1 -p "2024 to 2029"`

```
Yearly Income Statement 2024-01-01..2028-12-31, converted to cost, valued at period ends

              || Commodity     2024    2025     2026     2027     2028    Total
==============++================================================================
 Revenues     ||
--------------++----------------------------------------------------------------
 donation     || USD              0  486.91    60.00    60.00    60.00   666.91
   github     || USD              0  316.94        0        0        0   316.94
   patreon    || USD              0  169.97    60.00    60.00    60.00   349.97
--------------++----------------------------------------------------------------
              || USD              0  486.91    60.00    60.00    60.00   666.91
==============++================================================================
 Expenses     ||
--------------++----------------------------------------------------------------
 development  || USD         140.00  223.84    99.00    99.00    99.00   660.84
   membership || USD              0   99.00    99.00    99.00    99.00   396.00
   tool:llm   || USD         140.00  124.84        0        0        0   264.84
 fee          || USD              0   27.04     5.05     5.05     5.05    42.19
   conversion || USD              0    1.67        0        0        0     1.67
   payment    || USD              0   11.48        0        0        0    11.48
   payout     || USD              0    0.25     0.25     0.25     0.25     1.00
   platform   || USD              0   13.64     4.80     4.80     4.80    28.04
 marketing    || USD          45.00   74.00    45.00    45.00    45.00   254.00
   domain     || USD          45.00   45.00    45.00    45.00    45.00   225.00
   tool:video || USD              0   29.00        0        0        0    29.00
 tax:income   || USD              0  162.14    20.04    20.04    20.04   222.26
--------------++----------------------------------------------------------------
              || USD         185.00  487.02   169.09   169.09   169.09  1179.29
==============++================================================================
 Net:         || USD        -185.00   -0.11  -109.09  -109.09  -109.09  -512.38
```

### Income Statement

`hledger -f all.journal is -p "from 2024-04 to 2026" -TEVBQt not:payee:equity --layout=bare --drop=1`

```
Quarterly Income Statement 2024-04-01..2025-12-31, converted to cost, valued at period ends

              || Commodity  2024Q2  2024Q3   2024Q4  2025Q1  2025Q2  2025Q3  2025Q4    Total
==============++=============================================================================
 Revenues     ||
--------------++-----------------------------------------------------------------------------
 donation     || USD             0       0        0  317.50  105.14   49.27   15.00   486.91
   github     || USD             0       0        0  281.94   35.00       0       0   316.94
   patreon    || USD             0       0        0   35.56   70.14   49.27   15.00   169.97
--------------++-----------------------------------------------------------------------------
              || USD             0       0        0  317.50  105.14   49.27   15.00   486.91
==============++=============================================================================
 Expenses     ||
--------------++-----------------------------------------------------------------------------
 development  || USD         40.00   40.00    60.00  179.00   44.84       0       0   363.84
   membership || USD             0       0        0   99.00       0       0       0    99.00
   tool:llm   || USD         40.00   40.00    60.00   80.00   44.84       0       0   264.84
 fee          || USD             0       0        0    5.96   11.95    7.80    1.33    27.04
   conversion || USD             0       0        0    0.14    0.90    0.63       0     1.67
   payment    || USD             0       0        0    2.72    5.42    3.21    0.13    11.48
   payout     || USD             0       0        0    0.25       0       0       0     0.25
   platform   || USD             0       0        0    2.85    5.63    3.96    1.20    13.64
 marketing    || USD             0       0    45.00   29.00       0       0   45.00   119.00
   domain     || USD             0       0    45.00       0       0       0   45.00    90.00
   tool:video || USD             0       0        0   29.00       0       0       0    29.00
 tax:income   || USD             0       0        0  105.72   34.99   16.42    5.01   162.14
--------------++-----------------------------------------------------------------------------
              || USD         40.00   40.00   105.00  319.68   91.78   24.22   51.34   672.02
==============++=============================================================================
 Net:         || USD        -40.00  -40.00  -105.00   -2.18   13.36   25.05  -36.34  -185.11
```

### Balance Sheet

`hledger -f all.journal bs -p "from 2024-04 to 2026" -TEVBQt not:payee:equity --layout=bare --drop=1`

```
Quarterly Balance Sheet 2024-06-30..2025-12-31, converted to cost, valued at period ends

                        || Commodity  2024-06-30  2024-09-30  2024-12-31  2025-03-31  2025-06-30  2025-09-30  2025-12-31
========================++===============================================================================================
 Assets                 ||
------------------------++-----------------------------------------------------------------------------------------------
 balance                || USD                 0           0           0           0       58.19       99.66      113.33
   github               ||                     0           0           0           0           0           0           0
   patreon              || USD                 0           0           0           0       58.19       99.66      113.33
 cash:bank              || USD                 0           0           0      281.94       35.00           0           0
------------------------++-----------------------------------------------------------------------------------------------
                        || USD                 0           0           0      281.94       93.19       99.66      113.33
========================++===============================================================================================
 Liabilities            ||
------------------------++-----------------------------------------------------------------------------------------------
 payable:william_pierce || USD             40.00       80.00      185.00      498.72      267.01      248.43      298.44
------------------------++-----------------------------------------------------------------------------------------------
                        || USD             40.00       80.00      185.00      498.72      267.01      248.43      298.44
========================++===============================================================================================
 Net:                   || USD            -40.00      -80.00     -185.00     -216.78     -173.82     -148.77     -185.11
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

## Repository Structure

-   `all.journal` - Main journal file that includes all yearly files
-   `2024.journal` - Transactions from 2024
-   `2025.journal` - Transactions from 2025
-   `2026.journal` - Transactions from 2025

## Questions

For questions about project finances, contact:

-   William Pierce
-   Email: will@williampierce.io

## License

This financial data is made available under CC0-1.0. The intent is for this financial information to be public domain.
