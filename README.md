Investment Portfolio Tracker Dashboard

This is a simple, single-file HTML and JavaScript application designed to help users track transactions for investments, particularly those involving small units of measure (e.g., milligrams of a commodity).

The dashboard uses the First-In, First-Out (FIFO) accounting method to accurately calculate the realized Profit & Loss (P&L) when assets are sold. All data is processed client-side and can be loaded from or saved to a local CSV file.

Features

Single-File Application: Easy to run—just open dashboard.html in your browser.

Client-Side Data: All data management is done locally via CSV files (no database required).

FIFO Calculation: Automatically calculates the Cost of Goods Sold (COGS) and Realized P&L for "Sell" transactions using the FIFO method.

Tax Handling: Automatically separates the 3% tax from the total paid amount for "Buy" transactions.

Visualization: Displays a time-series chart of price per milligram (Price/mg).

Summary Metrics: Provides key figures like Total Investment, Total Revenue, Total Realized P&L, and Current Balance Weight.

Getting Started

Clone or download this repository.

Open the dashboard.html file in any modern web browser.

Start by adding transactions using the "Add New Transaction" form or load existing data using the "Load Transactions (CSV)" button.

Expected CSV File Format

The application strictly expects 7 fields in the CSV file, in the exact order listed below. These fields represent the raw, fundamental data required for the FIFO calculation and reporting.

Header

Description

Required for Type

Calculation Notes

Date

The date the transaction occurred (e.g., DD/MM/YYYY).

All

Must be a valid date string.

Type

The nature of the transaction.

All

Must be exactly Buy or Sell.

Spent

The Base Cost of the purchase (pre-tax amount).

Buy

For Buy, this is Total Paid / 1.03. For Sell, it must be 0.00.

Received

The total revenue generated from the sale.

Sell

For Sell, this is the amount received. For Buy, it must be 0.00.

Tax

The tax amount paid (3% of the total amount).

Buy

For Buy, this is Total Paid - Spent. For Sell, it must be 0.00.

Weight

The quantity of the asset transacted, in milligrams (mg).

All

Must be a positive numeric value.

COGSBasis

The calculated Cost of Goods Sold (COGS) used for the sale.

Sell

For Sell, this is the original cost of the units being sold (calculated via FIFO). For Buy, it must be 0.00.

Example CSV Data

Date,Type,Spent,Received,Tax,Weight,COGSBasis
15/06/2019,Buy,194.17,0.00,5.83,56.70,0.00
17/06/2019,Buy,194.17,0.00,5.83,56.80,0.00
15/11/2020,Sell,0.00,10.19,0.00,2.00,7.05


Note: When using the dashboard's "Add New Transaction" form, you enter the Total Paid/Received Amount. The application automatically calculates and populates the Spent, Tax, Received, and COGSBasis fields before saving to the CSV format.
