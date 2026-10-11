# Delhi Air Pollution Analysis

A statistical analysis of fine particulate matter (PM2.5) in Delhi, India. The project explores the temporal and meteorological drivers of PM2.5 concentrations across six monitoring stations and builds a multiple linear regression model to predict daily pollution levels.

**Author:** Yashkumar Burnwal

---

## Overview

PM2.5 is the fine particulate matter that poses the greatest health risk in air quality monitoring. Using hourly readings from six stations across Delhi (June 2018 – October 2019), this analysis:

- Cleans and structures roughly 70,000 hourly observations across 21 variables.
- Explores temporal patterns in PM2.5 (daily diurnal cycles, day-of-week effects, and seasonal trends).
- Identifies the pollutants and meteorological factors most strongly associated with PM2.5 through correlation and trivariate analyses.
- Evaluates a multiple linear regression model on an aggregated daily held-out test period using RMSE, MAE, and MAPE metrics.

The full analysis is written in R Markdown, ensuring all code, output, and figures are fully reproducible from a single source file.

---

## Repository Contents

| File | Description |
|---|---|
| `Delhi_AirPollution_Analysis.Rmd` | The R Markdown source file containing all code, narrative, and models. |
| `Delhi_AirPollution_Analysis.html` | The rendered, interactive HTML report with code-folding and formatted tables. |
| `Delhi_6Station_Hourly.csv` | The raw dataset containing hourly readings from six Delhi monitoring stations. |
| `README.md` | Project documentation, workflow log, and replication guidelines. |

---

## The Data

- **Source:** Hourly air quality and meteorological readings from six monitoring stations in Delhi.
- **Period:** June 1, 2018 – October 1, 2019.
- **Size:** ~70,227 rows × 21 columns.
- **Response Variable:** `PM2.5` (μg/m³).

**Variable Groups:**
- **Pollutants:** PM2.5, PM10, NO, NO2, NOx, SO2, Ozone, CO, Benzene, NH3.
- **Meteorology:** Ambient Temperature (AT), Barometric Pressure (BP), Solar Radiation (SR), Relative Humidity (RH), Wind Speed (WS), Wind Direction (WD).
- **Time/Location:** `year`, `month`, `day`, `hour`, and station identifier (`loc`).

---

## Analysis Structure

The report is organized into five core stages:

1. **Load and Inspect the Data** — Read raw data, examine structural dimensions, compute summary statistics, and classify variables.
2. **Construct Datetime and Clean Data** — Parse temporal components into `POSIXct` timestamps, derive date-time features (`hour_of_day`, `dow`, `is_weekend`), and run checks for missing values and physical outliers.
3. **Explore PM2.5 Over Time** — Evaluate distributions, longitudinal time series with LOESS smoothing, diurnal cycles, day-of-week trends, and seasonal regimes.
4. **Explore Relationships with Other Variables** — Compute correlation matrices, rank linear predictors, and construct multi-panel scatterplots and trivariate feature interactions.
5. **Training/Testing Split and Modeling** — Implement a chronological train/test split, aggregate hourly data to daily means, fit a multiple linear regression model, inspect diagnostic plots, and evaluate out-of-sample performance.

---

## Key Findings

- **Right-Skewed Distribution:** Mean PM2.5 is ~93 μg/m³ while the median is ~58 μg/m³, reflecting severe winter pollution episodes. Levels routinely exceed the WHO 24-hour guideline of 35 μg/m³.
- **Diurnal Dynamics:** Peak concentrations occur during morning (8–10 AM) and evening (9–11 PM) rush hours, while lowest concentrations occur in mid-afternoon (2–4 PM) due to vertical convective boundary layer mixing.
- **Modest Weekend Effect:** Differences between weekdays and weekends are slight, reflecting continuous baseload pollution sources (regional dust, power generation, biomass burning).
- **Primary Predictors:** PM10 exhibits the strongest positive correlation ($r \approx 0.79$), followed by combustion tracers (CO, NOx). Temperature shows a strong negative association due to winter thermal inversions trapping ground-level particles.
- **Regression Fit:** Multiple linear regression on daily means explains over 90% of the variance ($R^2 \approx 0.927$). On the held-out test period (July–October 2019), test RMSE was ~13.4 μg/m³, showing strong generalization across seasonal transitions.


---

## Reproducing the Analysis

### Requirements
- **R:** Version 4.0 or later
- **RStudio** (recommended)

### Package Dependencies
Install the required packages in R:

```r
install.packages(c(
  "tidyverse", "lubridate", "corrplot", "viridis", "scales",
  "gridExtra", "knitr", "kableExtra", "reshape2", "broom"
))
