# Banking Transaction & Fraud Analysis

## Project Overview

Analyzed banking transactions using PostgreSQL to identify fraudulent transaction patterns, high-risk transaction types, transaction-value patterns, and balance anomalies.

## Dataset

- 2,097,150 banking transactions
- Dataset includes transaction type, amount, sender and receiver accounts, account balances, fraud indicators, and flagged fraud status.
- Data was imported into PostgreSQL from a CSV file.

## Analysis Performed

The project includes SQL analysis covering:

- Total number of transactions
- Transaction type frequency
- Total transaction value
- Fraudulent vs normal transactions
- Overall fraud percentage
- Fraud count and fraud rate by transaction type
- Average transaction amount for fraudulent vs normal transactions
- Fraud activity by time step
- High-value fraudulent transactions
- Sender and receiver accounts with high fraud counts
- Balance anomalies
- Fraudulent transactions not flagged by the system

## Key Findings

- 2,097,150 transactions were analyzed.
- 2,284 fraudulent transactions were identified.
- Overall fraud rate was **0.11%**.
- Fraud was mainly concentrated in **TRANSFER** and **CASH_OUT** transactions.
- Average fraudulent transaction amount was approximately **₹11.93 lakh**, compared with approximately **₹1.58 lakh** for normal transactions.

## Business Recommendations

- Closely monitor **TRANSFER** and **CASH_OUT** transactions.
- Consider unusually high transaction amounts as an additional fraud-monitoring factor.
- Monitor unusual time-based spikes in fraudulent activity.

## Tools Used

- SQL
- PostgreSQL

## SQL Concepts Used
CREATE TABLE
SELECT and WHERE
Aggregate Functions (COUNT, SUM, AVG)
GROUP BY and ORDER BY
CASE WHEN
FILTER Clause
ROUND()
LIMIT
Conditional Aggregation
Fraud Rate Calculation
Data Quality Validation


## Dataset Source & Preparation

The original dataset was obtained from Kaggle:

[PaySim – Synthetic Financial Datasets For Fraud Detection](https://www.kaggle.com/datasets/ealaxi/paysim1)

The dataset was prepared in Microsoft Excel by renaming column headings for better readability before importing it into PostgreSQL.

The prepared dataset was used for the SQL-based banking transaction and fraud analysis.

**Dataset Format:** CSV

**Preparation Tool:** Microsoft Excel

**Analysis Tool:** PostgreSQL
