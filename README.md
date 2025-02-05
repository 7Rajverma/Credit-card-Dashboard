# Credit Card Report 

## Project Objective 
To develop a comprehensive weekly credit card dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to effectively monitor and analyze credit card operations.

## Import data to SQL Database
1. Prepare csv file
2. Create tables in SQL
3. Import csv file into SQL

## DAX Queries use in this dashboard
 1.AgeGroup = SWITCH(
     TRUE(),
     'public cust_detail'[customer_age] < 30, "20-30",
     'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
     'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
     'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
     'public cust_detail'[customer_age] >= 60, "60+",
     "unknown"
     )

2. IncomeGroup = SWITCH(
     TRUE(),
     'public cust_detail'[income] < 35000, "Low",
     'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
     'public cust_detail'[income] >= 70000, "High",
     "unknown"
     )
 
3. week_num2 = WEEKNUM('public cc_detail'[week_start_date])
 
4. Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
 
5. Current_week_Reveneue = CALCULATE(
     SUM('public cc_detail'[Revenue]),
     FILTER(
     ALL('public cc_detail'),
     'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])))
 
6. Previous_week_Reveneue = CALCULATE(
     SUM('public cc_detail'[Revenue]),
     FILTER(
     ALL('public cc_detail'),
     'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))

# Project Insights
### Week of week change:
  • Revenue increased by 28.8%
  • Total Transaction Amt & Count increased 
  • Customer count increased 
  
### Overview YTD:
   • Overall revenue is 57M
   • Total interest is 8M
   • Total transaction amount is 46M
   • Male customers are contributing more in revenue 31M, female 26M
   • Blue & Silver credit card are contributing to 93% of overall transactions 
   • TX, NY & CA is contributing to 68%
   • Overall Activation rate is 57.5%
   • Overall Delinquent rate is 6.06%


 

