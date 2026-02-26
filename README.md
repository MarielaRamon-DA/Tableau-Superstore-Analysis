# 💰 Superstore Performance Analysis
## 🚀 Overview
This repository features a comprehensive Business Intelligence project developed in **Tableau**. It analyzes the performance of Superstore, a US-based retail business, to identify the critical drivers behind regional sales trends, profitability erosion, and customer lifecycle value. By transforming raw market data into strategic assets, this project provides a data-driven roadmap to reverse business contraction and optimize Superstore’s operations across the US market.

## 📊 Project Deliverables
This project provides a suite of four strategic deliverables designed for cross-departmental stakeholders, ranging from interactive data visualizations to a comprehensive record of the analytical process:
1. **Net Sales & Profit Performance Dashboard**
* **Strategic Focus:** Visualizes the "Profit-Sales Divergence" specifically observed in Q4 2014.
* **Target Audience:** Sales & Executive Leadership.
* **[View Live on Tableau Public](https://public.tableau.com/views/Superstore_DashboardNetSalesandProfitPerformance/NetSalesProfitPerformanceOverview?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**
2. **Customer Performance Dashboard**
* **Strategic Focus:** Employs **RFM Analysis** to segment the customer base by engagement and profitability.
* **Target Audience:** Marketing & Retention Teams.
* **[View Live on Tableau Public](https://public.tableau.com/views/CustomerRFMAnalysisDashboard/CustomerRFMAnalysis?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**
3. **Superstore Data Story**
* **Strategic Focus:** A multi-layered narrative that deconstructs performance from high-level trends down to root-cause assessments of revenue efficiency and financial health.
* **[View Live on Tableau Public](https://public.tableau.com/views/SuperstorePerformanceAnalysis_17562391489100/SuperstorePerformanceAnalysis?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**
4. **Final Analysis Report** 📄
* **Strategic Focus:** A comprehensive document recording the complete data analysis lifecycle **(Ask, Prepare, Process, Analyze, Share, Act)** to provide a detailed account of the project's evolution.
* **Target Audience:** Data Leadership & Project Stakeholders.
* **[Read the Full Report](https://github.com/MarielaRamon-DA/Tableau-Superstore-Analysis/edit/main/Final_Report.md)**

## 📋 Project Specifications
1. **Data Engineering & Preparation**
* Cleaned and transformed using Google Sheets.
* Feature Engineering: Created `IsReturned` via cross-referencing and defined `Net Sales` as revenue post-returns and discounts.
* COGS Proxy: In the absence of direct cost metrics, COGS was derived from the delta between Net Sales and Profit to isolate operational efficiency.
2. **RFM Methodology**
* Customers were segmented into High, Medium, and Low tiers using quartile-based distribution.
* **Recency:** Days since last transaction.
* **Frequency:** Total order volume.
* **Monetary:** Total profit contribution per customer.
3. **User Interface Tips**
* **Reset Filters:** Use `Ctrl + R` (Windows) or `Cmd + R` (Mac).
* **Optimization:** Designed for **1350 x 680** resolution; full-screen mode recommended.
## 💡 Strategic Insights
### 1. The Growth-Profitability Paradox
Consistent sales growth masks a **structural decline in efficiency**. Post-2014 data shows that while volume is increasing, margins are eroding due to rising returns and diminishing cost-to-revenue synergy.
### 2. Reactive Strategy Risks
Profitability is undermined by a reliance on aggressive, reactive discounting. This creates a cycle where high-volume segments (Consumer) are significantly less profitable than lower-volume, high-value segments (Corporate/Home Office).
## 🎯 Recommendations
### 1. Shift to Profit-Centric Incentives
Transition sales targets from gross volume to **profitability quotas**, encouraging the promotion of high-margin product categories.
### 2. Targeted Policy Optimization
Address regional "Profit Holes" by revising discount thresholds in high-loss states (e.g., Texas, Illinois) and optimizing return policies for underperforming subcategories like Binders and Tables.
### 3. High-Value Segment Retention
Prioritize retention resources for the Corporate and Home Office segments while implementing a "Value-Up" strategy to convert the Consumer segment into a profitable cohort.
## 🛠️ Tools & Technologies
* **Visualization:** Tableau Desktop / Public
* **Data Prep:** Google Sheets
* **Version Control:** Git / GitHub
## 📧 Connect
* **Tableau Public:** [Mariela Ramon Corria](https://public.tableau.com/app/profile/mariela.ramon.corria)
* **LinkedIn:** [Mariela Ramon](https://www.linkedin.com/in/mariela-ramon-6b368732b)
* **Email:** marielaramon7107@gmail.com
