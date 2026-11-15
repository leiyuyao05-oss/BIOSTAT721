
# Air Pollution and Sickle Cell Disease: Exploratory Data Analysis

## 1. Project Description

This project conducts exploratory data analysis (EDA) of daily air quality measurements collected from the U.S. Environmental Protection Agency (EPA) monitoring station at Raleigh-Durham International Airport (RDU), North Carolina.

The project focuses on three air pollutants:

- Carbon monoxide (CO)
- Fine particulate matter (PM2.5)
- Ozone (O3)

The primary objectives are to:

1. Develop a reusable R function to clean and process raw daily air quality measurements.
2. Combine data from 2018, 2019, and 2020 into a single processed dataset.
3. Calculate annual minimum and maximum daily concentrations for each pollutant.
4. Examine monthly patterns in CO and O3 using monthly means and 95% confidence intervals.
5. Compare monthly distributions of PM2.5 across different years.

The analysis provides an exploratory overview of temporal variation in air pollution concentrations and may help inform future research investigating environmental exposures and sickle cell disease (SCD)-related healthcare utilization.

**Study period:** January 2018 – April 2020.

**Note:** The 2020 dataset contains observations only through April.

---

## 2. Data Source

The air quality data were obtained from the U.S. Environmental Protection Agency (EPA).

The measurements were collected from the EPA air pollution monitoring station at:

**Raleigh-Durham International Airport (RDU), North Carolina, USA.**

Three annual CSV files are used:

| Dataset | Coverage |
|---|---|
| AQ_2018.csv | January–December 2018 |
| AQ_2019.csv | January–December 2019 |
| AQ_2020.csv | January–April 2020 |

Each dataset contains daily measurements of:

- CO: Daily maximum 8-hour concentration (ppm).
- PM2.5: Daily mean concentration (µg/m³).
- O3: Daily maximum 8-hour concentration (ppm).

The original datasets may contain multiple measurements for the same date, exact duplicate records, negative measurements, and missing values. These issues are addressed in the data-processing function.

The original ozone measurements are assumed to be recorded in ppm. The processing function also supports conversion to ppb.

---

## 3. Repository Structure

The repository (URL: https://github.com/leiyuyao05-oss/BIOSTAT721.git) is organized as follows:

```text
Yuyao_Lei_Project2(branch)
│
├── R_airquality_SCD.Rproj
│
├── data/
│   ├── AQ_2018.csv
│   ├── AQ_2019.csv
│   └── AQ_2020.csv
│
├── project2.Rmd
│
├── README.md
│
└── .gitignore
```

### Key Files and Directories

| File/Directory | Description |
|---|---|
| `data/` | Contains the three original annual air quality CSV files. |
| `project2.Rmd` | Main analysis document containing data import, data cleaning, the processing function, descriptive statistics, plots, and interpretation. |
| `README.md` | Provides project documentation and instructions for reproducing the analysis. |
| `R_airquality_SCD.Rproj` | RStudio project file. |

The data-processing function is defined and documented directly in the R Markdown report.

---

## 4. Data Processing and Analysis

### 4.1 Data Processing

A reusable function, `process_air_quality()`, is developed to process one annual CSV file.

The function performs the following steps:

1. Reads the input CSV file.
2. Selects and renames the date and pollutant concentration variables.
3. Converts the date variable to the Date class and pollutant concentrations to numeric values.
4. Removes exact duplicate rows.
5. Replaces negative pollutant concentrations with zero.
6. Converts ozone concentrations to the requested unit (ppm or ppb).
7. Aggregates multiple measurements on the same date by calculating daily averages.

The function returns a clean tibble with one observation per calendar day.

### 4.2 Descriptive Statistics

For each year (2018, 2019, and 2020), minimum and maximum daily concentrations are calculated for CO, PM2.5, and O3.

All summary statistics are reported to three decimal places, with measurement units clearly indicated.

### 4.3 Exploratory Data Analysis

Two plots are generated:

**Plot 1: Monthly Patterns in CO and O3**

- Monthly mean daily concentrations are calculated by pooling all available observations from the three years.
- Error bars represent 95% confidence intervals calculated as:

  mean ± 1.96 × standard deviation / √n

- CO and O3 are displayed in separate panels with independent y-axis scales to accommodate their different concentration magnitudes.

**Plot 2: Monthly PM2.5 Distributions by Year**

- Daily PM2.5 measurements are grouped by calendar month and year.
- Boxplots are used to compare monthly distributions, medians, variability, and potential outliers.
- Different colors represent 2018, 2019, and 2020.

Because 2020 data are available only through April, comparisons for May through December include only 2018 and 2019.

---

## 5. How to Reproduce the Analysis

### 5.1 Software Requirements

The analysis requires:

- R (version 4.3.0 or later recommended).
- RStudio (recommended).
- R Markdown.
- A working LaTeX installation is not required because the report is rendered to Word.

### 5.2 Required R Packages

The following R packages are used:

| Package | Purpose |
|---|---|
| `tidyverse` | Data manipulation, reshaping, and visualization |
| `lubridate` | Date conversion and extraction of calendar months |
| `knitr` | Generating tables and rendering the R Markdown report |
| `scales` | Additional plotting scale utilities |

Install the required packages using:

```r
install.packages(c(
  "tidyverse",
  "lubridate",
  "knitr",
  "scales",
  "rmarkdown"
))
```

### 5.3 Clone the Repository

Clone the GitHub repository to your local computer:

```bash
git clone https://github.com/leiyuyao05-oss/BIOSTAT721.git
```

Open the downloaded project by double-clicking:

`R_airquality_SCD.Rproj`

Alternatively, open the project through RStudio.

### 5.4 Add the Data Files

Place the three original CSV files in the `data/` directory.

Ensure that their filenames match those specified in the R Markdown file:

```text
data/AQ_2018.csv
data/AQ_2019.csv
data/AQ_2020.csv
```

If the filenames differ, update the corresponding file paths in the data-import section of `Project2_Report.Rmd`.

### 5.5 Render the Report

Open `project2.Rmd` in RStudio.

The report can be rendered by clicking the **Knit** button and selecting Word output, or by running:

```r
rmarkdown::render(
  "project2.Rmd",
  output_format = "word_document"
)
```

The rendered Word document will be saved in the project directory as:

```text
project2.docx
```

The final Word document displays the analysis results, tables, plots, and interpretations while hiding the underlying R code.

---

## 6. Reproducibility and Version Control

The project is maintained using Git and GitHub.

Changes are committed throughout the development process to document the progress of data processing and analysis.

For example:

**First commit: Project setup and data processing**

```bash
git switch Yuyao_Lei_Project2
git add R_airquality_SCD.Rproj data/ project2.Rmd README.md
git commit -m "Set up project and implement air quality data processing"
git push -u origin Yuyao_Lei_Project2
```

**Second commit: EDA and report completion**

```bash
git switch Yuyao_Lei_Project2
git add project2.Rmd README.md project2.docx
git commit -m "Complete descriptive statistics and exploratory data analysis"
git push -u origin Yuyao_Lei_Project2
```

The repository contains the source data, analysis code, and project documentation required to reproduce the analysis.

---

## 7. Author and Date

**Author:** Yuyao Lei

**Institution:** Duke University, Master of Biostatistics

**Project:** Project 2 – Air Quality Exploratory Data Analysis

**Date:** November 15, 2026
