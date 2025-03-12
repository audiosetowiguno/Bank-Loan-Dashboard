# Bank Loan Validation Data - SQL Queries
Data validation using SQL aims to ensure that the values displayed on the dashboard are accurate and correct.

## KPI Queries
```sql
SELECT * FROM financial_loan;
```

## Total Loan Applications
```sql
SELECT COUNT(id) AS Total_Loan_Applicant FROM financial_loan;
```

## MTD Total Loan Application
```sql
SELECT COUNT(id) AS MTD_Total_Loan_Applicant FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```

```sql
SELECT COUNT(id) AS PMTD_Total_Loan_Applicant FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```

## Total Loan Amount
```sql
SELECT SUM(loan_amount) AS Total_Loan_Amount FROM financial_loan;
```

```sql
SELECT SUM(loan_amount) AS MTD_Loan_Amount FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```

```sql
SELECT SUM(loan_amount) AS PMTD_Loan_Amount FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```

## Total Loan Received
```sql
SELECT SUM(total_payment) AS Total_Loan_Received FROM financial_loan;
```

```sql
SELECT SUM(total_payment) AS MTD_Total_Loan_Received FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```

```sql
SELECT SUM(total_payment) AS PMTD_Total_Loan_Received FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```

## Average Interest Rate
```sql
SELECT AVG(int_rate) * 100 AS AVG_interest_rate FROM financial_loan;
```

```sql
SELECT ROUND(AVG(int_rate) * 100, 4) AS MTD_Average_Interest FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```

```sql
SELECT ROUND(AVG(int_rate) * 100, 4) AS PMTD_Average_Interest FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```

## Average DTI
```sql
SELECT ROUND(AVG(dti) * 100, 4) AS Average_DTI FROM financial_loan;
```

```sql
SELECT ROUND(AVG(dti) * 100, 4) AS MTD_Average_DTI FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```

```sql
SELECT ROUND(AVG(dti) * 100, 4) AS PMTD_Average_DTI FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```

## Good Loan Analysis
```sql
SELECT (COUNT(CASE WHEN loan_status IN ('Fully Paid', 'Current') THEN id END) * 100) / COUNT(id) AS Percentage_Good_Loan FROM financial_loan;
```

```sql
SELECT COUNT(id) AS Good_Loan_Application FROM financial_loan WHERE loan_status IN ('Fully Paid', 'Current');
```

```sql
SELECT SUM(loan_amount) AS GoodLoan_FundedAmount FROM financial_loan WHERE loan_status IN ('Fully Paid', 'Current');
```

```sql
SELECT SUM(total_payment) AS GoodLoan_Received FROM financial_loan WHERE loan_status IN ('Fully Paid', 'Current');
```

## Bad Loan Analysis
```sql
SELECT (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100) / COUNT(id) AS Percentage_BadLoan FROM financial_loan;
```

```sql
SELECT COUNT(id) AS Bad_Loan_Application FROM financial_loan WHERE loan_status = 'Charged Off';
```

```sql
SELECT SUM(loan_amount) AS BadLoan_FundedAmount FROM financial_loan WHERE loan_status = 'Charged Off';
```

```sql
SELECT SUM(total_payment) AS BadLoan_Received FROM financial_loan WHERE loan_status = 'Charged Off';
```

## Loan Status Breakdown
```sql
SELECT loan_status, COUNT(id) AS Total_Applications, SUM(total_payment) AS Total_Amount_Received, SUM(loan_amount) AS Total_Funded_Amount, AVG(int_rate * 100) AS Average_Interest_Rate, AVG(dti * 100) AS Average_DTI FROM financial_loan GROUP BY loan_status;
```

## Monthly Loan Summary
```sql
SELECT MONTH(issue_date) AS Month_Number, DATENAME(MONTH, issue_date) AS Month_Name, COUNT(id) AS Total_Applications, SUM(total_payment) AS Total_Amount_Received, SUM(loan_amount) AS Total_Funded_Amount FROM financial_loan GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date) ORDER BY MONTH(issue_date);
```

## Loan Applications by State
```sql
SELECT address_state AS State, COUNT(id) AS Total_Applications, SUM(total_payment) AS Total_Amount_Received, SUM(loan_amount) AS Total_Funded_Amount FROM financial_loan GROUP BY address_state;
```

## Loan Applications by Term
```sql
SELECT term AS Term, COUNT(id) AS Total_Loan_Applications, SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received FROM financial_loan GROUP BY term ORDER BY term;
```

## Loan Applications by Employment Length
```sql
SELECT emp_length AS Employee_Length, COUNT(id) AS Total_Loan_Applications, SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received FROM financial_loan GROUP BY emp_length;
```

## Loan Applications by Purpose
```sql
SELECT purpose AS Purpose, COUNT(id) AS Total_Loan_Applications, SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received FROM financial_loan GROUP BY purpose ORDER BY purpose;
```

## Loan Applications by Home Ownership
```sql
SELECT home_ownership AS Home_Ownership, COUNT(id) AS Total_Loan_Applications, SUM(loan_amount) AS Total_Funded_Amount, SUM(total_payment) AS Total_Amount_Received FROM financial_loan GROUP BY home_ownership ORDER BY home_ownership;
```

---



