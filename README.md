# Problem Statement  
> ### Email #1: Feature List
> The task is to create a feature list based on the email provided below from the client and a sample feature list. The email contains project requirements which need to be analyzed and included in the feature list. The sample feature list available in the download section serves as a reference for the created feature list. The created feature list must capture all the mentioned features and include relevant details.
> 
> **PILOT PROJECT REQUIREMENTS**
> 
> Dear Hemanand,  
I hope this email finds you well. I’m summarizing the requirements for the pilot project as discussed in the last call.
> 
> To begin, we would like to focus on understanding the number of customers we have and the total revenue we are generating. It would also be beneficial to track the daily revenue growth rate and daily customer growth rate to monitor our progress.  
>
> Monitoring changes in policies on a month-over-month basis is also important to identify trends and areas for improvement. It would be helpful to segment our customer base by age group and analyze revenue and customer numbers by city and age group.    
>
> To analyze trends in customer and revenue growth over time, it would be great to create a switch between revenue trend graphs and customer trend graphs. Additionally, using filters to analyze sales mode, age group, city, month, and policy ID would make the analysis more efficient.  
>
> It would be valuable to have a separate page for sales mode analysis to better understand our customer demographics. We can calculate total customers and total revenue split percentages by sales mode, and analyze the trend of sales mode over the month.    
>
> Having a separate page for age group analysis would also be helpful to understand the impact of age groups on our business. We can analyze age group data to understand expected settlement, sales mode, and policy preference, which will help us make informed business decisions.  
>
> We believe that this pilot project will help us gain valuable insights and build confidence in our collaboration. I would be happy to answer any questions that you may have.    
> I’m also attaching the data & metadata for your reference.  
Best regards,  
Mathew  
Business Analyst  
Shield Insurance
>

## 1. ASK  
### Questions: Preliminary Analysis  
- Show total customers, total revenue, daily revenue growth, daily customer growth as key metrics
- Month over month change% on key metrics
- Segment customers based on their age groups: 18-24, 25-30, 31-40, 41-50, 51-65, and 65+
- Total revenue split by age group, city
- Total customers split by age group, city
- Customers, daily customer growth trend by month
- Revenue, daily revenue growth trend by month
- Create a switch between revenue trend graph and customer trend graph
- Filters on sale mode, age group, city, month, policy ID
- Separate page for sales mode analysis
- Total customers split percentage by sales mode
- Total revenue split percentage by sales mode
- Trend of sales mode over month
- Separate page for age group analysis
- Age group vs expected settlement
- Age group vs sales mode
- Age group vs policy preference


## 2. PREPARE
### Data Storage:  
The dataset is completely available on the Code basis website platform where it stores and consolidates all available datasets for analysis.       

## 3. PROCESS
### Tools Used:
- Microsoft Excel
- Power BI, DAX Studio, DAX

### Data Used:  
This file contains all the meta information regarding the columns described in the CSV files. we have provided 5 CSV files:
1. dim_customer.csv
2. dim_date.csv
3. dim_policies.csv
4. fact_premiums.csv
5. fact_settlements.csv

### About Data:  
Column Description for dim_customer:  
This table contains all the information about the customers
1. customer_code: Unique code is given to each customer
2. dob: Customer's date of birth
3. city: It is the city where the customer is present  


Column Description for dim_date:  
This table contains the dates at daily, monthly levels and week numbers of the year  
1. date: date at the daily level
2. mmm_yy: date at the monthly level
3. day_type: weekday (Sunday, Monday, etc.)
3. week_no: week number of the year as per the date column


Column Description for dim_policies:  
This table contains all policies data  
1. policy_id: unique ID for a particular policy
2. base_cover: base cover amount for that particular policy
3. base_premium_amt(INR): The premium amount that the customer has to pay to get the policy


Column Description for fact_premiums:  
This table contains all information about policy orders.  
1. date: Date on which the policy is sold
2. customer_code: Unique code is given to each customer
3. Policy_id: Unique ID for each policy
4. sales_mode: mode of the sales (Offline-Agent, Offline-Direct, Online-App, Online-Website)
5. final_premium_amt(INR): The premium amount that is paid for that policy by the customer


Column Description for fact_settlements:  
This table contains information about policy settlement  
1. age: Age of the policyholder
2. settlement% : Percent of policy settlements happend for this age 

### Data Cleaning & Transformation:
- Microsoft Excel, Power Query was used to clean and transform raw data.
- From fact_settlement, remove the empty columns
- From fact_premiums, split sales_mode columns by delimiter '-' & renamed as Mode: Online/Offline , Mode: Through Medium
- Check all the data types & changed into necessary data type


# 4. ANALYZE
Data Analyzing  
Power BI was used to analyze data.

### Key Metrics:
- DRG: Daily Revenue Growth (DRG) can be calculated by dividing the total revenue earned in a specific month by the number of unique dates within that month. This calculation gives us a clear picture of how much, on average, the company's revenue is growing each day during that time period.
- DCG: Daily Customer Growth (DCR) measures the average daily increase in the customer base during a specific month. It's calculated by dividing the total new customers acquired in a month by the number of unique dates within that month.

DCR provides insights into the daily growth rate of the customer base, helping evaluate the company's ability to attract and retain customers on a day-to-day basis.

### Measures/ Parameters:
- %CustomerChange = DIVIDE([Total Customers] - [LM Customers], [LM Customers], 0)
- %DCGChange = DIVIDE([DCG] - [LM DCG], [LM DCG], 0)
- %DRGChange = DIVIDE([DRG] - [LM DRG], [LM DRG], 0)
- %RevenueChange = DIVIDE([Total Revenue] - [LM Revenue], [LM Revenue], 0)
- DCG = VAR _tot_cus = [Total Customers] VAR _date = DISTINCTCOUNT(dim_date[date]) RETURN DIVIDE(_tot_cus, _date, 0)
- DRG = VAR _tot_rev = [Total Revenue] VAR _date = DISTINCTCOUNT(dim_date[date]) RETURN DIVIDE(_tot_rev, _date, 0)
- LM Customers = CALCULATE([Total Customers], PREVIOUSMONTH(dim_date[date]))
- LM DCG = CALCULATE([DCG], PREVIOUSMONTH(dim_date[date]))
- LM Revenue = CALCULATE([Total Revenue], PREVIOUSMONTH(dim_date[date]))
- Total Customers = COUNT(dim_customer[customer_code])
- Total Revenue = SUM(fact_premiums[final_premium_amt(INR)])



# 5. SHARE


# 6. ACT	
### Insights:	
- 


### Recommendations:	
- 

Thank you for reading and evaluating my repo :)	                                								
Live Dashboard [Link](https://public.tableau.com/app/profile/ankit.negi7687/viz/MarketResearchDashboardEVHybridVehiclesIndustryAnalysis/MainPage)
