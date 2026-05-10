# Data Dictionary

This document defines the structure and metrics of the dataset used for the Financial Dashboard.

## Source Dataset Schema: `transactions`

| Field Name | Data Type | Description | Example |
|---|---|---|---|
| `transaction_id` | String | Unique identifier for the expense | `TRX-9821` |
| `date` | Date | Date the expense was incurred | `2026-05-10` |
| `department` | String | Department responsible for the spend | `Marketing` |
| `category` | String | Type of expense | `Software Subscriptions` |
| `amount` | Decimal | Amount spent in USD | `1500.00` |
| `vendor` | String | Name of the vendor | `Salesforce` |
| `status` | String | Current approval status | `Approved` |

## Calculated Key Performance Indicators (KPIs)

1. **Total Spend**: `SUM(amount)` where status = 'Approved'.
2. **Total Budget**: Static assigned value per department for the fiscal year.
3. **Remaining Budget**: `Total Budget - Total Spend`.
4. **Burn Rate (%)**: `(Total Spend / Total Budget) * 100`.
5. **Top Expense Category**: Category with the highest aggregated `amount`.
