German Electricity Demand Forecast Durability
Project Overview

This project examines how long an electricity-demand forecast remains useful after one fixed forecast origin. German electricity-load data from January 2015 to September 2020 are used to compare statistical, machine-learning and deep-learning forecasting methods across a 104-week test horizon.

Rather than relying only on one overall accuracy score, the test period is divided into four 26-week blocks. This makes it possible to identify whether model accuracy remains stable or deteriorates as the forecast moves further from the training period.

Research Question

Which forecasting model maintains useful accuracy as the forecast moves further from one fixed origin?

Dataset

The electricity-load data are obtained from the Open Power System Data platform:

https://data.open-power-system-data.org/time_series/

The analysis uses:

German electricity-load observations
Hourly measurements
Data from January 2015 to September 2020
Daily and weekly aggregated demand
Berlin temperature data from the Open-Meteo historical weather service
German public-holiday information
Forecasting Methods

The following models are evaluated:

Mean forecast
Naive forecast
Seasonal Naive forecast
Drift forecast
SARIMA
SARIMAX with temperature
Extra Trees Regressor
Long Short-Term Memory network

Seasonal Naive is used as the main benchmark because the weekly demand series shows strong annual dependence around lag 52.

Analysis Workflow

The project follows these stages:

Retrieve and clean hourly German electricity-load data.
Restrict the analysis to the selected study period.
Aggregate the load into daily and weekly values.
Conduct exploratory analysis and seasonal decomposition.
Examine autocorrelation and partial autocorrelation.
perform ADF and KPSS stationarity tests.
Generate benchmark forecasts.
Search for suitable SARIMA parameters using AIC.
evaluate statistical-model residuals and prediction intervals.
Add Berlin temperature as an external SARIMAX variable.
Train a feature-based tree ensemble.
Train and evaluate an hourly LSTM.
Compare RMSE, MAE and related metrics across four horizon blocks.
Examine cumulative error and changes in model ranking.
Main Python Libraries

The analysis requires Python 3 and the following libraries:

pandas
numpy
matplotlib
statsmodels
scikit-learn
tensorflow
requests
holidays

Install the required packages with:

pip install pandas numpy matplotlib statsmodels scikit-learn tensorflow requests holidays
How to Run the Project
Download or clone the repository.
Open the main analysis notebook in Jupyter Notebook, JupyterLab or Google Colab.
Install the required Python libraries.
Ensure that an internet connection is available for retrieving electricity and temperature data.
Run all notebook cells in order from the beginning.
Allow the statistical parameter search and LSTM training processes to finish.
Check the generated tables, forecast plots and evaluation metrics.

For reproducible results, the notebook should be restarted and executed from the first cell without manually changing intermediate variables.

Model Evaluation

Forecasts are evaluated over the complete 104-week horizon and separately across:

Weeks 1–26
Weeks 27–52
Weeks 53–78
Weeks 79–104

The principal evaluation measures include:

Root Mean Squared Error
Mean Absolute Error
Symmetric Mean Absolute Percentage Error
Prediction-interval coverage
Prediction-interval width
Rolling forecast error
Cumulative absolute error
Error growth across horizon blocks

The models are compared against the Seasonal Naive benchmark to determine whether added complexity produces a meaningful improvement.

Forecasting Assumptions

The experiment uses one fixed forecast origin. Actual demand from the test period should not be inserted into later recursive forecasts.

Observed test-period temperature creates a conditional forecast because future observed weather would not be available at the original forecast date. An operational implementation would require weather forecasts instead.

Expected Outputs

Running the project produces:

Cleaned hourly, daily and weekly demand summaries
Exploratory time-series plots
Seasonal decomposition
ACF and PACF diagnostics
Stationarity-test results
Benchmark forecast plots
SARIMA and SARIMAX forecasts
Prediction intervals
Extra Trees and LSTM forecasts
Full-horizon evaluation tables
Metrics for each 26-week block
Cumulative error and ranking comparisons
A final comparison of all forecasting approaches
Reproducibility Notes
Time-series observations are divided chronologically.
Random shuffling is not used for the final test split.
Scalers must be fitted using training data only.
Hyperparameter selection should use chronological validation data.
Recursive models must use their own predictions for later demand lags.
All models should be evaluated using the same weekly test dates.
Random seeds should be fixed where supported.
Limitations

The analysis uses Berlin temperature as a representative weather measure for the whole of Germany. National electricity demand may be influenced by regional weather differences, industrial activity, renewable generation, economic conditions and exceptional events.

The two-year fixed-origin design is deliberately demanding. In operational forecasting, models would normally be updated as new demand and weather observations become available.
