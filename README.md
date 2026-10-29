# 📱 App Insights Unlocked: Google Play Store Analytics (Tableau)

> An end-to-end analytics case study on 9,600+ Google Play Store apps: data analysed and visualised in Tableau with calculated fields, parameters and two interactive dashboards. It answers 25 business questions using cleaned market data and helps identify what drives app success across categories and app types.

---

## 📌 Table of Contents
1. [Project Overview](#-project-overview)
2. [Business Problem](#-business-problem)
3. [Project Requirements](#-project-requirements)
4. [Dataset](#-dataset)
5. [Tools & Technologies](#-tools--technologies)
6. [Data Cleaning in Excel](#-data-cleaning-in-excel)
7. [Tableau Calculated Fields & Parameters](#-tableau-calculated-fields--parameters)
8. [Challenges Faced](#-challenges-faced)
9. [Key Insights](#-key-insights)
10. [Dashboard Overview](#-dashboard-overview)
11. [Key Recommendations](#-key-recommendations)
12. [Suggested Improvements](#-suggested-improvements)

---

## 🎯 Project Overview

This project was created to explore one of the most competitive digital markets: the Google Play Store. The goal was to turn a raw dataset of mobile apps into business-ready insights for understanding app performance, customer preferences, pricing behaviour, and category-level opportunities.

The analysis focused on identifying what contributes to an app's success and how product teams can use these findings to improve their own app strategy. Rather than just describing the market, the project also aims to support real business decisions — what categories to enter, what pricing strategy to use, what rating targets to aim for, and how to build more competitive app offerings.

The project combines data cleaning, business analysis, and dashboard storytelling to generate a complete analytics narrative from raw app records to strategic recommendations.

---

## 🎯 Business Problem
A mobile-app company has acquired Google Play Store data. Management wants to know:
- What factors contribute to an app's success (ratings, installs, reviews)?
- How can the company use those factors to improve its own apps?
- What do the data say about user preferences and behaviour?

**Stakeholders:** App Developers, Product Managers, Marketing Team, Senior Management (internal); App Users, Advertisers, Partners (external).

---

## ✅ Project Requirements

This project required a practical and structured analytical approach:

- Work with a real-world mobile app dataset from the Google Play Store.
- Clean and standardize inconsistent raw values before analysis.
- Understand key performance metrics such as installs, ratings, reviews, price, and size.
- Segment the market by category, app type, and value tiers.
- Build interactive dashboards that communicate insights clearly.
- Translate findings into actionable business recommendations.
- Ensure that conclusions are based on reliable, cleaned data rather than raw inconsistencies.

The project also required balancing technical accuracy with business clarity, so the final output could be understood by both analysts and decision-makers.

---

## 🗂 Dataset
- **Source:** [Kaggle: Google Play Store Apps](https://www.kaggle.com/datasets/lava18/google-play-store-apps?select=googleplaystore.csv)

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

## 🛠 Tools & Technologies
- **Microsoft Excel:** data cleaning and preparation
- **Tableau:** calculated fields, parameters, bins/bands, dual dashboards, interactive filters
- **Concepts:** data cleaning, KPI design, binned analysis, dashboard storytelling
- **Business Analytics:** market segmentation, app performance evaluation, growth opportunity analysis

These tools were selected because they are well-suited for turning raw business data into clear visual and strategic insights. Excel handled the heavy lifting of data preparation, while Tableau brought the outputs to life through interactive dashboards.

---

##  Data Cleaning

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

## Tableau Calculated Fields & Parameters

```text
-- Installs Number (from text, if needed)
FLOAT( REPLACE( REPLACE([Installs], ",", ""), "+", "") )

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

## ⚠️ Challenges Faced

This project involved several real-world data challenges:

1. **Inconsistent data formats**  
   Install counts, prices, size values, and dates appeared in varying formats that required structuring before analysis.

2. **Missing and invalid data**  
   Some data points were blank or corrupted, which could have distorted the findings if not handled carefully.

3. **Duplicate records**  
   Repeated app entries needed removal to avoid inflating install and review totals.

4. **Segmenting the market correctly**  
   A raw category list alone was not enough; additional groupings such as install tiers and price bands were needed for interpreting market behavior.

5. **Avoiding misleading conclusions**  
   Very small or low-volume apps could skew metrics like average rating, so thresholds like `Min Reviews` were implemented to improve analysis quality.

6. **Balancing simplicity and depth**  
   The dashboard needed to be easy for stakeholders to read while still supporting deeper analysis and filtering.

These challenges reinforced the importance of strong data preparation and thoughtful dashboard design.

---

## 📈 Key Insights

The analysis generated several important insights:

- The market includes more than **9,637 apps** across **33 categories**.
- Total installs reached **75.22 B**, indicating a massive and highly active mobile app ecosystem.
- **Free apps dominate** the market, with around **92.6%** available at no cost.
- **Games** and **Communication** categories lead in installs, showing strong user demand in entertainment and connectivity.
- The overall **average app rating is 4.17**, suggesting a generally positive user experience in the market.
- Around **6,282 apps** hold a rating of **4.0 or above**, indicating a large concentration of well-performing apps.
- Niche categories such as **Events**, **Art & Design**, and **Education** show strong average ratings, creating potential opportunity areas.
- Price does not necessarily destroy satisfaction in the mid-range; many apps continue to receive strong ratings at moderate price points.
- App size varies by category, and optimizing asset size is especially important for mobile-heavy app types such as games.
- Update frequency and freshness matter, as a large share of app performance is associated with recent maintenance and product evolution.

These insights show that successful apps are shaped by more than a single metric; they are influenced by a combination of product quality, pricing, category demand, review volume, and user experience.

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

## Conclusion

The Google Play Store Analytics project demonstrates how Tableau can be used to convert application data into interactive visualizations and business insights.

By analyzing installations, ratings, reviews, pricing, genres, and application sizes, the project helps identify performance patterns and areas for further investigation.

The analysis also highlights the importance of evaluating multiple indicators together. Ratings, popularity, and review volume provide different perspectives on application performance, while additional retention, revenue, and historical data would support stronger business decisions.

The resulting dashboards provide a foundation for exploring the app market, comparing applications, and identifying opportunities to improve product quality and user satisfaction.

Project: Google Play Store Analytics Dashboard
Tool: Tableau
Domain: App Market Analytics and Data Visualization
Dataset: Google Play Store Apps
