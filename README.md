# Overview Project Finances

This repository tracks all financial transactions for the [Overview](https://github.com/williamcpierce/Overview) project using [hledger](https://hledger.org/), a free and open source plain text accounting system.

For information about the project's funding policies and donation methods, see the [main project repository](https://github.com/williamcpierce/Overview).

## Current Status (as of April 20, 2025)

### Forecast

`hledger -f budget.journal is --forecast "(expenses|income)" -YVBETt  --layout=bare  --drop=1 -p "2024 to 2028"`

```
Yearly Income Statement 2024-01-01..2027-12-31, converted to cost, valued at period ends

              || Commodity     2024    2025    2026    2027    Total
==============++=====================================================
 Revenues     ||
--------------++-----------------------------------------------------
 donation     || USD              0  625.50  384.00  384.00  1393.50
   github     || USD              0  346.94   60.00   60.00   466.94
   patreon    || USD              0  278.56  324.00  324.00   926.56
--------------++-----------------------------------------------------
              || USD              0  625.50  384.00  384.00  1393.50
==============++=====================================================
 Expenses     ||
--------------++-----------------------------------------------------
 development  || USD         140.00  183.84   99.00   99.00   521.84
   membership || USD              0   99.00   99.00   99.00   297.00
   tool:llm   || USD         140.00   84.84       0       0   224.84
 fee          || USD              0   50.67   59.53   59.53   169.73
   conversion || USD              0    3.29    4.20    4.20    11.69
   payment    || USD              0   24.59   29.16   29.16    82.91
   payout     || USD              0    0.50    0.25    0.25     1.00
   platform   || USD              0   22.29   25.92   25.92    74.13
 marketing    || USD          45.00   74.00   45.00   45.00   209.00
   domain     || USD          45.00   45.00   45.00   45.00   180.00
   tool:video || USD              0   29.00       0       0    29.00
 tax:income   || USD              0  208.32  127.92  127.92   464.16
--------------++-----------------------------------------------------
              || USD         185.00  516.83  331.45  331.45  1364.73
==============++=====================================================
 Net:         || USD        -185.00  108.67   52.55   52.55    28.77
```

### Income Statement

`hledger -f all.journal is -p "from 2024-04 to today" -TEVBQt not:payee:equity --layout=bare --drop=1`

```
Quarterly Income Statement 2024-04-01..2025-06-30, converted to cost, valued at period ends

              || Commodity  2024Q2  2024Q3   2024Q4  2025Q1  2025Q2    Total
==============++=============================================================
 Revenues     ||
--------------++-------------------------------------------------------------
 donation     || USD             0       0        0  317.50       0   317.50
   github     || USD             0       0        0  281.94       0   281.94
   patreon    || USD             0       0        0   35.56       0    35.56
--------------++-------------------------------------------------------------
              || USD             0       0        0  317.50       0   317.50
==============++=============================================================
 Expenses     ||
--------------++-------------------------------------------------------------
 development  || USD         40.00   40.00    60.00  179.00    4.84   323.84
   membership || USD             0       0        0   99.00       0    99.00
   tool:llm   || USD         40.00   40.00    60.00   80.00    4.84   224.84
 fee          || USD             0       0        0    5.96       0     5.96
   conversion || USD             0       0        0    0.14       0     0.14
   payment    || USD             0       0        0    2.72       0     2.72
   payout     || USD             0       0        0    0.25       0     0.25
   platform   || USD             0       0        0    2.85       0     2.85
 marketing    || USD             0       0    45.00   29.00       0    74.00
   domain     || USD             0       0    45.00       0       0    45.00
   tool:video || USD             0       0        0   29.00       0    29.00
 tax:income   || USD             0       0        0  105.72       0   105.72
--------------++-------------------------------------------------------------
              || USD         40.00   40.00   105.00  319.68    4.84   509.52
==============++=============================================================
 Net:         || USD        -40.00  -40.00  -105.00   -2.18   -4.84  -192.02
```

### Balance Sheet

`hledger -f all.journal bs -p "from 2024-04 to today" -TEVBQt not:payee:equity --layout=bare --drop=1`

```
Quarterly Balance Sheet 2024-06-30..2025-06-30, converted to cost, valued at period ends

                        || Commodity  2024-06-30  2024-09-30  2024-12-31  2025-03-31  2025-06-30
========================++=======================================================================
 Assets                 ||
------------------------++-----------------------------------------------------------------------
 balance                ||                     0           0           0           0           0
   github               ||                     0           0           0           0           0
   patreon              ||                     0           0           0           0           0
 cash:bank              || USD                 0           0           0      281.94           0
------------------------++-----------------------------------------------------------------------
                        || USD                 0           0           0      281.94           0
========================++=======================================================================
 Liabilities            ||
------------------------++-----------------------------------------------------------------------
 payable:william_pierce || USD             40.00       80.00      185.00      498.72      192.02
------------------------++-----------------------------------------------------------------------
                        || USD             40.00       80.00      185.00      498.72      192.02
========================++=======================================================================
 Net:                   || USD            -40.00      -80.00     -185.00     -216.78     -192.02
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
