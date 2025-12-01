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
## Seasonality & Anomaly Detection
This page focuses on understanding how sales change over time and identifying unusual patterns that need attention.
<img width="930" height="526" alt="Screenshot 2025-12-01 113038" src="https://github.com/user-attachments/assets/80e283c6-9a84-4f57-a311-9897a93ab666" />

- Sales with Anomalies
This line chart helps identify months where sales were unexpectedly high or low. For example, a dip in July 2024 or May 2025 could signal external issues (like low demand or stock shortages), while spikes highlight successful seasons or campaigns.
- Sales by Seasonality (High / Medium / Low)
This breakdown shows how much revenue is generated during different seasonal categories. Interestingly, High and Medium seasons generate almost equal sales, meaning the business performs quite consistently across the year.
- Seasonality Distribution (Pie Chart)
The pie chart shows how many months fall into each season type. Medium season months occur slightly more often. This helps the business predict revenue cycles and plan inventory or promotions accordingly.
## Sales & Marketing Insights
This page provides a clear overview of how marketing efforts relate to sales performance. It helps identify whether marketing spend is actually generating the expected business results.
<img width="963" height="542" alt="Sales   Marketing Insights" src="https://github.com/user-attachments/assets/04e2775d-5117-424f-9386-33fba5c0f136" />

- Marketing Spend by Year
This chart shows how much the company invested in marketing across different years. For example, a significant spike in 2024 indicates a strong marketing push, while 2025 shows a more moderate spend. This helps the business understand where major budgets were allocated.
- Sales vs Marketing
Here, sales and marketing are compared side-by-side. Even though marketing spend increased drastically in 2024, sales also rose, suggesting that the campaigns were effective. In 2025, sales remain steady even though marketing spend decreased, showing improved efficiency.
- Purchase Frequency
This visual highlights how often customers made purchases month-by-month. Peaks in months like June and December indicate high-traffic periods, possibly driven by promotions, festivals, or seasonal demand.
- Customer Demographic
This bar chart shows the age and gender distribution of customers. Most customers fall within the 25–50 age range. Males slightly dominate the customer base, but both genders show strong participation. This helps businesses target marketing campaigns more precisely.
## Sales & Revenue Analysis
This page focuses on understanding overall sales performance and how customer income and spending behaviour relate to revenue.
<img width="967" height="540" alt="sales and revenue analysis" src="https://github.com/user-attachments/assets/801b21bf-fee9-4fe6-a7ee-e68a231c1f0b" />

- Sales Trend
Sales fluctuate over the year with clear peaks in months like May 2024 and dips in months like July 2024 or May 2025. This trend helps businesses prepare for slow periods and maximise high-sales months.
- Income vs Sales
The data shows no strong correlation — customers with higher income don’t necessarily spend more. This means marketing strategies should target behaviour, not income.
- Spending Score vs Sales
Again, spending score does not strongly drive sales. A customer might have a high score but still make fewer purchases. This shows that multiple factors (offers, product interest, timing) influence sales.
## Customer Risk & Loan Default Analysis
This page helps the company understand customer risk levels and identify patterns in loan default behaviour.
<img width="970" height="545" alt="customer risk and loan default analysis" src="https://github.com/user-attachments/assets/be70c3a9-7ab9-41f3-a4c7-d5d920929058" />

- Purchase Frequency by Churn
Customers who churn generally show significantly lower purchase frequency. This means lack of engagement is a strong indicator of churn — a valuable insight for retention strategies.
- Credit Score vs Default
Even customers with higher credit scores show defaults. This suggests that credit score alone is not enough to judge risk. Additional checks (income stability, behaviour history) would improve risk assessment.
- Previous Defaults
This visual shows how many customers have defaulted before. A high count indicates that the company might be approving risky customers or needs better monitoring.
- Loan Amount by Income
Loan amounts do not increase consistently with income. This means some low-income customers received high loans. It highlights the need for stricter loan-to-income policies.
## Summary report outlining key findings and business recommendations.
## key findings
The raw dataset contained fifty missing values in each three columns (Income,
Credit_Score and Loan_Amount) which were filled with the mean values. A boxplot
and IQR analysis were used to detect outliers, but none were found. The majority of
customers are between 30-55 years; male customers show slightly higher market
spending scores and engagement with marketing campaigns. Customer with higher
income tend to have higher credit scores and lower default rates. A smaller group of
customers with moderate income but high spending show signs of potential credit
risk. Marketing spend and purchase frequency strongly affect sales. churn is
influenced by purchase frequency targeted retention campaigns should focus on
high-risk customers.
About 15% of customer have previous defaults. Customers with loan amounts above
7500 and credit scores below 450 are defaulting a high risk. 21 anomalous
transactions were detected these should be investigated for potential fraud or data
entry errors.thus monitoring anomalies helps to maintain data quqlity and financial
controls. three seasonality distributions high (34%), medium (34%), low (32%). All
three were distributed almost equally in the contribution of salaes volume.
Linear regression model was developed to predict sales as the dependent variable
and the predictors like marketing spend, seasonality, income, spending score. The
mean squared error (MSE) was 752506081.5 indicating some variation between
predicted and actual sales values.thus the marketing spend and seasonality play
significant roles in influencing sales performance. 
Spending score are spread across all range, but a higher frequency is observed
between 60-100. Certain gender group show more active spending patterns,
indicating stronger engagement with the brand. Low scores below 20 are relatively
fewer, showing that only a small segment exhibits limited spending behaviour.
The churn rate fluctuates across age groups, with notable spikes around ages
20,30,50 and 60. Younger under 25 and older above 55 customers show higher
churn tendencies. Middle aged groups 30-50 maintain relatively stable retention.
The highest concentration of defaults is near a credit score of 590. Customers with
scores above 700 rarely default, confirming strong financial reliability. Those below
500 also show a few defaults, likely due to pre-screening before loan approval.
## Business Recommendations
Focus marketing and loyalty programmes on high income and high spending
customers.use personalised offers to retain these profitable segments. Optimize marketing campaigns during seasonal peaks. Develop personalized retention
strategies for risk management.
Anomaly based decision support integrate sudden drop in sales, were Optimize
marketing spend during months with higher sales potential.
This visual identifies spikes in revenue, possibly due to seasonal effects or marketing
campaigns. The smart narrative provides AI generated insights summarizing about
these trends that sales showed periodic spikes in revenue across early 2024 and
early 2025, possibly reflecting seasonal patterns or campaign effects. Monthly
aggregation of sales showed seasonal peaks, indicating higher spending during
certain months. Lin charts visualized the trend clearly helping identify periods of high
revenue.
Adjust stock and staff schedules for high oscillation months. Introduce small
promotions during low months to stabilise demand. develop premium product lines
for high income segments who show strong sales correlation.Tailor marketing campaigns by gender and spending tier to increase engagement.
Introduce reward schemes to encourage medium spenders ro move into the high
spending category. Use data driven insights to identify underperforming gender
segments and promote customised offers.
offer flexible, trend-based products or loyalty discounts for younger customers. Use
targeted communication to win back older customers with retirement friendly offers
or value bundles. Implement churn prediction models to proactively identify and
retain high risk customers.
Tighten approval criteria or increase interest rates for applicants in the 550-600
credit score range. Offer financial education or credit buliding incentives to moderate
risk customers. Continuously monitor repayment behaviour for early warning signs in
mid range credit segments.
