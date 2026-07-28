# public-utility-company-regression-model# Revenue Forecasting with Seasonal OLS Regression

Revenue forecasting model built on the AICPA regression dataset, using OLS regression with seasonal dummy variables to capture how production-to-revenue relationships shift by season.

## Overview

This notebook builds and compares two linear regression models that forecast `revenue` from `production`, each augmented with a different seasonal dummy variable to test whether winter or fall months have a distinct effect on the production-revenue relationship.

## Data

- **Source:** `AICPA_regressionAnalysisData.csv`
- **Columns:** `type` (training/testing split), `date`, `revenue`, `production`, `coolDD` (cooling degree days), `heatDD` (heating degree days)
- **Split:** Data is pre-labeled as `dt4training` (2011–2013) and `dt4testing` (2014)

## Feature Engineering

- `date` converted to a proper datetime type
- `winter_DV`: dummy variable = 1 if month is Dec, Jan, or Feb, else 0
- `fall_DV`: dummy variable = 1 if month is Sep, Oct, or Nov, else 0
- `winter_interaction`: `production × winter_DV`
- `fall_interaction`: `production × fall_DV`

## Models

Both models are fit with `statsmodels.OLS` on the training split (`dt4training`).

**Model 1 — Winter effect**
`revenue ~ production + winter_DV + winter_interaction`

| Term | Coefficient |
|---|---|
| const | 5,629,257.08 |
| production | 13.51 |
| winter_DV | -201,742.73 |
| winter_interaction | 14.16 |

**Model 2 — Fall effect**
`revenue ~ production + fall_DV + fall_interaction`

| Term | Coefficient |
|---|---|
| const | 6,118,386.30 |
| production | 18.30 |
| fall_DV | -477,240.43 |
| fall_interaction | -7.67 |

## Visualizations

- **Winter model plot:** scatter of production vs. revenue with two fitted lines — non-winter months (pink) vs. winter months (blue). The winter line sits above and rises faster, indicating production converts to revenue more efficiently in winter months.
- **Fall model plot:** scatter of production vs. revenue with two fitted lines — non-fall months (yellow) vs. fall months (orange).

## Requirements

```
pandas
numpy
matplotlib
statsmodels
```

## Usage

Run the notebook top to bottom in Google Colab or Jupyter. Ensure `AICPA_regressionAnalysisData.csv` is in the working directory before running the first cell.

##Author

Aaliyah Thomas
