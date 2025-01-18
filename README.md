# Overview Project Finances

This repository tracks all financial transactions for the Overview project using [hledger](https://hledger.org/), a free and open source plain text accounting system. For information about the project's funding policies and donation methods, see the [main Overview repository](https://github.com/williamcpierce/Overview).

## Current Status (as of January 18, 2025)

```
                   0  assets:cash:bank
             $107.54  expenses:development:membership
             $140.00  expenses:development:tool:llm
            $-247.54  liabilities:payable:william_pierce
--------------------
                   0
```

Current expenses total $247.54, representing approved project expenses that are pending reimbursement:

-   Apple Developer Program membership ($107.54 with tax)
-   AI development tool subscriptions ($140.00)

## Repository Structure

-   `all.journal` - Main journal file that includes all yearly files
-   `2024.journal` - Transactions from 2024
-   `2025.journal` - Transactions from 2025

## Understanding the Ledger

This project uses double-entry bookkeeping, where each transaction must balance to zero. The main accounts are:

-   `assets:cash:bank` - Project bank account balance
-   `expenses:*` - Project expenses by category
-   `liabilities:payable:*` - Approved expenses pending reimbursement
-   `equity:*` - Opening/closing balances between years

### Example Transaction

```
2025-01-17 * Apple | Apple Developer Program
    expenses:development:membership             $99.00
    expenses:development:membership              $8.54  ; tax:sales
    liabilities:payable:william_pierce        $-107.54
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
