# Customer Behaviour and financial Dataset
## dataset used 
- CSV file <a href= "https://github.com/vishnuwin/powerbi-portfolio/blob/main/cleaned_data.csv">click here</a>
- Phyton pdf <a href= "python.pdf">click here</a>
- Power BI pdf <a href= "power BI dashboard.pdf">click here</a>
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
df.isnull().sum(). And replaced fifty each null values with mean by coding
df.fillna(df[['Income','Credit_Score','Loan_Amount']]. mean(),inplace=True)
df.head()
<img width="390" height="330" alt="Screenshot 2025-10-13 191121" src="https://github.com/user-attachments/assets/473a451e-2147-442f-aa20-70f1b87734f2" />

- To remove duplicates run the code df.duplicated().sum() and no duplicates
were found.
- Outliers are the data points that lie far away from the majority of values. IQR =
Q3 – Q1. Q1 is the 25th percentile (lower quartile) and Q3 is the 75th percentile
(upper quartile). Acceptable range is Value < Q1 – 1.5 * IQR or Value > Q3 +
1.5 * IQR.
- Out off 500 rows, 95 was removed as outliers. The cleaned dataset now
contains 405 reliable records. Outliers present in income, sales,
marketing_spend.
<img width="746" height="181" alt="Screenshot 2025-10-15 224906" src="https://github.com/user-attachments/assets/7bcc7832-c671-414e-857f-aedbb2ee5ad3" />

- This cleaning step ensured accurate summary statistics for better visualization
clarity in more reliable.
- Variables like income, sales, and marketing_spend had extreme values
beyond the whiskers(outliers). After removing outliers using IQR, the boxplots
became tighter and more symmetric, showing a more consistent distribution.
- After removing the dots, I replot boxplots, no isolated points for those columns
anymore thus this is the proof that outliers were successfully cleaned.now the
dataset is cleaned and ready for the analysis.
## Exploratory Data Analysis (EDA)
After removing outliers, the dataset contained 405 records. Descriptive statistics
revealed that the average customer age was 44, the mean income is 84398, the
spending score is 51, the credit score is 573, the loan amount is 2845, and the
average sales is 54. Thus, the dataset shows balanced spread across demographic
and financial metrics, making it ready for visual exploration.
<img width="1072" height="269" alt="Screenshot 2025-12-01 124648" src="https://github.com/user-attachments/assets/eaa82aef-deee-44a6-9c8e-f36c80ced344" />
Histograms and KDE plots to show how each variable is distributed. Histograms
were plotted for numeric columns such as 'Age', 'Income', 'Spending_Score',
'Credit_Score', 'Loan_Amount', 'Marketing_Spend', and 'Sales'. Most features
showed normal or slightly right skewed distributions, while income and sales had
wider ranges, indicating customer diversity.
<img width="655" height="394" alt="Screenshot 2025-12-01 124403" src="https://github.com/user-attachments/assets/76b2140a-f5ad-4344-b320-fa770a16985c" />

A correlation heatmap highlighted strong correlations between 'Age', 'Income',
'Spending_Score', 'Credit_Score', 'Loan_Amount', 'Marketing_Spend', and 'Sales',
suggesting these features are key business drivers. Weak correlations between
credit related and spending features indicates distinct customer behaviours for risk and revenue.
<img width="655" height="425" alt="Screenshot 2025-12-01 124917" src="https://github.com/user-attachments/assets/76469dcd-b715-4d73-bee8-0512cf18e72e" />

The relationship between seasonality and sales where analysed using bar plot
sns.barplot(x=’seasonality’, y=’sales’, data=df). This reveals seasonality impact on
revenue. The relationship between gender and income where spoted using boxplot
sns.boxplot(x=’gender’, y=’income’, data=df). This reveals gender wise income comparison.

<img width="556" height="481" alt="Screenshot 2025-10-28 173637" src="https://github.com/user-attachments/assets/84322fc5-888a-4a57-9bf9-1b77258205a7" />

Analyse which customers are likely to leave the company based on their income,
purchase frequency and spending behaviour and to visualize churn patterns before
buliding a prediction model. The first step count plot sns.countplot (x='Customer_
Churn', data=df) plt.title("Customer Churn Distribution (0 = Active, 1 = Churned)")
thus it indicated the moderate churn rate (24%) which mathes the statistic mean
(0.2419) from the dataset. The median income of churned customers is lower than
that of active customers. This means low income customers are more likely to churn
they may be more price censitive or less loyal.
## Predictive model
<img width="614" height="336" alt="Screenshot 2025-12-01 130155" src="https://github.com/user-attachments/assets/0fefb46a-8466-4cab-ae16-4eccdd922f39" />

The basic logistic regression provides a strating baseline for churn prediction slightly
55.6% accuracy better than random guessing but not strong. Weighted score
indicates moderate prediction balance. Precision for churners (1) 0.26 is the model
struggles to correctly identify chruners.
Linea regression with the independent variable (x) as customer income level and
marketing spend and dependent variable as sales total revenue for each customer.
Train test split 80% of the data used for training , 20% for testing. This ensures fair
performance evaluation on unseen data.

<img width="625" height="390" alt="Screenshot 2025-12-01 130243" src="https://github.com/user-attachments/assets/154d2496-c2b0-4792-8843-67c3da3b0f7c" />

lin_model fit a straight line that best explains the relationship between features and
sales. for the prediction and evaluation mean squared error (MSE) measures
prediction error lower=better. Here MSE=759,564,757 indicates large error between
actual and predicated sales. R2
 (-0.034) Score explains how much variance in sales
is explained by income and marketing spend. Here model performs worse than a
simple average model. Hence the model did not perform well suggesting that income
and marketing spend alone cannot accurately predict sales. The relationship
between these variables and sales may be non-linear or influenced by other features
like spending score, purchase frequency or seasonality. 
## Visualization using Power BI
## Customer Behaviour & Financial Dataset
<img width="970" height="542" alt="Customer Behaviour   Financial Insights" src="https://github.com/user-attachments/assets/d69a76f5-7132-4521-b70d-357b7f2b4b8a" />

- Total Sales, Total Customers & Spending Score
These KPIs give a quick snapshot of business health — total sales of 27M from 500 customers, with an average spending score of around 50. This helps understand overall customer value.
- Churn Rate & Default Rate
Both rates are high in this dataset (shown as 100%), suggesting that either:
 - the dataset is simulated, or
 - the company is facing serious customer retention and loan repayment issues.
- Age Group Distribution
This bar chart shows credit score variation across ages. The data appears scattered, indicating that age does not have a strong influence on credit score or financial behaviour.
- Income vs Spending Score (Scatter Plot)
The point indicates that customers with higher income might not always have a high spending score. It shows that income does not directly predict buying behaviour.
- Sales by Gender
Sales are distributed fairly evenly between males and females, meaning buying power is shared almost equally across genders.


