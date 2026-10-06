# PowerBI-StarSchema-VertiPaq-Optimization

An end-to-end Power BI analytics project focused on **Star Schema Architecture**, **VertiPaq Engine Optimization**, and **Integer Surrogate Key Implementation**. This project demonstrates how refactoring heavy, text-based composite keys into lean numeric relationships dramatically reduces memory footprint (RAM) and boosts query execution performance.

---

## 📽️ Project Overview 
## 📊 Dashboard & Data Model Showcase

### 1. Executive Sales Analytics Dashboard
Features soft container cards, dark-green executive theme palette, KPI summary metrics, seasonality line charts, and dynamic cross-filtering.

![Sales Analytics Dashboard](https://github.com/HagerSalahRamadan/PowerBI-StarSchema-VertiPaq-Optimization/blob/main/Sales%20Dashboard.png)

### 2. Optimized Star Schema Data Model
A pure Star Schema design linking `FactSales` to discrete dimension tables (`DimCustomer`, `DimBranch`, `DimProduct`, `DimCustomerBranch`, and `DimDate`).

![Power BI Data Model](https://github.com/HagerSalahRamadan/PowerBI-StarSchema-VertiPaq-Optimization/blob/main/Model.png)

---

## 🛠️ Power Query & Modeling Transformations

1. **Composite Business Key:** Combined `[CustomerCode]` & `"-"` & `[BranchCode]` inside `DimCustomerBranch`.
2. **Integer Surrogate Key:** Generated `[CustomerBranchKeyID]` as a 64-bit Integer Index column.
3. **Fact Table Refactoring:** Merged `[CustomerBranchKeyID]` into `FactSales` and stripped out all redundant descriptive text columns (`CustomerCode`, `BranchCode`, composite text strings).
4. **Time Intelligence Setup:** Configured a custom DAX `DimDate` table (2024–2025) marked as an official Date Table with 1-to-Many single-direction relationships.
5. **Data Governance:** Organized all core KPI measures (`Total Revenue`, `Sales Count`, `AOV`, `YoY Growth %`, `Sales SMLY`) inside a dedicated `_Measures` table.

---

## 🧠 Technical Q&A & Optimization Architecture

### Q1: Model Comparison (Before vs. After Optimization)

* **Fact Table Structure:**
  * **Before:** Bloated `FactSales` containing repetitive text columns (`CustomerCode`, `BranchCode`, composite text string).
  * **After:** Clean `FactSales` containing strictly numerical measures and a single foreign integer key (`CustomerBranchKeyID`).
* **Relationship Basis:**
  * **Before:** Complex, wide string matching using text patterns (`CUST1001-BR502`).
  * **After:** Fast, single-column **Integer-to-Integer** join.
* **VertiPaq Memory Footprint:**
  * **Before:** High RAM consumption due to storing wide, repetitive string dictionaries.
  * **After:** Optimized RAM compression via efficient Integer Value Encoding.
* **Data Architecture:**
  * **Before:** Denormalized/hybrid structure with duplicate business attributes inside the Fact table.
  * **After:** Pure Star Schema with strict separation of Facts and Dimensions.

---

### Q2: Why an Integer Surrogate Key is Preferable to Text Keys

1. **Engine Compression (VertiPaq Efficiency):** Power BI's columnar engine compresses numeric values far more efficiently than text strings. Storing string keys across thousands/millions of fact rows inflates memory footprint. Replacing them with a 64-bit integer surrogate key optimizes cache usage and reduces overall `.pbix` file size.
2. **Query & CPU-Level Join Performance:** Numeric joins (1, 2, 3...) evaluate directly on lower-level CPU registers. Cross-filtering, DAX measure evaluation, and aggregations perform significantly faster compared to character-by-character text matching.
3. **Star Schema Standards & Data Integrity:** Carrying descriptive attributes inside `FactSales` causes unnecessary Data Redundancy. Using `CustomerBranchKeyID` keeps descriptive text strictly inside dimension tables (`DimCustomerBranch`), maintaining a clean **Single Source of Truth** architecture.

---

### 📝 Optimization Note (Executive Summary)

> **Architectural Note:**  
> Multi-column text keys were replaced with a single 64-bit Integer Surrogate Key (`CustomerBranchKeyID`) in `FactSales`. This enforces a clean Star Schema, minimizes VertiPaq memory footprint via numeric dictionary encoding, and accelerates CPU-level join processing across all dashboard visuals.

---

## 📂 Repository Contents

* `Sales_Analytics_Report.pbix` - Final Power BI report file containing the optimized data model and interactive dashboard.
* `Dashboard.jpg` - High-resolution screenshot of the Executive Dashboard.
* `Model1.png` - Screenshot of the Star Schema relationship model.
* `README.md` - Technical project documentation.

---

## 📧 Contact

For any questions or feedback, feel free to reach out via email: hagersalah.r39@gmail.com

---

**Author:** Hager Salah  
**Role:** Data Analyst / BI Developer
