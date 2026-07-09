# Retail Trading on Post Shock Price Behavior

Honors thesis examining the relationship between retail trading activity and post-shock price behavior on the NYSE.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Data](#data)
- [Methods](#methods)
- [Repository Structure](#repository-structure)
- [Reproducing the Analysis](#reproducing-the-analysis)
- [Dependencies](#dependencies)
- [Results & Figures](#results--figures)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Project Overview

This repository contains code, notebooks, and supporting materials for an honors thesis investigating how retail trading activity relates to price behavior after large intraday shocks on the New York Stock Exchange (NYSE). The analysis focuses on short- and medium-term returns and liquidity following identified price shocks and studies whether retail participation affects subsequent price resilience or continuation.

## Data

The analysis uses high-frequency trade and quote information together with trade classification indicators that proxy retail activity (see the `data/` folder for preprocessing scripts and descriptions). Raw market data may be large and/or subject to vendor licensing; due to size and licensing constraints, raw datasets are not included in this repository. Example datasets or preprocessed samples used for demonstrations are stored in `data/sample/`.

If you plan to reproduce the results, ensure you have access to the original market data or provide appropriately formatted samples with the same column schema used in the preprocessing notebooks.

## Methods

Key steps in the project include:

- Identifying intraday price shocks using an event detection procedure (thresholds and lookback windows are implemented in `src/events.py`).
- Measuring post-shock price behavior using event-study windows (e.g., 5, 15, 60-minute horizons) and estimating abnormal returns.
- Quantifying retail trading activity around events using broker/trader classification or volume-based heuristics.
- Running cross-sectional and panel regressions to test whether retail activity predicts post-shock returns or affects price reversal/continuation.
- Robustness checks including alternative shock definitions, different windows, and control variables for liquidity, volatility, and market-wide factors.

Full details are documented in the thesis write-up and in the notebooks under `notebooks/`.

## Repository Structure

- `data/` — data preprocessing, sample datasets, and descriptions.
- `notebooks/` — Jupyter notebooks used for exploration, figures, and main results.
- `src/` — modular Python code used for data processing, event detection, and econometric analysis.
- `results/` — tables, figures, and intermediate outputs (kept small; large outputs excluded).
- `docs/` — supplementary documentation and thesis-related files.

## Reproducing the Analysis

1. Clone the repository:

   git clone https://github.com/MichaelwKaufmann/Retail-Trading-on-Post-Shock-Price-Behavior.git

2. Create and activate a Python virtual environment (recommended):

   python3 -m venv venv
   source venv/bin/activate

3. Install dependencies:

   pip install -r requirements.txt

4. Prepare your data following the schema in `data/README.md` and place preprocessed files in `data/processed/`.

5. Run the notebooks in `notebooks/` or execute the analysis scripts in `src/` to reproduce tables and figures.

## Dependencies

Typical Python dependencies include:

- Python 3.8+
- pandas
- numpy
- scipy
- statsmodels
- jupyterlab / notebook
- matplotlib / seaborn
- tqdm

Pin specific versions in a `requirements.txt` file for reproducibility.

## Results & Figures

Key tables and figures generated for the thesis are available in the `results/` folder. If you need high-resolution figures or raw output files, run the notebooks with the full dataset and the appropriate configuration in `notebooks/config.ipynb` (or `notebooks/config.json`).

## Contributing

Contributions are welcome. If you plan to submit changes, please open an issue describing the proposed change or create a pull request with a clear description and tests (when applicable).

## License

This repository does not yet specify a license. If you want to apply a license (e.g., MIT, CC-BY), add a `LICENSE` file at the repository root and update this section.

## Contact

Michael Kaufmann — see the GitHub profile for contact details.

---

Generated/edited by GitHub Copilot via an assistant on request. If you'd like different wording, additional sections (e.g., expected citations, thesis PDF, or dataset licensing), or a specific license added, tell me and I will update the file or create a branch + pull request as you prefer.
