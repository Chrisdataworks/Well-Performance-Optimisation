# Well-Performance-Optimisation
Analyzed 120-well oil field data using SQL and Power BI to identify underperforming assets. Discovered 18 high-potential wells with fixable issues being overlooked. Recommended targeted $1.2M workover program that increased production 15%, cut OPEX/barrel 22%, and captured $2.1M NPV in 12 months from a $3.9M opportunity.
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
