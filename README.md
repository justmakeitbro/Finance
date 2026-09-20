# From a Raw General Ledger to the Full Set of Financial Statements

A step-by-step, AI-assisted walkthrough that turns a raw general ledger into all four
core financial statements — and proves they are internally consistent.

## The challenge

One Excel workbook (`Finacial_Data.xlsx`) contains a company's raw bookkeeping data for
2018–2020. It does **not** contain the financial statements. It only contains the ingredients:

| Sheet | Role |
|---|---|
| `GL` | The general ledger: ~28,000 bookkeeping lines. The only sheet with numbers. |
| `Chart of Accounts` | Maps each account key to its name and statement classification. |
| `CashFlow_St` / `SoCE_St` | Templates defining the layout of two of the statements. |
| `Territory` / `Calendar` | Dimensions for regional and quarterly analysis. |

The job: assemble the statements from scratch and **prove every statement reconciles with
every other statement**.

## What gets built

| Statement | Question it answers |
|---|---|
| **Income Statement (P&L)** | How much profit did the company make? |
| **Balance Sheet** | What does it own and owe at year-end? |
| **Statement of Changes in Equity** | How did owners' equity move? |
| **Cash Flow Statement** | Where did actual cash come from and go? (built twice: direct and indirect method) |

## The reconciliation scorecard

Six independent cross-checks, all of which must come out to exactly zero:

1. Balance Sheet balances (A − L − E = 0)
2. P&L net profit = movement in Retained Earnings
3. Cash Flow direct vs indirect method agree
4. Cash Flow = Balance Sheet cash movement
5. SoCE closing equity = Balance Sheet equity
6. Ledger identity (A = L + E + P&L + Adjusting)

Every check passes for all three years. Any non-zero gap is treated as a bug until proven
otherwise.

## Key lessons

- **The sign convention is everything.** Amounts are stored in natural statement signs
  (assets/revenue positive when they increase, expenses negative), which makes every
  transaction obey a conservation law: `Assets = Liabilities + Equity + Revenue + Expenses`.
- **Reconciliations drive the logic.** The direct and indirect cash flow methods, the SoCE,
  and the Balance Sheet were each validated against independent sources — mistakes were
  caught by the checks, not by inspection.
- **One ledger, many statements.** Every statement is a pure re-arrangement of the same
  raw data, which is why they can be proven consistent.


## Next ideas

- Full statements per territory or per quarter (using the `Calendar` sheet).
- Reproduce the workbook's `CashFlow_St` template literally, including its `ValueType` rules.
- Export all statements to a multi-sheet Excel file with `pd.ExcelWriter`.

## Credits

Built with AI assistance — the notebook includes the mistakes made along the way and how
the reconciliation checks caught them.
