# 🟢 Basic-Level Questions

### Q1. What is the average rating of apps in the dataset?

**Answer:** The average rating is **4.17** out of 5.

**Insight:** Users are generally satisfied. New apps should aim to launch at or above ~4.2 to stand out.

---

### Q2. How many unique categories of apps are there?

**Answer:** There are **33 unique categories**.

**Insight:** The market is diverse. Smaller categories may offer less crowded opportunities for new apps.

---

### Q3. What is the distribution of app sizes? 📎

**Answer:** App sizes were grouped into **39 bins of ≈2.56 MB** each. The distribution is **right-skewed**: most apps are small (roughly under 20–30 MB), and the number of apps falls steadily as size grows, leaving a thin tail of very large apps.

**Insight:** Category matters. Tools average only **8.30 MB**, while Arcade (**39.34 MB**) and Action (**49.18 MB**) are several times heavier (see Q9). Size budgets should be set per category.

---

### Q4. How many free vs paid apps are there?

**Answer:**
| Type | Share of apps |
|---|---|
| Free | **92.62%** |
| Paid | **7.38%** |

**Insight:** The market is overwhelmingly free. Paid apps are a small niche, so a paid model needs strong differentiation and a free app should plan for ads or in-app purchases.

---

### Q5. What is the most common content rating?
📸 **Screenshot:**

<img width="1715" height="842" alt="Screenshot 2026-10-10 233313" src="https://github.com/user-attachments/assets/95926a64-1557-4330-af8a-870e08318d39" />


**Answer:** **Everyone** is by far the most common, with **7,883 apps (~82%)** (7,233 free + 650 paid).

**Insight:** Designing for "Everyone" reaches the broadest audience and avoids age-related restrictions.

---

### Q6. What are the top 5 most installed apps?
📸 **Screenshot:**


**Answer:** The table lists Facebook, WhatsApp Messenger, Instagram, Messenger – Text and Video Chat for Free, and Subway Surfers. Each is displayed as having 1B installs.

**Insight:** These apps are the benchmark for marketing and retention.

---

### Q7. How many apps have a rating of 4.0 and above?

**Answer:** **6,282 apps (~65%)** are rated 4.0 or higher.

**Insight:** About two-thirds of apps clear the 4.0 mark, so 4.0 is the minimum quality bar. Below it, an app is in the weaker third.

---

### Q8. What is the average number of reviews for free vs paid apps?
📸 **Screenshot:**

<img width="430" height="252" alt="Screenshot 2026-10-10 233504" src="https://github.com/user-attachments/assets/a3abf673-94d3-4477-9182-3a594a3f9e05" />

**Insight:** Free apps get **~27× more reviews** on average. Low friction means more users and more feedback. Paid apps should actively prompt satisfied users to review.

---

### Q9. What is the average app size for each category? 📎

**Answer:**
| Genre | Avg Size (MB) |
|---|---|
| Tools | 8.30 |
| Communication | 11.95 |
| Productivity | 12.06 |
| Photography | 15.78 |
| Video Players & Editors | 15.93 |
| Entertainment | 16.92 |
| Social | 17.31 |
| Casual | 32.84 |
| Arcade | 39.34 |
| Action | 49.18 |

**Insight:** Utility apps (Tools, Communication, Productivity) are light at about 8–12 MB, while games run 33–49 MB. Games need extra optimisation such as asset compression and on-demand downloads.

---

### Q10. How many apps were last updated in 2018?

📸 **Screenshot:**

<img width="1917" height="842" alt="Screenshot 2026-10-10 233301" src="https://github.com/user-attachments/assets/efe9e523-3fbf-4fad-abc7-bf72d1c13c8b" />


**Answer:** **6,271 apps (~65% of the dataset)** were last updated in 2018.

**Insight:** Most apps are actively maintained. Regular updates are the norm, and a stale app stands out as neglected.

---

# 🟡 Medium-Level Questions

### Q11. What is the correlation between installs and rating?

**Answer:** There is a **weak positive relationship**. Average rating rises from **4.10** (lowest install bin) to **4.39** at 100M+ installs, then eases to 4.38 at 500M and 4.22 at 1B+ (full bins in Q23).

**Insight:** Popular apps tend to be rated slightly higher, but installs alone don't guarantee quality.

---

### Q12. Which app categories have the highest average rating?

**Answer:**
| Rank | Category | Avg Rating |
|---|---|---|
| 1 | Events | 4.44 |
| 2 | Art & Design | 4.38 |
| 3 | Education | 4.36 |
| 4 | Books & Reference | 4.34 |
| 5 | Personalization | 4.33 |
| 6 | Parenting | 4.30 |
| 7 | Beauty | 4.28 |
| 8 | Game | 4.25 |

For the biggest categories in the Tableau view: Game 4.25 and Social 4.25 lead, Productivity and Family are 4.18, and Tools is lowest at 4.04.

**Insight:** Niche, purpose-driven categories (Events, Art & Design, Education) satisfy users most. High install volume does not mean high satisfaction.

---

### Q13. How does the price of an app affect its average rating?

📸 **Screenshot:**

<img width="1917" height="877" alt="Screenshot 2026-10-10 233435" src="https://github.com/user-attachments/assets/f90c9e4b-8985-4350-8df4-e539dacd8893" />

**Insight:** Ratings are **flat (~4.26–4.29) up to $20**, so charging more doesn't hurt satisfaction there. Beyond $20 the numbers swing (4.09 → 4.60 → 3.87), but these bands contain very few apps, so treat them as outliers. Value for money matters more than price level.

---

### Q14. How are ratings distributed across content ratings?

📸 **Screenshot:**

<img width="237" height="170" alt="image" src="https://github.com/user-attachments/assets/1e837f54-5436-469f-b4e9-e2b6d8ac439a" />

**Insight:** Differences are small (4.10–4.30), so content rating has little effect on satisfaction. Treat the 18+ and Unrated figures cautiously because of tiny sample sizes.

---

### Q15. Which genres have the most apps with over 1 million installs?

📸 **Screenshot:**

<img width="1917" height="832" alt="Screenshot 2026-10-10 233848" src="https://github.com/user-attachments/assets/ae5d42f4-f7d5-437c-bc7f-a4021ce3696f" />


**Insight:** Tools dominate the 1M+ club. Utility and entertainment genres are the most proven routes to scale.

---

### Q16. How frequently do apps get updated? (average time between updates)

**Answer:** The dataset has **only one `Last Updated` date per app**, so the gap between consecutive updates can't be calculated.

**Insight:** Collecting update history over time would be needed to measure true update frequency.

---

### Q17. What is the impact of app size on installs?

**Answer:** The scatter plot (app size vs number of apps) shows that **most apps cluster at small sizes** (about 5–25 MB), the count falls steadily past ~30 MB, and very large apps (60–80 MB+) are rare.

**Insight:** Teams usually keep apps lean. Size is closely tied to category: games are heavy while utilities are light (see Q9). To isolate size's direct effect on installs, compare average installs per size band within the same category.

---

### Q18. Which apps have the most reviews, and what are their ratings?


**Answer (Top 10):**
| App | Reviews | Rating |
|---|---|---|
| Facebook | 78.16M | 4.1 |
| WhatsApp Messenger | 69.12M | 4.4 |
| Instagram | 66.58M | 4.5 |
| Messenger | ~57M | 4.0 |
| Clash of Clans | 44.89M | 4.6 |
| Clean Master | 42.92M | 4.7 |
| Subway Surfers | 27.73M | 4.5 |
| YouTube | 25.66M | 4.3 |
| Security Master | 24.90M | 4.7 |
| Clash Royale | 23.14M | 4.6 |

**Insight:** The most-reviewed apps are **social/messaging apps and mobile games**. Social apps score lower (4.0–4.5) than games and cleaner/security utilities (4.5–4.7). Scale does not guarantee satisfaction.

---

### Q19. How does the content-rating distribution differ between free and paid apps?

**Answer:**
| Content Rating | Free | Paid |
|---|---|---|
| Everyone | 7,233 | 650 |
| Teen | 983 | 52 |
| Mature 17+ | 374 | 18 |
| Everyone 10+ | 290 | 31 |
| Adults only 18+ | 3 | — |
| Unrated | 2 | — |

**Insight:** Both types are dominated by "Everyone" (~81% of free vs ~87% of paid). Paid apps skew slightly more toward family-friendly content and have a smaller share of Teen apps.

---

### Q20. What are the top 5 categories by installs?

**Answer:**
| Rank | Category | Total Installs |
|---|---|---|
| 1 | Game | 13.46 B |
| 2 | Communication | 11.04 B |
| 3 | Tools | 8.00 B |
| 4 | Productivity | 5.79 B |
| 5 | Social | 5.49 B |

**Insight:** These five categories hold about **58% of all installs** (43.8 B of 75.2 B). Games and Communication alone account for roughly one-third.

---

# 🔴 Advanced-Level Questions

### Q21. Top 10 highest-rated apps: how do reviews and installs compare? 📎

**Answer:** After filtering for apps with more than 100K reviews, the top 10 all rate between 4.8 and 4.9. Learn Japanese, Korean... has a rating of 4.9, with 133.1K reviews and 1 million installs.
- JW Library has a rating of 4.9, with 922.8K reviews and 10 million installs.
- Six Pack in 30 Days has a rating of 4.9, with 272.3K reviews and 10 million installs.
- PewDiePie's Tuber Simulator has a rating of 4.8, with 1.5 million reviews and 10 million installs.
- DU Recorder has a rating of 4.8, with 2.6 million reviews and 50 million installs, making it the most reviewed and most installed app among the ten shown.


---

### Q22. Trend of app updates over time: any patterns?

📸 **Screenshot:**

<img width="1917" height="842" alt="Screenshot 2026-10-10 233301" src="https://github.com/user-attachments/assets/bfd825af-be99-4ea8-8348-39596a60f33a" />


**Answer:**
| Year | 2010 | 2011 | 2012 | 2013 | 2014 | 2015 | 2016 | 2017 | 2018 |
|---|---|---|---|---|---|---|---|---|---|
| Apps | 1 | 15 | 26 | 108 | 202 | 448 | 779 | 1,787 | 6,271 |

**Insight:** The curve is **exponential**, with 2018 alone having more than three times 2017's count. Because only the latest update is stored, this mostly reflects how recent the data is, and true seasonality needs the month-level view (`Update_Month`).

---

### Q23. How does average rating change with installs? (binned analysis)

**Answer:**
| Installs (bin) | Avg Rating |
|---|---|
| 0 | 4.10 |
| 100,000 | 4.12 |
| 500,000 | 4.17 |
| 1,000,000 | 4.22 |
| 5,000,000 | 4.23 |
| 10,000,000 | 4.30 |
| 50,000,000 | 4.33 |
| 100,000,000 | 4.39 |
| 500,000,000 | 4.38 |
| 1,000,000,000 | 4.22 |

**Insight:** Ratings **climb steadily with popularity up to 100M installs** (4.10 → 4.39). Great apps earn more installs, and installs bring more feedback to improve the app. At the 1B+ level the average falls back to 4.22, since mass-market apps are harder to please.

---

### Q24. Sentiment analysis on app reviews
**Answer:** **Not possible with this file.** `googleplaystore.csv` holds review *counts*, not review *text*. The same Kaggle dataset has `googleplaystore_user_reviews.csv`, which could be used for a future sentiment analysis.

---

### Q25. Relationship between genre and rating

**Answer (average / median rating):**
| Genre | Avg | Median |
|---|---|---|
| Comics | 4.80 | 4.80 |
| Music | 4.53 | 4.60 |
| Strategy | 4.53 | 4.55 |
| Tools | 4.50 | 4.50 |
| Puzzle | 4.37 | 4.40 |
| Simulation | 4.35 | 4.30 |
| Arcade | 4.35 | 4.50 |
| Sports | 4.35 | 4.40 |
| Action | 4.32 | 4.30 |
| Education | 4.31 | 4.40 |
| Communication | 4.20 | 4.20 |
| Books & Reference | 4.20 | 4.20 |
| Lifestyle | 4.15 | 4.15 |

**Sub-genres:** Brain Games 4.36 · Creativity 4.31 · Action & Adventure 4.29 · Education 4.27 · Pretend Play 4.24 · Music & Video 4.23.

**Insight:** Entertainment and creative genres (Music, Strategy, Puzzle, Comics) are consistently rated highest, and mean and median agree. Communication, Books & Reference and Lifestyle sit lowest. Comics' very high score likely rests on a small number of apps, so treat it with caution.
