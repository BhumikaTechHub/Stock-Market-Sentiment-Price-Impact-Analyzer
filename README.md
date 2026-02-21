# Stock-Market-Sentiment-Price-Impact-Analyzer

Here is a professional, highly scannable `README.md` file crafted from your project report. It is structured to highlight your rigorous methodology, econometric modeling, and quantitative results, making it perfect for data science and quantitative finance portfolios.

---

# Stock Market Sentiment & Price Impact Analyzer

##  Overview

This project investigates whether short-run volatility in the Indian stock market is triggered by upper management transitions, such as the resignation or appointment of directors, CEOs, and CFOs. By combining an event-study design with advanced econometric volatility models (GARCH-family) and Natural Language Processing (NLP), this project evaluates how leadership changes and the surrounding news sentiment act as short-term volatility shocks.

##  Problem Statement

Corporate governance events represent periods of extreme uncertainty for firms, often altering investor expectations, cash flow projections, and overall market stability. In the Indian market—especially following enhanced SEBI disclosure requirements—board-level changes are often met with harsh market responses.

Despite this, there is a lack of empirical research modeling the short-term fluctuation patterns of these specific governance shocks. This project bridges that gap by quantifying the direct impact of management changes on stock volatility and testing whether financial news sentiment amplifies or dampens these effects.

##  Data Collection & Preprocessing

The project evaluates NSE-listed (NIFTY 50) companies from 2006 to 2014, matching event data with daily market prices.

* **Market Data:** Daily price data (Open, High, Low, Close, Volume) extracted using the `yfinance` API.
* **Event Data:** A synthetic dataset of 2,375 board-level changes built using real Indian resignation statistics and distributions.
* **Sentiment Data:** Analyzed news tone over a ±7-day window around events using two NLP models:
* **FinBERT:** A finance-specific transformer model.
* **VADER:** A rule-based lexicon sentiment analyzer.



## Methodology & Econometric Modeling

### 1. Event Study Analysis

Used to measure the immediate market reaction to management changes within a ±30-day window.

* **Log Returns:** 

* **Cumulative Abnormal Returns (CAR):** Quantifies short-term price reactions. 


### 2. Time-Series Volatility Modeling

To test the effect of sentiment and event-day shocks, the following GARCH-family models were implemented:

* **GARCH-X:** Incorporates sentiment and event dummies directly into the mean and variance equations.
* *Mean Equation:* 

* *Variance Equation:* 



* **EGARCH (Exponential GARCH):** Captures asymmetric volatility (testing if bad news has a stronger effect).
* **GJR-GARCH:** Captures the leverage effect, measuring how negative shocks increase volatility relative to positive ones.

### 3. Forecasting Models

* **ARIMAX:** Used to forecast short-term returns using past returns, NLP sentiment, and event dummies.
* **Random Forest Regression:** Deployed as a machine-learning benchmark to predict next-day volatility and capture non-linear relationships.

## 📈 Key Findings & Results

The empirical results indicate that volatilities are highly concentrated along event dates, with intense reactions surrounding unexpected or negative exits. Interestingly, while the events themselves cause massive volatility, the NLP sentiment of the surrounding news did not show a statistically significant impact on the variance equation.

| Metric / Variable | Numerical Result | Interpretation |
| --- | --- | --- |
| **CAR (0,1)** | `-4.89%` | Stocks typically lose ~4.9% within two trading days of a board resignation. |
| **CAR (0,5)** | `-2.60%` | Continued market weakness; stocks do not fully recover within five days. |
| **Max Volatility Spike** | `0.11` | A ~5x increase in volatility immediately following an event. |
| **Event Day Effect (GARCH-X)** | `-3.38%` return | Strong, statistically significant negative impact (). |
| **EGARCH Leverage Effect** |  | Strong asymmetric leverage effect; negative shocks disproportionately spike volatility. |
| **Clustered Resignations** | `+6%` to `+11%` | Multiple exits in one year create significantly higher market disruption. |
| **Machine Learning (RF)** |  | Model fails entirely; standard tree-based ML is unsuitable for short-window financial volatility forecasting. |

##  Limitations & Future Scope

* **Limitations:** Historical news data and real MCA-21 filings for the 2006–2014 period are largely restricted behind paid APIs, necessitating the use of statistically accurate synthetic events and sentiment distributions.
* **Future Work:** * Integrate high-frequency (5-minute or hourly) intraday data for more granular shock transmission analysis.
* Segment the modeling by industry sector to identify which markets respond most aggressively to governance shocks.
* Apply live data pipelines using paid corporate announcement APIs (e.g., BloombergQuint, ET) for real-time volatility prediction.


