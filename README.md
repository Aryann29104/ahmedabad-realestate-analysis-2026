# 🏠 Ahmedabad Real Estate Analysis 2026

> Scraped, analysed, and visualised 1,105 live property listings across 10 Ahmedabad Diverse localities to answer one question: **where should you buy a flat in Ahmedabad in 2026?**

---

## 📌 Project Overview

Most real estate "analysis" projects use old Kaggle datasets. This one doesn't.

I scraped **live listings directly from MagicBricks** using Python, cleaned and stored the data in MySQL, ran SQL queries to extract business insights, and built an interactive 3-page Power BI dashboard covering the full end to end data analyst workflow.

**Localities covered:**
1. Prahlad Nagar
2. Bopal
3. Satellite
4. Sindhu Bhavan Road (SBR)
5. Thaltej
6. Naranpura
7. Chandkheda
8. Nikol
9. Khodiyar Nagar
10. Science City

<img width="1408" height="768" alt="Gemini_Generated_Image_fbgos3fbgos3fbgo" src="https://github.com/user-attachments/assets/05842fec-db35-4062-a838-42bba19ae734" />


---

## 🛠️ Tools & Technologies

| Layer | Tool |
|---|---|
| Data Collection | Python (BeautifulSoup, Requests) |
| Data Cleaning | Python (Pandas) |
| Database | MySQL (MySQL Workbench) |
| Analysis | SQL + Python |
| Visualisation | Power BI |
| Environment | Jupyter Notebook |

---

## 📁 Project Structure

```
ahmedabad-realestate-analysis/
│
├── ahmedabad_realestate.ipynb   ← Full notebook: scraping + cleaning + SQL + analysis
├── ahmedabad_clean.csv          ← Final clean dataset (1,105 listings)
├── screenshots/
│   ├── page1_city_overview.png
│   ├── page2_locality_deep_dive.png
│   └── page3_value_finder.png
└── README.md
```

---

## 🔄 Project Workflow

```
MagicBricks Website
       ↓
Python Scraper (BeautifulSoup)
       ↓
Raw CSV (1,283 listings)
       ↓
Data Cleaning (Pandas)
       ↓
Clean CSV (1,105 listings)
       ↓
MySQL Database
       ↓
SQL Analysis (4 queries)
       ↓
Power BI Dashboard (3 pages)
```

---

## 📊 SQL Analysis

### Query 1 — Best Value Locality (Cheapest → Costliest)

```sql
SELECT locality,
       ROUND(AVG(price_per_sqft), 0) AS avg_price_sqft
FROM ahmedabad_listings
GROUP BY locality
ORDER BY avg_price_sqft ASC;
```

**Result:**

| Rank | Locality | Avg ₹/sqft |
|---|---|---|
| 1 | Nikol | ₹4,758 |
| 2 | Khodiyar Nagar | ₹4,912 |
| 3 | Chandkheda | ₹4,986 |
| 4 | Bopal | ₹5,694 |
| 5 | SBR | ₹6,198 |
| 6 | Science City | ₹6,661 |
| 7 | Naranpura | ₹6,878 |
| 8 | Prahlad Nagar | ₹7,851 |
| 9 | Thaltej | ₹7,993 |
| 10 | Satellite | ₹8,603 |

---

### Query 2 — Market Activity (Most to Least Listings)

```sql
SELECT locality,
       COUNT(*) AS listing_count
FROM ahmedabad_listings
GROUP BY locality
ORDER BY listing_count DESC;
```

**Result:** Bopal leads with highest listing volume indicating strongest resale liquidity.

---

### Query 3 — Dominant BHK Type per Locality

```sql
SELECT locality,
       bhk,
       COUNT(*) AS count
FROM ahmedabad_listings
GROUP BY locality, bhk
ORDER BY locality, count DESC;
```

**Result:** 3BHK dominates 8 out of 10 localities. SBR and Thaltej are 4BHK dominant signalling a premium/luxury buyer profile in those corridors. While Nikol is the only 2BHK dominant locality indicating a first time/middle income market.

---

### Query 4 — Best 3BHK Under ₹80 Lakh

```sql
SELECT locality,
       ROUND(AVG(price_per_sqft), 0) AS avg_price_sqft,
       ROUND(AVG(area_sqft), 0)      AS avg_area_sqft,
       COUNT(*)                       AS listings
FROM ahmedabad_listings
WHERE bhk = 3
AND   price_lakh <= 80
GROUP BY locality
ORDER BY avg_price_sqft ASC;
```

**Result:** SBR offers the best value 3BHK under ₹80L at ₹4,332/sqft with average area of 1,267 sqft across 52 available listings.

---

## 💡 Key Insights

**Insight 1 — Price Gap**
> Satellite is **80.8% more expensive** per sqft than Nikol the widest price gap across all 10 localities analysed.

**Insight 2 — Best Value**
> Nikol offers ₹4,758/sqft, 45% cheaper than Satellite (₹8,603/sqft) for equivalent floor area.

**Insight 3 — Market Liquidity**
> Bopal is the most liquid market with the highest listing volume nearly 8x more active than Khodiyar Nagar, signalling stronger resale potential.

**Insight 4 — Luxury Corridors**
> SBR and Thaltej are the only localities where 4BHK dominates indicating a premium buyer profile concentrated in the western corridor.

**Insight 5 — Best Under ₹80L**
> For a 3BHK under ₹80L, SBR offers the best value at ₹4,332/sqft with avg area of 1,267 sqft across 52 listings.

---

## 🔗 [Ahmedabad Real Estate 2026 Dashboard](https://app.powerbi.com/links/G-WmxO8BbD?ctid=c30f7e5d-d78c-44b6-be17-02d4b3e5cd5c&pbi_source=linkShare)

---
## 📸 Dashboard Screenshots

### Page 1 — City Overview
<img width="838" height="474" alt="Screenshot 2026-05-19 at 10 06 50" src="https://github.com/user-attachments/assets/5cd45512-2e78-4fab-ada3-9bfffa6ccd68" />


### Page 2 — Locality Deep Dive
<img width="840" height="475" alt="Screenshot 2026-05-19 at 09 36 26" src="https://github.com/user-attachments/assets/5f07c746-6efc-4003-bdb2-719c656a90cf" />



### Page 3 — Value Finder
<img width="838" height="474" alt="Screenshot 2026-05-19 at 09 39 08" src="https://github.com/user-attachments/assets/b01f3c18-f81d-46a6-8e06-88272c031ab8" />


---

## 📂 Dataset

| Column | Description |
|---|---|
| locality | One of 10 Diverse Ahmedabad localities |
| locality_detail | Society/building name |
| bhk | Number of bedrooms (1–5) |
| price_lakh | Total price in lakhs (₹) |
| area_sqft | Carpet/built up area in sq.ft |
| price_per_sqft | Price per sq.ft (₹) |

**Source:** Live scraped from MagicBricks.com — May 2026
**Raw listings:** 1,283
**After cleaning:** 1,105

---

## ▶️ How to Run

**1. Clone the repo**
```bash
git clone https://github.com/Aryann29104/ahmedabad-realestate-analysis-2026.git
```

**2. Install dependencies**
```bash
pip install requests beautifulsoup4 pandas mysql-connector-python openpyxl
```

**3. Open the notebook**
```bash
jupyter notebook ahmedabad_realestate.ipynb
```

**4. Run cells in order**
- Cell 1–2: Imports and setup
- Cell 3–7: Scraping (skip if using provided CSV)
- Cell 8–9: Cleaning and analysis
- Cell 10: SQL queries

> **Note:** To skip scraping, use the provided `ahmedabad_clean.csv` 
> directly and start from Cell 8 onwards.
---

## 👤 Author

**Aryansinh Chauhan**
Aspiring Data Analyst - Ahmedabad, Gujarat
📧 chauhan.aryansinh29@gmail.com
🔗 (🔗 [LinkedIn](https://www.linkedin.com/in/aryansinh-chauhan-653105283))

---

*Data scraped May 2026. Prices reflect market listings at time of collection.*
