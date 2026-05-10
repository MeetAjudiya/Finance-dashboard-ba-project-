# Process Flow: Financial Expense Reporting

This document outlines the "As-Is" (current) process compared to the "To-Be" (proposed) automated process.

## As-Is Process (Manual)
```mermaid
graph TD;
    A[Department Head Submits Expense] --> B[Finance Analyst Collects Receipts]
    B --> C[Manual Entry into Excel Master Sheet]
    C --> D{Is it End of Month?}
    D -- Yes --> E[Consolidate Data]
    D -- No --> B
    E --> F[Generate PDF Report]
    F --> G[Email Report to CFO]
```

## To-Be Process (Automated Dashboard)
```mermaid
graph TD;
    A[Department Head Submits Expense via ERP] --> B[Automated API Data Extraction]
    B --> C[(Data Warehouse)]
    C --> D[BI Tool / Dashboard Processes Data]
    D --> E{Threshold Alert?}
    E -- Budget > 90% --> F[Automated Email Alert to Dept Head & CFO]
    E -- Normal --> G[Dashboard Updates in Real-Time]
    F --> G
    G --> H[CFO / FP&A View Live Dashboard]
```
