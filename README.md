# Project Title: Superstore Sales & Profitability Analysis with Tableau

## 🚀 Overview

This repository showcases a comprehensive Business Intelligence project developed using Tableau, centered on the foundational Superstore dataset. The goal is to transform raw sales data into actionable insights for strategic decision-making, focusing on performance, profitability, and customer behavior.

## 📊 Project Design

This project includes the following interactive Tableau visualizations, designed for various business stakeholders:

1.  **Net Sales & Profit Performance Overview Dashboard:**
    * **Description:** This high-level executive dashboard offers a comprehensive view of `Net Sales` and `Profit` performance. It presents **diverse trend charts, including forecasting scenarios**, analyzed across **State Level, Product Category, and Sub-Category**. Primarily **oriented towards Sales Department stakeholders**, it serves as an instrument to **show and explore the critical divergence between sales growth and profitability specifically observed in November-December 2014**, providing a clear overview for strategic discussions.
    * **View Live on Tableau Public:** [(https://public.tableau.com/views/Superstore_DashboardNetSalesandProfitPerformance/NetSalesProfitPerformanceOverview?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)]
          
2.  **Customer Performance Dashboard:**
    * **Description:** This dashboard provides an in-depth exploration of customer behavior and value, primarily **intended for Marketing Department stakeholders**. It features **RFM (Recency, Frequency, Monetary) analysis** to segment customers, revealing their purchasing patterns, engagement levels, and overall profitability. This allows for the development of targeted marketing campaigns, customer retention strategies, and identification of high-value segments.
    * **View Live on Tableau Public:** [(https://public.tableau.com/views/CustomerRFMAnalysisDashboard/CustomerRFMAnalysis?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)]

3. ### Superstore Data Story
**Description:** An interactive narrative that guides users through a multi-layered analytical design, shifting **from high-level performance to granular detail**. The story is structured around four core analytical pillars:

* **Hierarchical Performance Decomposition:** Establishing **Sales & Profit trends** across **Location and Product hierarchies**.
* **Root Cause Analysis & Profitability Assessment:** A deep-dive into underperformance patterns linked to **different views combination** and  **Customer Satisfaction**.
* **Interactive Customer Strategy & Segment Analysis:** Utilizing key metrics (**Profit Margin, Discount, Returns**), Customer Performance KPI's, and scenarios (**Location, Product**) to measure segment performance and determine **Customer Expansion**.
* **Revenue Efficiency & Financial Health Assessment:** The final assessment of operational efficiency and financial health.
  
The narrative culminates in a summary of **Key Insights** derived from these analytical pillars, providing actionable, data-driven **Recommendations** for strategic business impact.

   * **View Live on Tableau Public:** [View Live](https://public.tableau.com/views/SuperstorePerformanceAnalysis_17562391489100/SuperstorePerformanceAnalysis?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
    
## 📋 Project Specifications

1.  **Data Preparation**
    * The original database was clean, with all data preparation performed in Google Sheets. A new field, IsReturned, was added by cross-referencing returned items from a separate    sheet. To ensure an accurate representation of revenue, the Net Sales field was calculated to represent the final revenue after subtracting both returns and any dollar discounts. The Order Date field was split into separate fields for analysis. The prepared data was then connected directly to Tableau for visualization.

    * Due to the lack of specific cost measures in the database, such as cost of shipment or storage, a general term for **COGS** was used in the **Critical Divergence Profit-Net Sales Dashboard for November and December of 2014**. For this analysis, COGS was inferred directly from the available data by subtracting profit from Net Sales, as returns and discounts were analyzed separately.

2.  **RFM Analysis Ranges**
    * **The RFM value ranges (High, Medium, Low)** were determined by dividing customers into three groups based on the middle points between quartiles, reflecting the distribution of the data.

    * For each case of the **RFM analysis**, the following measures were used for the quartile calculations:

         **Recency**: The number of days since a customer's last purchase.

         **Frequency**: The total number of orders a customer has made.

         **Monetary Value**: The total profit generated from a customer's purchases.

3.  **Hotkeys**
**Ctrl + R** (Windows/Linux) or **Cmd + R** (Mac): Restores all filters to their default state.


## 🛠️ Tools & Technologies

* **Data Visualization:** Tableau Desktop / Tableau Public
* **Data Source:** Superstore Sample Dataset (included with Tableau)
* **Version Control:** Git / GitHub


## 📧 Connect with Me

* **Tableau Public Profile:** [(https://public.tableau.com/app/profile/mariela.ramon.corria)]
* **LinkedIn:** [www.linkedin.com/in/mariela-ramon-6b368732b]
* **Email:** [marielaramon7107@gmail.com]

