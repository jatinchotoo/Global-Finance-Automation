# 💎 Global Finance Automation & Capital Efficiency Platform

## 🎯 Executive Overview
This platform is an enterprise-grade financial engineering solution designed to consolidate multi-currency subsidiary data into a single, auditable USD "Source of Truth." 

The system replaces fragmented, manual spreadsheets with a deterministic Python pipeline that enables **ROIC (Return on Invested Capital)** benchmarking and executive-level capital allocation decisions across 6 global jurisdictions (ZAR, CHF, GBP, BRL, INR, EUR).

---

## ⚙️ Solution Architecture
The platform implements a modular ETL (Extract, Transform, Load) architecture:

1.  **`pipeline.py` (The ETL Engine):** - Ingests raw subsidiary ledgers.
    - Handles "Malformed Hybrid" data (Excel files containing comma-separated strings).
    - Executes deterministic FX normalization.
    - Standardizes disparate Charts of Accounts (CoA) via `dim_Mapping_Logic`.

2.  **`analytics.py` (Executive Intelligence):** - Consumes the consolidated master fact table.
    - Derives NOPAT (Net Operating Profit After Tax) and Invested Capital.
    - Benchmarks entities against a 10% target hurdle rate.

---

## 🛠 Technical Challenge: The "Data Integrity" Recovery
**The Problem:** Initial data ingestion resulted in a "False Zero" ROIC for 5 out of 6 entities. This was caused by malformed hybrid source files—Excel extensions containing single-column comma-separated values—which prevented the Join-Key from mapping to the master logic.

**The Fix:** - Implemented a **Preprocessing String-Splitting Layer** to "unpack" the hybrid files.
- Developed a **Brute-Force Column Normalizer** to handle inconsistent header naming (e.g., `Account Code` vs `ACCOUNTCODE`).
- **Result:** Recovered full data visibility, identifying **CryptoFlow (Brazil)** as a high-efficiency star with a **167.86% ROIC**.

---

## 🧮 Financial Engineering Logic
- **NOPAT:** EBIT adjusted for a 25% weighted-average jurisdictional tax assumption.
- **Invested Capital:** Balance-sheet driven capital employed calculation.
- **ROIC:** Primary capital efficiency metric used to distinguish value-creators from capital-dilutive entities.

---

## 🚀 How to Run
1. **Prepare Data:** Ensure raw ledgers are in the `/data` folder.
2. **Execute Pipeline:** ```bash
   python pipeline.py
   import pandas as pd
import numpy as np
import os

# Point to the data folder
base_path = os.path.join(os.getcwd(), 'data')
master_file = os.path.join(base_path, "Master_Consolidated_Fact.csv")

print("--- GENERATING EXECUTIVE ROIC REPORT ---")

try:
    df = pd.read_csv(master_file)
    
    # Grouping
    pivot = df.pivot_table(index='Entity', columns='Group_Category', values='Amount_USD', aggfunc='sum').fillna(0)
    
    # Financial Formulas
    pivot['EBIT'] = pivot['Revenue'] - pivot['OpEx']
    pivot['NOPAT'] = pivot['EBIT'] * 0.75 
    pivot['ROIC_%'] = (pivot['NOPAT'] / pivot['Assets'].replace(0, np.nan)) * 100

    print("\n" + "="*65)
    print("             GLOBAL ALPHA PORTFOLIO STRATEGY REPORT")
    print("="*65)
    report = pivot[['Revenue', 'NOPAT', 'Assets', 'ROIC_%']].sort_values(by='ROIC_%', ascending=False)
    print(report.round(2))
    print("="*65)
    
    # --- EXPORT SECTION ---
    # Save to CSV and Excel
    report.to_csv(os.path.join(base_path, 'Final_ROIC_Report.csv'))
    report.to_excel(os.path.join(base_path, 'Executive_Performance_Summary.xlsx'))
    
    print("✅ Reports exported to /data/ folder.")
    print("✅ ANALYSIS COMPLETE")

except FileNotFoundError:
    print("❌ Error: Master_Consolidated_Fact.csv not found. Run pipeline.py first!")

    2. **Execute Pipeline:** ```bash
   python pipeline.py
