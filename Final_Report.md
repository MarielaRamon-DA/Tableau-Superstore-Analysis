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
