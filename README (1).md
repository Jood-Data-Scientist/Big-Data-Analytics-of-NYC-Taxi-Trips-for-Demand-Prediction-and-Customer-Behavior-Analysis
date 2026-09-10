# Big Data Analytics of NYC Taxi Trips

**DS5411 — Big Data Mining | Umm Al-Qura University**
Supervised by A/Prof. Olfat Mirza

## Team
Asayel Sloom Alharbi · Reem Ghazi Alosaimi · Wed Fawaz Alshehri · Jood Mohammed Algarni · Shatha Talal Alsulami

## Overview
An end-to-end Big Data pipeline analyzing NYC Yellow Taxi trip data to predict fares and uncover urban demand patterns, supporting smart transportation decisions.

## Architecture
`CSV (Kaggle) → PySpark ingestion → Google Drive (raw storage) → Spark processing/cleaning → Parquet (processed storage) → K-Means & Random Forest (ML) → Power BI dashboard`

## Data
NYC TLC Yellow Taxi trips (Kaggle), ~1M rows → 938,823 after cleaning (outlier/invalid removal, missing value handling).

## Key Steps
- **Feature Engineering:** trip duration, speed, pickup hour, rush hour, day of week; K-Means (K=5) on pickup locations.
- **ML Model:** Random Forest Regressor (PySpark MLlib) for fare prediction — **RMSE = 8.14**.
- **Visualization:** Power BI dashboard with demand, speed, and vendor comparisons.

## Key Results
- Peak demand at 7 PM, with a morning surge from 7 AM.
- Rush hours show consistently higher fares → supports dynamic pricing.
- Average speed 11.73 mph, indicating congestion.
- VeriFone leads in trip volume; CMT leads in speed and single-rider trips.

[Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZGY0YmJiOWYtMTA2OC00MjYwLWJiZWEtYWI4N2IxMDkyMTJmIiwidCI6Ijc5YTA1N2ZiLWIwZDUtNDRkZC04ZjkwLTBiZjcxNTFmNWMzZiIsImMiOjl9) · [Dataset](https://www.kaggle.com/datasets/elemento/nyc-yellow-taxi-trip-data?resource=download) · [Colab Notebook](https://colab.research.google.com/drive/1J_MRkLdDzyctU9khc0eDnu1ePS4GsybN?usp=sharing)

## Notes
Publicly available, non-identifiable data (NYC TLC). Built in Google Colab (single-node) using PySpark to simulate distributed processing; future work targets AWS EMR/Databricks.
