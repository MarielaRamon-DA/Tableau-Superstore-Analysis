# 📂 Final Project: Superstore Sales & Customer Strategic Analysis
## 1. Business Task (Ask)

**The objective of this analysis** is to evaluate Superstore’s performance across a 4-year horizon (2011–2014) to establish a data-driven roadmap for 2015. This project treats the data not just as a series of transactions, but as a Trading Lifecycle that requires a balance between volume and fiscal health.

To guide the analysis, the project was framed around four critical business inquiries:

**Financial Integrity: Is our growth healthy?**

**Diagnostic: Which specific drivers are eroding our margins and customer value?**

**Behavioral Analysis: What is our customer behavior based on RFM analysis?**

**Strategic Sustainability: Is our current Sales & Marketing architecture optimized for the long term?**

To ensure the insights are actionable across the organization, the project provides four distinct deliverables tailored to the specific needs of key stakeholders:

| Stakeholder | Deliverable | Strategic Objective |
| :--- | :--- | :--- |
| **CEO** | Sales & Profit KPI Dashboard | Provide a high-level "Health Check". |
|**Marketing Manager** | RFM Behavioral Dashboard | Enable precise customer targeting and conversion strategies for the "Other" segment. |
|**Board of Directors** | Strategic Data Story (2014-2015) | Present the financial narrative required to approve the 2015 budget and strategic pivot. |
|**Technical Lead** | Final Analytical Report | Document the methodology, midpoint calculations, and data integrity for peer review. |

## 2. Data Sources Description (Prepare) 
### Data Storage & Organization

**Primary Source:** The dataset was sourced from the Tableau Public Sample Data Repository.

**Specific Dataset:** Sample - Superstore.csv (Standardized Edition).

**Direct Access Link:**  (Historical Archive).

**Local Repository:** A copy of this .csv file is stored in the **/data/raw/** directory of this GitHub repository to ensure the reproducibility of the 2015 Strategic Audit.

**Time Horizon:** 4 years of transactional data **(January 1, 2011 – December 31, 2014)**.

The dataset consists of a single spreadsheet organized into three relational sheets. The data is organized in Long Format.

**1. Returns**: A relational table used to audit transaction success. It contains two columns:

`Returned`: A string indicator ('Yes').

`Order ID`: The unique identifier used to link returns to the 'OrdersClean' sheet.

**2. People**: A secondary reference table defining regional governance. It contains:

`Person`: The Regional Manager (Stakeholder) responsible for the area.

`Region`: The geographic territory (East, West, Central, South).

**3. OrdersClean**: The primary transaction table containing **9,994 unique records** covering the United States market. Each row represents a unique Transaction ID per Product, allowing for granular time-series and categorical analysis. It follows a denormalized flat-file structure organized into **three primary dimensions**.

* **1. Temporal Dimension (The "When")**
   Key Variables: `Order Date`, `Ship Date`.

* **2. Geographic Dimension (The "Where")**
   Key Variables: `Country`, `Region`, `State`, `City`, `Postal Code`.

* **3. Categorical Dimension (The "What")**
   Key Variables: `Category`, `Sub-Category`, `Product Name`.

In addition to the dimensions above, the database contains the `Customer Segment`, the `shipping mode`, and the **Quantitative Measures** (the Facts) that we use for our calculations: **Financial Facts:** `Sales`, `Quantity`, `Discount`, `Profit`.

### Bias, Credibility, and Integrity (ROCCC Analysis)

To verify the data’s suitability for a strategic audit, I assessed it against the ROCCC standards:

**Reliable:** The data is a standardized public dataset commonly used for retail modeling; however, it is a synthetic business scenario.

**Original:** Public domain (Superstore Sample Data).

**Comprehensive:** It contains all necessary fields (Sales, Profit, Quantity, Discount, Geography) to calculate RFM and profitability trends.

**Current:** While the data covers 2011–2014, it remains relevant for demonstrating the analytical framework for the 2015 fiscal year.

**Cited:** Sourced from public business data repositories.

### Licensing, Privacy, & Security

**Licensing:** Open-source public data.

**Privacy & Security:** The dataset contains no Personally Identifiable Information (PII). Customer names are associated with generic IDs, ensuring compliance with data privacy standards (GDPR/CCPA simulation).

**Accessibility:** All files are hosted in this GitHub repository for transparency and peer review.

### Integrity Verification
I verified the data integrity by performing a Cross-Field Audit:

**Mathematical Consistency:** Checked for anomalies in the Discount column.

**Date Alignment:** Ensured all Order Dates fall within the 2011–2014 range with no gaps in the 48-month period.

**Deduplication:** Confirmed no duplicate Row IDs were present.

### Alignment with Business Questions
This data provides the raw financial metrics (Sales/Profit) needed to answer the Financial Integrity question and the customer-level transactional history required to calculate the RFM midpoints for behavioral analysis.

### Data limitations
**1. Absence of COGS (Cost of Goods Sold)**
While the dataset provides a Profit column, it lacks a dedicated COGS or Unit Cost field.

**Impact:** We cannot perform a Gross Margin vs. Net Margin analysis. We must assume the Profit column is a pre-calculated Net Profit, which limits our ability to see exactly where production costs end and operational costs begin.

**2. Shipping Cost Transparency**
In many versions of the Superstore dataset, the Shipping Cost is either missing or bundled into the profit calculation without a separate breakdown for every transaction.

**Impact:** We cannot isolate if a "Negative Profit" order was due to a high discount (Marketing) or expensive shipping (Logistics).

**3. Lack of Customer Demographics**
The data provides Geography (State/City) but lacks Customer Age, Gender, or Income.

**Impact:** Our RFM Analysis remains purely behavioral. We can tell what they did, but not who they are, which limits the Marketing Manager's ability to create demographic-based personas for 2015.

## 3. Data Cleaning & Manipulation (Process) 

### **Tools & Rationale**
* **Google Sheets:** Used as the primary ETL tool for row-level cleaning, relational logic, and calculating core financial metrics in the `OrdersClean` sheet.
* **Tableau:** Utilized for data profiling, metadata validation, and the creation of three distinct analytical workbooks.
* **Reasoning:** Processing calculated fields in Google Sheets ensures a consistent "Source of Truth" that feeds into Tableau, ensuring that Net Sales and Return logic are locked before visualization.

### **Detailed Cleaning & Transformation Steps (Google Sheets)**

1. **Relational Logic for Returns:**
   Instead of a standard lookup, I used a conditional counting method in the `OrdersClean` sheet to identify returned transactions.
   * **Formula:** `=IF(COUNT.IF(Returns!OrderId_Range; OrdersClean!OrderId) > 0; 1; 0)`
   * **Result:** This created the binary field **`IsReturned`**, where **1** indicates the Order ID exists in the Returns sheet, and **0** indicates a successful transaction.

2. **Creation of Calculated Columns:**
      * **`Net_Sales`:** Calculated to reflect actual revenue after discounts and excluding returns.
     * **Formula:** `=IF(IsReturned=0; Sales * (1-Discount); 0)`
   * **`Profit_Margin`:** Calculated as IF(Net Sales = 0; 0; `[Profit] / [Net Sales]` .

3. **Data Quality Audits:**
   * **Null Value Handling:** I used the **Filter** command to scan the dataset and identified one **null value** in the "Product Description" field. I manually corrected this record to ensure categorical consistency.
   * **Deduplication:** I used the **"Data > Data Cleanup > Remove Duplicates"** tool on the `Row ID` column. The tool confirmed that all 9,994 records are unique.
   * **Whitespace Cleaning:** I applied **"Data > Data Cleanup > Trim Whitespace"** to ensure all text strings were clean for Tableau’s filters and mapping engine.

### **Profiling & Final Verification (Tableau)**
* **Metadata Check:** Upon connecting the Google Sheet, I verified that Tableau correctly assigned **Geographic Roles** (globe icon) to `Postal Code` and `State`.
* **Temporal Integrity:** I confirmed that `Order Date` was recognized as a Date format (calendar icon).
* **Zero-Unknown Audit:** I verified the status indicator in Tableau to ensure **"0 Unknowns"** remained after the cleaning process, confirming the dataset is "Clean and Ready."

## 4. Analysis Summary (Analyze)

###  Strategic Data Organization

The analytical phase was organized around three pillars as follows. These interactive visualizations leverage Tableau’s native resources to facilitate a deep-dive tailored to the specific interests of the stakeholders identified in Section 1, ensuring each business question is answered through a specialized lens.

#### **Pillar 1: Sales & Profit Performance Dashboard**
A 360-degree view of business health was established, prioritizing **Functional Interactivity** to allow for the monitoring of performance across the 2011–2014 period.

* **Hierarchical Structuring:** Custom hierarchies were defined for **Location** (`Country` > `Region` > `State` > `City`) and **Category** (`Category` > `Sub-Category` > `Product`). This structure was implemented to allow for deep-dive root cause analysis of underperforming areas.
* **Global & Parametric Control:** * **Global Filter:** The `Order Date` was established to ensure temporal consistency across all visualizations.
    * **Dynamic Selectors:** Through the use of `Select Filter View` and `Trend Chart Selector` parameters, the workspace can be toggled between geographic/categorical views and switched between Growth, Efficiency, and Predictive (Forecasting) metrics.
* **Executive KPIs:** Real-time benchmarks were integrated into the dashboard footer, including: `Total Net Sales`, `Profit`, `AOV`, `Net Sales to Gross Sales Ratio`, and `Direct Cost to Net Sales Ratio`.

#### **Pillar 2: Customer RFM Analysis Dashboard**
Transactional data was transformed into behavioral segments (such as Champions, Hibernating, and At Risk) to serve marketing stakeholders.

* **Strategic Purpose:** This segmentation was designed to move beyond standard demographics (`Consumer`, `Corporate`, `Home Office`) to reveal the **behavioral health** of the customer base. This enables the strategic allocation of the 2015 budget by identifying which "At Risk" customers require re-engagement.
* **Interactive Filtering:** * **Segment Bar Graphs:** Customer distribution is visualized by Marketing Segment and specific RFM combinations. 
    * **Profit-Driven Heat Map:** Both bar graphs act as filters for a centralized Heat Map. A 4th dimension—**Profit**—was introduced via color coding to identify whether high-spending individuals are contributing positively to the bottom line.

#### **Pillar 3: The Data Story (Executive Focus)**
Findings from the preceding dashboards were synthesized into a **Tableau Story**. The narrative was focused on the 2014 performance challenges to provide evidence-based recommendations aimed at mitigating financial issues for the 2015 fiscal year.

### Analytical Logic & Calculated Fields

To transition from raw data to actionable insights, several custom calculations were authored within Tableau. These fields were categorized to support Descriptive, Diagnostic, and Predictive analysis, ensuring a rigorous evaluation of business efficiency and stakeholder needs.

### **Performance KPI Framework & Efficiency Metrics**
A baseline for business health was established using specific metrics designed to quantify operational efficiency and the impact of returns:

* **Net Sales to Gross Sales Ratio:** This metric was implemented to measure the efficiency of finalized transactions after accounting for returns:
  `SUM([Net Sales]) / SUM([Sales])`
* **Direct Cost to Revenue Ratio:** This field was developed to visualize the weight of operational costs against realized revenue:
  `(SUM([Net Sales]) - SUM([Profit])) / SUM([Net Sales])`
* **Sales Weighted Average Discount:** To understand the true impact of pricing strategies, a weighted calculation was applied to avoid distortion by low-volume transactions:
  `IF SUM([Net Sales]) != 0 THEN SUM([Discount] * [Sales]) / SUM([Net Sales]) ELSE 0 END`
* **Average Order Value (AOV) & Unique Customers:** These were utilized to monitor transaction quality and provide a baseline for behavioral analysis using `COUNTD([Customer Name])`.

### **Statistical Validation and Calibration of RFM Thresholds**
To ensure the behavioral segmentation was grounded in the actual distribution of the 2011-2014 data, a descriptive statistical summary was performed.

* **Methodology:** The distribution was analyzed using **Quartile Measures**. For the `Monetary_Value` dimension, the benchmarks identified were: **Lower Quartile (Q1): 864**, **Median (Q2): 1,736**, and **Upper Quartile (Q3): 3,026**.
* **Threshold Calibration:** Boundary values for the `High`, `Medium`, and `Low` ranges were derived from the midpoints between these quartiles and further calibrated to align with data density. For instance, the **High** threshold for `Monetary_Value` was set at **2,380**, while the **Medium** threshold was adjusted to **1,050** to better capture emerging customer clusters.

### **Behavioral Segmentation (RFM Logic)**
A behavioral model was constructed to transform transactional history into actionable segments. This was achieved through a multi-conditional calculation:

* **RFM Score Concatenation:** A combined string was generated to visualize the full behavioral profile: 
  `[Recency_Range] + " | " + [Frequency_Range] + " | " + [Monetary_Value_Range]`
* **Customer Segment Logic:** Customers were assigned to groups such as **Champions**, **Loyal Customers**, and **At-Risk**. This allows for the strategic allocation of the 2015 budget by identifying which groups require re-engagement and which drive the highest profitability.

### **Diagnostic & Predictive Analysis**
* **Growth Metrics:** `Monthly` and `Quarterly Revenue Growth Rates` were applied to identify volatility during seasonal troughs (February and October).
* **Time-Series Forecasting:** Tableau’s native exponential smoothing models were applied to generate a **1-year forecast**, providing stakeholders with a statistical baseline for 2015 expectations.

### **Trends, Patterns, and Relationships**

This section documents the observed trajectories and mathematical correlations identified across the 2011–2014 period. These data points establish the baseline for the subsequent diagnostic findings.

#### **Temporal and Seasonality Trends**
* **Consistent Upward Trend:** A baseline upward trajectory exists in global sales and profit from 2011 to 2014. Growth is concentrated in the **second semester**, specifically in **Q4**.
* **Fixed Seasonality:** Peaks occur in **March, September, and November**, with recurring troughs in **February and October**. 
* **General Upward Trend in Returns and Discounts:** Both variables show a consistent increase, with peaks aligned with sales highpoints in **March, September, and November**. 
* **2014 Returns Surge:** Returns experienced a significant increase of **109%** during 2014 compared to previous periods.
* **Unsustainable YoY Growth Tendency:** The sales trajectory exhibits "Growth Exhaustion". Revenue peaks are followed by immediate, deep troughs, resulting in a pattern of short-lived bursts and operational fatigue.
* **The 2014 Contraction:** A structural anomaly was identified in the 2014 growth rate. Unlike the 2011–2013 period, the final year presents a contraction where traditional seasonal cycles failed to yield historical momentum.

#### **2015 Forecasting Overview**
* **Sales Continuity:** The Sales Forecast for 2015 maintains a positive linear trend, projecting a continued increase in volume following the historical growth pattern.
* **Profit Margin Constraint:** The Profit Forecast indicates a much shallower growth slope than sales, projecting a continued struggle to convert high volume into significant utility indicating that without strategic intervention, the efficiency gap will persist.
  
#### **Key Variable Relationships **
* **Profit Hypersensitivity (YoY Growth Rate):** Direct relationship between the monthly YoY growth rate of Sales and Profit reveals extreme sensitivity. Decreases in sales lead to disproportionate collapses in profit, while significant sales increases generate exponential profit growth:
* **Reverse Sales-Profit Relationship (Nov-Dec 2014):** A reverse correlation was detected exclusively during November and December 2014. In this specific window, the effort to drive volume resulted in a mathematical inverse where the increase in sales did not translate into a proportional increase in utility.
* **Slope of Negative Efficiency (2014):** The regression analysis for 2014 confirms a contrary pattern upon 2011-2013. A **negative efficiency slope**, proving that additional sales volume during this year resulted in a net reduction of business utility.
* **CLV and Ratio Decay:** A consistent **downward trend in CLV** was identified across all years. Simultaneously, 2014 shows a sharp drop in **Average Order Value (AOV)** and the **Net Sales to Gross Sales Ratio**.

#### **RFM Analysis: Customer Quality & Value Distribution**

The RFM (Recency, Frequency, Monetary Value) analysis allowed for the segmentation of the database to understand the behavior behind the decline in efficiency.

* **Dominance of the "Other" Segment (Occasional Customers):** It was identified that the vast majority of customers fall into the "Other" category. This is due to them being **occasional customers** with Frequency levels situated in the **Medium and Low** ranges. This finding explains why the CLV (Customer Lifetime Value) is in decline: the growth of the database is not driven by loyal customers, but by isolated transactions.
* **Customer Base Polarization (HHH vs. LLL):** The most populated and defined segments are the extremes: the **Leaders (High-High-High)** and the **Low Priority (Low-Low-Low)** segment. There is a vacuum in the intermediate segments that should be under development.
* **The Fourth Dimension (Profitability Risk):** Integrating profitability into the RFM analysis reveals that the **"Promising"** segment—despite high potential and recent engagement—is a high-risk zone characterized by **extreme negative profit margins**. This indicates that acquisition efforts for this group are attracting price-sensitive profiles who rely on aggressive, margin-destroying discounts.
* **Profit Erosion in "Loyal Customers":** A significant finding is the presence of negative returns within the **Loyal Customers** segment. This proves that long-term retention is being propped up by unsustainable pricing concessions, transforming historically "safe" assets into value destroyers.
* **Efficiency Collapse in "At Risk":** The **At Risk** segment exhibits a synchronized decay in both Recency and Profit. Attempts to re-engage this group are yielding high-cost, low-margin transactions that further exacerbate the negative efficiency slope identified in 2014.

#### **How These Insights Answer the Business Questions**

The trends and relationships identified during the 2011–2014 period do not just describe the past; they provide the diagnostic framework required to address the core strategic questions for the 2015 roadmap:

* **Addressing Financial Integrity:** The insights into **Profit Hypersensitivity** and the **Negative Efficiency Slope (2014)** provide the mathematical evidence needed to evaluate growth health. By identifying the exact moments where volume increases resulted in utility decreases (specifically Q4 2014), the business can now distinguish between "productive growth" and "value-eroding volume."
* **Diagnosing Margin and Value Drivers:** The data regarding the **109% surge in returns** and the decay in the **Net Sales to Gross Sales Ratio** pinpoints exactly where margins are leaking. These insights transition the conversation from general "profit loss" to specific operational failures, such as aggressive year-end discounting and a lack of quality control in high-volume transactions.
* **Analyzing Behavioral Patterns (RFM):** The identification of the **"Other" segment dominance** and the **polarization between HHH and LLL** segments explains the "Who" behind the numbers. Understanding that **Promising** and **Loyal** customers are currently operating within negative profit ranges allows the business to stop guessing and start targeting specific behavioral clusters for margin recovery.
* **Evaluating Strategic Sustainability:** The **2015 Forecasting Overview** and the consistent **downward trend in CLV** act as a direct assessment of the current Sales & Marketing architecture. These insights prove that the current model is optimized for short-term "bursts" (Seasonality Peaks) rather than long-term equity, highlighting the urgent need for a shift from a "Sales-at-all-costs" mindset to an efficiency-first strategy.
   
## Key Findings & Visualizations (Share)

This section summarizes the primary discoveries derived from the data analysis, focusing on the root causes of efficiency loss and the structural failures identified in the current business model.

#### **Descriptive Analysis:Sales & Profit by dimensions**
* **Technology dominance:** leader in Sales and Profit.
* **Customer Distribution:** **Consumer** Segment is the most populated followed by **Corporate** and **AHome Office**. Analysis confirms that the **Corporate** and **Home Office** segments represent the highest responsability in profit erosion, especially Corporate segment.
* **Regional Dominance:** A small group of "Power States" generates the majority of revenue. East Region lead Sales followed by West, Central and South. West Region lead profit followed by East, South, and Central. Central Region is the main responsable in 2014 contraction followed by South Region, with the highest levels of profit Erosion.
**Subcategory Performance Crisis (2014):** While there is an overall upward trend in Net Sales and Profit, the profit trajectory has become dangerously volatile and disconnected from sales volume.
* **The "Sales-at-all-Costs" Limit:** Relying on a shrinking profit leader (**Copiers**) while suffering a dual decline in **Machines** and **Tables**—despite aggressive discounting—proves that price cuts are no longer driving sustainable growth.
* **Structural Gap:** A hollowed growth model has emerged where profitable categories are stagnating while discounted categories (intended to drive volume) fail to yield growth.
* **Growth Restraint Drivers:** The restraint in overall Sales Growth was heavily influenced by specific drag from **Technology** (Copiers and Machines) and **Furniture** (Furnishings, Bookcases, and Tables).
* **Underperformed Subcategories:** The following subcategories were identified as the primary drivers of inefficiency: **Bookcases, Tables, Supplies, Binders, and Machines**.

#### **Structural Price Model Failure at State-Level(2014)** 
* **Cross-Regional Profit Variance:** A critical discovery revealed that specific sub-categories (e.g., **Tables** and **Bookcases**) yield positive profit in certain states while generating consistent losses in others. 
* **Localized Pricing Inefficiency:** This variance confirms that the deficit is not inherent to the products themselves, but is the result of a **failed localized pricing and discount structure** in high-loss states. The price model in these loss-centers fails to account for local operational costs and shipping overhead.
* **Preemptive/Inefficient Discounting:** "Slow-moving" products frequently carry **discounts from the very first sale**. This proves that base prices are misaligned with market reality, sacrificing all potential margin before the product gains commercial traction.

#### **Segment and Category Profit Paradox**

* **Corporate Segment Erosion:** The **Corporate segment** was identified as the primary driver of profit erosion. High-volume contracts within this segment are currently poorly calibrated, where the "Sales Weighted Average Discount" applied to large orders effectively eliminates the net profit margin.
* **Value Destroyers (Structural Loss):** Within the **Furniture** category, sub-categories like Tables and Bookcases operate under a negative structural margin. These products act as "Value Destroyers" across most dimensions, requiring a total overhaul of their cost-to-revenue strategy.

#### **Efficiency Metrics Degradation**
* **Net Sales to Gross Sales Gap:** The increasing gap between gross and net sales is driven by a **109% surge in returns** during 2014. This indicates that the aggressive sales tactics used to hit end-of-year targets are resulting in lower-quality sales and higher reverse-logistics costs.
* **CLV Decay:** The consistent downward trend in **Customer Lifetime Value** proves that current customer acquisition is focused on "transactional" shoppers attracted by discounts, rather than loyal, high-value customers who contribute to long-term sustainability.

