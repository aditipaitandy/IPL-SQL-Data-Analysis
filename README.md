# 🏏 Men's IPL (2018–2019) SQL Data Analysis

An analytical deep dive into the 2018 and 2019 Indian Premier League (IPL) seasons. This project utilizes structured SQL queries to extract key performance indicators (KPIs) for batsmen and bowlers, evaluate team distributions, and track cross-season player consistency.

[![View Portfolio Deck](https://img.shields.io/badge/View_Portfolio_Deck-PDF-FFB800?style=for-the-badge\&logo=adobeacrobatreader\&logoColor=black)](IPL_2018_2019_Analysis_Presentation.pdf)

---

## 📊 Portfolio Presentation Deck

To make this technical analysis accessible to executive stakeholders, I have synthesized my findings into an insight-led slide deck.

*(Click the badge above to open the PDF slide deck directly in your browser!)*

---

# 🚀 Key Insights & SQL Implementations

## 1. The Volume Trap & Outlier Bias

**Analytical Goal:** Expose how lookups on raw averages can deceive decision-makers if workload volumes are ignored.

**Deduction:** On paper, players like Yusuf Pathan look like defensive masterminds. However, evaluating bowlers using run suppression metrics without applying a threshold constraint (such as `Overs >= 10.0`) introduces heavy statistical bias.

```sql id="0n52it"
/* Identifying bowlers with minimal workload to avoid bias */
SELECT Player, Overs, Runs
FROM `men_IPL.2018_Bowlers`
ORDER BY Overs ASC
LIMIT 5;
```

---

## 2. High-Yield Bowler Identification

**Analytical Goal:** Isolate premium, defensive anchor bowlers who maintain an exceptional economy rate while delivering consistent wickets.

**Deduction:** Rashid Khan and Jasprit Bumrah emerged as the premier defensive assets of the 2018 season—delivering high wicket volumes while successfully suffocating run production under the elite 7.00 RPO ceiling.

```sql id="jlr6qq"
SELECT Player, Wkts, E_R
FROM `men_IPL.2018_Bowlers`
WHERE E_R < 7
ORDER BY Wkts DESC;
```

---

## 3. Multi-Season Stability (The Roster Anchor)

**Analytical Goal:** Map historical data across separate tables to find the single most consistent scoring anchor.

**Deduction:** K.L. Rahul represents the peak of batting longevity, contributing a massive 1,252 runs as a reliable top-order foundation over a 24-month period.

```sql id="yqsrz4"
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

---

# 🛠️ Skills Demonstrated

### Relational Query Operations

INNER JOIN logic to merge historical datasets side-by-side.

### Data Aggregation & Filtering

Advanced GROUP BY, ORDER BY, LIMIT, and multi-conditional WHERE clauses.

### Data Integrity

Identifying and resolving structural bias (e.g., small sample sizes distorting averages).

### Strategic Translation

Converting raw SQL outputs into operational recommendations for sports management.

---

# 💼 Recruiter Quick-Start Kit

If you are a recruiter looking to share or review this work, feel free to use the following:

## Recruiter-Focused Summary

> "Data is meaningless without a business context. I don't just query databases; I extract strategic answers. This project showcases my ability to clean disparate IPL datasets, join multi-year tables in BigQuery, and translate performance metrics into executive-ready insights."

---

## LinkedIn Caption

**How do you build a championship-winning IPL franchise? 🏏📊**

Most sports franchises make the mistake of overpaying for peak single-season performers. Using Google BigQuery, I analyzed player statistics across the 2018–2019 IPL seasons to uncover the hidden signals of multi-year consistency.

Check out my full case study below!

👉 Portfolio: https://github.com/aditipaitandy

👉 Connect with me: https://www.linkedin.com/in/aditi-paitandy-750629317

#DataAnalytics #SQL #BigQuery #SportsAnalytics #BusinessIntelligence #DataStorytelling #IPLAnalytics #DataAnalystJobs

---

# 📬 Contact

**Aditi Paitandy**

🔗 LinkedIn: https://www.linkedin.com/in/aditi-paitandy-750629317

💻 Portfolio & GitHub: https://github.com/aditipaitandy

📧 Email: [aditipaitandy2003@gmail.com](mailto:aditipaitandy2003@gmail.com)
