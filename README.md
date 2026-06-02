# Data Cleaning Project — Tech Layoffs Dataset

## Overview
This project demonstrates end-to-end data cleaning of a real-world tech layoffs dataset using **MySQL**. The raw data contains duplicates, inconsistent formatting, null values, and incorrect data types — all of which are systematically identified and resolved.

## Tools & Skills Used
- **MySQL** — window functions, CTEs, JOINs, ALTER TABLE, STR_TO_DATE
- Data staging with duplicate table strategy
- String normalization and date type conversion
- Self-join technique to populate missing values from related rows

## What the Project Covers

### 1. Remove Duplicates
- Created a staging table (`layoffs_staging`) to preserve the original data
- Used `ROW_NUMBER()` with `PARTITION BY` across all key columns to flag exact duplicates
- Deleted duplicate rows safely via a second staging table (`layoffs_staging2`)

### 2. Standardise the Data
- Trimmed leading/trailing whitespace from `company` names using `TRIM()`
- Consolidated variant industry labels (e.g. `Crypto Currency` → `Crypto`) using `LIKE` matching
- Cleaned trailing punctuation from `country` values (e.g. `United States.` → `United States`)
- Converted `date` column from text to proper `DATE` type using `STR_TO_DATE()` and `ALTER TABLE`

### 3. Handle NULL and Blank Values
- Standardised blank strings to `NULL` for consistent querying
- Used a **self-join** on `company` to backfill missing `industry` values from matching rows
- Removed rows where both `total_laid_off` and `percentage_laid_off` were NULL (unusable records)

### 4. Remove Unnecessary Columns
- Dropped the `row_num` helper column after deduplication was complete

## Key SQL Techniques Demonstrated

| Technique | Purpose |
|---|---|
| `ROW_NUMBER() OVER (PARTITION BY ...)` | Detect duplicates |
| CTE (`WITH ... AS`) | Isolate duplicates before deletion |
| Self-JOIN | Fill NULL industry from sibling rows |
| `STR_TO_DATE()` + `ALTER TABLE` | Fix column data type |
| `TRIM()` / `LIKE` / `UPDATE` | Standardise text fields |

## Dataset
The dataset tracks tech industry layoffs including company, location, industry, total laid off, percentage laid off, funding stage, country, and funds raised.

> Raw data sourced from public layoffs tracking records.

## How to Run
1. Import the original `layoffs` table into your MySQL database
2. Run `data_cleaning_project1.sql` in order — each section is labelled with a comment
3. The final cleaned table is `layoffs_staging2`

## Files
| File | Description |
|---|---|
| `data_cleaning_project1.sql` | Full data cleaning script |
| `README.md` | Project documentation |
