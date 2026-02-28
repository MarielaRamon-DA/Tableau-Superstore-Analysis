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

## 💡 Business Questions & Strategic Insights

### 1. Growth Quality Assessment: Is our current expansion generating sustainable financial and customer value?
* **No.** **Sales Growth Masks Underlying Contraction.** Systemic patterns show a consistent upward trend in absolute sales and profit, but a fundamental contraction in profitability and efficiency.
    * **Profitability is eroding:** This is **fueled** by a contraction in sales growth and the systemic issue of returns.
    * **Efficiency is declining:** The synergy between revenue retention and direct cost efficiency broke down in 2014, indicating that growth is getting more expensive. Margins are shrinking even as sales increase, signaling a critical business contraction.
* **Customer Value is declining (CLV):** There is clear evidence that the long-term health of the customer base is deteriorating. This is specifically evident in the **Corporate** and **Home Office** segments, which have been the primary drivers of profit erosion. Despite the **RFM Analysis** identifying 12 combinations within the 'Other' segment with significant monetary potential (Medium to High), the current sales strategy fails to convert this potential into loyalty, leaving the base stagnant in a purely transactional and low-frequency state.

### 2. Diagnostic: Which specific factors are eroding our margins and customer value?
The **root cause** is a reactive sales strategy disconnected from long-term profitability. This creates a structural dependency where profit is a passive passenger of sales volume, leaving the business vulnerable to the following erosive factors:
* **Net Sales Contraction as a Catalyst:** The fundamental slowdown in sales growth serves as the primary trigger for profit erosion. Without an independent margin-protection strategy, this contraction disproportionately collapses profitability.
* **Price Policy Failures (State-Level):** Aggressive, reactive discounting to meet competitive pressure. This lack of "State Market Fit" suggests the business is "buying" revenue at the cost of its bottom line.
* **Sales Process Stress:** A 2014 **109% surge in returns**, suggesting operational failures—such as dispatch errors or excessive pressure to close sales—which degrades customer satisfaction and erodes margins through logistical overhead.
* **Aggressive Inventory Management:** A vicious cycle where sales decelerations trigger **deeper discounts** to move stock, further eroding the very margins the strategy **intended to protect**.

### 3. Behavioral Analysis: What is our customer base profile and behavior?
The customer base is currently suffering from a **"Loyalty Crisis"** and high geographic vulnerability, acting as a "transactional engine" rather than a loyalty builder.
* **Market Concentration Risk:** The customer base is highly localized, with a heavy concentration in only **8 key states**. To ensure future stability, the business must aggressively expand its market presence to reduce dependency on these specific territories.
* **Segment Responsibility for Contraction:** While the Consumer segment is the largest, the **Corporate and Home Office segments** carry the highest responsibility for the 2014 contraction in both Sales and Profit. High-volume contracts in these tiers are poorly calibrated, failing to yield proportional growth.
* **RFM Behavioral Evidence:** RFM analysis identifies "Value Destroyers" even among frequent buyers. The overwhelming concentration of customers in the **"Other" (Occasional)** segment—representing **60% of the base**—and the downward trend in **Customer Lifetime Value (CLV)** prove that the current architecture fails to migrate customers into Loyal or Champion tiers due to inefficient initial transactions and high return rates.

---

## 🎯 Strategic Recommendations

### 🤝 Sales & Marketing Structural Alignment
* **Action: Implement a "Value-Shield" in the CRM.** Integrate the CRM system to block automatic discounts for high-potential customers (*Loyal/Promising*) identified by Marketing, forcing Sales to compete on service excellence rather than price erosion.
* **Action: Establish State-Level Floor Pricing.** Implement automatic system blocks on discounts for critical subcategories **only in states where they show negative profit** (e.g., Texas, Illinois, Tennessee, North Carolina). This prevents localized losses from eroding regional margins.
* **Action: Create an Integrated Planning Committee (S&OP).** Reconcile real-time demand among Marketing, Sales, and Procurement to address the **sales contraction** of profitable products like *Copiers* and align inventory with financial targets.

### 🛒 Portfolio Management & Sourcing Re-engineering
* **Action: Optimize Sourcing for Critical Subcategories.** Replace current high-cost suppliers of subcategories with historical losses (e.g., *Tables, Bookcases*) with local providers to cut logistical expenses and restore category margins.
* **Action: "Profit-or-Exit" Catalog Policy.** Introduce high-margin "white-label" options. If a product cannot achieve profitability in a specific state after a supplier switch, it must be removed from that state’s active catalog.
* **Action: Strategic Regional Cooperation.** Facilitate a collaborative framework where high-performing regions mentor **Central and South** managers—who suffered the deepest contraction—through shared operational best practices.

### 📦 Operational Excellence & Return Mitigation
* **Action: Re-engineer Shipping for Complex Orders.** Implement a mandatory **Double-Validation Protocol** (Technical Checklist + Dispatch Audit) for Corporate and Home Office orders. This eliminates reverse logistics expenses and protects **Business Growth**.

### 📅 Market Expansion & RFM Migration
* **Action: Internal Market Expansion (The "Frequency Bridge").** Specifically target the **18 RFM sub-segments** within the "Other" category that exhibit High/Medium-Monetary potential. Offer service-based incentives (Priority Shipping, Dedicated Account Managers) conditioned on a second and third purchase within a **120-day window** to convert them into **Champions** or **Loyal** tiers.
* **Action: Geographic Penetration Plan.** Map out expansion into low-presence states by establishing **Local Warehouse Hubs** to neutralize high shipping costs in non-core centers.
## 🛠️ Tools & Technologies
* **Visualization:** Tableau Desktop / Public
* **Data Prep:** Google Sheets
* **Version Control:** Git / GitHub
## 📧 Connect
* **Tableau Public:** [Mariela Ramon Corria](https://public.tableau.com/app/profile/mariela.ramon.corria)
* **LinkedIn:** [Mariela Ramon](https://www.linkedin.com/in/mariela-ramon-6b368732b)
* **Email:** marielaramon7107@gmail.com
