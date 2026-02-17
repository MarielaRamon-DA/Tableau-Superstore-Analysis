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

## 2. Prepare (Data Integrity & Governance)
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

## 3. Process (Data Cleaning & Transformation)

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
