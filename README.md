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

## 📋 Methodology: Data Analysis Lifecycle
This project is structured around a six-phase analytical framework to ensure data-driven decision-making and technical rigor:

* **Ask (Define):** Defining the business challenge and identifying the core questions that drive the analysis. This phase involves understanding stakeholder expectations and establishing clear, measurable objectives.
* **Prepare (Collect & Describe):** Sourcing the data and performing a comprehensive technical description of the dataset. This includes evaluating data integrity using the **ROCCC** standard and documenting the metadata and variables.
* **Process (Clean & Transform):** Executing data hygiene through cleaning, normalization, feature engineering, and documenting to ensure the dataset is accurate, consistent, and ready for advanced calculation.
* **Analyze (Discover):** Utilizing various analytical techniques—such as **Trend Analysis**, **Forecasting**, **Statistical Modeling**, and **Behavioral Segmentation**—to identify patterns, correlations, and root causes.
* **Share (Communicate):** Interpreting the results and translating complex data into intuitive, high-impact visualizations and narratives tailored for diverse stakeholders.
* **Act (Recommend):** Providing evidence-based conclusions and actionable strategic recommendations to solve the initial business problem.
  
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
## 🎯 Business Questions & Strategic Insights

This analysis addresses four core pillars of the Superstore business model, moving from high-level growth quality to specific operational diagnostics.

### 1. Growth Quality Assessment: Is our current expansion generating sustainable financial and customer value?
* **Analysis:** **No.** Systemic patterns show a consistent upward trend in absolute sales and profit, but a fundamental contraction in profitability and efficiency.
    * **Profitability is eroding:** This is **fueled** by a contraction in sales growth and the systemic issue of returns.
    * **Efficiency is declining:** The synergy between revenue retention and direct cost efficiency broke down in 2014, indicating that growth is getting more expensive. Margins are shrinking even as sales increase, signaling a critical business contraction.
    * **Customer Value is declining (CLV):** There is clear evidence that the long-term health of the customer base is deteriorating, shifting from loyal engagement to discount-driven transactions.

### 2. Diagnostic: Which specific drivers are eroding our margins and customer value?
* **Analysis:** The primary **driver** is a reactive sales strategy disconnected from long-term profitability, manifested through:
    * **Price Policy Failures:** Aggressive, reactive discounting to meet competitive pressure (lack of regional Market Fit).
    * **Sales Process Stress:** A **109% surge in returns**, suggesting errors in dispatch or excessive pressure during the sales cycle, which degrades customer satisfaction.
    * **Aggressive Inventory Management:** A cycle where sales slowdowns trigger higher discounts, further eroding the margins they intended to protect.

### 3. Behavioral Analysis: What is our customer base profile and behavior?
* **Analysis:** The current model prioritizes short-term transactions over lifecycle value. **RFM Analysis** identifies a "Frequency Gap" within the "Other" segment: 55% of these customers possess high monetary potential but lack recurring engagement. This confirms the base is responsive to aggressive discounts but is not being retained through a sustainable strategy.

### 4. Strategic Sustainability: Is our current Sales & Marketing architecture optimized for the long term?
* **Analysis:** **No.** The architecture is heavily "Volume-Centric." Sustainability requires a fundamental shift: moving from gross sales targets to **Net Profitability Quotas** and re-engineering regional logistics to mitigate the impact of returns and erratic pricing.
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
