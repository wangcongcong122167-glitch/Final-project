# Event Study Analysis for Financial Assets

This project performs an event study analysis on various financial assets (stocks, cryptocurrencies, and indices) in response to major US macroeconomic announcements (CPI, FOMC, NFP). The workflow includes data loading, preprocessing, event study calculation, statistical testing, regression analysis, and exporting results.

## Project Structure

- **main.ipynb**: Main notebook containing all data processing, event study, statistical analysis, regression, and export steps.
- **data/**: Folder containing all raw CSV/XLSX data files for assets and announcements.
- **.pkl files**: Intermediate and final results are saved as pickle files for efficient reuse.
- **all_results.xlsx**: Final Excel file containing all summary tables.

## Workflow

1. **Data Loading & Preprocessing**
   - Loads daily and minute-level price data for assets (e.g., BTC, ETH, FTSE, AZN, BP, HSBA).
   - Loads macroeconomic announcement data (CPI, FOMC, NFP).
   - Cleans and standardizes columns, ensures all timestamps are UTC-aware.

2. **Metric Calculation**
   - Computes returns, rolling volatility, and standardized volume for each asset.

3. **Event Study Calculation**
   - For each announcement, calculates abnormal returns, volatility, and volume in event windows (daily: [-5, +5] days; minute: [-60, +60] minutes) relative to estimation windows.
   - Saves raw abnormal value lists for further analysis.

4. **Statistical Testing**
   - Performs one-sample t-tests on abnormal values to assess significance.
   - Saves summary statistics (mean abnormal, t-statistic, p-value).

5. **Regression Analysis**
   - Runs OLS regressions to estimate the effect of announcements on abnormal returns, volatility, and volume.
   - Saves regression coefficients, p-values, and R-squared values.

6. **Exporting Results**
   - Converts all results to DataFrames and exports to a single Excel file (`all_results.xlsx`) with multiple sheets.

7. **Visualization**
   - Provides scripts to plot average returns, cumulative returns, and volume around events, grouped by surprise category.

## How to Run

1. Place all required data files in the `data/` directory.
2. Run each cell in `main.ipynb` sequentially.
3. Intermediate results will be saved as `.pkl` files.
4. Final summary tables will be exported to `all_results.xlsx`.
5. Use the provided plotting scripts to generate and save event-aligned figures.

## Requirements

- Python 3.8+
- pandas, numpy, matplotlib, statsmodels, scipy, openpyxl
- (Optional for GARCH modeling) `arch` package

Install dependencies with:
```sh
pip install pandas numpy matplotlib statsmodels scipy openpyxl arch
```

## Notes

- All timestamps are handled in UTC.
- The code is modular: you can reuse or adapt each step for other assets or events.
- For large event windows or high-frequency data, ensure sufficient system memory.

## Output

- `all_results.xlsx`: Contains statistical and regression results for all assets and events.
- PNG figures: Saved to your Desktop, showing event-aligned average and cumulative returns and volume.
