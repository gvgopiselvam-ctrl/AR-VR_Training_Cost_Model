# AR/VR Operational Training: CapEx/OpEx Cash Model & Throughput Optimization

## 1. Executive Summary & Business Position
> **The Position We Take:** Scale the non-technical AR/VR warehouse training program across **Campus Hubs A and B** at a **2.5:1 student-to-headset ratio (30 students / 12 headsets)** while pausing hardware expansion at Regional Center D. This configuration drops blended training cost to **$57.40 per student (-32.5% vs. the $85.00 physical warehouse benchmark)** and achieves hardware CapEx payback within **9 cohorts**.

---

## 2. Real Business Problem (Multi-Departmental Scope)
Traditional physical warehouse & forklift training costs **$85.00 per student** due to equipment lockups, safety supervision, and consumable wear. Launching a 500+ student AR/VR pilot triggered three competing stakeholder questions:
* **Finance (CapEx / Cash Flow):** How many cohorts must a $650 headset survive before amortized CapEx + recurring software licensing beats the $85.00 physical training benchmark?
* **Operations (Lab Throughput & Downtime):** What is the maximum student-to-headset ratio we can run before battery thermal throttling and device downtime degrade lab schedules?
* **Training Delivery (Completion & SLA):** Does sharing headsets across larger cohorts hurt module completion rates in high-complexity simulations (e.g., *Hub Dock Safety & Forklift AR*)?

---

## 3. System Architecture & Multi-Source Data Enrichment
Rather than analyzing a single static spreadsheet, this project combines three operational layers:
1. **Source 1 — LMS & Headset IoT Telemetry Logs (`/data/arvr_cohort_cost_parameters.csv`):** Tracks cohort batch sizes, active headset allocations, session duration, and hardware downtime percentages.
2. **Source 2 — ERP Facility & Labor Cost Ledger (`/data/erp_facility_overhead_ledger.csv`):** Enriches raw cohort logs with regional campus facility overhead, technician maintenance rates, and commercial software seat tiers.
3. **Tool Stack:** **Python** (`iot_telemetry_erp_etl.py` for ingestion & data hygiene) $\rightarrow$ **SQL** (`arvr_iot_erp_enrichment_pipeline.sql` for ERP joins) $\rightarrow$ **Advanced Excel** (`ARVR_Operational_Cash_Model.xlsx` dynamic sensitivity matrix).

---

## 4. Key Analytical Findings
| Student-to-Headset Ratio | Avg Batch Size | Hardware Downtime (%) | Completion Rate (%) | Blended Unit Cost ($/Student) | Net Savings vs. $85 Benchmark |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **1.7 : 1 (Over-provisioned)** | 20 | 3.8% | 96.4% | $74.20 | +$10.80 (12.7%) |
| **2.5 : 1 (Optimal Sweet Spot)** | **30** | **5.2%** | **95.1%** | **$57.40** | **+$27.60 (32.5%)** |
| **3.3 : 1 (Over-saturated)** | 40 | 10.9% | 88.5% | $61.85 | +$23.15 (27.2%) |

* **The 2.5:1 Inflection Point:** Pushing past 2.5 students per headset forces back-to-back charging cycles, doubling thermal downtime from **5.2% to 10.9%** and requiring overtime facilitator hours that erase hardware savings.

---

## 5. Visual Diagnostic
![AR/VR Unit Economics Curve](visuals/arvr_unit_economics_curve.png)

---

## 6. Repository Structure
* `/model/ARVR_Operational_Cash_Model.xlsx` — Multi-tab workbook featuring the Executive Summary dashboard, Cohort Cash Model, and 2-Way Sensitivity Matrix.
* `/python/iot_telemetry_erp_etl.py` — Automated telemetry hygiene and ERP merge script.
* `/sql/arvr_iot_erp_enrichment_pipeline.sql` — Data cleaning, ERP enrichment joins, and unit-economics SQL queries.
* `/data/arvr_cohort_cost_parameters.csv` — Primary IoT telemetry dataset.
* `/data/erp_facility_overhead_ledger.csv` — Secondary ERP cost-center enrichment table.
* `/visuals/arvr_unit_economics_curve.png` — Dark-mode unit cost vs. hardware downtime inflection chart.
