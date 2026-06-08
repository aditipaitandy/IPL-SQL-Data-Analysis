🏏 Men's IPL (2018–2019) Data Analysis using SQLAn analytical deep dive into the 2018 and 2019 Indian Premier League (IPL) seasons. This project utilizes structured SQL queries to extract key performance indicators (KPIs) for batsmen and bowlers, evaluate team distributions, and track cross-season player consistency.📊 Portfolio Presentation DeckTo make this technical analysis accessible to executive stakeholders, I have synthesized my findings into an insight-led slide deck.(Click the badge above to open the PDF slide deck directly in your browser via GitHub's native viewer!)🚀 Key Insights & SQL Implementations1. The Volume Trap & Outlier Bias (Bowler Workloads)Analytical Goal: Expose how lookups on raw averages can deceive decision-makers if workload volumes are ignored.-- Initial Query: Identifying bowlers with the absolute lowest runs conceded in 2018
SELECT Player, Runs 
FROM `men_IPL.2018_Bowlers` 
ORDER BY Runs 
LIMIT 3;
Query Output:RowPlayerRuns Conceded1Pathan, Y K142Short, D J M193Rana, N44The Analytical Catch (Exposed via Workload Query):-- Investigating the workload (overs bowled) for these "defensive" outliers
SELECT Player, Overs 
FROM `men_IPL.2018_Bowlers` 
ORDER BY Overs ASC 
LIMIT 5;
Workload Output:RowPlayerOvers BowledRuns Conceded1Pathan, Y K2.0142Short, D J M3.0193Rana, N6.144💡 Deduction: On paper, Yusuf Pathan and D'Arcy Short look like defensive masterminds. In reality, they bowled just 12 and 18 deliveries respectively. Evaluating bowlers using run suppression metrics without applying a threshold constraint (such as $Overs \ge 10.0$) introduces heavy statistical bias.2. High-Yield Bowler Identification (Strategic Defending)Analytical Goal: Isolate premium, defensive anchor bowlers who maintain an exceptional economy rate while delivering consistent wickets.-- Filtering for bowlers with an Economy Rate (E_R) under 7.00 runs per over, sorted by wickets
SELECT Player, Wkts, E_R 
FROM `men_IPL.2018_Bowlers` 
WHERE E_R < 7 
ORDER BY Wkts DESC;
Query Output:RowPlayerWicketsEconomy Rate (E_R)1Rashid Khan216.742Bumrah, J J176.893Mujeeb Ur Rahman146.994Ngidi, L116.00💡 Deduction: Rashid Khan and Jasprit Bumrah emerge as the premier defensive assets of the 2018 season—delivering high wicket volumes (21 and 17) while successfully suffocating run production under the elite $7.00$ runs-per-over ceiling.3. Multi-Season Stability (The Core Roster Anchor)Analytical Goal: Run a relational mapping across separate seasonal database tables to find the single most consistent scoring anchor.-- Executing an INNER JOIN to aggregate runs across 2018 and 2019
SELECT 
  a.Player, 
  (SUM(a.Runs) + SUM(b.Runs)) AS CombinedRuns 
FROM `men_IPL.2018_Batsmen` AS a 
INNER JOIN `men_IPL.2019_Batsmen` AS b 
  ON a.Player = b.Player 
GROUP BY a.Player 
ORDER BY CombinedRuns DESC 
LIMIT 1;
Query Output:RowPlayerCombined Runs (2018-2019)1Rahul, K L1252💡 Deduction: K L Rahul represents the peak of batting longevity and stability over this 24-month period, contributing a massive 1,252 runs as a reliable top-order foundation.4. Roster Density AnalysisAnalytical Goal: Query team concentrations to identify active player squad density patterns in the 2019 batsmen dataset.-- Counting active batsmen registered across different franchise cohorts
SELECT Team, COUNT(Player) AS TotalCount 
FROM `men_IPL.2019_Batsmen` 
GROUP BY Team;
Query Output:RowTeamRegistered Batsmen1Chennai Super Kings72Kings XI Punjab73Rajasthan Royals74Royal Challengers Bangalore65Mumbai Indians66Sunrisers Hyderabad67Kolkata Knight Riders68Delhi Capitals5🛠️ Skills DemonstratedRelational Query Operations: INNER JOIN logic to merge historical datasets side-by-side.Data Aggregation & Filtering: Advanced utilization of GROUP BY, ORDER BY, LIMIT, and multi-conditional WHERE clauses.Data Integrity Checks: Identifying and resolving structural bias and statistical noise (e.g., small sample sizes distorting averages).Strategic Translation: Converting raw system outputs into operational recommendations for sports managers.📬 Contact & ConnectionsName: Aditi PaitandyLinkedIn: Aditi Paitandy on LinkedInEmail: aditipaitandy2003@gmail.comGitHub Repository: IPL-SQL-Data-Analysis
