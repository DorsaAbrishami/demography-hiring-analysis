# Demography Hiring Analysis

This project analyzes demographic patterns in the U.S. labor market using Bureau of Labor Statistics (BLS) time series. The analysis focuses on gender differences in employment, unemployment, and labor force participation, and compares overall trends with prime-age (25-54) employment.

## Project Overview

The notebook builds a complete end-to-end analysis pipeline:

- Ingests all datasets from `data/` as source of truth
- Cleans and standardizes each BLS file
- Aligns all series by monthly `Date`
- Merges into one analytics dataset
- Engineers gap and growth features
- Produces portfolio-ready charts and interprets findings
- Saves outputs to `outputs/`

## Data Sources

All datasets are from the BLS Current Population Survey and are stored in `data/`:

- `Men_BLS.csv` (Employment Level - Men)
- `Women_BLS.csv` (Employment Level - Women)
- `Employment Level_25-54 yrs.csv` (Prime-age Employment Level)
- `Unemployment Rate - Men.csv`
- `Unemployment Rate - Women.csv`
- `Labor Force Participation Rate - Men.csv`
- `Labor Force Participation Rate - Women.csv`

## Methodology

1. **Data cleaning**
   - Keep monthly observations only (`M01` to `M12`)
   - Convert `Value` to numeric and handle `-` as missing
   - Parse `Label` into datetime
   - Standardize metric column names

2. **Data alignment and merge**
   - Merge all cleaned series on `Date`
   - Build a single analysis table with:
     - `Men_Employment`, `Women_Employment`, `Prime_Age_Employment`
     - `Men_Unemployment`, `Women_Unemployment`
     - `Men_Participation`, `Women_Participation`

3. **Feature engineering**
   - `Employment_Gap = Men_Employment - Women_Employment`
   - `Participation_Gap = Men_Participation - Women_Participation`
   - `Unemployment_Gap = Men_Unemployment - Women_Unemployment`
   - Month-over-month growth rates for employment series

4. **Visualization and interpretation**
   - Men vs women employment trends
   - Employment gap trend
   - Unemployment comparison
   - Participation comparison
   - Prime-age employment trend
   - Participation vs unemployment driver view

## Key Findings (Current Sample Window)

- The employment gap narrowed by about **1,567 thousand** (from ~8,941 to ~7,374), indicating improved gender parity in employment levels.
- Women employment increased substantially more than men in this period (women: **+1,641 thousand**, men: **+74 thousand**), suggesting the narrowing gap was primarily women-side improvement.
- Participation differences appear much larger than unemployment differences (average participation gap: **~10.43 pp** vs unemployment gap: **~0.15 pp**), indicating participation is the stronger structural driver of the employment gap.
- Men unemployment was slightly higher on average than women unemployment in this sample (~4.23% vs ~4.08%).
- Prime-age employment increased by **~1,534 thousand**, consistent with a generally expanding labor market backdrop.

## Outputs

Running `notebooks/analysis.ipynb` generates:

- Clean dataset: `outputs/cleaned_data.csv`
- Charts:
  - `outputs/01_men_vs_women_employment.png`
  - `outputs/02_employment_gap_over_time.png`
  - `outputs/03_unemployment_comparison.png`
  - `outputs/04_participation_comparison.png`
  - `outputs/05_prime_age_employment_trend.png`
  - `outputs/06_gap_driver_participation_vs_unemployment.png`
- Text summary: `outputs/insights_summary.txt`

## Tools

- Python
- Pandas
- Matplotlib
- Jupyter Notebook