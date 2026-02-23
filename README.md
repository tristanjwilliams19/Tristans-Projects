# 🏀 March Madness Tournament Success Analysis (2024)

**Author:** Tristan Williams

**Project Type:** Sports Analytics | Predictive Analysis

**Tools:** SQL / Excel / Tableau

---

## 📌 Project Overview

The NCAA March Madness tournament is well known for its unpredictability and frequent upsets. Year after year the most dominant teams tend to "underperform" with the dark horses seeking triumphant cinderella victories. This project analyzes historical tournament and regular-season data to identify the statistical factors most strongly associated with championship success and potential upset outcomes.

The goal is to move beyond the narrative of “madness” and determine whether measurable performance indicators can meaningfully explain tournament outcomes.

[View Presentation](march-madness-analysis.pdf)

---

## 🎯 Objectives

This analysis focuses on two primary questions:

1. **Which metrics best indicate a team’s likelihood of winning March Madness?**
2. **Which statistical signals can help identify potential upset outcomes?**

---

## 🗂️ Dataset

* **Source:** NCAA / KenPom / Kaggle.com
* **Time Range:** 2013–2021 NCAA tournament and regular season data
* **Exclusions:**

  * 2020 tournament (cancelled due to COVID-19)
  * 2022–2023 used only for validation examples
* **Scope:** Tournament teams only

---

## ⚙️ Methodology

The analysis followed this workflow:

1. Exploratory analysis of team seedings vs. regular-season performance
2. Evaluation of key efficiency stat metrics
3. Historical review of championship team profiles
4. Identification of upset-team characteristics
5. Validation & Comparison using recent tournament winners

---

## 📊 Key Metrics Used

* **Effective Field Goal Percentage (EFG%)**
  Measues a team's shooting efficiency by adjusting weighting 3pt field goals 50% more valuable than regular field goals.

* **Two-Point Field Goal Percentage (2P%)**
  Measures finishing efficiency inside the arc(3-pt line).

* **Regular Season Wins**
  Proxy for overall team strength.

* **Wins Above Bubble (WAB)**
  Measures team performance relative to the NCAA tournament selection cutoff.

* **Seed**
  NCAA tournament ranking based on regular season performance and committee selection.

---

## 🗄 SQL Analysis

**📊 Query 1: Average Seed of Champions**

What seed typically wins the NCAA tournament?

```sql
SELECT AVG(seed) AS avg_champion_seed
FROM CBB
WHERE POSTSEASON = 'Champions';
```


**📊 Query 2: Identify Lower-Seed Teams Making Deep Runs**

How often do lower-seeded teams (9–16) advance past the Round of 64?

```sql
SELECT *
FROM CBB
WHERE (
    POSTSEASON = 'R32' AND SEED >= 9 OR
    POSTSEASON = 'S16' AND SEED >= 9 OR
    POSTSEASON = 'E8' AND SEED >= 9 OR
    POSTSEASON = 'F4' AND SEED >= 9
);
```


**📊 Query 3: Count of Champions in Dataset**

How many championship teams exist in the dataset?

```sql
SELECT COUNT(*) AS champion_count
FROM CBB
WHERE POSTSEASON = 'Champions';
```


**📊 Query 4: Frequency of Lower-Seed Upsets**

How frequently do Seeds 9–16 outperform expectations?

```sql
SELECT COUNT(*) AS upset_count
FROM CBB
WHERE (
    POSTSEASON = 'R32' AND SEED >= 9 OR
    POSTSEASON = 'S16' AND SEED >= 9 OR
    POSTSEASON = 'E8' AND SEED >= 9 OR
    POSTSEASON = 'F4' AND SEED >= 9
);
```


Reinforces the “Madness” narrative while still showing structural patterns
---

## 🔍 Key Findings

### 🥇 Championship Profile

Historical champions (2013–2021) typically share the following characteristics:

* Seeded between **1–7**
* At least **22 regular-season wins**
* **EFG% ≥ 50.6%**
* Strong strength-of-schedule indicators (WAB)

**Mean (AVG) championship seed:** 1.89

**Modal (Most frequent) champion seed:** #1 seed

👉 Interpretation: While upsets occur, championship winners still overwhelmingly come from highly ranked teams with elite efficiency metrics.

---

### 📈 Seeding Insights

* Strong negative correlation between seed number and regular-season wins
* #1 seeds average ~31 wins
* #16 seeds average ~18 wins
* Some mid-seeds (12–14) show strong 2P% efficiency, partially explaining first-round upset potential

---

### ⚠️ Upset Team Signals ("The Outcasts")

Teams seeded **9–16** that outperform expectations often show:

* High EFG%
* Strong win totals
* Efficient inside scoring

**Case Study:**
2018 Loyola Chicago (11 seed)

* EFG%: 57.7%
* Wins: 32
* Deep tournament run (Final Four)

However…

---

### 🧠 Why Elite Mid-Majors Still Fall Short

Wins Above Bubble (WAB) reveals the missing piece:

* Top championship teams (e.g., Duke, Villanova, Virginia) had **WAB ≥ 10**
* Loyola Chicago had **WAB = 2**

👉 Conclusion:
**Strength of competition matters significantly.**
Efficiency alone is not sufficient to predict championship success.

---

## ✅ Validation Check

Applying the model thresholds to a recent champion:

**2022 Champion: Kansas**

* Seed: 1
* Wins: 35
* EFG%: 53.8%

Kansas exceeded all identified championship benchmarks, supporting the model’s directional validity.

---

## 📌 Conclusions

### Objective 1 — Championship Predictors

The strongest indicators of tournament success:

* Seed
* Regular season wins
* Effective Field Goal %
* Wins Above Bubble
* Two-point FG %

No single metric guarantees success, but combinations significantly improve signal strength.

---

### Objective 2 — Upset Identification

Potential upset teams often exhibit:

* Above-average shooting efficiency
* Strong win totals relative to seed
* Undervalued mid-seed placement

However, tournament outcomes remain partially driven by matchup variance and randomness.

---

## ⚠️ Limitations

* Dataset limited to 2013–2021
* Tournament variance inherently high
* Model is descriptive, not fully predictive
* Seeding assumed to be correctly assigned
* Strength-of-schedule metrics limited by available data

---

## 🚀 Future Improvements

* Incorporate machine learning classification models
* Add matchup-level features
* Include player-level advanced metrics
* Build a bracket simulation tool
* Develop an interactive dashboard

---

## 📎 Executive Presentation

See the full slide deck:

**/presentation/March_Madness_Analysis.pdf**

---

## 🔗 References

* [March Madness Historical Data - Kaggle.com](https://www.kaggle.com/datasets/arnavs19/march-madness-historical-data-2012-2023)
* [WarrenNolan.com](https://www.warrennolan.com/basketball/2022/stats-adv-efg-percent)​
* [NCAA.com](https://www.ncaa.com/brackets/basketball-men/d1/2022)
* [Kenpom.com](https://kenpom.com/)

---

## 💡 Analytical Takeaway

Even in high-variance environments like March Madness, elite teams consistently share measurable efficiency and strength-of-schedule characteristics. While upsets remain part of the tournament’s appeal, data can meaningfully improve bracket strategy and team evaluation.

---

**Disclaimer:** This analysis is for analytical purposes only and is not gambling advice.
