# Global Climate Trends Analysis

An end-to-end data pipeline and Power BI dashboard on long-term temperature anomaly trends across **226 countries**, using Berkeley Earth records from 1850 to 2020.

<img width="1555" alt="Power BI dashboard" src="https://github.com/user-attachments/assets/70cac20e-2176-48e8-8376-91cf1d0549fc" />

## What it demonstrates

- Web scraping and automated bulk downloads
- Cleaning semi-structured text files
- Coverage-based validation (only analysing years where global reporting is reliable)
- Climate feature engineering: trend, volatility, baseline change, z-scores, seasonality
- An interactive Power BI dashboard

## Data

The data is the [Berkeley Earth](https://berkeleyearth.org/temperature-country-list/) archive of monthly temperature anomalies by country. Each value is a deviation from the long-term average, so regions with very different climates can be compared.

## Method

1. **Extract:** scrape the country list, normalise the names, and download each country's monthly anomaly file (226 of 237 downloaded successfully).
2. **Transform:** strip metadata and malformed rows, type the columns (`year`, `month`, `anomaly`) and combine everything into one dataset of 515,429 rows.
3. **Validate coverage:** find the first year where at least 95% of countries report data (**1892**) and filter to that point, leaving 344,422 rows.
4. **Feature engineering:**
   - per country: warming trend (°C/year, linear regression), volatility, mean anomaly
   - per observation: season, baseline anomaly, change from baseline, z-score
5. **Load:** export clean CSVs and build the Power BI dashboard.

## Key findings

- The average warming trend across countries is **~0.011 °C per year**, about 1.1 °C per century.
- Warming speeds up markedly from the late 20th century.
- Northern regions warm faster. Antarctica has the steepest trend in the dataset (~0.018 °C/year).
- Extreme anomalies become more frequent after about 1980.
- Seasonal warming isn't uniform.

## Repository contents

```
Global_Climate_Trends_Analysis.ipynb   # full pipeline (extract → transform → features → export)
ClimateProjectData/
├── temperature_data_clean.csv         # filtered monthly anomalies
└── country_features.csv               # per-country trend / volatility / mean anomaly
Documents/
├── Climate Change Dashboard.pbix      # Power BI dashboard
├── Global Climate Trends Analysis - Aaron Darcy.pdf
└── Global Climate Trends Analysis - Aaron Darcy.pptx
requirements.txt
```

## Running it

```bash
python -m venv venv
venv\Scripts\activate          # macOS/Linux: source venv/bin/activate
pip install -r requirements.txt
jupyter notebook Global_Climate_Trends_Analysis.ipynb
```

The notebook downloads the raw Berkeley Earth files when it runs. Open `Documents/Climate Change Dashboard.pbix` in Power BI Desktop to explore the dashboard.

## Context

Data Operations & Management module, MSc in Data Science (November 2025).

## Licence

See [LICENSE](LICENSE).
