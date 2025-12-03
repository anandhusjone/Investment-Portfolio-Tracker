# Investment Portfolio Tracker Dashboard

A simple, single-file HTML + JavaScript application to track investment transactions measured in small units (e.g., milligrams of gold). The dashboard runs entirely client-side, supports CSV import/export, and uses the **FIFO** method to compute realized Profit & Loss (P&L) for sell transactions.

## Features
- **Single-file application** — open `investment_tracker.html` in a modern browser to run.
- **Client-side storage** — load/save transactions from/to a local CSV file (no server or database).
- **FIFO accounting** — Cost of Goods Sold (COGS) and realized P&L for sells are calculated using FIFO.
- **Automatic tax handling** — Buy transactions separate a 3% tax from the total paid amount.
- **Visualization** — time-series chart of price per milligram (Price/mg).
- **Summary metrics** — Total Investment, Total Revenue, Total Realized P&L, Current Balance Weight.

## Getting Started
1. Clone or download this repository.
2. Open `dashboard.html` in any modern web browser.
3. Add transactions using the **Add New Transaction** form or load an existing CSV via **Load Transactions (CSV)**.
4. Export transactions to CSV when you need to save or transfer data.

## Expected CSV File Format

The application expects exactly **7 fields** in the CSV, in this order. These are the raw attributes required for FIFO calculations and reporting.

| Header    | Description                                                                 | Required for Type | Calculation Notes |
|-----------|-----------------------------------------------------------------------------|-------------------|-------------------|
| `Date`    | Date of the transaction (e.g., `DD/MM/YYYY`)                                | All               | Must be a valid date string. |
| `Type`    | Transaction type                                                            | All               | Must be exactly `Buy` or `Sell`. |
| `Spent`   | Base cost of the purchase (pre-tax amount)                                  | Buy               | For Buy: `Total Paid / 1.03`. For Sell: `0.00`. |
| `Received`| Total revenue received from the sale                                        | Sell              | For Sell: amount received. For Buy: `0.00`. |
| `Tax`     | Tax amount (3% of total paid)                                               | Buy               | For Buy: `Total Paid - Spent`. For Sell: `0.00`. |
| `Weight`  | Quantity transacted in **milligrams (mg)**                                  | All               | Must be a positive numeric value. |
| `COGSBasis`| Calculated COGS used for the sale (original cost of sold units via FIFO)   | Sell              | For Sell: computed from prior Buy records using FIFO. For Buy: `0.00`. |

### Notes on CSV usage
- The CSV must contain the header row exactly as shown above.
- All numeric fields use decimal notation (e.g., `194.17`, `0.00`).
- Date strings must follow the `DD/MM/YYYY` format (or another format your browser/locale can reliably parse).

## Example CSV Data
Date,Type,Spent,Received,Tax,Weight,COGSBasis
15/06/2019,Buy,194.17,0.00,5.83,56.70,0.00
17/06/2019,Buy,194.17,0.00,5.83,56.80,0.00
15/11/2020,Sell,0.00,10.19,0.00,2.00,7.05

## How fields are derived when using the UI
When adding a transaction through the dashboard form you enter the **Total Paid** (for Buys) or **Total Received** (for Sells). The application will:
- For **Buy**: compute `Spent = Total Paid / 1.03`, `Tax = Total Paid - Spent`, set `Received = 0.00`, `COGSBasis = 0.00`.
- For **Sell**: set `Spent = 0.00`, `Tax = 0.00`, compute `COGSBasis` by consuming prior Buy records using FIFO to determine the original cost of the sold units; `Received` is set to the amount entered.


