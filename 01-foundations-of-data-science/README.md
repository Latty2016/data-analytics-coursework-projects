# NYC Taxi Fare Data — Inspection & Cleaning Readiness Review

**Course:** Foundations of Data Science (Google Advanced Data Analytics Certificate)
**Client scenario:** Automatidata
**Tools:** Python, pandas, NumPy, Jupyter Notebook

## Project Overview

This project reviews a 2017 NYC Yellow Taxi trip dataset (22,699 trips, 18 columns) to assess its structure and quality ahead of building a predictive model for `fare_amount`. The goal was not to build the model itself, but to determine whether the data is **ready for exploratory data analysis (EDA)** — checking data types, completeness, and flagging anomalies that could distort future analysis or modeling.

## What I Did

- Loaded the dataset into a pandas DataFrame and ran a full structural review (`.info()`, `.describe()`, `.dtypes`, `.isnull().sum()`)
- Sorted and inspected key variables (`trip_distance`, `total_amount`) at both extremes to identify outliers and anomalies
- Grouped and aggregated data (e.g., average tip by passenger count, average total by vendor) to surface patterns
- Distinguished true continuous numeric variables from categorical/ID fields stored as numbers (e.g., `VendorID`, `RatecodeID`, `payment_type`) to avoid misleading statistics
- Documented data quality issues and made recommendations for next steps, following the PACE (Plan, Analyze, Construct, Execute) framework

## Key Findings

- **No missing values** across any of the 22,699 rows or 18 columns
- **Implausible values** found: negative fares, taxes, and surcharges (as low as -$120); 0-passenger trips; 0-mile trips (some with real elapsed time, suggesting recording errors rather than genuine zero-distance rides)
- **Invalid category code**: `RatecodeID` includes a value of 99, outside the documented range of valid rate codes
- **Extreme outliers**: a small number of records with unusually high `fare_amount`, `tip_amount`, and `total_amount` (e.g., a single $1,200.29 total — more than double the next-highest value)
- **Right-skewed fare distribution**: mean `fare_amount` ($13.03) is notably higher than the median ($9.50), indicating the average is being pulled upward by outliers
- Datetime columns (`tpep_pickup_datetime`, `tpep_dropoff_datetime`) are stored as text and need conversion before they can be used to engineer features like trip duration

## Recommended Predictors

Based on this review, **`trip_distance`** and an engineered **trip duration** variable (from the pickup/dropoff timestamps) are the strongest candidates for predicting `fare_amount`, given their direct, logical relationship to how taxi fares are calculated.

## Recommended Next Steps

1. Convert datetime columns and engineer a `trip_duration` feature
2. Investigate and resolve negative-value and outlier records
3. Decide how to handle 0-passenger and 0-distance trips
4. Proceed to full exploratory data analysis on the cleaned dataset

## Files in This Folder

| File | Description |
|---|---|
| `Automatidata_project_proposal.docx` | Initial project proposal outlining scope, milestones, and stakeholders |
| `Automatidata_data_inspection.ipynb` | Full notebook: data loading, structural review, sorting, filtering, and grouping analysis |
| `PACE_strategy_document.docx` | Planning and reflection document following the PACE framework |
| `Automatidata_Executive_Summary.pptx` | Stakeholder-facing summary slide of key findings and recommendations |

## Skills Demonstrated

`pandas` · data structure inspection · missing value & outlier detection · data quality assessment · categorical vs. continuous variable handling · exploratory groupby analysis · stakeholder communication
