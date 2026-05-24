# Tech Layoffs — End-to-End SQL Analysis (2020–2023)

A complete data analytics project covering the full workflow from raw data to business insights — data cleaning, standardization, and exploratory analysis on global tech industry layoffs using MySQL.

---

## Project Structure

- `1_data_cleaning.sql` — Step 1: Clean and prepare the raw data
- `2_exploratory_analysis.sql` — Step 2: Analyze the cleaned data

Run `1_data_cleaning.sql` first. It produces `layoffs_staging2`, which is the input for `2_exploratory_analysis.sql`.

---

## Dataset

- **Source:** layoffs.fyi — tracking global tech layoffs since COVID-19
- **Coverage:** 2020–2023
- **Fields:** Company, location, industry, total laid off, percentage laid off, date, funding stage, country, funds raised

---

## Script 1 — Data Cleaning

Starting from raw, unprocessed layoffs data, this script builds a professional multi-stage cleaning pipeline that produces a reliable, analysis-ready dataset.

**Duplicate Removal**
- Creates a staging table to preserve the original raw data before making any changes
- Uses ROW_NUMBER() window functions with PARTITION BY across all key columns to flag duplicate records
- Builds a secondary staging table to safely delete duplicates without touching the source data

**Standardization**
- Trims leading and trailing whitespace from all company names using TRIM()
- Consolidates all Crypto industry variants into a single standardized value
- Removes trailing periods from country name entries
- Converts the date column from VARCHAR string format to proper SQL DATE type using STR_TO_DATE()

**Null Handling**
- Identifies and investigates NULL and blank values across key columns
- Removes records where both total_laid_off and percentage_laid_off are NULL

**Skills Demonstrated**
- Staging table methodology
- Window functions (ROW_NUMBER, PARTITION BY)
- String cleaning (TRIM, LIKE, trailing character removal)
- Data type conversion (VARCHAR to DATE)
- NULL handling and targeted record deletion
- Schema modification using ALTER TABLE

---

## Script 2 — Exploratory Data Analysis

Using the cleaned `layoffs_staging2` table as input, this script surfaces meaningful trends and patterns across companies, industries, countries, and time periods.

**Questions Explored**
- Which companies laid off the most employees in total?
- Which industries and countries were hit hardest?
- How did layoffs trend month over month?
- Which companies laid off 100% of their workforce and how much had they raised?
- Who were the top 5 companies by layoffs each year?

**Key Findings**
- Amazon, Google, Meta, Salesforce, and Microsoft ranked among the highest total layoffs
- The Consumer and Retail industries were hit hardest by total headcount reductions
- The United States accounted for the vast majority of all layoffs in the dataset
- 2022 and 2023 saw the sharpest spike driven by post-pandemic correction and rising interest rates
- Several companies that raised hundreds of millions still laid off 100% of their workforce
- Post-IPO stage companies accounted for the highest total layoffs

**Skills Demonstrated**
- Aggregate functions (SUM, MAX, AVG, MIN)
- GROUP BY with multiple dimensions
- Time-series analysis using SUBSTRING date parsing
- Rolling totals using SUM() OVER window functions
- DENSE_RANK() with PARTITION BY for year-over-year ranking
- Nested CTEs for multi-step analytical pipelines

---

## Tools
- MySQL
- MySQL Workbench

---

## How to Run
1. Open MySQL Workbench and connect to your local server
2. Run `1_data_cleaning.sql` — this creates and populates `layoffs_staging2`
3. Run `2_exploratory_analysis.sql` — this queries `layoffs_staging2` for insights
