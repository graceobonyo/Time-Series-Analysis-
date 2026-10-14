# Air Quality Forecasting Using Time Series Analysis

## Introduction

This project focuses on forecasting PM2.5 air pollution concentrations using time series analysis techniques. Historical air quality and meteorological data from 2013 to 2017 were analyzed to develop predictive models capable of forecasting future PM2.5 levels. Three forecasting approaches, namely ARIMA, SARIMA, and Prophet, were evaluated and compared to determine the most effective model.

## Objectives

- Load and preprocess air quality data from an ARFF file.
- Handle missing values and outliers.
- Perform exploratory data analysis on PM2.5 concentrations.
- Conduct stationarity testing using the Augmented Dickey-Fuller (ADF) test.
- Decompose the PM2.5 time series into trend, seasonal, and residual components.
- Develop ARIMA, SARIMA, and Prophet forecasting models.
- Evaluate forecasting performance using RMSE and MAE.
- Perform hyperparameter tuning on the Prophet model.
- Analyze model bias and variance.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Statsmodels
- Prophet
- Scikit-learn

## Dataset Description

The dataset contains hourly air quality and meteorological measurements including:

- PM2.5
- PM10
- SO2
- NO2
- CO
- O3
- Temperature (TEMP)
- Pressure (PRES)
- Dew Point (DEWP)
- Rainfall (RAIN)
- Wind Speed (WSPM)

The data covers the period from 2013 to 2017.

## Data Preprocessing

### Missing Value Treatment

Missing values represented by "?" were replaced with NaN values and handled through linear interpolation to ensure continuity within the time series.

### Data Type Conversion

All numerical attributes were converted into appropriate numeric data types to facilitate statistical analysis and forecasting.

### Datetime Construction

The year, month, day, and hour variables were merged into a single datetime column, which was subsequently set as the DataFrame index.

### Outlier Detection and Treatment

Outliers were detected using the Interquartile Range (IQR) method. To reduce the influence of extreme observations without removing data points, Winsorization was applied by capping values at the calculated upper and lower bounds.

## Exploratory Data Analysis

### PM2.5 Trend Analysis

The PM2.5 concentration levels fluctuated considerably between 2013 and 2017. Several periods of high pollution were observed alongside cleaner periods. Although substantial variability was present throughout the series, no strong long-term upward or downward trend was detected.

### Correlation Analysis

A correlation heatmap revealed strong positive relationships between PM2.5 and PM10, CO, and NO₂ concentrations. These findings suggest that pollutants likely originate from similar sources such as transportation and industrial activities. Wind speed demonstrated a negative relationship with PM2.5, indicating that stronger winds help disperse atmospheric pollutants.

## Feature Engineering

Several features were generated to improve forecasting performance.

### Lag Features

- PM25_lag_1
- PM25_lag_24
- PM25_lag_48

### Moving Average Features

- MA_24
- MA_72

### Time-Based Features

- Month
- Day of Week
- Hour

## Stationarity Testing

The Augmented Dickey-Fuller (ADF) test was used to determine whether the PM2.5 series was stationary.

### Results

- ADF Statistic: -22.03
- P-value: 0.0000

### Interpretation

The p-value was significantly below the 0.05 significance level, indicating that the null hypothesis of non-stationarity was rejected. Consequently, the PM2.5 series was considered stationary and suitable for time series forecasting.

## Seasonal Decomposition

Seasonal decomposition separated the PM2.5 series into trend, seasonal, and residual components.

The decomposition analysis revealed:

- A general decline in PM2.5 concentrations between 2013 and 2015.
- Recurring seasonal patterns affecting air quality.
- Random fluctuations and pollution spikes represented by the residual component.

These findings indicate that PM2.5 concentrations are influenced by both predictable seasonal effects and unpredictable environmental events.

## Forecasting Models

The dataset was split into training and testing sets using an 80:20 ratio.

### ARIMA Model

Configuration:

ARIMA(5,1,2)

Performance:

- RMSE: 57.23
- MAE: 45.40

The ARIMA model captured the overall pattern of PM2.5 concentrations but experienced difficulty forecasting extreme pollution events.

### SARIMA Model

Configuration:

SARIMA(1,1,1)(1,1,1,12)

Performance:

- RMSE: 58.02
- MAE: 44.63

The SARIMA model incorporated seasonality and achieved performance comparable to ARIMA.

### Prophet Model

Performance:

- RMSE: 54.76
- MAE: 41.02

The Prophet model achieved the lowest forecasting errors among all evaluated models. It effectively captured both trend and seasonal patterns within the PM2.5 time series.

## Model Comparison

| Model | RMSE | MAE |
|--------|------|------|
| ARIMA | 57.23 | 45.40 |
| SARIMA | 58.02 | 44.63 |
| Prophet | 54.76 | 41.02 |

The results indicate that Prophet outperformed both ARIMA and SARIMA, achieving the lowest RMSE and MAE values.

## Hyperparameter Tuning

Prophet hyperparameter tuning was performed using Grid Search to identify the optimal parameter combination.

The following parameters were tuned:

- changepoint_prior_scale
- seasonality_prior_scale
- seasonality_mode

The best-performing parameter combination was selected based on the lowest RMSE value and used to train the final forecasting model.

## Actual vs Predicted Analysis

Comparison of actual and predicted PM2.5 values demonstrated that Prophet successfully captured the overall trend and seasonal movement of the series. The predictions were smoother than the observed values and occasionally underestimated extreme pollution spikes. Despite this limitation, the model produced the most reliable forecasts among all evaluated approaches.

#### Bias-Variance Trade-off

The Prophet model achieved a good balance between bias and variance. Although the model exhibited moderate bias by smoothing predictions and underestimating some extreme PM2.5 spikes, it maintained low variance by avoiding overfitting to noise and short-term fluctuations in the data.

This trade-off allowed the model to generalize effectively to unseen observations while maintaining stable forecasting performance. As a result, Prophet was able to capture the underlying trend and seasonal patterns of PM2.5 concentrations more effectively than ARIMA and SARIMA, leading to lower prediction errors.

#### Conclusion

The Prophet model was identified as the most suitable forecasting approach for PM2.5 prediction in this study. Its ability to model trend and seasonality while maintaining relatively low forecasting errors makes it a valuable tool for air quality monitoring, environmental planning, and decision-making.