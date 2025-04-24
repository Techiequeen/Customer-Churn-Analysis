# Customer-Churn-Analysis

### Project Overview
Customer churn refers to the phenomenon where customers stop using a company's product or service, resulting in lost revenue and potential long-term damage to the business. Understanding the factors that contribute to customer churn is crucial for businesses to develop effective retention strategies and improve customer satisfaction.
This project analyzes a customer churn dataset to identify key factors contributing to customer churn and provide insights for business improvement. The analysis explores customer behavior, usage patterns, and demographic characteristics to inform data-driven decision-making.

### Data Sources

The analysis is based on a customer churn dataset containing the following columns:
- Customer ID
- Age
- Gender
- Tenure
- Usage frequency
- Support calls
- Payment delay
- Subscription type
- Contract length
- Total spend
- Last interaction
- Churn

### Tool Used

- Excel: Data Cleaning
- SQL Server: Data Analysis
- Power BI: Data Visualization.

### Data Cleaning/Pre-processing

Data cleaning and pre-processing were carried out to ensure data quality. The following tasks were performed:
- Data loading and inspection
- Handling spelling errors
- Assigning data type to columns

### Exploratory Data Analysis (EDA)

The EDA process involves analyzing the customer churn dataset to understand the distribution of variables, identify patterns and trends, and detect potential issues. Some key questions explored include:
1. How has the churn rate changed over time?
2. What is the average age of customers who churned and those who did not?
3. Which gender has a higher churn count?
4. What is the distribution of customers by age group?
5. Which subscription type has the highest churn count?
6. How does payment delay affect churn count?
7. Average tenure by churn count.
8. How does usage frequency affect churn?
9. Are customers with higher total spend more or less likely to churn?

### Data Analysis

Data analysis was done in SQL Server. 
~~~sql
Q1. How has the churn rate changed over time
SELECT Contract_Length,
ROUND(COUNT(CASE WHEN Churn = 1
THEN CustomerID END) * 100.0 / COUNT(CustomerID), 2)  AS Churn_Rate
FROM customer_churn
GROUP BY Contract_Length
ORDER BY Contract_Length;
~~~
~~~sql
--Q2. What is the average age of customers who churned and those who did not?
SELECT AVG(Age) AS AverageChurnedAge
FROM customer_churn
WHERE Churn = 1; 
SELECT AVG(Age) AS AverageNotChurnedAge
FROM customer_churn
WHERE Churn = 0;
~~~
![image](https://github.com/user-attachments/assets/26b6ad36-f97f-4c51-8d8c-d8dea28205e3)
~~~sql
--Q3. Which gender has a higher churn count?
SELECT Gender, SUM(CASE WHEN Churn = 1 THEN 1 END) AS Churn_count
FROM customer_churn
GROUP BY Gender
ORDER BY Churn_count DESC;
~~~
![image](https://github.com/user-attachments/assets/384e8938-eccb-4c64-85bc-519d0855b2cf)
~~~sql
--Q4. What is the distribution of customers by age group?
SELECT 
	CASE
	WHEN Age >= 18 AND Age <= 28
THEN '18-28'
	WHEN Age >= 29 AND Age <= 38
THEN '29-38'
	WHEN Age >= 39 AND Age <= 48
THEN '39-48'
	WHEN Age >= 49 AND Age <= 58
THEN '49-58'
	WHEN Age >= 59  THEN '68+'
	ELSE 'UNKNOWN'
	END AS Age_group,
	COUNT(*) AS Customer_count
FROM Customer_churn
GROUP BY 
	CASE
	WHEN Age >= 18 AND Age <= 28
THEN '18-28'
	WHEN Age >= 29 AND Age <= 38
THEN '29-38'
	WHEN Age >= 39 AND Age <= 48
THEN '39-48'
	WHEN Age >= 49 AND Age <= 58
THEN '49-58'
	WHEN Age >= 59 THEN '68+'
	ELSE 'UNKNOWN'
	END
ORDER BY Age_group;
~~~
![image](https://github.com/user-attachments/assets/81c54bc6-edc0-4b57-8f41-5048098c4e6b)
~~~sql
--Q5. Which subscription type has the highest churn count?
SELECT Subscription_Type, SUM(CASE WHEN Churn = 1 THEN 1 END) AS TotalChurn
FROM customer_churn
GROUP BY Subscription_Type;
~~~
![image](https://github.com/user-attachments/assets/7a661700-a064-42c8-b748-43159f575f67)
~~~sql
--Q6. How does payment delay affect churn count?
SELECT Payment_Delay, SUM(CASE WHEN Churn = 1 THEN 1 END) AS Churn_count
FROM customer_churn
GROUP BY Payment_Delay
ORDER BY Churn_count DESC;
~~~
![image](https://github.com/user-attachments/assets/fe71e40c-ef75-4e74-a267-9ecb27f2d674)
~~~sql
--Q7. What is the average tenure of customers who churned and those who did not?
SELECT Churn,
AVG(Tenure) AS Average_tenure
FROM customer_churn
GROUP BY Churn;
~~~
![image](https://github.com/user-attachments/assets/d6063b3e-eb80-4d72-a453-43e9668f5341)
~~~sql
--Q8.How does usage frequency affect churn?

SELECT Usage_Frequency, SUM(CASE WHEN Churn = 1 THEN 1 END) AS Churn_count
FROM customer_churn
GROUP BY Usage_Frequency;
~~~
![image](https://github.com/user-attachments/assets/09eed270-f09f-4fb8-8e77-074c471625ed)
~~~sql
--Q9.Are customers with higher total spend more or less likely to churn?
SELECT Churn,
SUM(Total_Spend) AS Total_Spend
FROM customer_churn
GROUP BY  Churn;
~~~
![image](https://github.com/user-attachments/assets/e7185ddb-cc9b-403e-acd6-4f599bbaaca1)

### Results/Findings

The analysis of the customer churn dataset reveals:
1. Key factors contributing to churn: Usage frequency, support calls, payment delay, and contract length
2. Customer segments with high churn rates: Young customers with short tenure and high usage frequency
3. Insights into customer behavior: Customers with high support calls and payment delay are more likely to churn

### Recommendations

Based on the analysis, here are some recommendations:
1. Improve Customer Support: Reduce support calls by providing timely and effective support.
2. Optimize Pricing and Contract: Offer flexible pricing plans and contract lengths to reduce churn.
3. Enhance Customer Engagement: Engage with customers regularly to improve usage frequency and reduce churn.
4. Monitor and Analyze Churn: Regularly analyze churn data to identify trends and opportunities for improvement.

### Limitations
This analysis has several limitations:
- Data scope: The analysis is based on a specific dataset and may not reflect current market trends or conditions.
- External factors: The analysis does not account for external factors, such as economic changes or competitor activity, that may impact customer churn.














