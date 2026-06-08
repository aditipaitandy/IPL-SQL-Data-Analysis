# 🏏 Men's IPL (2018–2019) Data Analysis using SQL

An analytical deep dive into the 2018 and 2019 Indian Premier League (IPL) seasons. This project utilizes structured SQL queries to extract key performance indicators (KPIs) for batsmen and bowlers, evaluate team distributions, and track cross-season player consistency.

## 📊 Portfolio Presentation Deck

To make this technical analysis accessible to executive stakeholders, I have synthesized my findings into an insight-led slide deck.

[![View Portfolio Deck](https://img.shields.io/badge/View_Portfolio_Deck-PDF-FFB800?style=for-the-badge&logo=adobeacrobatreader&logoColor=black)](IPL_2018_2019_Analysis_Presentation.pdf)

*(Click the badge above to open the PDF slide deck directly in your browser via GitHub's native viewer!)*

# 🚀 Key Insights & SQL Implementations

## 1. The Volume Trap & Outlier Bias (Bowler Workloads)

**Analytical Goal:** Expose how lookups on raw averages can deceive decision-makers if workload volumes are ignored.

### Initial Query: Identifying bowlers with the absolute lowest runs conceded in 2018

```sql
SELECT Player, Runs
FROM `men_IPL.2018_Bowlers`
ORDER BY Runs
LIMIT 3;
```

### Query Output

| Row | Player       | Runs Conceded |
| --- | ------------ | ------------- |
| 1   | Pathan, Y K  | 14            |
| 2   | Short, D J M | 19            |
| 3   | Rana, N      | 44            |

### The Analytical Catch (Exposed via Workload Query)

```sql
SELECT Player, Overs
FROM `men_IPL.2018_Bowlers`
ORDER BY Overs ASC
LIMIT 5;
```

### Workload Output

| Row | Player       | Overs Bowled | Runs Conceded |
| --- | ------------ | ------------ | ------------- |
| 1   | Pathan, Y K  | 2.0          | 14            |
| 2   | Short, D J M | 3.0          | 19            |
| 3   | Rana, N      | 6.1          | 44            |

💡 **Deduction:** On paper, Yusuf Pathan and D'Arcy Short look like defensive masterminds. In reality, they bowled just 12 and 18 deliveries respectively. Evaluating bowlers using run suppression metrics without applying a threshold constraint (such as `Overs ≥ 10.0`) introduces heavy statistical bias.

---

## 2. High-Yield Bowler Identification (Strategic Defending)

**Analytical Goal:** Isolate premium, defensive anchor bowlers who maintain an exceptional economy rate while delivering consistent wickets.

### Filtering for bowlers with an Economy Rate (E_R) under 7.00 runs per over, sorted by wickets

```sql
SELECT Player, Wkts, E_R
FROM `men_IPL.2018_Bowlers`
WHERE E_R < 7
ORDER BY Wkts DESC;
```

### Query Output

| Row | Player           | Wickets | Economy Rate (E_R) |
| --- | ---------------- | ------- | ------------------ |
| 1   | Rashid Khan      | 21      | 6.74               |
| 2   | Bumrah, J J      | 17      | 6.89               |
| 3   | Mujeeb Ur Rahman | 14      | 6.99               |
| 4   | Ngidi, L         | 11      | 6.00               |

💡 **Deduction:** Rashid Khan and Jasprit Bumrah emerge as the premier defensive assets of the 2018 season—delivering high wicket volumes (21 and 17) while successfully suffocating run production under the elite 7.00 runs-per-over ceiling.

---

## 3. Multi-Season Stability (The Core Roster Anchor)

**Analytical Goal:** Run a relational mapping across separate seasonal database tables to find the single most consistent scoring anchor.

### Executing an INNER JOIN to aggregate runs across 2018 and 2019

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

### Query Output

| Row | Player     | Combined Runs (2018–2019) |
| --- | ---------- | ------------------------- |
| 1   | Rahul, K L | 1252                      |

💡 **Deduction:** K L Rahul represents the peak of batting longevity and stability over this 24-month period, contributing a massive 1,252 runs as a reliable top-order foundation.

---

## 4. Roster Density Analysis

**Analytical Goal:** Query team concentrations to identify active player squad density patterns in the 2019 batsmen dataset.

### Counting active batsmen registered across different franchise cohorts

```sql
SELECT Team, COUNT(Player) AS TotalCount
FROM `men_IPL.2019_Batsmen`
GROUP BY Team;
```

### Query Output

| Row | Team                        | Registered Batsmen |
| --- | --------------------------- | ------------------ |
| 1   | Chennai Super Kings         | 7                  |
| 2   | Kings XI Punjab             | 7                  |
| 3   | Rajasthan Royals            | 7                  |
| 4   | Royal Challengers Bangalore | 6                  |
| 5   | Mumbai Indians              | 6                  |
| 6   | Sunrisers Hyderabad         | 6                  |
| 7   | Kolkata Knight Riders       | 6                  |
| 8   | Delhi Capitals              | 5                  |

---

# 🛠️ Skills Demonstrated

### Relational Query Operations

INNER JOIN logic to merge historical datasets side-by-side.

### Data Aggregation & Filtering

Advanced utilization of GROUP BY, ORDER BY, LIMIT, and multi-conditional WHERE clauses.

### Data Integrity Checks

Identifying and resolving structural bias and statistical noise (e.g., small sample sizes distorting averages).

### Strategic Translation

Converting raw system outputs into operational recommendations for sports managers.

---

# 📬 Contact & Connections

**Name:** Aditi Paitandy

**LinkedIn:** Aditi Paitandy on LinkedIn

**Email:** [aditipaitandy2003@gmail.com](mailto:aditipaitandy2003@gmail.com)

**GitHub Repository:** IPL-SQL-Data-Analysis
