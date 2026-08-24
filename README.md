# Employee Dataset Cleaning & Preprocessing Pipeline

An automated data cleaning and transformation pipeline built in Python to process, clean, and standardize messy human resources (HR) records. The pipeline resolves typical data quality issues—such as missing values, inconsistent department and job title casing, unformatted compensation fields, mixed date formats, and duplicate records.

---

## Project Overview

* **Task:** Raw HR / Employee Data Cleaning & Wrangling
* **Core Objectives:**
  * Clean and normalize categorical fields (Department, Job Title, Employment Status).
  * Standardize compensation values by stripping currency symbols, commas, and parsing invalid entries.
  * Parse multi-format hire and termination dates into standard `datetime` objects.
  * Validate and format contact details (emails, phone numbers).
  * Identify and resolve duplicate employee entries and handle missing data systematically.

---

## Dataset Schema

### Initial Attributes
* `EmployeeID`: Unique employee identifier.
* `FullName`: Employee name with inconsistent casing and extra whitespace.
* `Department`: Department name with varied formatting and abbreviations.
* `JobTitle`: Role/designation with irregular capitalization.
* `HireDate`: Date of joining stored in inconsistent string formats.
* `Salary`: Compensation containing currency symbols (`$`, `€`), commas, and text markers (`N/A`, `unknown`).
* `EmploymentStatus`: Current status (Full-Time, Part-Time, Contract, Terminated).
* `Email`: Work email addresses requiring validation and lowercase formatting.

### Engineered Features
* `TenureYears`: Calculated years of service based on hire date and termination/current date.
* `SalaryNumeric`: Clean numeric compensation value cast to `float64`.
* `HireYear`, `HireMonth`, `HireQuarter`: Extracted time features for workforce analytics.

---

## Data Cleaning & Transformation Pipeline

| Step | Problem Identified | Solution Applied |
| :--- | :--- | :--- |
| **1. Missing & Empty Records** | Completely empty rows and unindexed entries. | Removed fully empty rows and handled missing identifiers. |
| **2. Whitespace & Text Standardization** | Irregular spaces and mixed text cases. | Applied `.str.strip()` and converted categorical fields to Title Case. |
| **3. Compensation Parsing** | Currency symbols (`$`, `,`), string nulls in salary. | Stripped non-numeric characters using regex and converted to `float64`. |
| **4. Date Normalization** | Mixed date formats (`YYYY-MM-DD`, `MM/DD/YYYY`, `Month DD, YYYY`). | Standardized all dates to uniform `YYYY-MM-DD` datetime format using `dateutil.parser`. |
| **5. Email & Phone Formatting** | Casing inconsistencies and missing domains in emails. | Converted emails to lowercase and validated formatting via regular expressions. |
| **6. Deduplication** | Redundant records matching on `EmployeeID`. | Retained the most recent entry and removed duplicate records. |

---

## Tech Stack & Dependencies

* **Language:** Python 3.10+
* **Libraries:**
  * `pandas` - Data manipulation and cleaning
  * `numpy` - Vectorized operations and missing value handling
  * `python-dateutil` - Multi-format datetime parsing
  * `re` - Regular expressions for text and string pattern matching

---

## Project Structure

```text
├── data/
│   ├── raw_employee_data.csv        # Raw dataset
│   └── cleaned_employee_data.csv    # Exported clean dataset
├── notebooks/
│   └── employee_data_cleaning.ipynb # Step-by-step cleaning notebook
├── requirements.txt                 # Environment dependencies
├── .gitignore
└── README.md
