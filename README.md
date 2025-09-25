# Project Title: Superstore Sales & Profitability Analysis with Tableau

## 🚀 Overview

This repository showcases a comprehensive Business Intelligence project developed using Tableau, centered on the foundational Superstore dataset. The goal is to transform raw sales data into actionable insights for strategic decision-making, focusing on performance, profitability, and customer behavior.

## 📊 Key Dashboards & Story

This project includes the following interactive Tableau visualizations, designed for various business stakeholders:

1.  **Net Sales & Profit Performance Overview Dashboard:**
    * **Description:** This high-level executive dashboard offers a comprehensive view of `Net Sales` and `Profit` performance. It presents **diverse trend charts, including forecasting scenarios**, analyzed across **State Level, Product Category, and Sub-Category**. Primarily **oriented towards Sales Department stakeholders**, it serves as an instrument to **show and explore the critical divergence between sales growth and profitability specifically observed in November-December 2014**, providing a clear overview for strategic discussions.
    * **View Live on Tableau Public:** [(https://public.tableau.com/views/Superstore_DashboardNetSalesandProfitPerformance/NetSalesProfitPerformanceOverview?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)]
          
2.  **Customer Performance Dashboard:**
    * **Description:** This dashboard provides an in-depth exploration of customer behavior and value, primarily **intended for Marketing Department stakeholders**. It features **RFM (Recency, Frequency, Monetary) analysis** to segment customers, revealing their purchasing patterns, engagement levels, and overall profitability. This allows for the development of targeted marketing campaigns, customer retention strategies, and identification of high-value segments.
    * **View Live on Tableau Public:** [(https://public.tableau.com/views/CustomerRFMAnalysisDashboard/CustomerRFMAnalysis?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)]

3.  **Superstore Data Story:**
    * **Description:** An interactive narrative guiding users through key findings and insights derived from the Superstore data, connecting various visualizations into a cohesive story of business performance.
    * **View Live on Tableau Public:** [(https://public.tableau.com/shared/8BYHQH9TX?:display_count=n&:origin=viz_share_link)]
    
## 📋 Project Specifications

1.  **Data Preparation**
The original database was clean, with all data preparation performed in Google Sheets. A new field, IsReturned, was added by cross-referencing returned items from a separate sheet. To ensure an accurate representation of revenue, the Net Sales field was calculated to represent the final revenue after subtracting both returns and any dollar discounts. The Order Date field was split into separate fields for analysis. The prepared data was then connected directly to Tableau for visualization.

Due to the lack of specific cost measures in the database, such as cost of shipment or storage, a general term for **COGS** was used. For this analysis, COGS was inferred directly from the available data by subtracting profit from Net Sales, as returns and discounts were analyzed separately in the Critical Divergence Profit-Net Sales Dashboard for November and December of 2014.

3.  **RFM Analysis Ranges**
The RFM value ranges (High, Medium, Low) were determined by dividing customers into three groups based on the middle points between quartiles, reflecting the distribution of the data.

For each case of the **RFM analysis**, the following measures were used for the quartile calculations:

**Recency**: The number of days since a customer's last purchase.

**Frequency**: The total number of orders a customer has made.

**Monetary Value**: The total profit generated from a customer's purchases.

3.  **Hotkeys**
**Ctrl + R** (Windows/Linux) or **Cmd + R** (Mac): Restores all filters to their default state.


## 🛠️ Tools & Technologies

* **Data Visualization:** Tableau Desktop / Tableau Public
* **Data Source:** Superstore Sample Dataset (included with Tableau)
* **Version Control:** Git / GitHub

## 💡 Key Insights (Optional - you can expand on your findings here)

* Identified a critical divergence between sales growth and profit margins in specific periods (e.g., Nov-Dec 2014).
* Pinpointed sub-categories and product segments contributing most significantly to profit erosion.
* Analyzed the impact of discount strategies and return rates on overall profitability.

## 📧 Connect with Me

* **Tableau Public Profile:** [Link to your Tableau Public Profile]
* **LinkedIn:** [Link to your LinkedIn Profile]
* **Email:** [Your Email Address]

## © License

[Optional: e.g., MIT License if you want to allow others to use your code/files, or state "All Rights Reserved" if you prefer.]
