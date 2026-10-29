# 📱 App Insights Unlocked: Google Play Store Analytics (Tableau)

> An end-to-end analytics case study on 9,600+ Google Play Store apps: data analysed and visualised in **Tableau** with calculated fields, parameters and two interactive dashboards. It answers 25 business questions (basic → advanced) and ends with recommendations for an app-development company.


---

## 📌 Table of Contents
1. [Business Problem](#-business-problem)
2. [Dataset](#-dataset)
3. [Tools & Skills](#-tools--skills)
4. [Data Cleaning in Excel](#-data-cleaning-in-excel)
5. [Tableau Calculated Fields & Parameters](#-tableau-calculated-fields--parameters)
6. [Dashboard Overview](#-dashboard-overview)
7. [Basic-Level Questions](#-basic-level-questions)
8. [Medium-Level Questions](#-medium-level-questions)
9. [Advanced-Level Questions](#-advanced-level-questions)
10. [Key Recommendations](#-key-recommendations)

---

## 🎯 Business Problem
A mobile-app company has acquired Google Play Store data. Management wants to know:
- What factors contribute to an app's success (ratings, installs, reviews)?
- How can the company use those factors to improve its own apps?
- What do the data say about user preferences and behaviour?

**Stakeholders:** App Developers, Product Managers, Marketing Team, Senior Management (internal); App Users, Advertisers, Partners (external).

---

## 🗂 Dataset
- **Source:** [Kaggle: Google Play Store Apps](https://www.kaggle.com/datasets/lava18/google-play-store-apps?select=googleplaystore.csv)
- **Raw file:** `googleplaystore.csv` → **Cleaned file (Excel):** `googleplaystore_looker_clean.csv`
- **After cleaning:** **9,637 apps** across **33 categories**

| Column | Description |
|---|---|
| App | Name of the app |
| Category | Category of the app |
| Rating | Average user rating (0–5) |
| Reviews | Number of user reviews |
| Size | Size of the app |
| Installs | Number of installs (e.g. 1,000+) |
| Type | Free or Paid |
| Price | Price of the app |
| Content Rating | Age group the app is appropriate for |
| Genres | Genre(s) of the app |
| Last Updated | Date of last update |
| Current Ver | Current version |
| Android Ver | Minimum Android version required |

---

## 🛠 Tools & Skills
- **Microsoft Excel:** data cleaning and preparation
- **Tableau:** calculated fields, parameters, bins/bands, dual dashboards, interactive filters
- **Concepts:** data cleaning, KPI design, binned analysis, dashboard storytelling

---

## 🧹 Data Cleaning 

| Step | What I did | Why |
|---|---|---|
| **Missing values** | Checked every column; handled missing Rating, Type and other blanks | Prevents distorted averages |
| **Remove duplicates** | Removed duplicate app rows | Avoids double-counting installs and reviews |
| **Remove corrupted row** | Deleted the row whose columns were shifted | It produced a fake category value |
| **Installs → numeric** | Removed `+` and `,` → new column `Installs_Num` | Needed for sums and bins |
| **Reviews → numeric** | Converted to `Reviews_Num` | Needed for sums and averages |
| **Price → numeric** | Removed `$` → `Price_USD` | Needed for price analysis |
| **Size → MB** | Converted `k`/`M` text to `Size_MB` | Needed for size analysis |
| **Standardise text** | Cleaned Category names (underscores removed, title case, `AND` → `&`) and trimmed Genres | Consistent labels |
| **Date formatting** | Converted `Last Updated` to a date and extracted `Update_Year`, `Update_Month` | Trend analysis |
| **Helper columns** | Created `Install_Tier` and `Rating_4Plus` flag | Faster analysis in Tableau |

---

## 🧮 Tableau Calculated Fields & Parameters

```text
-- Installs Number (from text, if needed)
FLOAT( REPLACE( REPLACE([Installs], ",", ""), "+", "" ) )

-- Size MB
IF RIGHT([Size],1) = "M" THEN FLOAT(LEFT([Size], LEN([Size])-1))
ELSEIF RIGHT([Size],1) = "k" THEN FLOAT(LEFT([Size], LEN([Size])-1)) / 1024
ELSE NULL END

-- Is Rated 4+  /  Apps With Rating 4+
IF [Rating] >= 4 THEN 1 ELSE 0 END
SUM(IF [Rating] >= 4 THEN 1 ELSE 0 END)

-- Installs Bin
IF [Installs Number] < 100000 THEN "0–100K"
ELSEIF [Installs Number] < 500000 THEN "100K–500K"
ELSEIF [Installs Number] < 1000000 THEN "500K–1M"
ELSEIF [Installs Number] < 5000000 THEN "1M–5M"
ELSEIF [Installs Number] < 10000000 THEN "5M–10M"
ELSEIF [Installs Number] < 50000000 THEN "10M–50M"
ELSEIF [Installs Number] < 100000000 THEN "50M–100M"
ELSEIF [Installs Number] < 500000000 THEN "100M–500M"
ELSEIF [Installs Number] < 1000000000 THEN "500M–1B"
ELSE "1B+" END

-- Price Band
IF [Price USD] = 0 THEN "Free"
ELSEIF [Price USD] < 5 THEN "$0.99–$4.99"
ELSEIF [Price USD] < 10 THEN "$5–$9.99"
ELSEIF [Price USD] < 20 THEN "$10–$19.99"
ELSEIF [Price USD] < 50 THEN "$20–$49.99"
ELSEIF [Price USD] < 100 THEN "$50–$99.99"
ELSE "$100+" END

-- Size Band (null-safe)
IF ISNULL([Size MB]) THEN "Varies with device"
ELSEIF [Size MB] < 5 THEN "0–5 MB"
ELSEIF [Size MB] < 10 THEN "5–10 MB"
ELSEIF [Size MB] < 25 THEN "10–25 MB"
ELSEIF [Size MB] < 50 THEN "25–50 MB"
ELSEIF [Size MB] < 75 THEN "50–75 MB"
ELSE "75–100 MB" END

-- Primary Genre (split "Education;Pretend Play")
TRIM( SPLIT([Genres], ";", 1) )

-- Reviews Filter (uses parameter Min Reviews = 1000)
[Reviews] >= [Min Reviews]

-- Rating Score (rank by rating, tie-break by reviews)
MAX([Rating]) * 100000000 + MAX([Reviews])
```

**Parameter:** `Min Reviews` (default **1,000**) lets users set a minimum review count so tiny apps with a perfect 5.0 don't dominate "highest rated" lists.

---

## 📊 Dashboard Overview

**Dashboard 1: APP INSIGHTS (executive summary)**

| KPI | Value |
|---|---|
| Total Installs | **75.22 B** |
| Total Apps | **9,637** |
| Avg. Rating | **4.17** |
| Categories | **33** |
| Apps With Rating 4+ | **6,282** |

Visuals: Apps Distribution (Free vs Paid), Content Rating: Free vs Paid heatmap, Top 5 Categories By Installs, Updates Trend.

<img width="600" height="400" alt="Screenshot 2026-10-10 230959" src="https://github.com/user-attachments/assets/21689c0c-18fd-43dc-aee4-bcd8cc6dacbc" />


**Dashboard 2:** Most Reviewed Apps · Price vs Avg Rating · Total Apps By Installs · Size vs Installs

<img width="700" height="500" alt="Screenshot 2026-10-10 232522" src="https://github.com/user-attachments/assets/375fbebf-79e9-4efb-9922-afb10aae5800" />


---



---

## 🚀 Key Recommendations
1. **Target proven demand:** Game and Communication each exceed 11 B installs, and the top 5 categories hold ~58% of all installs.
2. **Look for niche opportunities:** Events, Art & Design and Education have the highest average ratings, a sign of satisfied users in less crowded spaces.
3. **Launch at 4.2+:** the market average is 4.17 and about 65% of apps are rated 4.0+.
4. **Go free-first:** 92.6% of apps are free, and free apps collect ~27× more reviews. Monetise through ads or in-app purchases.
5. **Price for value, not level:** ratings stay ~4.26–4.29 up to $20, so premium pricing doesn't hurt satisfaction when the app delivers.
6. **Optimise size by category:** keep utilities near 8–12 MB, and compress assets for games (33–49 MB average).
7. **Design for "Everyone":** ~82% of apps use this rating, giving the widest reach.
8. **Keep apps fresh and benchmark with volume:** about two-thirds of apps were updated in 2018, and comparisons should use apps with 1,000+ reviews (the `Min Reviews` parameter).

---
