# Time Series Analysis of NYC Temperature Data

## Project Overview
This project performs a comprehensive time series analysis of historical temperature data for New York City (NYC) from 1970 to 2013, sourced from the Berkeley Earth dataset via 
[Kaggle](https://www.kaggle.com/datasets/berkeleyearth/climate-change-earth-surface-temperature-data).
The primary objectives are to preprocess and explore the temperature data, visualize seasonal patterns, evaluate forecasting models (ARIMA, SARIMA, and Prophet), and generate future temperature forecasts for 2014–2033 using the best-performing model. The analysis also estimates the rate of temperature increase and examines seasonal changes.

## Dataset
The dataset used is derived from the `GlobalLandTemperaturesByCity.csv` file from Kaggle's Berkeley Earth dataset. It contains monthly average temperatures for various cities, with this project focusing on NYC data from 1970 to 2013. The processed dataset is saved as `nyc_berkeley_temperature.csv`, which includes:
- **Columns**: `date` (monthly timestamp), `AverageTemperature` (°C)
- **Rows**: 528 (January 1970 to December 2013)
- **Preprocessing**:
  - Filtered for NYC and the period 1970–2013.
  - Missing values interpolated.
  - Outliers checked using Tukey's fences (none found).
  - Missing values for October–December 2013 filled with monthly averages.

## Methodology
The analysis is conducted in a Jupyter notebook (`Time Series Analysis of NYC Temperature Data.ipynb`), converted to a Python script. Key steps include:

1. **Data Preprocessing**:
   - Load and filter the dataset for NYC.
   - Convert dates to datetime format and set as index.
   - Interpolate missing values and fill specific 2013 data points.
   - Verify no outliers using boxplot and Tukey's fences.

2. **Exploratory Data Analysis (EDA)**:
   - Visualize monthly temperature trends (1970–2013).
   - Compute summary statistics (mean: 10.41°C, std: 9.09°C).
   - Analyze yearly and monthly mean temperatures.
   - Perform seasonal decomposition (additive model, 12-month period) to extract observed, trend, seasonal, and residual components.

3. **Forecasting Models**:
   - **Training Period**: 1970–2003 (408 months).
   - **Test Period**: 2004–2013 (120 months).
   - Models evaluated:
     - **ARIMA**: Non-seasonal model (order: (1,1,1)).
     - **SARIMA**: Seasonal model (order: (1,1,1), seasonal_order: (1,1,1,12)).
     - **Prophet**: Facebook's Prophet with yearly seasonality.
   - Forecasts saved in `forecasts_test.csv`.

4. **Model Evaluation**:
   - Metrics: Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), Mean Absolute Percentage Error (MAPE).
   - Results:
     ```
                  MAE       RMSE         MAPE
     ARIMA    23.433833  25.182140  1767.303216
     SARIMA    1.196698   1.547555   113.663099
     Prophet   1.196858   1.558340   105.415449
     ```
   - **Best Model**: SARIMA (lowest RMSE: 1.547555).

5. **Future Forecasting**:
   - Refit SARIMA on the full dataset (1970–2013).
   - Forecast temperatures for 2014–2033 (240 months).
   - Calculate:
     - Historical mean: 10.38°C.
     - Forecast mean: 11.28°C.
     - Rate of increase: 0.45°C/decade.
   - Analyze seasonal temperature changes (2014–2033 vs. 1970–2013).

6. **Visualizations**:
   - Time series plot of historical temperatures.
   - Seasonal decomposition plot (`decomposition.png`).
   - Forecast comparison (2004–2013) vs. actual (`forecast_comparison.png`).
   - Future forecast (2014–2033) (`future_forecast.png`).
   - Seasonal temperature difference (`seasonal_diff.png`).
   - Yearly and monthly mean temperature plots.

## Repository Structure
```
shubhamgoel26-time-series-analysis-of-nyc-climate-data/
├── forecasts_test.csv              # Forecasted temperatures (2004–2013) for ARIMA, SARIMA, Prophet
├── nyc_berkeley_temperature.csv    # Processed NYC temperature data (1970–2013)
├── Time Series Analysis of NYC Temperature Data.ipynb  # Jupyter notebook with analysis
└── plots/
    └── read.md                     # Placeholder for plot descriptions
```

## Key Findings
- **Temperature Trends**: NYC temperatures show a clear seasonal pattern, with peaks in July (mean: 22.93°C) and lows in January (mean: -2.83°C).
- **Model Performance**: SARIMA outperformed ARIMA and Prophet, with the lowest RMSE (1.55°C) and MAE (1.20°C).
- **Future Projections**: Forecasted temperatures for 2014–2033 indicate a rise of 0.45°C per decade, with a mean temperature increase from 10.38°C to 11.28°C.
- **Seasonal Changes**: Future forecasts show consistent seasonal patterns, with slight increases across all months.

## Requirements
To run the analysis, install the following Python packages:
```bash
pip install pandas matplotlib statsmodels prophet sklearn numpy
```

## How to Run
1. Clone the repository.
2. Ensure the required packages are installed.
3. Open `Time Series Analysis of NYC Temperature Data.ipynb` in Jupyter Notebook.
4. Update the path to `GlobalLandTemperaturesByCity.csv` in the notebook (not included in the repo).
5. Run all cells to reproduce the analysis, generate plots, and save outputs.

## Outputs
- **Data**: `nyc_berkeley_temperature.csv`, `forecasts_test.csv`.
- **Plots**: Saved in the `plots/` directory (e.g., `decomposition.png`, `forecast_comparison.png`).
- **Metrics**: Printed in the notebook (MAE, RMSE, MAPE for each model).
- **Forecasts**: Future predictions (2014–2033) plotted and analyzed.

## Future Work
- Incorporate additional climate variables (e.g., precipitation, humidity).
- Explore advanced models like LSTM or XGBoost for forecasting.
- Analyze the impact of climate change on seasonal patterns in greater detail.

## Author
Shubham Goel
