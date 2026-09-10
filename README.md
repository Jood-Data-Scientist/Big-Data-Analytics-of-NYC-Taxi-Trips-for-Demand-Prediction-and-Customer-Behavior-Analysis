Big Data Analytics of NYC Taxi Trips for Demand Prediction and Customer Behavior Analysis


Overview

This project analyzes NYC Yellow Taxi trip data to extract urban mobility patterns and investigate factors affecting trip duration and cost, supporting data-driven decision-making for smart transportation systems. It qualifies as a Big Data problem due to its Volume (millions of records), Variety (temporal, spatial, financial, and operational attributes), and Value (actionable insights for demand prediction and fleet management).



Objectives

Taxi Fare Prediction — Estimate total fare amount from trip characteristics (distance, duration, time of day) to support dynamic pricing and pricing transparency.
Urban Demand Analysis — Identify peak demand periods, high-traffic areas, and passenger behavior to help optimize fleet distribution and service efficiency.
Architecture
The system follows a multi-layer Big Data ecosystem:




Data Source (NYC TLC CSV, Kaggle)


   → Data Ingestion (PySpark, batch load from Google Drive)
   
   → Distributed Storage (Google Drive, simulating cloud object storage)
   
   → Processing Layer (Apache Spark / PySpark — cleaning, transformation, feature engineering)
   
   → Processed Storage (Parquet)
   
   → Analytics & ML (K-Means clustering, Random Forest Regression via PySpark MLlib)
   
   → Visualization Layer (Power BI interactive dashboard)
   



Data

Source: NYC Yellow Taxi Trip Data (Kaggle), based on official NYC Taxi and Limousine Commission (TLC) records.

Format: CSV, multiple files (~2 GB each), millions of records; original working sample of 1,000,000 rows.

Key attributes: pickup/drop-off timestamps, geographic coordinates, trip distance, passenger count, fare components, total amount, payment type.




Data Processing

Converted pickup/drop-off datetime columns to timestamp format.

Handled missing values (row removal for critical fields, median imputation for passenger count).

Removed invalid trips (negative/zero distance or fare) and outliers (IQR-based filtering on trip distance).

Rows reduced from 1,000,000 → 938,823 after cleaning.




Feature Engineering

trip_duration (minutes), speed (distance/duration), pickup_hour, rush_hour flag, day_of_week.

Expanded dataset to 20+ columns.

K-Means clustering (K=5) applied to pickup coordinates to identify major geographic demand clusters (kept as a separate output, not merged into the final saved dataset).




Machine Learning

Model: Random Forest Regressor (PySpark ML), trained on a 5% sample for memory efficiency.

Pipeline: StringIndexer (categorical encoding) → VectorAssembler (feature vector: trip distance, duration, pickup hour, rush hour) → RandomForestRegressor.

Split: 80% train / 20% test.

Evaluation: RMSE = 8.14 on fare prediction.




Results & Insights

Peak demand: Hour 19 (7 PM), with a secondary morning surge starting at 7 AM.

Dynamic pricing signal: Rush-hour fares are consistently higher across short, medium, and long trip distances.

Average trip speed: 11.73 mph overall, reflecting significant urban congestion.

Vendor comparison (CMT vs. VeriFone):

VeriFone: ~489.5K trips, more diverse group-size passenger distribution.

CMT: ~449.2K trips, dominated by single-passenger trips (64.32%), higher average speed (12.10 mph).

Both vendors show consistent tipping behavior (~12.82% average tip).

Revenue: Saturday is the highest-revenue day (over $2M).




Interactive dashboard: Power BI Dashboard



Resources

Google Colab Implementation (PySpark Notebook)

NYC Yellow Taxi Trip Dataset (Kaggle)
