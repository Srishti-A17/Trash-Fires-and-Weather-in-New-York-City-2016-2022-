# Trash Fires and Weather in New York City (2016–2022)

**Applied Data Science | End Semester Project**

---

## Overview

This project investigates the relationship between weather conditions and daily trash fire incidents in New York City between 2016 and 2022. Using FDNY incident records and hourly NYC weather data, we aggregate both datasets to the daily level and study whether temperature, precipitation, wind speed, and cloud cover can explain and predict changes in trash fire frequency across the five boroughs.

---

## Research Question

> How do weather conditions (temperature, precipitation, wind speed, and cloud cover as a proxy for humidity) relate to daily trash fire incidents in New York City between 2016 and 2022?

---

## Project Structure

```
trash-fires-nyc/
│
├── data/
│   ├── Incidents_Responded_to_by_Fire_Companies.csv   # FDNY incidents raw data
│   └── NYC_Weather_2016_2022.csv                      # Hourly weather data
│
├── ADS_End_sem_project.ipynb                          # Main project notebook
└── README.md
```

---

## Data Sources

### 1. FDNY Trash Fire Incidents
- **Source:** FDNY "Incidents Responded to by Fire Companies"
- **Filter applied:** Incident type `118 - Trash or rubbish fire, contained`
- **Fields used:**
  - `incident_datetime` — date and time of the incident
  - `borough` — NYC borough where the incident occurred
  - `incident_duration` — total duration of the incident
  - `action_taken` — action taken by fire companies
  - `fire_spread` — extent of fire spread

### 2. NYC Weather Data (2016–2022)
- **Source:** `NYC_Weather_2016_2022.csv`
- **Resolution:** Hourly
- **Variables used:**

| Variable | Unit | Description |
|---|---|---|
| `temperature` | °C | Ambient air temperature |
| `precipitation` | mm | Total precipitation |
| `rain` | mm | Rainfall amount |
| `cloud_cover` | % | Cloud coverage (proxy for humidity) |
| `wind_speed` | km/h | Wind speed |
| `wind_direction` | degrees | Wind direction |

Both datasets are aggregated to **daily resolution** (per calendar date) before analysis.

---

## Methodology

The project follows a standard applied data science pipeline:

### 1. Data Cleaning
- Parse and standardize datetime columns across both datasets
- Filter FDNY incidents to trash fire type only (`118`)
- Remove invalid or out-of-range values
- Handle missing weather observations
- Aggregate hourly weather data to daily means/totals
- Aggregate FDNY incidents to daily counts per borough

### 2. Descriptive Analysis and EDA
- Daily trash fire counts over the full 2016–2022 period
- Temporal patterns: by year, month, season, day of week
- Spatial patterns: fire counts by borough
- Weather variable distributions and time series plots
- Correlation matrix between weather variables and fire counts

### 3. Data Distribution Checks
- Test whether daily fire counts follow a normal distribution
- Check skewness of weather variables
- Identify outliers and anomalous days
- Assess stationarity of the time series

### 4. Hypothesis Testing
- Test whether mean daily fire counts differ significantly across seasons
- Test whether rainy days have significantly fewer fires than dry days
- Test whether high temperature days have more fires than low temperature days
- Use appropriate statistical tests (t-test, Mann-Whitney U, ANOVA) based on distribution checks

### 5. Regression Modelling
- Fit OLS regression of daily fire count on weather predictors
- Predictors: daily mean temperature, total precipitation, mean wind speed, mean cloud cover
- Check regression assumptions: linearity, homoscedasticity, normality of residuals
- Report coefficients, confidence intervals, and R²
- Interpret which weather variables are significant predictors

### 6. Interpretation and Conclusion
- Summarise key findings on weather-fire relationships
- Discuss borough-level differences
- Note limitations of the analysis
- Suggest directions for future work

---

## Expected Findings

Based on prior literature on urban fire incidents and weather:

- **Temperature** is expected to positively correlate with fire counts (hotter days → more outdoor activity and dry conditions)
- **Precipitation** is expected to negatively correlate (rain suppresses fires and reduces dry fuel)
- **Wind speed** may positively correlate (wind can spread and intensify fires)
- **Cloud cover** as a humidity proxy may negatively correlate (higher humidity → less dry material)
- Seasonal patterns are expected with summer peaks and winter troughs

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
```

Install all dependencies:
```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels
```

---

## Running the Notebook

### Locally (Jupyter)
```bash
jupyter notebook ADS_End_sem_project.ipynb
```

Place both data files in the same directory as the notebook and update the file paths accordingly. The notebook was originally built for Google Colab — replace the Colab upload cell with:

```python
import pandas as pd

fdny = pd.read_csv("Incidents_Responded_to_by_Fire_Companies.csv")
weather = pd.read_csv("NYC_Weather_2016_2022.csv")
```

### Google Colab
Upload both files when prompted by the `files.upload()` cell.

---

## Limitations

- Weather data is city-wide (single station) and does not capture borough-level microclimatic variation
- Trash fire incidents may be underreported in some boroughs or time periods
- The analysis is correlational — causality between weather and fire counts cannot be established
- Other confounders such as population density, sanitation schedules, and special events are not controlled for
- The 2020 COVID-19 period may introduce anomalies in both fire incident rates and mobility patterns that affect results

---

## Course Context

This project was completed as part of the Applied Data Science course end semester project. The methodology follows the course framework:

- Data cleaning and preprocessing
- Exploratory data analysis
- Statistical hypothesis testing
- Regression modelling
- Interpretation and communication of results

---

*Applied Data Science | End Semester Project*
