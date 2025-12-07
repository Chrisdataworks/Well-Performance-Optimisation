# Well-Performance-Optimisation

### Table of Contents
- [Problem Statement]
- [The Challenge]
- [Data Source]
- [Tools]
- [Exploratory Data Analysis (Metrics](Exploratory-data-analysis-(metrics))
- [Data analysis](data-analysis)
- [Findings/Insight](findings/insight)
- [Recommendation](Recommendation)




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


### Data Analysis

~~~mysql
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

### Dashboard (Power BI)


### Findings/Insights

The data revealed that 80% of the production decline was concentrated in just 25% of the wells. More critically, we found a cluster of 18 wells with moderately high water cut but still strong pressure—a classic sign of a fixable mechanical issue. These wells were being flagged as 'problematic', but their high NPV uplift potential was being overlooked due to high near-term water handling costs.


### Recommendation.

1. Immediate Workover: Prioritize the 18 identified wells for re-perforation and pump optimization.
2. Defer Expensive Interventions: Postpone high-cost, low-NPV activities (e.g., major fracturing on 5 poor-geology wells).
3. Implement Predictive Monitoring: Use the model to flag early signs of decline in top-performing wells.


### Assumption/Limitation

- The project relies heavily on forward-looking metrics (NPV, EUR, projected production uplift) and assumes there is evidence of model validation, confidence intervals, or scenario analysis.
  
- The project identifies 18 wells with high water cut but strong pressure as having "fixable mechanical issues" and recommends re-perforation and pump optimization, and assumes the diagnostic evidence presented (pressure transient analysis, downhole camera surveys,  cement bond logs) aligns.
  
- The project treats each well as an independent optimization problem without acknowledging that production in one well can affect neighbouring wells through reservoir pressure depletion, water or gas influx, or interference from nearby injection wells.
