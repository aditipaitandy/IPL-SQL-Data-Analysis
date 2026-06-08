# 🏏 IPL Data Analysis (2018–2019) Using SQL

## 📌 Project Overview

This project analyzes player and team performance across the 2018 and 2019 Indian Premier League (IPL) seasons using SQL. By leveraging structured queries, I explored batting and bowling statistics, identified performance trends, and uncovered insights that can support data-driven decision-making in sports analytics.

The analysis focuses on extracting meaningful KPIs, evaluating player consistency across seasons, identifying statistical outliers, and translating raw data into actionable insights.

---

## 🎯 Objectives

* Analyze batting and bowling performances using SQL.
* Identify high-performing players based on multiple metrics.
* Compare player consistency across seasons.
* Detect statistical biases caused by small sample sizes.
* Generate business-style insights from sports datasets.

---

## 🛠️ Technologies Used

* SQL (Google BigQuery)
* Data Analysis
* Aggregations & Filtering
* Joins
* Sports Analytics

---

# 📊 Key Insights & SQL Analysis

## 1️⃣ The Volume Trap: Why Context Matters

### Analytical Goal

Identify bowlers who conceded the fewest runs during the 2018 season.

### SQL Query

```sql
SELECT Player, Runs
FROM `men_IPL.2018_Bowlers`
ORDER BY Runs
LIMIT 3;
```

### Result

| Player       | Runs Conceded |
| ------------ | ------------- |
| Pathan, Y K  | 14            |
| Short, D J M | 19            |
| Rana, N      | 44            |

At first glance, these players appear to be the most economical bowlers.

### Validation Query

```sql
SELECT Player, Overs
FROM `men_IPL.2018_Bowlers`
ORDER BY Overs ASC
LIMIT 5;
```

### Insight

The analysis revealed that these bowlers had delivered very few overs:

| Player       | Overs Bowled |
| ------------ | ------------ |
| Pathan, Y K  | 2.0          |
| Short, D J M | 3.0          |
| Rana, N      | 6.1          |

### Key Finding

Low run totals alone can be misleading. Bowlers with extremely small workloads may appear highly effective despite limited participation.

**Recommendation:** Apply workload thresholds (e.g., Overs ≥ 10) before evaluating bowling efficiency.

---

## 2️⃣ Identifying Elite Defensive Bowlers

### Analytical Goal

Find bowlers who combined wicket-taking ability with exceptional economy rates.

### SQL Query

```sql
SELECT Player, Wkts, E_R
FROM `men_IPL.2018_Bowlers`
WHERE E_R < 7
ORDER BY Wkts DESC;
```

### Result

| Player           | Wickets | Economy Rate |
| ---------------- | ------- | ------------ |
| Rashid Khan      | 21      | 6.74         |
| Bumrah, J J      | 17      | 6.89         |
| Mujeeb Ur Rahman | 14      | 6.99         |
| Ngidi, L         | 11      | 6.00         |

### Key Finding

Rashid Khan and Jasprit Bumrah emerged as the most effective defensive bowlers, maintaining elite economy rates while consistently taking wickets.

---

## 3️⃣ Cross-Season Consistency Analysis

### Analytical Goal

Determine the most consistent run-scorer across both IPL seasons.

### SQL Query

```sql
SELECT
    a.Player,
    (SUM(a.Runs) + SUM(b.Runs)) AS CombinedRuns
FROM `men_IPL.2018_Batsmen` AS a
INNER JOIN `men_IPL.2019_Batsmen` AS b
ON a.Player = b.Player
GROUP BY a.Player
ORDER BY CombinedRuns DESC
LIMIT 1;
```

### Result

| Player     | Combined Runs |
| ---------- | ------------- |
| Rahul, K L | 1252          |

### Key Finding

K. L. Rahul was the most consistent batter across the two seasons, accumulating 1,252 runs and demonstrating sustained top-order performance.

---

## 4️⃣ Team Roster Density Analysis

### Analytical Goal

Analyze player distribution across IPL franchises in 2019.

### SQL Query

```sql
SELECT Team,
       COUNT(Player) AS TotalCount
FROM `men_IPL.2019_Batsmen`
GROUP BY Team;
```

### Result

| Team                        | Registered Batsmen |
| --------------------------- | ------------------ |
| Chennai Super Kings         | 7                  |
| Kings XI Punjab             | 7                  |
| Rajasthan Royals            | 7                  |
| Royal Challengers Bangalore | 6                  |
| Mumbai Indians              | 6                  |
| Sunrisers Hyderabad         | 6                  |
| Kolkata Knight Riders       | 6                  |
| Delhi Capitals              | 5                  |

### Key Finding

Most franchises maintained similar squad distributions, while Delhi Capitals had the smallest representation within the dataset.

---

# 💡 Skills Demonstrated

### SQL & Data Analysis

* Complex filtering using WHERE clauses
* Aggregations with COUNT(), SUM(), and GROUP BY
* Sorting and ranking using ORDER BY and LIMIT
* Relational analysis using INNER JOIN

### Analytical Thinking

* Identifying misleading statistical patterns
* Detecting outliers and sample-size bias
* Converting data into business insights

### Data Storytelling

* Translating SQL outputs into actionable recommendations
* Presenting technical findings in a stakeholder-friendly format

---

## 🚀 Key Takeaway

This project demonstrates how SQL can be used not only to retrieve data but also to uncover meaningful patterns, validate assumptions, and support strategic decision-making through sports analytics.

---

## 📬 Connect With Me

**Aditi Paitandy**

* LinkedIn: [www.linkedin.com/in/aditi-paitandy](http://www.linkedin.com/in/aditi-paitandy)
* Email: [aditipaitandy2003@gmail.com](mailto:aditipaitandy2003@gmail.com)
* GitHub: github.com/aditipaitandy

If you found this project interesting, feel free to ⭐ the repository and connect with me.
