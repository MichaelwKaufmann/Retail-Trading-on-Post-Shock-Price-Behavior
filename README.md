# Retail Trading on Post-Shock Price Reversion

**An Honors Thesis by Michael Kaufmann**  
Economic Departmental Honors Program, Clemson University  
Advisor: Dr. Robert Fleck  
May 1st, 2026

---

## Table of Contents

- [Abstract](#abstract)
- [Research Question & Hypothesis](#research-question--hypothesis)
- [Data & Sample](#data--sample)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Repository Structure](#repository-structure)
- [Interpreting the Results](#interpreting-the-results)
- [Limitations & Future Research](#limitations--future-research)
- [Getting Started](#getting-started)
- [References](#references)

---

## Abstract

This study examines the relationship between retail trading activity and post-shock price behavior over a five-day horizon. Using oddlot rates as a proxy for individual retail investor participation, we employ a fixed-effects regression model to analyze approximately 185 NYSE-listed securities from January 2019 to January 2024. 

**Key Finding:** Retail trading intensity is associated with **lower cumulative abnormal returns** (CAR[1,5]) in the five trading days following idiosyncratic price shocks, with effects varying asymmetrically across positive and negative shocks. The relationship is most pronounced following strong negative price movements, suggesting retail investors may exhibit disposition effect behavior or early profit-taking that creates downward price pressure.

---

## Research Question & Hypothesis

### Motivation

The democratization of financial markets through commission-free trading platforms (e.g., Robinhood, launched 2013) has dramatically increased retail investor participation. Yet the impact of retail trading on market efficiency remains contested:

- **Efficient Market Hypothesis:** Retail trading is noise that rational arbitrageurs quickly correct.
- **Noise Trader Theory:** Limited arbitrage opportunities allow sentiment-driven retail trading to persistently move prices away from fundamentals.

### Core Hypothesis

**Increases in retail participation in conjunction with abnormal price shocks will be associated with significant price reversals in the subsequent five trading days.**

Theoretically, if retail traders are predominantly sentiment-driven and uninformed, their participation in price shocks should create transient pressure that institutional arbitrageurs correct over a 5-day window.

---

## Data & Sample

### Sources
- **Market Data:** Wharton Research Data Services (WRDS) MSEC and CRSP databases
- **Market Benchmark:** S&P 500 daily prices (FRED database)
- **Sample Period:** January 1, 2019 – January 5, 2024
- **Securities:** 185 NYSE-listed stocks across diverse market capitalizations and sectors

### Key Variables

| Variable | Definition |
|----------|-----------|
| **Idiosyncratic Return** | Daily percent difference: Individual security return − S&P 500 return |
| **CAR[1,5]** | Cumulative abnormal idiosyncratic return over 5 trading days post-shock |
| **Retail Intensity** | Standardized oddlot rate (z-score): deviations from full-sample mean |
| **Shock Intensity** | Categorical bins based on shock direction and magnitude (see Table 1) |

### Shock Classification (Table 1)

| Shock Type | Threshold | Observations |
|-----------|-----------|---------|
| Extreme Positive | z > 2 | 5,115 |
| Moderate Positive | z > 1 | 17,900 |
| Positive | z > 0 | 83,263 |
| Negative | z < 0 | 88,291 |
| Moderate Negative | z < -1 | 18,367 |
| Extreme Negative | z < -2 | 4,335 |

---

## Methodology

### Model Specification

We employ a **date fixed-effects regression** to isolate the relationship between retail trading and post-shock returns while controlling for market-wide shocks and time-varying factors:

$$\text{CAR}[1,5]_{i,t} = \beta_0 + \sum_j \beta_j (\text{Retail Intensity}_{i,t} \times \text{Shock Intensity}_j) + \gamma \mathbf{X}_{i,t} + \alpha_t + \epsilon_{i,t}$$

**Key Components:**

- **Dependent Variable:** CAR[1,5] — cumulative idiosyncratic return over 5 days post-shock
- **Primary Predictors:** Interaction terms between retail intensity and categorical shock bins (6 categories × retail intensity)
  - Allows testing of asymmetric effects across shock magnitudes and directions
- **Control Variables:**
  - log(Volume) — controls for liquidity differences
  - log(Price) — controls for price-level biases
  - Historical Volatility (sd_pct_change) — isolates compositional effect from volatility differences
- **Fixed Effects:** Date fixed effects (α_t) absorb market-wide shocks and temporal factors (critical during COVID-19 period)
- **Standard Errors:** Clustered by ticker to account for intra-firm correlations

### Why This Approach

The interaction model directly tests the Noise Trader Hypothesis by revealing whether retail sentiment predicts reversals, and whether predictive power varies between:
- **Positive vs. negative shocks** (testing disposition effect)
- **Moderate vs. extreme shocks** (testing attention/arbitrage capacity)

---

## Key Findings

### Main Results (Table 2)

#### Baseline Effect
- **Retail Intensity (standalone):** β = −0.002, p < 0.05
  - Increases in retail participation are modestly associated with lower 5-day CAR, independent of shock type

#### Asymmetric Effects on Negative Shocks
- **Negative shocks + retail intensity:** β = −0.003, p < 0.01
- **Moderate negative + retail intensity:** β = −0.002, p < 0.01
- **Extreme negative + retail intensity:** β = −0.006, p < 0.001 (strongest effect)

**Interpretation:** When negative price shocks co-occur with high retail trading, returns remain depressed over the next 5 days (momentum, not reversal). Retail investors appear to be **reinforcing downturns** rather than creating transient pressure for later correction.

#### Mixed Effects on Positive Shocks
- **Positive + retail intensity:** β = −0.002, p < 0.05
- **Moderate positive + retail intensity:** β = −0.002, p < 0.10
- **Extreme positive + retail intensity:** β = −0.004, not significant

**Interpretation:** In positive shocks, higher retail intensity is associated with *lower* post-shock returns, suggesting some **mean reversion**. However, this effect diminishes in extreme cases, possibly due to small sample size or changing market dynamics at extreme moves.

#### Control Variables
- **Historical Volatility (sd_pct_change):** β = 0.134, p < 0.001 (strong predictor of returns)
- **log(Volume) & log(Price):** Near-zero coefficients, ensuring the retail effect is not merely a liquidity or price-level artifact

---

## Interpreting the Results

### The Disposition Effect Hypothesis

The findings are **inconsistent with the original hypothesis** of retail-driven sentiment reversals. Instead, they suggest retail investors exhibit **disposition effect behavior:**

1. **On negative shocks:** Retail traders hold or add positions, but may eventually exit with losses, creating persistent downward pressure. This amplifies downturns rather than correcting them.

2. **On positive shocks:** Retail traders may be more aggressive profit-takers, selling winners early and creating post-shock reversals.

3. **Asymmetry:** The stronger effect in negative shocks aligns with behavioral evidence that loss realization aversion and regret minimization differ from gain-realization patterns.

### Implications

- **Market Efficiency:** Retail trading creates *predictable* post-shock patterns but not in the direction of efficient arbitrage. Instead, it appears to **reinforce transient price pressure** rather than correct it.
- **Institutional Role:** Institutional arbitrageurs may not fully counteract retail-driven momentum within the 5-day window, possibly due to volatility-driven risk aversion or uncertainty about sentiment persistence.

---

## Repository Structure

```
.
├── README.md                    # This file
├── data/
│   ├── raw/                     # Original WRDS/CRSP data (not included; proprietary)
│   ├── processed/               # Cleaned datasets with computed variables
│   └── README.md                # Data schema and preprocessing details
├── notebooks/
│   ├── 01_data_exploration.ipynb      # Descriptive statistics and distributions
│   ├── 02_event_detection.ipynb       # Price shock identification
│   ├── 03_car_calculation.ipynb       # Cumulative abnormal returns
│   ├── 04_regression_analysis.ipynb   # Fixed-effects regression and results
│   └── 05_robustness_checks.ipynb     # Alternative specs and sensitivity tests
├── src/
│   ├── events.py                # Event detection (shock identification thresholds)
│   ├── returns.py               # CAR and idiosyncratic return calculations
│   ├── regression.py            # Regression model setup and estimation
│   └── utils.py                 # Helper functions (data loading, formatting)
├── results/
│   ├── tables/                  # Regression output tables
│   ├── figures/                 # Plots and visualizations
│   └── README.md                # Output descriptions
└── requirements.txt             # Python dependencies
```

---

## Getting Started

### Prerequisites
- Python 3.8+
- Access to WRDS (Wharton Research Data Services) for original data
- See `requirements.txt` for package dependencies

### Setup & Reproduction

1. **Clone the repository:**
   ```bash
   git clone https://github.com/MichaelwKaufmann/Retail-Trading-on-Post-Shock-Price-Behavior.git
   cd Retail-Trading-on-Post-Shock-Price-Behavior
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Prepare data:**
   - Follow instructions in `data/README.md` to download and preprocess WRDS/CRSP data
   - Place processed files in `data/processed/`

5. **Run analysis:**
   - Execute notebooks in `notebooks/` sequentially (01 → 05)
   - Or run scripts directly via `src/` modules for custom analyses

---

## Limitations & Future Research

### Primary Limitations

1. **Oddlot Proxy Validity**
   - Historically, oddlot trades indicated retail activity. However, algorithmic high-frequency trading has blurred this distinction—institutional traders now execute more oddlots, introducing noise into the retail intensity metric.

2. **Temporal Window**
   - The 5-day CAR window may not capture the full price adjustment. Sentiment effects could dissipate intraday or persist beyond 5 days.

3. **Behavioral Assumptions**
   - The model assumes lower-volume traders are inherently less informed. Sophisticated retail ("sub-institutional") investors may violate this assumption.

### Suggested Future Directions

- **High-Frequency Data:** Implement intraday data with trade-size filters (e.g., < $5,000) to more precisely identify individual retail trades, bypassing the oddlot limitation.
- **Extended Horizons:** Analyze intraday windows (minutes to hours) for immediate effects and longer-term windows (weeks to months) for persistent patterns.
- **Behavioral Mechanisms:** Incorporate order flow data, options market activity, or survey-based sentiment to directly measure retail expectations and trading patterns.
- **Alternative Measures:** Cross-validate retail intensity using broker data, retail options activity, or social media sentiment (e.g., r/wallstreetbets).

---

## References

Barber, B. M., & Odean, T. (2008). All That Glitters: The Effect of Attention and News on the Buying Behavior of Individual and Institutional Investors. *Review of Financial Studies*, 21(2), 785–818.

Bertone, S. (2011). Uninformed trader risk and market inefficiency (Master's thesis, Concordia University). https://spectrum.library.concordia.ca/id/eprint/7280/1/Bertone_MSc_S2011.pdf

Center for Research in Security Prices. (2024). CRSP daily stock file [Data set]. Wharton Research Data Services. https://wrds-www.wharton.upenn.edu/pages/get-data/center-research-security-prices-crsp/annual-update/stock-security-files/daily-stock-file/

Fama, E. F. (1970). Efficient Capital Markets: A Review of Theory and Empirical Work. *The Journal of Finance*, 25(2), 383–417. https://doi.org/10.2307/2325486

Heston, S. L., & Sinha, N. R. (2016). News versus sentiment: Predicting stock returns from news stories (Finance and Economics Discussion Series No. 2016-048). Board of Governors of the Federal Reserve System. https://doi.org/10.17016/FEDS.2016.048

J Bradford De Long, Shleifer, A., Summers, L. H., & Waldmann, R. J. (1990). Noise Trader Risk in Financial Markets. *The Journal of Political Economy*, 98(4), 703–738.

Kudryavtsev, A. (2019). The effect of trading volumes on stock returns following large price moves. *Economic Annals*, 64(220), 85–116. https://doi.org/10.2298/EKA1920085K

Shefrin, H., & Statman, M. (1985). The disposition to sell winners too early and ride losers too long: Theory and evidence. *The Journal of Finance*, 40(3), 777–790. https://doi.org/10.1111/j.1540-6261.1985.tb05002.x

Shleifer, A., & Summers, L. H. (1990). The noise trader approach to finance. *Journal of Economic Perspectives*, 4(2), 19–33. https://doi.org/10.1257/jep.4.2.19

Shleifer, A., & Vishny, R. W. (1997). The Limits of Arbitrage. *The Journal of Finance*, 52(1), 35–55. https://doi.org/10.1111/j.1540-6261.1997.tb03807.x

Wheat, C., & Eckerd, G. (2025). A decade in the market: How retail investing behavior has shifted since 2015. JPMorganChase Institute.

---

## Contact & License

**Author:** Michael Kaufmann (Economic Departmental Honors Program, Clemson University)

**License:** This repository does not yet specify a formal license. If you plan to use or adapt this work, please contact the author or add a LICENSE file (e.g., MIT, CC-BY).

---

*Last Updated: July 2026*
