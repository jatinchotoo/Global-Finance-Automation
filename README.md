# 💎 Global Finance Automation & Capital Efficiency Platform

## 🎯 Executive Overview
This platform is a financial engineering solution designed to consolidate multi-currency subsidiary data into a single, auditable USD "Source of Truth." 

---

## ⚙️ Solution Architecture


1. **`pipeline.py` (The ETL Engine):** Processes raw data, fixes malformed strings, and normalizes currencies.
2. **`analytics.py` (Executive Intelligence):** Calculates ROIC and generates performance reports (CSV/Excel).

---

## 🛠 Technical Challenge: The "Data Integrity" Recovery
**The Problem:** Initial ingestion failed due to "hybrid" files (Excel extensions containing CSV strings).
**The Fix:** Implemented a string-splitting layer to unpack data, recovering an elite **167.86% ROIC** for the CryptoFlow subsidiary.

---

## 🚀 How to Run
1. **Prepare Data:** Ensure raw ledgers are in the `/data` folder.
2. **Execute Pipeline:** ```bash
   python pipeline.py
   