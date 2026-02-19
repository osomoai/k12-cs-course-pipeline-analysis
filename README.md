# k12-cs-course-analysis
A reproducible R-based pipeline that cleans, harmonizes, and integrates CRDC and CCD data to support analysis of K–12 computer science course access and enrollment in U.S. schools (2020–2022). 

**Author:** Omodolapo Ojo, PhD  

---

## Project Overview

This project analyzes the availability and enrollment patterns of K–12 Computer Science (CS) courses across U.S. public schools using the Civil Rights Data Collection (CRDC) and the Common Core of Data (CCD) for the 2020–21 and 2021–22 school years.

**This repository demonstrates a full data engineering pipeline**, including:

- Data ingestion from multiple raw sources  
- Cleaning and harmonization of inconsistent variables  
- Standardization of unique school identifiers (`NCESSCH` / `Combined_Key`)  
- Merging multi-year datasets  
- Validation of logical consistency and negative values  
- Derivation of aggregated and proportional variables  
- Production of analysis-ready datasets and visualizations  

This is not just analysis — it is a **reproducible, multi-step data engineering workflow** that transforms messy administrative datasets into a clean, integrated resource ready for policy research.

---

## Focus Questions

1. How widely available are CS courses across U.S. schools?  
2. Does CS access differ by Title I status?  
3. How does CS availability vary by school level?  
4. What are the gender participation patterns in CS?  
5. What is the racial composition of CS enrollment?  
6. Did CS access change between 2020–21 and 2021–22?  

---

## Data Sources

### Civil Rights Data Collection (CRDC)  
- Contains school-level enrollment, course offerings, and student demographic data  
- Publicly available: [CRDC Data Portal](https://ocrdata.ed.gov/)  
- Datasets used: 2020–21 and 2021–22 K–12 CS enrollment tables  

### Common Core of Data (CCD)  
- Contains school characteristics, enrollment counts by grade, and Title I status  
- Publicly available: [CCD Data Files](https://nces.ed.gov/ccd/)  
- Datasets used: School characteristics and membership files for 2020–21 and 2021–22  

**Note:** Raw datasets are not hosted here due to size. Users must download them separately and place them in the `data/` folder before running the analysis.

---

## Method/Data Engineering Pipeline

1. **Data Ingestion**
   - Read multiple CSV files from CRDC and CCD for 2020–21 and 2021–22  
   - Separate files for enrollment, school characteristics, and membership

2. **Variable Selection & Harmonization**
   - Selected only necessary columns  
   - Renamed all variables to **human-readable, consistent names**  
   - Standardized categorical variables (e.g., LEP → EL)

3. **Identifier Standardization**
   - Converted `Combined_Key` and `NCESSCH` to 12-character strings  
   - Ensured uniqueness of identifiers for safe joins

4. **Dataset Merging**
   - Left-joined CRDC and CCD datasets with membership files  
   - Collapsed multi-grade membership data into school-level totals  
   - Produced one long-format multi-year dataset

5. **Data Validation & Cleaning**
   - Replaced negative values with `NA`  
   - Flagged inconsistencies (e.g., race totals exceeding total enrollment)  
   - Removed logically inconsistent rows  

6. **Derived Variables**
   - Aggregated race and gender totals  
   - Calculated proportional participation by race and gender  
   - Derived school-level indicators for Title I and grade levels

7. **Output Generation**
   - Clean analytical datasets (`combined_data_clean_final.csv`)  
   - Data dictionary (`data_dictionary.csv`)  
   - Summary tables (Title I, grade, race, gender, CS participation)  
   - Visualizations (histograms, bar charts, participation status plots)  

> **Note:** Every step is reproducible via `K12_CS_Analysis.Rmd`. This is a full **data engineering → analysis → visualization pipeline**.

---

## Outputs

### 1. Cleaned Analytical Dataset
Located in `output/`

- `combined_data_clean_sample.csv` — Sample of final harmonized dataset  
- `data_dictionary.csv` — Variable definitions, types, and descriptions  

---

### 2. Summary Tables
Located in `output/`

| File | Description |
|------|-------------|
| `titleI_summary.csv` | CS access by Title I status |
| `grade_level_summary.csv` | CS availability by school level |
| `gender_summary.csv` | Average gender composition of CS enrollment |
| `race_summary.csv` | Racial composition of CS enrollment |
| `cs_status_table.csv` | Schools offering vs. not offering CS |
| `distribution_summary.csv` | Distribution of CS classes offered |

---

### 3. Visualizations
Located in `figures/`

| File | Description |
|------|-------------|
| `fig1_distribution.png` | Distribution of CS classes offered |
| `fig_cs_status.png` | CS participation status |
| `gender_share.png` | Gender composition of CS enrollment |
| `titleI_access.png` | CS access by Title I status |
| `grade_level_access.png` | CS availability by grade level |

---

### 4. Reproducible Report

- `K12_CS_Analysis.Rmd` — Full R Markdown workflow with code, tables, and figures  
- `K12_CS_Analysis.html` — Rendered HTML report for a formatted view  

All figures and tables are automatically generated when you knit the `.Rmd` file.

---

## Data Description

Key variables in the final dataset:

| Variable | Description |
|----------|-------------|
| `Combined_Key` | Unique 12-digit school identifier |
| `SCHOOL_YEAR` | School year of data (2020–21 or 2021–22) |
| `CS_Classes_Offered` | Number of CS courses offered at the school |
| `Total_CS_Enrolment` | Total students enrolled in CS courses |
| `Prop_Male_CS` | Proportion of male students in CS courses |
| `Prop_White_CS`, `Prop_Black_CS`, etc. | Proportion of students in CS by race |
| `TITLEI_STATUS_TEXT` | Title I status of the school |
| `Elementary`, `Middle`, `High` | School grade-level indicators |
| Additional columns | Derived enrollment totals, proportional measures, and validation flags |

---

## Reproducibility

To reproduce the analysis:

1. Download CRDC and CCD datasets from the links above.  
2. Place them in the `data/` folder of this repository.  
3. Open `K12_CS_Analysis.Rmd` in RStudio and click **Knit**.  

All figures, tables, and the cleaned dataset will be automatically generated.

---

## Contribution

This repository demonstrates:

- Large-scale administrative data integration  
- End-to-end reproducible data engineering workflows  
- Equity-focused education policy analysis  
- Structured validation and transformation pipelines  

---

