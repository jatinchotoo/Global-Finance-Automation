# 💎 Global Finance Automation & Capital Efficiency Platform

## 🎯 Executive Overview
This platform is an enterprise-grade financial engineering solution designed to consolidate multi-currency subsidiary data into a single, auditable USD "Source of Truth." 

The system replaces fragmented spreadsheets with a deterministic Python pipeline that enables **ROIC (Return on Invested Capital)** benchmarking across 6 global jurisdictions.

---

## ⚙️ Solution Architecture


1.  **`pipeline.py` (The ETL Engine):** Ingests raw subsidiary ledgers, handles "Malformed Hybrid" data, and executes deterministic FX normalization.
2.  **`analytics.py` (Executive Intelligence):** Calculates **NOPAT** and **Invested Capital** to generate automated CSV/Excel reports.

---

## 🛠 Technical Challenge: The "Data Integrity" Recovery
**The Problem:** Initial data ingestion resulted in a "False Zero" ROIC for several entities due to malformed hybrid files (Excel extensions containing CSV strings).

**The Fix:** Implemented a **Preprocessing String-Splitting Layer** to unpack data and a **Column Normalizer** to handle inconsistent header naming across regions.

---

## 🚀 How to Run
1.  **Prepare Data:** Ensure raw ledgers are in the `/data` folder.
2.  **Execute Pipeline:** ```bash
    python pipeline.py
    ```
3.  **Generate Analytics:** ```bash
    python analytics.py
    ```

---

## 📊 Performance Intelligence & Results
![ROIC Results Table](images/roic_results.png)

* **Top Performer:** **CryptoFlow (Brazil)** achieves an elite **167.86% ROIC**.
* **Audit Trail:** Automatic export of `Executive_Performance_Summary.xlsx` in the `/data` folder.