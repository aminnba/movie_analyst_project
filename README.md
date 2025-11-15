# 🎬 Movie Success Analysis — End-to-End Data Project

> A full analytical workflow exploring what drives movie success using financial data, audience reception, and critic scores.

## 1. Project Overview

This project explores the financial and critical performance of movies using two datasets:
- **movies.csv** – box office, production, and audience variables  
- **movies_initial.csv** – IMDb and Metacritic metadata  

I approached this project as a learning analyst: focusing on structured thinking, cleaner methodology, and responsible interpretation — not just producing charts.

The analysis answers:
- What genres, budgets, directors, and casts tend to perform best?
- Do higher budgets actually deliver higher returns?
- Do critic scores (Metacritic) relate to profitability?
- How aligned are critics and audiences (Metacritic vs. IMDb)?
- How have movie trends evolved over time?
- How creative factors (writers) relate to success.

## 2. Project Structure

```
data/
   raw/          # Original datasets (from Kaggle & IMDb)
   cleaned/      # Cleaned + merged datasets

notebooks/
   main_notebook.ipynb

reports/
   figures/      # Exported plots
   tables/       # Exported summary tables

README.md
requirements.txt
```

## 3. Data Cleaning Summary

### 3.1 Key Tasks
- Convert dates → datetime  
- Parse genres, cast, and countries  
- Fix invalid budgets (huge ROI distortion)  
- Handle missing & zero budgets/revenue  
- Add quality flags:
  - `missing_critical`
  - `runtime_suspicious`
  - `financial_outlier`
  - `invalid_budget`

### 3.2 Why Cleaning Was Essential
Financial metrics are extremely sensitive to invalid entries.  
A budget of **$1 or $10** creates ROI values in the thousands, corrupting the analysis.

After cleaning:
- Avg ROI moved from **~2500×** (distorted) → **~7.5×** (realistic).
- Profitability estimates became meaningful.
- Genre/director/cast performance became interpretable.

## 4. Feature Engineering

Added:
- **profit** = revenue − budget  
- **roi** = profit / budget  
- **profit_margin** = profit / revenue  
- **audience_engagement** = vote_count × vote_average  
- **success_flag** = profit > 0  

These KPIs drive the entire Phase 1 analysis.

## 5. Phase 1 Analysis — Production & Financial Success

### 🔹 Genre Performance
- Horror, Mystery, and Documentary have the highest ROI.
- Comedy and Thriller deliver consistent success with large movie counts.

### 🔹 Budget Tiers
Budget bins reveal:
- <1M budgets can yield extreme ROI (low cost, high efficiency).
- Large budgets (100M+) offer safer success rate but lower ROI.

### 🔹 Directors
ROI tends to follow **genre consistency + low-budget efficiency**, not fame.

### 🔹 Cast Performance
High ROI cast members often appear in efficient genres (horror, indie, low-budget franchises).

## 6. Phase 2 — Merging IMDb & Metacritic Data

After light cleaning of df2:
- Titles standardized
- Writer cleaned with regex
- Year extracted
- Merged using (title, year)

Merge coverage:
- **Matched: 91.26%**
- **Metacritic coverage: 74%**

## 7. Phase 2 Analysis — Critics & Audience Success

### 🔹 Critics vs Financial Performance
Correlation between Metacritic and ROI:
- **Raw r = 0.02** (outliers distort)
- **Winsorized r = 0.19** (weak but positive)

Critics do *not* strongly predict ROI.

### 🔹 Critics vs Audience Alignment
Metacritic vs IMDb rating:
- **r = 0.75** → Strong alignment  
Critics and audiences generally agree on movie quality.

### 🔹 Creative Factors (Writers)
Top-performing writers often come from:
- Horror franchises
- Low-budget independent films
- Documentaries

Creative influence shows patterns similar to directors:  
**Efficiency + genre consistency** matter more than fame.

### 🔹 Trends Over Time (1980–2015)
Key patterns:
- ROI decreased over time (from ~4.5 → ~1.8)
- Audience ratings declined (7.5 → 6.2)
- Critic scores declined (68 → 48)
- Budgets increased steadily (3–4 × 10⁷ USD)
- Revenue increased slightly
  

## 8. My Analytical Takeaways (Personal Perspective)

This project helped me think more like an analyst:

- I learned to clean *before* analyzing.
- I saw how much outliers can mislead conclusions.
- I learned to evaluate what the data can and cannot answer.
- Adding a second dataset was not a convenience, it was necessary to answer critic-related questions properly.
- I realized interpretation matters as much as code.

This workflow reflects my growth when it comes to working with data:
**ask a clear question → validate data → analyze → interpret responsibly.**

## 9. Reproducibility

To reproduce:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/Main_notebook.ipynb
```

All datasets used in the analysis are stored under:
```
data/raw/
data/cleaned/
```

