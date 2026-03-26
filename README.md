# Flight Activity & Customer Loyalty Analysis: A Data-Driven Insights Project

  Author: Natalia Pozo 
  Bootcamp: Adalab - Data Analytics (Module 3)
  Target Environment: Python 3.13.9

## 📝 Descripction

This project delivers a comprehensive end-to-end data analysis workflow, transforming raw airline transactional and demographic data into actionable insights.

The primary goal is to process and analyze two distinct datasets from an airline's loyalty program to identify patterns in flight activity and evaluate correlations within customer demographic profiles.

The project focuses on ensuring data quality through rigorous processing and provides a statistical foundation for understanding customer behavior within a loyalty framework.

## 📂 Data Architecture & Repository

The project structure is organized to separate raw inputs, processed outputs, and analytical stages:

### Source Layers (Raw Data):
- Customer Flight Activity.csv: Transactional core with >405,000 records. Contains time-series data of monthly bookings, distances, and points.
- Customer Loyalty History.csv: Demographic master file with >16,000 records (location, education, salary, and loyalty tier).

### Production Layer (Processed Data):
- customer_loyalty_cleaned.csv: Fully integrated dataset after cleaning, MNAR handling, and segmented imputation.

### Analytical Layers:
- flight_loyalty_analysis.ipynb: Focuses on EDA, Outlier Auditing, and Spearman Correlation.
- flight_loyalty_questions.ipynb: Dedicated to Business Intelligence (Phase 3) and Hypothesis Evaluation (Phase 4).

## ✨ Methodological Framework

### Phase 1: Advanced Data Engineering & Cleaning
- Transactional Merge (Broadcasting Strategy): Implemented a Left Join using the flight activity table as the anchor and 'Loyalty Number' as the unique relational identifier (Primary Key). This approach preserves the monthly granularity of the transactional data while broadcasting static demographic attributes to every flight record. Optimized using int64 identifiers for memory efficiency.
- MNAR Handling (Cancellation Logic): Identified a Missing Not At Random (MNAR) pattern in cancellation dates. Since 87.65% of the data was missing because customers hadn't cancelled, we transformed this into a boolean "Active Status" feature.
- Segmented Salary Imputation: Handled 25.32% missingness in Salary using Grouped Imputation Logic (Education + Loyalty Card) via Lambda functions, preserving the natural variance of the population.

### Phase 2: Statistical Rigor & Correlation
- Visual Outlier Audit: Used Boxplots with independent scales to inspect dispersion in Flights, Salary, and Points Accumulated.
- Non-parametric Correlation (Spearman): Essential due to the non-normal distribution of demographic data. This was the tool that statistically disproved the link between income and travel frequency.

### Phase 3 & 4: Business Intelligence & Integrity Safeguards
- Dual-Track Analysis: To prevent Synthetic Bias, specific socio-economic questions were cross-referenced between original and imputed datasets.
- The "College" Category Case: To maintain high data standards, "College" graduates were excluded from salary-based charts because their missing values were deemed non-imputable under strict reliability criteria. Analysis focused on the 75% core data.


## 🛠️ echnical Stack & Environment
- Core: Python 3.13.9
- Libraries: pandas, numpy, seaborn, matplotlib (including ticker and Line2D).
- Configuration: warnings suppressed for production-clean output; pd.set_option configured for full feature inspection.

## 🔮 Strategic Recommendations (Roadmap)
- ID Governance: Maintain the Loyalty Number as the primary index in future ETL migrations to ensure transactional traceability.
- Imputation Policy: Collaborate with business stakeholders to define a formal standard for "College" salary estimation to complete the demographic profile.
- Churn Analysis: Leverage the new "Active Status" flag to develop a Retention Predictive Model.
- Interactive BI: Transition static reporting to a Streamlit/Plotly Dashboard for real-time stakeholder exploration.

> *This documentation serves as a record of analytical excellence and data-driven decision support. Any feedback on the code or structure is welcome*

