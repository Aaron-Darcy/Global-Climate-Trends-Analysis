# Global Climate Trends Analysis

End-to-end data pipeline and dashboard exploring long-term global temperature anomaly trends using Berkeley Earth country-level records (1850–2020). The project includes automated data extraction (web scraping + bulk downloads), cleaning and coverage validation, climate feature engineering, and an interactive Power BI dashboard for exploration and comparison.

## Project overview

**Goal:** Analyse long-term global temperature change and produce a reproducible dataset and dashboard suitable for exploratory analysis and reporting.

**What this project demonstrates**
- Web scraping and automated bulk data ingestion
- Data cleaning of semi-structured text files
- Coverage-based validation (restricting analysis to periods with reliable global reporting)
- Feature engineering for climate analytics (trend, volatility, baseline change, z-scores, seasonality)
- Dashboarding in Power BI for interactive exploration

## Data source

- **Berkeley Earth Temperature Archive** (monthly temperature anomalies by country)
- Each record is an anomaly (deviation from a long-term average), enabling comparison across regions with different baseline climates.
- Source country list page: https://berkeleyearth.org/temperature-country-list/

> Note: This repo does not include the raw Berkeley Earth text files by default. The pipeline downloads raw data at runtime.

## Method

1. **Extract**
   - Scrape the Berkeley Earth country list
   - Normalise country names to match repository filenames
   - Download monthly anomaly text files per country

2. **Transform**
   - Remove metadata/comment lines and malformed rows
   - Convert to typed columns: `year`, `month`, `anomaly`
   - Combine country files into a single dataset
   - Perform **coverage analysis** and filter to the first year where ≥95% of countries have data (cutoff used in this project: **1892**)

3. **Feature engineer**
   - Warming trend (°C/year) via linear regression
   - Volatility (std dev of anomalies)
   - Mean anomaly
   - Baseline anomaly and change from baseline
   - Season classification (Winter/Spring/Summer/Autumn)
   - Country-level anomaly z-scores

4. **Load / Visualise**
   - Export cleaned datasets as CSV for Power BI
   - Build an interactive dashboard for global/country comparison

## Outputs

Generated files (after running the notebook/pipeline):
- `data/processed/temperature_data_clean.csv`
- `data/processed/country_features.csv`

Power BI:
- Interactive dashboard built from the exported datasets (see `assets/dashboard.png`).

## Key findings (high level)

- Global warming accelerates notably from the late 20th century onward.
- Northern regions show faster warming rates.
- Extreme anomaly events increase after ~1980.
- Seasonal warming is not uniform, with some seasons showing higher anomalies.

## How to run

### Option A: Notebook
1. Create a virtual environment
2. Install dependencies:
   ```bash
   pip install -r requirements.txt


<img width="1555" height="832" alt="image" src="https://github.com/user-attachments/assets/70cac20e-2176-48e8-8376-91cf1d0549fc" />

