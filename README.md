# E-commerce Sales Analysis: Revenue Drivers and Customer Segments

## 📌 Overview
Analysis of 349,545 website sessions of an online furniture store over three months (1 Nov 2020 – 31 Jan 2021). The goal was to understand what drives revenue: which products, countries, channels and devices matter most, how sales change over time, and where the business can grow. The project covers the full cycle: SQL extraction, data cleaning, KPI calculation, segment and time analysis, correlation and hypothesis tests, and an interactive Tableau dashboard.

## 📈 Dashboard
[Open the interactive Tableau dashboard](https://public.tableau.com/views/portfolio_17931156253050/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

![E-commerce sales dashboard](images/dashboard.png)

## 📂 Data
- **Source:** Google BigQuery, project `data-analytics-mate`, dataset `DA`. Six tables (`session`, `session_params`, `account_session`, `account`, `order`, `product`) joined with `LEFT JOIN` from the sessions table.
- **Grain:** one row = one session (at most one purchased item per session; each registered account appears in one session).
- **Size:** 349,545 sessions, 23 columns (18 from SQL + 5 derived: `day_of_week`, `month_num`, `month_name`, `channel_grouped`, `user_type`).
- **File:** `data/portfolio.csv.gz` (compressed; read it directly with `pd.read_csv('data/portfolio.csv.gz', index_col=0)`).

## 🛠 Tools
Python (pandas, NumPy, matplotlib, seaborn, SciPy, statsmodels), SQL (BigQuery), Google Colab, Tableau Public

## 🔍 Methodology
1. **Extraction:** SQL query joining six tables into one session-level dataset.
2. **Cleaning and standardisation:** data types, `(not set)` and `<Other>` values unified, browser languages grouped, missing accounts marked as `guest`, duplicate check (none found).
3. **KPIs:** sessions, orders, revenue, conversion rate (CR), average and median order value, revenue per session.
4. **Segment analysis:** continent, country, product category, device, traffic channel, language.
5. **Time analysis:** daily and monthly revenue, day-of-week patterns, trends by channel and device.
6. **Pivot tables:** channel × device, category × country.
7. **Statistical tests:** Pearson correlation, Shapiro-Wilk, Wilcoxon, Kruskal-Wallis, two-proportion z-test.
8. **Visualisation:** interactive Tableau dashboard with filters and a metric selector.

## 📊 Key Findings
- **Overall:** 33,538 orders, $31.97M revenue, CR 9.59%, average order value $953 vs median $445. The gap shows that a small number of expensive items pulls the average up.
- **Products drive revenue:** Sofas & armchairs, Chairs and Beds bring 60.9% of revenue. Bookcases & shelving units lead by orders (22.8%) but give only 11.4% of revenue (average order $477), while Sofas have 12.8% of orders and 26.2% of revenue (average order $1,950).
- **Geography is concentrated:** the US gives 43.6% of revenue; together with India (8.8%) and Canada (7.6%) it reaches 60%. By continent: Americas 55.3%, Asia 23.8%, Europe 18.6%.
- **No weak segment:** across devices, channels and continents, CR stays at 9.2–9.8% and average order value at about $940–1,000. Differences in revenue come from traffic volume, not from conversion.
- **Devices and channels:** desktop 59.0% of revenue, mobile 38.7%, tablet 2.3%. Organic Search 35.8%, Paid Search 26.6%, Direct 23.4%.
- **Time:** December was the strongest month ($12.4M vs $9.9M in November). Revenue peaks on Tuesdays and Wednesdays and is lowest on weekends.
- **Guests vs registered users:** no significant difference in revenue per session (Wilcoxon, p = 0.134), so higher guest sales come from more sessions, not higher session value.
- **Organic share:** no significant difference between the Americas and Europe (z-test, p = 0.77).

## ⚠️ Data Quality Notes
- No orders were recorded from 28 to 31 January 2021, although sessions continued (about 2,800–4,100 per day). This is most likely a tracking failure. These days were excluded from correlation tests but kept in the overall KPIs, so January revenue and overall CR are slightly understated.
- 32.7% of sessions have no language, 6.1% have an "Undefined" channel, 0.8% have no country.
- Three months of data do not allow assessing annual seasonality.

## 💡 Recommendations
- Focus advertising on high-ticket categories (Sofas & armchairs, Chairs, Beds) and offer cheaper items as add-ons to raise the order value.
- Test marketing campaigns in Asia and Europe: conversion there is the same as in the Americas, so more traffic could bring proportional growth.
- Schedule promotions and newsletters early in the week and design separate weekend offers.
- Improve session tagging (language, channel, country, browser) and fix order tracking to make future analysis more reliable.

## 📁 Repository Structure
- `notebooks/` — Colab notebook with SQL extraction, analysis and conclusions (English and Ukrainian)
- `data/` — session-level dataset (compressed CSV)
- `images/` — dashboard screenshot

## 🚀 How to Run
The notebook is designed for Google Colab and reads data from BigQuery, which requires access to the source project. To reproduce the analysis without BigQuery, load `data/portfolio.csv.gz` with pandas and run the cells starting from the "Main Metrics" section.

## 👩‍💻 Author
Daria Shcherbak · [Tableau Public](https://public.tableau.com/app/profile/daria.shcherbak7028) · [LinkedIn]((https://www.linkedin.com/in/daria-shcherbak1/)) · email: shcherbakdasha11@gmail.com
