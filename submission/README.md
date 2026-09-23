# Booze 'R' Us — City-Category Sales Forecast: Code Bundle

This folder contains the full, reproducible code behind the Booze 'R' Us
final report and presentation: forecasting monthly bottle demand by city and
alcohol category for Iowa's ten largest liquor markets, using linear
regression.

## What's included

Three notebooks, meant to be run in order. Each one's output is the input to
the next:

| # | Notebook | Produces | Depends on |
|---|---|---|---|
| 1 | `01_build_raw_liquor_sales_data.ipynb` | `liquor_2022_2026.parquet` | raw yearly exports (see **Data** below) |
| 2 | `02_build_city_category_month_data.ipynb` | `city_category_month.parquet` | `liquor_2022_2026.parquet` |
| 3 | `03_city_category_sales_forecast_analysis.ipynb` | the forecast, model comparison, and recommendation charts used in the final report | `city_category_month.parquet` |

Notebook 3 is the actual analysis: it fits and compares several linear
regression models on a time-based holdout, selects a final model, forecasts
the next 12 months, and produces the city-by-city recommendation table and
charts used in the final report and presentation.

Each notebook has already been run once and includes its outputs (printed
row counts, model comparison tables, charts) so the results can be reviewed
without needing to re-run anything.

## Data

**No raw data is included in this bundle** (the raw transaction export alone
is several gigabytes). Here is what it is and how to reproduce it:

- **Source:** Iowa Liquor Sales retail transaction data, from Iowa's open
  data portal (`idh-be.iowa.gov`). Each calendar year is published there as
  its own dataset/export.
- **Files used:** the 2022–2026 yearly exports, downloaded as zip files
  named `iowa_liquor_sales_<year>_<dataset id>_rows.zip`:
  - `iowa_liquor_sales_2022_1259_rows.zip`
  - `iowa_liquor_sales_2023_1260_rows.zip`
  - `iowa_liquor_sales_2024_1261_rows.zip`
  - `iowa_liquor_sales_2025_1262_rows.zip`
  - `iowa_liquor_sales_2026_1263_rows.zip`
- **To reproduce from scratch:** download those five yearly exports from
  Iowa's data portal, place them in a folder named `liquor_2022_2026/`
  alongside the notebooks, and run `01_build_raw_liquor_sales_data.ipynb`.
  It extracts, deduplicates, and combines them into
  `liquor_2022_2026.parquet`.

Everything downstream of that raw file is derived data built by these
notebooks (`city_category_month.parquet`), not raw data, and is likewise not
included — running notebooks 2 and 3 in order regenerates it.

## How to run

1. Place the five raw yearly export zips in a `liquor_2022_2026/` folder
   next to the notebooks (see **Data** above).
2. Run `01_build_raw_liquor_sales_data.ipynb` top to bottom.
3. Run `02_build_city_category_month_data.ipynb` top to bottom.
4. Run `03_city_category_sales_forecast_analysis.ipynb` top to bottom.

All three notebooks use plain relative file paths and expect to be run from
this folder (or with the data files copied alongside them).

# DEAD Notebook

All analysis for DEAD is located within the `DEAD_Final_Analysis.ipynb` file. This file uses the `liquor_2022_2026.parquet` file built from the notebooks for Booze 'R Us. DEAD analysis also uses data from the 2020 U.S. Census, which can be obtained through the U.S. Census API.

# Environment

Python 3, with:

```
pandas
numpy
duckdb
statsmodels
scikit-learn
matplotlib
seaborn
jinja2          # required for the styled tables in notebook 3
```


# Generative AI disclosure

Generative AI (Claude Code) was used in assisting writing code and
debugging throughout this project.