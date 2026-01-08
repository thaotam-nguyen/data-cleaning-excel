# Data Cleaning with Excel – eCommerce Sales Dataset

## Business Context
GameZone is a global eCommerce company operating in the gaming industry, selling new and refurbished products through online platforms and mobile applications.  
As transaction data is used for sales reporting and regional performance analysis, ensuring data quality is critical for reliable downstream analytics.

---

## Project Overview
This project focuses on cleaning and validating transactional data using Excel.  
Key objectives include identifying data quality issues, classifying them as solvable or unsolvable, documenting resolution decisions, and producing a clean, analysis-ready dataset for reporting and exploratory analysis.

---

## Dataset Description
- **Total rows:** 21,865  
- **Total columns:** 11  
- **Fact table:** Orders  
- **Dimension table:** Region  

**Key fields:**  
Order ID, Purchase Timestamp, Ship Timestamp, Product Name, USD Price, Country Code, Marketing Channel, Account Creation Method, Region

---

## Data Conceptualization

### Data Grain
Each row represents **one product line within an order placed by a specific user at a given purchase timestamp**.

### Key Metric
- `usd_price` – primary sales metric used for revenue analysis

### Key Dimension
- Geography (Region)

Based on the stakeholder’s business question —  
*“What are the overall sales trends across a variety of different regions?”* —  
non-essential columns were deprioritized to maintain analytical focus.

---

## Data Quality Issues Identified

Data quality issues were identified through column-level inspection, filtering, and constraint checks, and documented in an issue log for traceability.

### Common Issue Types
- **Data consistency:** inconsistent date formats, spelling variations
- **Data completeness:** missing categorical values, missing timestamps
- **Data integrity:** duplicate orders, business rule violations

Key issues identified include:
- Inconsistent date formats in `purchase_ts`
- Missing values across several categorical fields
- Inconsistent product name spelling
- Duplicate user assignments within the same Order ID
- Ship timestamps occurring before purchase timestamps

---

## Issue Classification: Solvable vs Unsolvable

Each issue was evaluated based on:
- Business logic availability
- Ability to infer correct values reliably
- Potential impact on downstream analysis

### Solvable Issues
- Inconsistent date formats → standardized using Excel date functions  
- Product name spelling inconsistencies → recategorized to the correct label  
- Missing marketing channel and account creation method → recoded as `unknown`  
- Invalid or missing region values → resolved via country–region lookup  
- Duplicate records within Order ID → de-duplicated

### Unsolvable Issues
- Missing purchase dates (1 row)  
- Missing or zero USD price transactions (34 rows)  
- Missing country codes (37 rows)  
- Ship timestamps earlier than purchase timestamps (2,000 rows)

These records were retained with null values due to the absence of reliable business rules to infer correct data. All limitations were documented.

---

## Data Augmentation
A derived metric, **Time to Ship**, was created to support operational performance analysis and service quality evaluation.

---

## Final Validation
The issue log was reviewed to ensure:
- All identified issues were documented
- Magnitude of each issue was quantified
- Resolution decisions were consistently applied

*(Issue Log screenshot attached below)*

---

## Output
- Cleaned, analysis-ready Excel dataset  
- Comprehensive issue log with resolution rationale  
- Derived operational metric (Time to Ship)  
- Clear documentation of unresolved data limitations
