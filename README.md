This project evaluates the operational resilience of Toronto’s shelter system using daily 2024–2025 capacity data.

Our goal is to identify structural fragility, evaluate the impact of temporary capacity loss, and determine how targeted buffer strategies can stabilize the system.

 What We Analyze

* Daily occupancy and capacity utilization
* Operational strain (pressure relative to capacity)
* Sector-level vulnerability (Women, Youth, Families, etc.)
* Geographic clustering of strain
* Time trends in unavailable beds

Strain is defined as:

> **Strain = 1 − (Occupied Capacity / Total Capacity)**

Higher strain indicates lower available slack and increased operational risk.

 Simulations

We conduct three scenario-based simulations:

**1. Demand Shock**
Increase demand by 5% and 10% to assess overflow risk by sector.

**2. Capacity Restoration**
Reactivate unavailable beds to measure potential reduction in overflow.

**3. Strategic Buffering**
Add outsourced beds in addition to restored capacity to evaluate stabilization impact.

 Key Insights

* The system operates near saturation.
* Women and Youth shelters are the most shock-sensitive.
* Restoring unavailable beds meaningfully reduces strain.
* Expanding family shelter capacity yields the largest overall reduction in overflow.
* The system lacks sufficient buffer capacity to absorb modest demand increases.

 Repository Contents

* `SDSSDatathon2026.ipynb` – Main analysis and simulations
* `postal_codes_geocoded.csv` – Geocoded reference data
* `README.md` – Project documentation

Scope

This analysis focuses on short-term operational resilience using 2024–2025 daily shelter data. It does not model long-term housing policy, prevention strategies, or funding reform.

 How to Run

Open `SDSSDatathon2026.ipynb` and run all cells. Users must have the original dataset which we cannot provide due to the hackathon terms of service.

Required libraries:
`pandas`, `numpy`, `matplotlib`, `seaborn`, `geopandas`
