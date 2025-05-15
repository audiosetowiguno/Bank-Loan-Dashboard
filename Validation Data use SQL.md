# Bank Loan Validation Data - SQL Queries
Data validation using SQL aims to ensure that the values displayed on the dashboard are accurate and correct. I use SQL Database Management to validation my own dashboard.

## Total Loan Applications
```sql
SELECT COUNT(id) AS Total_Loan_Applicant FROM financial_loan;
```
| Total_Loan_Applicant |
| -------------------- |
| 38576                |

### MTD (Month-To-Date) and PMTD (Previous-Month-To-Date) Total Loan Application
```sql
SELECT COUNT(id)
  AS MTD_Total_Loan_Applicant
FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```
| MTD_Total_Loan_Applicant |
| ------------------------ |
| 4314 |

```sql
SELECT
  COUNT(id) AS PMTD_Total_Loan_Applicant
FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```
| PMTD_Total_Loan_Applicant |
| ------------------------- |
| 4035 |

## Total Loan Amount ($)
```sql
SELECT
  SUM(loan_amount) AS Total_Loan_Amount
FROM financial_loan;
```
| Total_Loan_Amount |
| ----------------- |
| 435757075 |

### MTD (Month-To-Date) and PMTD (Previous-Month-To-Date) Loan Amount ($)
```sql
SELECT
  SUM(loan_amount) AS MTD_Loan_Amount
FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```
| MTD_Loan_Amount |
| ----------------- |
| 53981425 |

```sql
SELECT
  SUM(loan_amount)AS PMTD_Loan_Amount
FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```
| PMTD_Loan_Amount |
| ----------------- |
| 47754825 |

## Total Loan Received ($)
```sql
SELECT
  SUM(total_payment) AS Total_Loan_Received
FROM financial_loan;
```
| Total_Loan_Received |
| ----------------- |
| 473070933 |


### MTD (Month-To-Date) and PMTD (Previous-Month-To-Date) Loan Received ($)
```sql
SELECT
  SUM(total_payment) AS MTD_Total_Loan_Received
FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```
| MTD_Total_Loan_Received |
| ----------------- |
| 58074380 |

```sql
SELECT
  SUM(total_payment) AS PMTD_Total_Loan_Received
FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```
| PMTD_Total_Loan_Received |
| ----------------- |
| 50132030 |

## Average Interest Rate (%)
```sql
SELECT AVG(int_rate) * 100 AS AVG_interest_rate FROM financial_loan;
```
| AVG_interest_rate |
| ----------------- |
| 12.0488314172048 |

### MTD (Month-To-Date) and PMTD (Previous-Month-To-Date) Average Interest (%)
```sql
SELECT
  ROUND(AVG(int_rate) * 100, 4) AS MTD_Average_Interest
FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```
| MTD_Average_Interest  |
| ----------------- |
| 12.356 |

```sql
SELECT
  ROUND(AVG(int_rate) * 100, 4) AS PMTD_Average_Interest
FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```
| PMTD_Average_Interest  |
| ----------------- |
| 11.9471 |


## Average DTI (%)
```sql
SELECT ROUND(AVG(dti) * 100, 4) AS Average_DTI FROM financial_loan;
```
| Average_DTI  |
| ----------------- |
| 13.3274 |

### MTD (Month-To-Date) and PMTD (Previous-Month-To-Date) Average DTI ($)
```sql
SELECT
  ROUND(AVG(dti) * 100, 4) AS MTD_Average_DTI
FROM financial_loan
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;
```
| MTD_Average_DTI  |
| ----------------- |
| 13.6655 |


```sql
SELECT
  ROUND(AVG(dti) * 100, 4) AS PMTD_Average_DTI
FROM financial_loan
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;
```
| PMTD_Average_DTI  |
| ----------------- |
| 13.3027 |

## Good Loan Analysis
```sql
SELECT
  (COUNT(CASE WHEN loan_status IN ('Fully Paid', 'Current') THEN id END) * 100) / COUNT(id) AS Percentage_Good_Loan
FROM financial_loan;
```
| Percentage_Good_Loan |
| ----------------- |
| 86 |

```sql
SELECT
  COUNT(id) AS Good_Loan_Application
FROM financial_loan
WHERE loan_status IN ('Fully Paid', 'Current');
```
| Good_Loan_Application |
| ----------------- |
| 33243 |

```sql
SELECT
  SUM(loan_amount) AS GoodLoan_FundedAmount
FROM financial_loan
WHERE loan_status IN ('Fully Paid', 'Current');
```
| GoodLoan_FundedAmount |
| ----------------- |
| 370224850 |

```sql
SELECT
  SUM(total_payment) AS GoodLoan_Received
FROM financial_loan
WHERE loan_status IN ('Fully Paid', 'Current');
```
| GoodLoan_Received |
| ----------------- |
| 435786170 |

## Bad Loan Analysis
```sql
SELECT
(COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100) / COUNT(id) AS Percentage_BadLoan
FROM financial_loan;
```
| Percentage_BadLoan |
| ----------------- |
| 13 |

```sql
SELECT
  COUNT(id) AS Bad_Loan_Application
FROM financial_loan
WHERE loan_status = 'Charged Off';
```
| Bad_Loan_Application |
| ----------------- |
| 5333 |

```sql
SELECT
  SUM(loan_amount) AS BadLoan_FundedAmount
FROM financial_loan
WHERE loan_status = 'Charged Off';
```
| BadLoan_FundedAmount |
| ----------------- |
| 65532225 |

```sql
SELECT
  SUM(total_payment) AS BadLoan_Received
FROM financial_loan
WHERE loan_status = 'Charged Off';
```
| BadLoan_Received |
| ----------------- |
| 37284763 |

## Loan Status Breakdown
```sql
SELECT
  loan_status,
  COUNT(id) AS Total_Applications,
  SUM(total_payment) AS Total_Loan_Received,
  SUM(loan_amount) AS Total_Loan_Amount,
  AVG(int_rate * 100) AS AVG_Interest_Rate,
  AVG(dti * 100) AS Average_DTI
FROM financial_loan GROUP BY loan_status;
```
| loan_status | Total_Applications | Total_Loan_Received | Total_Loan_Amount | AVG_Interest_Rate | Average_DTI    |
|-------------|-----------|------------------------|----------------------|---------------------|-------------------|
| Fully Paid  | 32145     | 411586256              | 351358350            | 11.6410707918092    | 13.1673507557434  |
| Charged Off | 5333      | 37284763               | 66532225             | 13.8785749318289    | 14.0047328005517  |
| Current     | 1098      | 24199914               | 18866500             | 15.0993260800947    | 14.7243442736843  |

```sql
SELECT 
	loan_status, 
	SUM(total_payment) AS MTD_Total_Amount_Received, 
	SUM(loan_amount) AS MTD_Total_Funded_Amount 
FROM bank_loan_data
WHERE MONTH(issue_date) = 12 
GROUP BY loan_status
```
| loan_status | MTD_Total_Loan_Received | MTD_Total_Loan_Amount |
|-------------|---------------------------|--------------------------|
| Fully Paid  | 47815851                  | 41302025                 |
| Charged Off | 5324211                   | 8732775                  |
| Current     | 4934318                   | 3946625                  |


## Monthly Loan Summary
```sql
SELECT
  MONTH(issue_date) AS Month_Number,
  DATENAME(MONTH, issue_date) AS Month_Name,
  COUNT(id) AS Total_Applications,
  SUM(total_payment) AS Total_Loan_Amount,
  SUM(loan_amount) AS Total_Loan_Received
FROM financial_loan
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date);
```
| Month_Number | Month_name | Total_Loan_Applications  | Total_Loan_Amount  | Total_Amount_Received  |
|--------------|------------|--------------------------|----------------------|------------------------|
| 1            | January    | 2332                     | 25031650             | 27578836               |
| 2            | February   | 2279                     | 24647825             | 27717745               |
| 3            | March      | 2627                     | 28875700             | 32264400               |
| 4            | April      | 2755                     | 29800800             | 32495533               |
| 5            | May        | 2911                     | 31738350             | 33750523               |
| 6            | June       | 3184                     | 34161475             | 36164533               |
| 7            | July       | 3366                     | 35813900             | 38827220               |
| 8            | August     | 3441                     | 38149600             | 42682218               |
| 9            | September  | 3536                     | 40907725             | 43983948               |
| 10           | October    | 3796                     | 44893800             | 49399567               |
| 11           | November   | 4035                     | 47754825             | 50132030               |
| 12           | December   | 4314                     | 53981425             | 58074380               |


## Loan Applications by Term
```sql
SELECT
  term AS Term,
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Loan_Amount,
  SUM(total_payment) AS Total_Loan_Received
FROM financial_loan
GROUP BY term ORDER BY term;
```
| Term        | Total_Loan_Applications | Total_Loan_Amount | Total_Loan_Received |
|-------------|--------------------------|----------------------|------------------------|
| 36 months   | 28237                    | 273041225            | 294709458              |
| 60 months   | 10339                    | 162715850            | 178361475              |



## Loan Applications by Employment Length
```sql
SELECT
  emp_length AS Employee_Length,
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Loan_Amount,
  SUM(total_payment) AS Total_Loan_Received
FROM financial_loan
GROUP BY emp_length;
```
| Employee_Length | Total_Loan_Applications | Total_Loan_Amount | Total_Loan_Received |
|------------------|--------------------------|----------------------|------------------------|
| < 1 year         | 4575                     | 44210625             | 47545011               |
| 1 year           | 3229                     | 32883125             | 35498348               |
| 10+ years        | 8870                     | 116115950            | 125871616              |
| 2 years          | 4382                     | 44967975             | 49206961               |
| 3 years          | 4088                     | 43937850             | 47551832               |
| 4 years          | 3428                     | 37600375             | 40964850               |
| 5 years          | 3273                     | 36973625             | 40397571               |
| 6 years          | 2228                     | 25612650             | 27908658               |
| 7 years          | 1772                     | 20811725             | 22584136               |
| 8 years          | 1476                     | 17558950             | 19025777               |
| 9 years          | 1255                     | 15084225             | 16516173               |



## Loan Applications by Purpose
```sql
SELECT
  purpose AS Purpose,
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM financial_loan
GROUP BY purpose ORDER BY purpose;
```
| PURPOSE            | Total_Loan_Applications | Total_Loan_Amount | Total_Loan_Received |
|--------------------|--------------------------|----------------------|------------------------|
| car                | 1497                     | 10223575             | 11324914               |
| credit card        | 4998                     | 58885175             | 65214084               |
| Debt consolidation | 18214                    | 232459675            | 253801871              |
| educational        | 315                      | 2161650              | 2248380                |
| home improvement   | 2876                     | 33350775             | 36380930               |
| house              | 366                      | 4824925              | 5185538                |
| major purchase     | 2110                     | 17251600             | 18676927               |
| medical            | 667                      | 5533225              | 5851372                |
| moving             | 559                      | 3748125              | 3999899                |
| other              | 3824                     | 31155750             | 33289676               |
| renewable_energy   | 94                       | 845750               | 898931                 |
| small business     | 1776                     | 24123100             | 23814817               |
| vacation           | 352                      | 1967950              | 2116738                |
| wedding            | 928                      | 9225800              | 10266856               |


## Loan Applications by Home Ownership
```sql
SELECT
home_ownership AS Home_Ownership,
COUNT(id) AS Total_Loan_Applications,
SUM(loan_amount) AS Total_Loan_Amount,
SUM(total_payment) AS Total_Loan_Received
FROM financial_loan
GROUP BY home_ownership
ORDER BY home_ownership;
```
| Home_Ownership | Total_Loan_Applications | Total_Loan_Amount | Total_Loan_Received |
|----------------|--------------------------|----------------------|------------------------|
| MORTGAGE       | 17198                    | 219329150            | 238474438              |
| NONE           | 3                        | 16800                | 19053                  |
| OTHER          | 98                       | 1044975              | 1025257                |
| OWN            | 2838                     | 29597675             | 31729129               |
| RENT           | 18439                    | 185768475            | 201823056              |

---



