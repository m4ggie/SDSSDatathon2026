# SDSSDatathon2026
SDSS Datahon 2026 Public Services Category

This data analysis and simulation project exlores  shelter occupancy, demand, and redistribution in the Greater Toronto Area (GTA)


## Overview

The vast majority of Toronto’s shelter operating at or near capacity, causing the entire system to be vulnerable to shocks and preventing people from accessing the housing they need. We wanted to determine which service sectors experience the most pressure and how to use existing resources to improve distribution of shelter demand.

This project analyzes
* Daily occupancy and capacity utilization
* Operational strain (pressure relative to capacity)
* Sector-level vulnerability (Women, youth, families, etc.)
* Geographic clustering of strain
* Time trends in unavailable beds

Strain is defined as 
`Strain = 1 - (Occupied Capacity/Total Capacity)`.
Higher strain indicates increased operational risk.

# Getting Started
## Prerequisites
```bash
pip install folium geopy matplotlib pandas pgeocode
```

## Data Setup
Before running the notebook, download and upload the following files to your runtime:
1. **`public_services_dataset.xlsx`** - the main shelter dataset.
Users must have the dataset personally due to sharing constraints.
2. **`postal_codes_geocoded.csv`** - geocoded postal codes. available in the github

## Project Structure
```
SDSSDatathon2026.ipynb # main analysis notebook
postal_codes_geocoded.csv # geocoded postal codes (download required)
public_services_dataset.xlsx # source shelter data (upload required)
cleaned_data.csv # output: cleaned dataset
forecasted_data.csv # output: scenario simulation results
```

## Methodology
### Data Cleaning
Rows with negative values in `ACTUAL_CAPACITY`, `OCCUPIED_CAPACITY`, `UNAVAILABLE_CAPACITY`, and `OCCUPANCY_RATE` were dropped. Entries with missing postal codes or program model were also removed. Each shelter location is joined with geocoded latitude/longitude coordinates obtained from geocodio.

### Exploratory Data Analysis
The notebook examines the distribution of shelters across four key dimensions (Mixed Adult, Men, Women, Youth, Families), program model (Emergency, Transitional), program area, and capacity type.

### Simulation (`simulation()`)
Runs combinations of three interventions to assess their impact on shelter-nights over capacity, broken down by sector:
| Parameter | Values Tested | Explanation|
|---|---|---|
| Demand shock | +5%, +10%, +15% | Assesses overflow risk by sector
| Capacity Restoration | 0%, 50%, 100% | Reactivate unavailable beds to measure potential reduction in overflow
| Strategic Buffering | +0% to +4% | Add outsourced beds in additiona to restored capacity to evaluate stabilization impact.

### FSA Redistribution Simulation (`redistribution_region()`)
Simulates redistributing overflow demand to shelters with spare capacity **within the same Forward Sortation Area (FSA)** — the first three characters of a postal code. This models what could be achieved by relaxing sector constraints locally. We chose FSAs as the redistribution region because they represent compact neighbourhoods within Toronto. Redistributing within an FSA means moving people short distaces. Since postal codes were already in the dataset, FSAs could be derived without additional geocoding or boundary data. 

A **Redistribution Effectiveness Index (REI)** quantifies how much of the system-wide over-capacity is resolved through redistribution:

```
REI = (baseline_overcapacity_rate - post_redistribution_rate) / baseline_overcapacity_rate
```

Results include a shelter-level map dataframe with latitude/longitude for spatial visualization.

## Key Findings
- The system currently operates near saturation and lacks sufficient buffer capacity to absorb modest demand increases
- **Mixed Adult** shelters are the most common, followed by Men, Women, Youth, and Families. Women and Youth shelters are the most shock-sensitive
- The majority of shelters operate under an **Emergency** program model.
- **General Base** is the most common program area.
- Even a modest **5% demand increase** pushes a significant share of shelter-nights over capacity across all sectors.
- FSA-level redistribution (REI ≈ 0.07 at baseline) shows modest but meaningful gains, suggesting that redirecting people experiencing homelessness to other shelters with remaining beds within neighbourhoods could reduce crowding.
- Restoring unavailable beds meaningfully reduces strain
- Expanding family shelter capacity yields the largest overall reduction in overflow.
