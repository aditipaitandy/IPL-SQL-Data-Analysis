# 🏏 Men's IPL (2018–2019) Data Analysis using SQL

An analytical deep dive into the 2018 and 2019 Indian Premier League (IPL) seasons. This project utilizes structured SQL queries to extract key performance indicators (KPIs) for batsmen and bowlers, evaluate team distributions, and track cross-season player consistency.

## 🚀 Project Overview
The goal of this project is to transform raw seasonal cricket statistics into actionable sports insights. By writing structured queries, this analysis isolates top-tier athletic performances, identifies robust team structures, and tracks multi-year player trends.

## 📊 Key Insights Uncovered
* **Multi-Year Consistency:** Leveraged `INNER JOIN` operations to isolate players who maintained high performance (and strike rates greater than or equal to 130) across both the 2018 and 2019 seasons.
* **Roster Dispersions:** Grouped and aggregated player counts per franchise to evaluate squad depth and strategic balance between bowling and batting units.
* **Impact Outliers:** Identified high-impact bowlers by filtering multi-wicket hauls (4w+) and analyzing economy rates under 7 runs per over.

## 🛠️ Tech Stack & Concepts Used
* **Dialect:** Standard SQL / BigQuery SQL
* **Joins & Set Operations:** `INNER JOIN` for cross-season performance mapping.
* **Aggregations:** `SUM()`, `COUNT()`, `AVG()` with `GROUP BY` and `HAVING` clauses.
* **Data Filtering:** Conditional logic using `WHERE`, `LIKE`, and relational operators.
* **Sorting & Subsetting:** Advanced use of `ORDER BY` and `LIMIT` to extract top performers.

## 📂 Repository Contents
* `/queries/ipl_analysis_queries.sql`: Contains the complete production-ready SQL script with comprehensive comments documenting each query's objective.

## 📈 Sample Query Example
Below is an example of the logic used to evaluate cross-season boundary dominance ($4\text{s} + 6\text{s}$):

```sql
SELECT 
    Player, 
    (`4s` + `6s`) AS TotalBoundaries 
FROM 
    `men_IPL.2018_Batsmen` 
ORDER BY 
    TotalBoundaries DESC 
LIMIT 1;
