
# PluviaRisk: Parametric Insurance Risk Modelling

A Python-based quantitative risk modelling project that analyses historical monsoon rainfall, simulates parametric insurance payouts, estimates expected claims, and evaluates pricing sensitivity using statistical analysis and bootstrap resampling.

---

## Table of Contents

- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Project Objectives](#project-objectives)
- [How Parametric Insurance Works](#how-parametric-insurance-works)
- [Dataset](#dataset)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Insurance Contract Design](#insurance-contract-design)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Payout Modelling](#payout-modelling)
- [Risk and Pricing Analysis](#risk-and-pricing-analysis)
- [Statistical Analysis](#statistical-analysis)
- [Model Validation](#model-validation)
- [Key Results](#key-results)
- [Installation and Setup](#installation-and-setup)
- [How to Run](#how-to-run)
- [Assumptions and Limitations](#assumptions-and-limitations)
- [Future Improvements](#future-improvements)
- [Disclaimer](#disclaimer)

---

## Overview

PluviaRisk explores how historical rainfall data can be used to design and evaluate a simple parametric rainfall insurance contract.

The project uses daily precipitation observations for Ahmedabad, Gujarat, India, covering 2015–2024. Daily observations are aggregated into June–September monsoon seasons and used to simulate insurance payouts under a predefined rainfall trigger.

The analysis combines data processing, exploratory data analysis, quantitative risk metrics, insurance payout simulation, premium sensitivity analysis, bootstrap resampling, and chronological evaluation.

The objective is to demonstrate the quantitative workflow behind a simplified rainfall-linked insurance product.

### Key Features

- Historical rainfall data acquisition using a weather API
- Data cleaning and quality checks
- Daily and seasonal rainfall analysis
- Monsoon rainfall aggregation
- Parametric insurance payout simulation
- Claim frequency and severity analysis
- Expected annual payout estimation
- Indicative premium calculation
- Trigger sensitivity analysis
- Bootstrap resampling for uncertainty exploration
- Chronological calibration and test-period comparison
- Automated validation of insurance contract rules

---

## Problem Statement

Agriculture and other weather-sensitive economic activities are exposed to rainfall variability, drought conditions, and extreme precipitation events.

Traditional insurance may require individual loss assessments, which can involve additional time and administrative effort.

Parametric insurance offers an alternative approach in which payouts depend on predefined, measurable environmental conditions rather than solely on the assessment of actual individual losses.

However, designing a useful parametric product requires careful consideration of:

- Historical weather patterns
- Trigger thresholds
- Payout structures
- Expected claims
- Pricing assumptions
- Uncertainty in historical estimates
- The relationship between the selected trigger and actual economic losses

PluviaRisk implements a simplified analytical framework to investigate these factors using historical monsoon rainfall.

---

## Project Objectives

1. Collect and analyse historical rainfall observations.
2. Understand rainfall distribution and seasonal variability.
3. Calculate annual and monsoon-season rainfall metrics.
4. Define a hypothetical parametric rainfall insurance contract.
5. Simulate payouts using a predefined trigger and payout schedule.
6. Estimate historical claim frequency and average payout.
7. Explore indicative premiums under different loading assumptions.
8. Evaluate the sensitivity of expected payouts to trigger selection.
9. Use bootstrap resampling to investigate uncertainty in historical payout estimates.
10. Compare payout behaviour across chronological calibration and test periods.
11. Identify limitations that must be addressed before real-world insurance pricing.

---

## How Parametric Insurance Works

Parametric insurance uses a predefined measurable variable, such as rainfall, temperature, wind speed, or another environmental indicator, to determine whether a payout is triggered.

In a rainfall-linked insurance product, the contract may specify a minimum seasonal rainfall threshold.

For example, suppose a contract defines:

- Seasonal rainfall trigger: 800 mm
- Payout rate: ₹100 per millimetre below the trigger
- Maximum payout: ₹20,000

If measured monsoon rainfall is 750 mm, the rainfall shortfall is 50 mm and the resulting payout is ₹5,000.

If rainfall is 1,000 mm, the rainfall trigger is not breached and the payout is zero.

The contract is evaluated using the agreed rainfall measurement and the exact policy terms.

---

## Dataset

### Data Source

Historical daily precipitation data was retrieved from the Open-Meteo Historical Weather API.

API endpoint:

https://archive-api.open-meteo.com/v1/archive

### Geographic Scope

| Parameter | Value |
|---|---|
| Location | Ahmedabad, Gujarat, India |
| Latitude | 23.0225 |
| Longitude | 72.5714 |
| Start date | 2015-01-01 |
| End date | 2024-12-31 |
| Original observations | 3,653 daily records |
| Primary variable | Daily precipitation |
| Unit | Millimetres |
| Time zone | Asia/Kolkata |

### Dataset Fields

| Column | Description |
|---|---|
| `date` | Date of the rainfall observation |
| `rainfall_mm` | Daily precipitation in millimetres |
| `year` | Calendar year derived from the observation date |

The monsoon analysis includes observations from June through September.

The resulting seasonal dataset contains ten annual monsoon observations, one for each year from 2015 through 2024.

### Data Quality Checks

The initial dataset was checked for:

- Missing dates and missing rainfall values
- Number of observations
- Zero-rainfall days
- Rainfall distribution
- Extreme daily rainfall observations
- Annual and seasonal aggregation consistency

The retrieved dataset contained 3,653 records and no missing values in the date or rainfall columns.

**Reproducibility note:** Historical API responses can change as weather datasets are revised. Re-running the API request may therefore produce slightly different values. For reproducibility, preserve the downloaded dataset alongside the notebook.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Pandas | Data manipulation and aggregation |
| NumPy | Numerical calculations and bootstrap resampling |
| Matplotlib | Statistical visualisation |
| Requests | API communication |
| Kaggle Notebooks | Development and execution environment |
| Git and GitHub | Version control and project hosting |

---

## Project Structure

```text
PluviaRisk/
│
├── README.md
├── PluviaRisk.ipynb
├── requirements.txt
├── .gitignore
│
├── data/
│   └── monsoon_rainfall_payouts.csv
│
└── outputs/
    ├── trigger_sensitivity.csv
    └── calibration_test_comparison.csv
```

### File Descriptions

- `README.md`: Project documentation, methodology, results, and limitations.
- `PluviaRisk.ipynb`: Notebook containing data retrieval, analysis, payout simulation, statistical calculations, and visualisations.
- `requirements.txt`: Python dependencies.
- `data/monsoon_rainfall_payouts.csv`: Seasonal rainfall and simulated payout results.
- `outputs/trigger_sensitivity.csv`: Historical payout estimates under different rainfall triggers.
- `outputs/calibration_test_comparison.csv`: Summary of calibration and test-period results.
- `.gitignore`: Excludes temporary files and unnecessary local artifacts.

The directory structure above is the intended repository layout. Create the `data/` and `outputs/` directories when organising the downloaded files.

---

## Methodology

The project follows a sequential quantitative workflow.

### 1. Data Acquisition

Daily precipitation observations were downloaded through the Open-Meteo Historical Weather API.

The response was converted into a Pandas DataFrame for further processing.

### 2. Data Quality Assessment

The dataset was inspected for missing values and basic consistency.

The initial data contained 3,653 observations, with no missing date or precipitation values.

### 3. Exploratory Data Analysis

Descriptive statistics were calculated to understand rainfall behaviour, including:

- Mean and median rainfall
- Standard deviation
- Minimum and maximum rainfall
- Dry-day frequency
- Rainfall distribution
- Annual rainfall totals

### 4. Seasonal Aggregation

Daily observations were filtered to include June, July, August, and September.

The daily rainfall values were summed for each year to calculate seasonal monsoon rainfall.

### 5. Contract Definition

A hypothetical insurance contract was established with a seasonal rainfall trigger, payout rate, and maximum payout.

### 6. Payout Simulation

Each monsoon season was evaluated against the rainfall trigger to calculate its corresponding payout.

### 7. Risk Analysis

Historical payout frequency, average annual payout, total payouts, and average payout conditional on a claim were calculated.

### 8. Pricing Sensitivity

Different premium loading assumptions were applied to the historical average payout.

Alternative rainfall triggers were also tested to evaluate how the expected payout changes with the contract design.

### 9. Bootstrap Resampling

Historical annual payouts were repeatedly resampled with replacement to explore uncertainty in the estimated average payout.

### 10. Chronological Comparison

The historical observations were divided into a calibration period and a later test period to compare payout behaviour across time.

### 11. Contract Validation

Assertions were used to verify that payouts remained non-negative, did not exceed the contract maximum, and matched the defined payout formula.

---

## Insurance Contract Design

The project uses the following illustrative contract parameters.

| Parameter | Value |
|---|---:|
| Reference location | Ahmedabad |
| Covered season | June–September |
| Rainfall trigger | 800 mm |
| Payout rate | ₹100 per mm below trigger |
| Maximum payout | ₹20,000 per season |
| Premium loading assumption | 25% in the initial example |

### Payout Formula

Let:

- \(R\) = observed seasonal rainfall in millimetres
- \(T\) = rainfall trigger
- \(k\) = payout per millimetre of shortfall
- \(M\) = maximum payout

The payout is calculated as:

\[
P(R)=\min\left(\max(T-R,0)\times k,\ M\right)
\]

For the initial contract:

\[
T=800,\quad k=100,\quad M=20{,}000
\]

### Example Calculations

| Seasonal rainfall | Shortfall | Payout |
|---:|---:|---:|
| 500 mm | 300 mm | ₹20,000 |
| 600 mm | 200 mm | ₹20,000 |
| 750 mm | 50 mm | ₹5,000 |
| 800 mm | 0 mm | ₹0 |
| 1,000 mm | 0 mm | ₹0 |

These examples illustrate the contractual payout mechanism rather than an empirically validated insurance product.

---

## Exploratory Data Analysis

The initial daily rainfall analysis produced the following results.

| Metric | Observed value |
|---|---:|
| Daily observations | 3,653 |
| Mean daily rainfall | 2.83 mm |
| Median daily rainfall | 0 mm |
| Standard deviation | 12.42 mm |
| Minimum daily rainfall | 0 mm |
| Maximum daily rainfall | 339.9 mm |
| Dry days | 2,530 |
| Rainy days | 1,123 |
| Percentage of dry days | 69.26% |

The distribution contains a large concentration of zero-rainfall observations and a long right tail.

This indicates that daily rainfall is strongly non-normal and that extreme rainfall observations can have a substantial influence on summary statistics.

### Monsoon Rainfall Results

The June–September aggregation produced the following results.

| Metric | Observed value |
|---|---:|
| Number of monsoon seasons | 10 |
| Average seasonal rainfall | 971.34 mm |
| Standard deviation | 304.43 mm |
| Minimum seasonal rainfall | 564.9 mm |
| Maximum seasonal rainfall | 1,561.5 mm |

The seasonal rainfall values demonstrate substantial variability between years.

These observations provide a starting point for trigger analysis, but ten seasons are insufficient to establish a robust long-term climate-risk distribution.

---

## Payout Modelling

The initial insurance contract was applied to all ten monsoon seasons.

| Year | Monsoon rainfall (mm) | Simulated payout |
|---|---:|---:|
| 2015 | 564.9 | ₹20,000 |
| 2016 | 594.0 | ₹20,000 |
| 2017 | 1,561.5 | ₹0 |
| 2018 | 750.0 | ₹5,000 |
| 2019 | 1,177.4 | ₹0 |
| 2020 | 984.8 | ₹0 |
| 2021 | 935.5 | ₹0 |
| 2022 | 949.5 | ₹0 |
| 2023 | 935.4 | ₹0 |
| 2024 | 1,260.4 | ₹0 |

### Payout Calculation

For 2018:

\[
P=\min((800-750)\times100,\ 20{,}000)
\]

\[
P=₹5{,}000
\]

For 2015:

\[
P=\min((800-564.9)\times100,\ 20{,}000)
\]

The uncapped payout exceeds the maximum, so the contract pays ₹20,000.

### Historical Payout Summary

| Metric | Result |
|---|---:|
| Total seasons | 10 |
| Seasons with payouts | 3 |
| Historical payout frequency | 30% |
| Total payouts | ₹45,000 |
| Average annual payout | ₹4,500 |
| Average payout conditional on a claim | ₹15,000 |
| Maximum annual payout | ₹20,000 |

The average annual payout includes all ten seasons, including those with zero payouts.

The average payout conditional on a claim includes only the three seasons with positive payouts.

---

## Risk and Pricing Analysis


### 1. Expected Annual Payout

The historical expected payout is the average payout across all 10 observed monsoon seasons.

**Formula:**

Average Annual Payout = Total Historical Payouts / Number of Seasons

**Calculation:**

Average Annual Payout = ₹45,000 / 10 = **₹4,500**

This represents the historical average payout under the selected insurance contract. It is not automatically equal to the premium required for a sustainable insurance product.

### 2. Indicative Premium

A simplified premium estimate can be calculated by applying a loading rate to the historical average payout.

**Formula:**

Indicative Premium = Average Annual Payout × (1 + Loading Rate)

Where:
- Average Annual Payout = ₹4,500
- Loading Rate = 25% or 0.25

**Calculation:**

Indicative Premium = ₹4,500 × (1 + 0.25)

Indicative Premium = ₹4,500 × 1.25 = **₹5,625**

The resulting illustrative annual premium is **₹5,625 per policy**.

The 25% loading is hypothetical. It has not been calibrated using actual expenses, capital requirements, reinsurance costs, or actuarial risk margins.



### 3. Premium Sensitivity Analysis

| Assumed loading | Indicative annual premium |
|---:|---:|
| 10% | ₹4,950 |
| 25% | ₹5,625 |
| 40% | ₹6,300 |
| 50% | ₹6,750 |

The analysis demonstrates how premium estimates change when the loading assumption changes.

It does not establish which loading is appropriate for a commercial insurance product.

---

## Trigger Sensitivity Analysis

The payout model was also evaluated using alternative rainfall triggers.

The payout rate remained ₹100 per millimetre, and the maximum payout remained ₹20,000.

| Rainfall trigger | Payout frequency | Average annual payout |
|---:|---:|---:|
| 700 mm | 20% | ₹2,411 |
| 800 mm | 30% | ₹4,500 |
| 900 mm | 30% | ₹5,500 |
| 1,000 mm | 70% | ₹7,948 |

The historical results show that a higher rainfall trigger generally increases the payout exposure under this contract.

Payout frequency and average payout do not necessarily increase at the same rate because the amount paid in each triggered season also matters.

Trigger selection should ultimately reflect the intended coverage, agricultural requirements, available loss data, and the financial characteristics of the insurance product.

---

## Statistical Analysis

### 1. Bootstrap Resampling

Bootstrap resampling was used to investigate how the estimated average annual payout varies when the ten historical annual payouts are resampled with replacement.

The procedure used 10,000 bootstrap samples, each containing ten observations.

For each sample, the average annual payout was calculated.

The 2.5th and 97.5th percentiles of the resulting bootstrap distribution were used to construct a percentile interval.

The initial run produced an approximate 95% bootstrap interval of ₹0–₹10,000.

This interval is sensitive to the small sample and the presence of years with zero payouts and years with maximum payouts.

It should not be interpreted as a guarantee of future payouts or as a complete actuarial uncertainty estimate.

### 2. Annual Payout Variability

| Metric | Result |
|---|---:|
| Mean annual payout | ₹4,500 |
| Standard deviation of annual payouts | ₹8,316.65 |
| Years with zero payout | 7 |
| Years with maximum payout | 2 |

The large standard deviation relative to the mean indicates substantial variability in the observed annual payouts.

This reinforces the need for a longer historical record and more comprehensive risk modelling before making pricing decisions.

---

## Model Validation

The payout calculation was validated using automated assertions.

The checks verified that:

1. Every payout is non-negative.
2. No payout exceeds the maximum contractual payout.
3. The simulated payout matches the specified trigger and payout formula.

All validation checks passed.

These checks establish that the payout calculation follows the implemented contract rules. They do not establish that the selected contract is economically optimal or that the model accurately predicts future rainfall.

---

## Chronological Calibration and Test Comparison

For an initial temporal comparison, the observations were split chronologically.

- Calibration period: 2015–2021
- Test period: 2022–2024

The same illustrative 800 mm trigger and payout structure were used throughout.

| Metric | Calibration | Test |
|---|---:|---:|
| Number of years | 7 | 3 |
| Trigger breaches | 3 | 0 |
| Trigger breach frequency | 42.86% | 0% |
| Total payouts | ₹45,000 | ₹0 |
| Average annual payout | ₹6,428.57 | ₹0 |

The test period had no trigger breaches because all three seasonal rainfall totals exceeded 800 mm.

This result illustrates sensitivity to the observation period, rather than proving that the insurance contract has failed.

The test period contains only three seasons, so the comparison is too limited to establish reliable long-term payout frequency or premium adequacy.

Additionally, the trigger was specified as a hypothetical contract parameter rather than selected through a formal training procedure. Therefore, this analysis is a chronological stability check, not a complete predictive model validation exercise.

---

## Installation and Setup

### Prerequisites

- Python 3.10 or later recommended
- Jupyter Notebook or Kaggle Notebooks
- Internet access for the initial API request

### Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd PluviaRisk
```

Replace the placeholder with your actual GitHub repository URL.

### Install Dependencies

```bash
pip install -r requirements.txt
```

The `requirements.txt` file contains the Python libraries used in the project.

---

## How to Run

1. Clone or download the repository.
2. Install the dependencies.
3. Open `PluviaRisk.ipynb` in Jupyter Notebook or upload it to Kaggle.
4. Execute the notebook cells in order.
5. Retrieve the historical rainfall data if required.
6. Review the descriptive statistics and visualisations.
7. Execute the payout simulation.
8. Review the trigger and premium sensitivity analyses.
9. Inspect the bootstrap results and chronological comparison.
10. Review the exported CSV files.

### Expected Outputs

The analysis produces:

- Daily rainfall statistics
- Annual rainfall summaries
- Monsoon rainfall summaries
- Historical payout calculations
- Payout frequency and severity metrics
- Premium sensitivity results
- Bootstrap distribution and interval
- Trigger sensitivity comparison
- Calibration and test-period comparison
- Contract validation results
- CSV files for further analysis

---

## Assumptions and Limitations

The current implementation is an educational quantitative modelling project. Its results should be interpreted within the following limitations.

### Limited Historical Sample

Only ten monsoon seasons are included. This is a small sample for estimating rare events, long-term rainfall variability, and insurance payout distributions.

### Single Geographic Location

The analysis focuses on one set of coordinates in Ahmedabad. Results cannot automatically be generalised to other regions or individual agricultural locations.

### Simplified Rainfall Trigger

The 800 mm trigger is illustrative. It has not been calibrated against crop-specific water requirements, soil conditions, crop calendars, or historical agricultural losses.

### Simplified Payout Structure

The contract uses a fixed payout per millimetre below the trigger, subject to a maximum payout. Actual insurance products may use more complex payout schedules and policy conditions.

### No Actual Loss Dataset

No observed crop-loss or farmer-income data is included. Consequently, the model does not quantify basis risk or establish the relationship between rainfall shortfalls and actual financial losses.

### Simplified Premium Calculation

The indicative premium uses a hypothetical loading over the historical average payout. It does not include a complete actuarial assessment of expenses, uncertainty, capital costs, reinsurance, or regulatory requirements.

### Bootstrap Limitations

Bootstrap resampling of ten historical seasons cannot fully capture climate trends, structural changes, or events absent from the sample.

### Limited Test Period

The test period contains only three seasons. The zero-payout result should not be interpreted as a forecast of future claim frequency.

### Data Source Limitations

Historical weather observations may be revised. The chosen coordinates and precipitation variable may not represent rainfall conditions at every insured farm.

---

## Future Improvements

Potential extensions include:

1. **Longer Historical Analysis:** Extend the observation period where reliable data is available.
2. **Regional Risk Modelling:** Compare multiple locations and spatial rainfall patterns.
3. **Crop-Specific Triggers:** Incorporate crop calendars and agricultural requirements.
4. **Basis Risk Analysis:** Integrate actual crop-loss observations or a defensible loss proxy.
5. **Trigger Optimisation:** Evaluate alternative trigger levels against a clearly defined insurance objective.
6. **Advanced Statistical Modelling:** Investigate extreme-value methods and suitable approaches to rainfall distributions.
7. **Climate Trend Analysis:** Examine possible changes in seasonal rainfall and extreme-event frequency.
8. **Actuarial Pricing:** Incorporate expenses, uncertainty, capital requirements, and justified risk margins.
9. **Out-of-Sample Evaluation:** Use longer chronological holdout periods and rolling-origin evaluation where data permits.
10. **Interactive Dashboard:** Develop a dashboard for exploring triggers, payouts, and pricing scenarios.
11. **Automated Data Pipeline:** Separate data retrieval, preprocessing, modelling, and reporting into reusable Python modules.
12. **Reproducibility Improvements:** Record data retrieval dates, preserve source data, and document dependency versions.

---

## Disclaimer

PluviaRisk is an educational and analytical project developed to demonstrate quantitative risk modelling concepts using historical rainfall data.

The insurance contract parameters and premium loading assumptions are illustrative. The estimated payouts and premiums are not validated commercial insurance prices, actuarial advice, or a recommendation to issue an insurance product.

Real-world implementation would require appropriate loss data, robust statistical validation, product-specific calibration, and review by qualified insurance and actuarial professionals.

---

## Author

**Kunal Pramanik**

M.Sc. Data Science

Dhirubhai Ambani University (DA-IICT), Gandhinagar, India

- GitHub: [Kunal-Pramanik](https://github.com/Kunal-Pramanik)
- LinkedIn: [Kunal Pramanik](https://linkedin.com/in/kunal-pramanik-5aa131267)

---

*PluviaRisk — Quantifying rainfall risk through data-driven insurance modelling.*
