# Swat River and KPK flood dataset: analysis

Source: https://www.kaggle.com/datasets/mmumairkhattak/swat-kpk-flood-dataset

## What this is

Three small CSV files about the Swat River basin in Khyber Pakhtunkhwa, Pakistan:

- `daily_hydro_met.csv`: 975 daily rows for one gauge (Chakdara_Gauge), 1 Jan 2024 to 1 Sep 2026, with rainfall, average temperature, river discharge, water level and a flood label
- `historical_floods.csv`: 17 yearly rows (2010 to 2026) with peak discharge, monsoon rainfall anomaly, a flood flag and damages
- `basin_geospatial_features.csv`: 4 sub-basins with elevation, slope, forest cover and an encroachment index

The data is synthetic. The author's own README says so (kept here as `README_kaggle.md`). The daily series is simulated, not observed gauge data, and nothing here should be read as a fact about the real river.

## Headline numbers

- Daily file: 975 rows, 7 columns, no missing values, no duplicates, no gaps in the calendar
- Cleaned file: 975 rows, 10 columns (nothing dropped; dates parsed, columns renamed, values rounded, year / month / monsoon flag added)
- July and August are 186 of the 975 days and hold 69.2% of all rainfall (18.89 mm/day against 1.98 mm/day in other months)
- Mean discharge is 21,840 cusecs in July-August and 10,110 cusecs otherwise
- Same-day rainfall vs discharge correlation 0.77; 3-day rainfall total vs discharge 0.96
- `Flood_Label` is 0 on all 975 days
- Water level is exactly 2.1 + discharge / 50,000

## Highest / lowest / most

- Wettest day: 93.60 mm on 2025-07-18. Driest: 0.01 mm on 2024-03-13. No day has zero rain.
- Highest discharge: 49,542.5 cusecs on 2025-07-18 (water level 3.091 m)
- Lowest discharge: 5,089.7 cusecs on 2025-10-03 (water level 2.202 m)
- Largest one-day rise in discharge: 20,728 cusecs on 2025-07-18
- Hottest day: 39.93 C on 2024-03-29. Coldest: -0.07 C on 2025-09-16
- Wettest calendar month: August 2024, 652.8 mm. Driest full month: June 2026, 42.8 mm
- Highest monthly mean discharge: July 2025, 24,148 cusecs. Lowest: October 2025, 6,868 cusecs
- 8 days with 50 mm or more of rain and 8 days at or above 40,000 cusecs, all in July or August
- Flood table: highest peak 247,000 cusecs in 2022 (anomaly +78%, damages PKR 35,000 million); lowest 40,000 cusecs in 2017
- Flood table: flood years are 2010, 2020, 2022 and 2025; 2010 and 2022 account for 93.1% of the PKR 50,470 million in listed damages
- Basin table: Upper Swat (Kalam) is highest (2,500 m), steepest (32 degrees) and most forested (35%); Lower Swat (Mingora) has the highest encroachment index (9 of 10)

## Caveats

- Synthetic data. Describes a generator, not the river.
- The flood label has no positive cases, so it cannot be used as a classification target.
- Water level is a linear function of discharge and adds no information.
- The temperature cycle is out of phase with the real climate: it peaks in March-April (about 34 C) and is lowest in September-October (about 5.6 C).
- The daily series and the yearly flood table disagree in the years they share. Daily maxima are 45,078, 49,543 and 49,372 cusecs for 2024-2026 against listed annual peaks of 75,000, 98,000 and 88,000 (50 to 60%). 2025 is a flood year in the table but has no flood-labelled day.
- One station, under three years, and 2026 is a partial year (ends 1 September).
- The flood table (17 rows) and basin table (4 rows) are only described; no statistical conclusions are drawn from them.
- How the columns were generated, and how the encroachment index and rainfall anomaly are defined, is not documented.

## Folder layout

```
daily_hydro_met.csv              original
historical_floods.csv            original
basin_geospatial_features.csv    original
swat_floods_cleaned.csv          cleaned daily file
swat_floods_analysis.ipynb       notebook, saved with outputs
swat_floods_report.pdf           written report
README_kaggle.md                 original dataset readme (renamed from README.md)
README.md                        this file
charts/                          PNG charts written by the notebook
```

## How to run

From this folder, with the shared environment one level up:

```
../.venv/bin/jupyter nbconvert --to notebook --execute --inplace swat_floods_analysis.ipynb
```

or open the notebook and run all cells. It uses relative paths, reads the three original CSVs, and rewrites `swat_floods_cleaned.csv` and everything in `charts/`.
