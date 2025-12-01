# Customer Behaviour and financial Dataset
## Data collection
On final inspection, the data contains five hundred rows and fourteen columns
representing comprehensive customer behaviour and financial information.
- Customer_ID-unique ID assigned to each customer for tracking, not used for
analysis. The range is between 1-500 and it is an integer identifier.
- Age-this column represents the customer’s age, helps to group by young,
middle, and major age. The range is between 18-69, and it is a continuous
numeric variable.
- Gender-this is a categorical type with male and female values. Defines
customer demographic.
- Income-this column shows customer’s income level of spending and
purchasing capacity. Range between 20,055-149,922. This belongs to
numerical value.
- Spending_score-internal score between 1-99 showing spending behaviour; a
higher score indicates a higher value customer.
- Cerdit_score- range value of 300-848, continuous numeric variable of float
type. Reflects the customer’s credit worth; lower scores imply higher loan risk.
- Loan_Amount- amount borrowed by the customer; shows credit exposure
and repayment size at the range of 5,163-49,936. Float data type with a
numeric variable.
- Previous_Defaults-integer data type with numerical discrete value. Number
of past loan defaults; range 0-2 vibes customer reliability and financial risk.
- Marketing_spend-amount spent on marketing to that segment; (range 1,024-
19,990) indicates business investment. It is a continuous numeric with an
integer data type.
- Purchase_Frequency-integer data type numerical discrete variable shows
range between 1-29 number of purchases made in a given period; measures
engagement or loyalty.
- Seasonality-indicates the categorical type high, medium and low. seasonal
context for data; used to analyse time-based trends and patterns.
- Sales-range value of 5,203-99,835. Total sales revenue per customer;
continuous numeric key business performance indicator.
- Customer_Churn-integer data type of binary variable (0 active, 1 churned)
indicates if a customer stop doing business, much helpful for retention
analysis.
- Defaulted- integer data type of binary variable (0 No, 1 Yes) shows whether
the customer defaulted on a loan; measures financial risk.
- Seasonality_date-this is a temporal type (01/01/2020 - 31/12/2024) date of
transaction or sales event used for time series anomalie decetion and trend
analysis.
## Data cleaning
- Uploaded raw dataset, on Power BI go to Home, Get Data, CSV file Select
the dataset and click Load.
- The dataset contains 500 rows and 14 columns with attributes including
Customer_ID, Age, Gender, Income, Spending_Score, Credit_Score,
Loan_Amount, Previous_Defaults, Marketing_Spend, Purchase_Frequency,
Seasonality, Sales, Customer_Churn, Defaulted.
- The raw dataset contained fifty missing values in each three columns
(Income, Credit_Score and Loan_Amount) which were filled with the mean
values. In power query editor right clicking missing value columns and select
replace values. Perhape double checked in pandas script coding
df.isnull().sum().
Column name Missing values Filled mean value
Income 50 84398.055556
Credit_Score 50 573.411111
Loan_Amount 50 28456.928889
