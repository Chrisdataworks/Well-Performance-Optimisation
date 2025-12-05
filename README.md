# Well-Performance-Optimisation


## Problem Statement

Forcado Global is an oil & gas operator that was experiencing declining production and rising operational costs across its 120-well field. Management lacked a clear, data-driven view to prioritize intervention budgets. 

### The Challenge
Identify underperforming wells with the highest potential for production uplift and cost savings to maximize the asset’s net present value (NPV).


### Data Source
The data set used for this project is for 'Production table', 'Well information table', and 'Cost estimate table'

### Tools
- Excel - Data Cleaning [Download Here](https://microsoft.com)
- SQL - Data Analysis
- Power bi - Data Reporting

### Exploratory Data Analysis (Metrics)
EDA involves exploring the data to answer the following questions.
1. What is the production Volume & Decline Rate? (Core indicators of well health and performance)
2. What is the Operating Expenses (OPEX) per Barrel? (Efficiency metric. High OPEX/barrel kills profitability.)
3. What is the Water Cut / Gas-Oil Ratio (GOR)? (Technical indicators of well problems [e.g., water breakthrough].)
4. What is the Net Present Value (NPV)? (The ultimate financial metric.)
5. What is the Estimated Ultimate Recovery (EUR)? (Helps assess long-term potential.)












~~~sql
SELECT 
well_production_12_months.Well_ID,
well_production_12_months.Well_Name,
well_production_12_months.Location,
DATE_FORMAT(well_production_12_months.Date,'%Y-%m') AS Month,
SUM(well_production_12_months.Production_bbl) AS Monthly_Oil,
well_cost_info_120.Monthly_OPEX,
GROUP_CONCAT(well_intervention_results_120.Intervention_Type) AS Intervention
FROM well_production_12_months
JOIN well_cost_info_120 ON well_production_12_months.Well_ID = well_cost_info_120.Well_ID
JOIN well_intervention_results_120 ON well_production_12_months.Well_ID = well_intervention_results_120.Well_ID
GROUP BY 
well_production_12_months.Well_ID,
well_production_12_months.Well_Name,
well_production_12_months.Location,
well_cost_info_120.Monthly_OPEX,
Month
ORDER BY
well_production_12_months.Well_ID,
Month;
~~~
