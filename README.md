# Well-Performance-Optimisation


## Problem Statement

Forcado Global is an oil & gas operator that was experiencing declining production and rising operational costs across its 120-well field. Management lacked a clear, data-driven view to prioritize intervention budgets. 

### The Challenge
Identify underperforming wells with the highest potential for production uplift and cost savings to maximize the asset’s net present value (NPV).








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
