# Forecasting Portugal's GDP with ARIMA

A group project for the **Forecasting Methods** course at **NOVA IMS** (Lisbon), 2026.

We used Portugal's quarterly GDP data to build a simple time series model and forecast GDP for 2026–2028. Then we compared our forecast with forecasts from institutions like the European Commission, the IMF and the OECD.

## Authors

- **Leon Efe Apaydın**
- **Dominik Zelger**
- **Anna Sándorfi**

## View the report

| File | What it is |
|------|------------|
| [Report (Markdown)](gdp_forecast_portugal.md) | The full report with all tables and charts. You can read it right here on GitHub. |
| [Report (PDF)](gdp_forecast_portugal.pdf) | The same report as a PDF. |
| [Source code (R Markdown)](gdp_forecast_portugal.Rmd) | The R code and text that produce the report. |

## What we did

1. **Data:** We used Portugal's quarterly GDP from Eurostat, from 1995 Q1 to 2025 Q4. It is in current prices (million EUR) and seasonally adjusted.
2. **Train/test split:** We trained our models on data up to 2022 Q4. We kept 2023 Q1 – 2025 Q4 aside to test the forecasts.
3. **Box-Jenkins method:**
   - We took the log of GDP and differenced it once to make the series stationary. We checked this with the ADF test.
   - We compared several ARIMA models using AIC and BIC.
   - We checked the residuals with ACF plots and the Ljung-Box test.
4. **Testing:** We compared ARIMA(3,1,0) and ARIMA(0,1,3) on the test period. **ARIMA(3,1,0)** did best, with a MAPE of about **5.15%**.
5. **Forecast:** We fitted ARIMA(3,1,0) again on all the data and forecast GDP for 2026–2028.
6. **Comparison:** We turned the institutions' real GDP growth forecasts into nominal growth and compared them with our results.

## Main results

| Year | Our forecast (nominal GDP growth) |
|------|-----------------------------------|
| 2026 | 5.47% |
| 2027 | 4.46% |
| 2028 | 4.33% |

Our forecast is a bit higher than the institutions' forecasts for 2026 (4.65%–5.27%). Like them, it expects growth to slow down in 2027. A simple model that only uses past GDP data gets fairly close to what the big institutions expect.

**Limitation:** Our model only uses past GDP values. It cannot predict sudden shocks such as COVID-19 or the 2022–2023 inflation spike.

## How to run it

You need R with these packages:

```r
install.packages(c("tidyverse", "eurostat", "feasts", "tsibble", "ggtime",
                   "urca", "fable", "scales", "rmarkdown"))
```

Then open `gdp_forecast_portugal.Rmd` in RStudio and click **Knit**.

> **Note:** The code downloads the data from Eurostat each time it runs. The data is cut at **2025 Q4** so the results stay the same as in our report, even after Eurostat publishes newer data.
