# Hotel Booking Demand Analysis
## Overview

This project explores hotel booking demand patterns using a real-world dataset containing reservation information for both city hotels and resort hotels. The goal of the analysis is to understand booking behavior, cancellation patterns, seasonal trends, and factors that influence hotel demand.

## Problem Statement
The hospitality industry operates in a highly competitive environment where understanding customer booking behavior is essential for improving operational efficiency and revenue management. Hotels must analyze patterns in reservations, cancellations, pricing, and customer preferences to make informed business decisions.

This project uses exploratory data analysis (EDA) on a hotel booking dataset to identify trends in demand, customer behavior, and booking characteristics. The analysis aims to uncover insights that can support strategic decision-making related to pricing strategies, marketing efforts, and service improvements.

## Key objectives include:

* Analyzing booking demand and seasonal trends
* Understanding customer segments and booking channels
* Investigating cancellation patterns
* Evaluating pricing behavior through Average Daily Rate (ADR)
* Insights from this analysis can help hotels optimize occupancy rates, revenue generation, and overall customer satisfaction.

## Dataset
This dataset is obtained from Kaggle. It includes bookings for both City Hotel and Resort Hotel, allowing comparisons between different hotel types. 

Key variables used in the analysis include:

| Column | Description |
|------|-------------|
| hotel | Type of hotel (City Hotel or Resort Hotel) |
| lead_time | Number of days between booking and arrival |
| arrival_date_year | Year of arrival |
| arrival_date_month | Month of arrival |
| stays_in_weekend_nights | Number of weekend nights booked |
| stays_in_week_nights | Number of weekday nights booked |
| adults, children, babies | Number of guests in the reservation |
| market_segment | Market segment category |
| is_canceled | Indicates whether the booking was canceled |
| adr | Average Daily Rate (room price per night) |
| customer_type | Type of customer making the reservation |

## Key Analysis Areas

The analysis focuses on several important aspects of hotel operations:
* Booking trends over time
* Seasonality of hotel demand
* Cancellation patterns
* Customer segmentation
* Length of stay behavior
* Pricing patterns (ADR)

## Exploratory Data Analysis (EDA)
<img width="1022" height="188" alt="image" src="https://github.com/user-attachments/assets/0c6fa01b-7497-432a-965b-2add5ee65410" />
<img width="1307" height="183" alt="image" src="https://github.com/user-attachments/assets/00ea089d-a4e4-4e30-8314-67e149a9418a" />
The hotel DataFrame contains 119,390 entries and 32 columns. It has null values in the following fields: children (4), country (452), agent (12,193), and company (82,137). Additionally, there are 31,994 duplicate entries.

After cleaning and transformation, the final dataset has 87212 rows and 35 columns.

## EDA Charts 
**Cancellation by Market Segment**

<img width="579" height="340" alt="image" src="https://github.com/user-attachments/assets/deae843a-fc45-4cde-8d10-ab6986dbe266" />

Cancellation rates are highest for Groups and Online TA bookings and lowest for Corporate and Complementary bookings.

**Cancellation Distribution and Cancellation By Hotel Type**

<img width="533" height="353" alt="image" src="https://github.com/user-attachments/assets/786cb9bd-9afd-4fbc-8b94-637f6ed4e468" />

Most bookings are completed, but cancellation rates differ by hotel type, with city hotels experiencing more cancellations than resort hotels.

**Lead Time vs. Cancellation**

<img width="395" height="305" alt="image" src="https://github.com/user-attachments/assets/c605c16d-182a-4c73-bf63-6e4e5ab7198f" />

The adverage cancellation lead time is around 80 days. The canceled box is also wider/longer, which means there's more variability in lead time. The upper whisker is much higher for the cancel boxplot, indicating some bookings made very far in advance have been canceled. Cancelled bookings generally have longer lead times than non-cancelled bookings, suggesting that reservations made further in advance are more uncertain.

**Cancellation by Weekdays**

<img width="580" height="382" alt="image" src="https://github.com/user-attachments/assets/eb8f6f92-8ca1-422d-85f1-0a6ec91ed22f" />

Cancellation rates increase toward the weekend, peaking on Friday (30.6%) and Saturday (30.1%). This pattern indicates that leisure travelers who are more likely to book weekend stays, show greater booking flexibility and higher cancellation behavior than weekday travelers.

**Average Monthly ADR and Cancellation Rate Chart**

<img width="857" height="437" alt="image" src="https://github.com/user-attachments/assets/6fa4393a-5b89-41d2-bd3f-a678e80b6d38" />

Higher ADR during peak months (June–August) coincides with elevated cancellation rates, highlighting a trade-off between revenue maximization and booking reliability. This suggests opportunities for strategies such as dynamic pricing, deposits, or overbooking to manage risk during high-demand periods.

**Cancellation by Deposit Type**

<img width="558" height="649" alt="image" src="https://github.com/user-attachments/assets/b5869b14-f90c-413b-9239-4d44b0fe49da" />

Most bookings are made without deposits. Non-refundable deposits show the highest cancellation rate, while refundable deposits have the lowest. However, refundable bookings account for only a small number of reservations, so **the percentage should be interpreted with caution.**

## Heatmap Chart

<img width="967" height="779" alt="image" src="https://github.com/user-attachments/assets/ab1ee4e1-4150-4084-aa7e-f369f917544a" />

The heatmap shows several redundant variables. For example, total_nights is highly correlated with stays_in_week_nights (0.95) and stays_in_weekend_nights (0.78), while total_guests is strongly correlated with adults (0.74) and children (0.67). These relationships suggest overlapping information among features.

Most numerical features show weak correlations with booking cancellations. Lead time and average daily rate (ADR) show modest positive relationships with cancellations, while required parking spaces and special requests show negative relationships, suggesting stronger commitment among these bookings.

## Models
### Logistic Regression

A Logistic Regression model is used as the initial baseline classifier to predict booking cancellations. Since is_canceled is a binary outcome, Logistic Regression provides an interpretable and efficient starting point for evaluating how booking characteristics relate to cancellation behavior.

### Random Forest

Random Forest is a tree-based ensemble model to capture nonlinear relationships and interactions among booking features. Unlike Logistic Regression, which assumes a linear relationship between predictors and the outcome, Random Forest constructs multiple decision trees using bootstrapped samples of the data and aggregates their predictions. This approach can improve predictive performance and robustness, particularly when complex patterns exist in the dataset. The Random Forest model is evaluated alongside Logistic Regression to determine whether a more flexible, non-linear method improves cancellation prediction accuracy.

## Model Comparison
### Confusion Matrix

<img width="766" height="414" alt="image" src="https://github.com/user-attachments/assets/e2471e9b-fa79-4871-aeae-170a0812769f" />

## Model Evaulation
### Classification Report

<img width="430" height="551" alt="image" src="https://github.com/user-attachments/assets/a9770cd7-a509-4a9c-9a17-42d7618f6a55" />

The Logistic Regression classification report shows that When the model predicts that a booking will not be canceled, it is correct 90% of the time. It also correctly identifies 77% of cancellations, but its precision is lower (53%), meaning some bookings predicted as canceled are actually completed. This Logistic Regression is the first baseline model.

The Random Forest classification report shows that When the model predicts that a booking will not be canceled, it is slightly less correct 87% of the time. It also correctly identifying fewer cancellations at 63%, but its precision is higher (77%), meaning some bookings predicted as canceled are actually completed.

Random Forest achieves the highest overall accuracy (85% vs 75%)and precision when predicting cancellations. However, Logistic Regression has higher recall for canceled bookings, meaning it identifies a larger share of actual cancellations. This highlights the trade-off between minimizing false positives and capturing more true cancellations.

The F1-scores for both completed bookings and canceled bookings are higher for Random Forest (0.90 and 0.69) than for Logistic Regression (0.81 and 0.63). This indicates that Random Forest provides a better overall balance between precision and recall across both classes, resulting in stronger overall predictive performance.

### ROC Curves and AUC Scores

<img width="467" height="361" alt="image" src="https://github.com/user-attachments/assets/6c31d6c1-f4f0-455f-b5be-9af0df078e64" />

The ROC curve compares the classification performance of Logistic Regression and Random Forest across different probability thresholds. The Random Forest model achieves a higher AUC (0.91) than Logistic Regression (0.84), indicating a stronger ability to distinguish between canceled and non-canceled bookings.

The steeper and wider curve of the Random Forest model shows that it achieves a higher true positive rate for the same false positive rate across most thresholds. This suggests that Random Forest provides better overall predictive performance for the cancellation prediction task.

## Key Insights & Business Implications

1. Cancellation prediction can support revenue management.
Predicting cancellations allows hotels to anticipate lost bookings and adjust pricing, overbooking strategies, or promotional offers to maintain occupancy levels.

2. Model choice affects operational strategy.
Logistic Regression identifies a larger share of actual cancellations, which may help hotels proactively manage potential revenue loss. Random Forest, however, provides more reliable predictions when identifying cancellations, reducing false alarms.

3. Trade-off between recall and precision.
If the business goal is to capture as many potential cancellations as possible, Logistic Regression may be preferred. If the goal is to avoid unnecessary interventions, Random Forest may be the better choice.

4. Predictive analytics can improve operational planning.
Early detection of cancellation risk allows hotels to adjust staffing, marketing campaigns, and room inventory management.

## Conclusion
This analysis compared Logistic Regression and Random Forest models to predict hotel booking cancellations. While Logistic Regression serves as a strong baseline and captures a larger share of actual cancellations, Random Forest provides better overall predictive performance, achieving higher accuracy and stronger F1-scores across both classes. These results demonstrate the value of ensemble models when modeling complex booking behavior.

Future work could extend this analysis by exploring additional predictive tasks such as forecasting booking revenue, predicting average daily rate (ADR), or improving cancellation prediction using additional features and more advanced models.

➡️ Full analysis: [`eda-and-cancellation-analysis.ipynb`](eda-and-cancellation-analysis.ipynb)
