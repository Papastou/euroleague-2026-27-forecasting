# EuroLeague 2026–27 Season Forecasting

## Overview

An independent basketball analytics project that estimates team strength
and forecasts the final EuroLeague regular-season standings using
Ridge regression and Monte Carlo simulation.

The analysis uses a fixed snapshot of 91 completed games from the
2026–27 regular season, covering all 20 teams.

## Objectives

- Estimate team strength using possession-adjusted scoring margins.
- Account for home-court advantage.
- Evaluate the model against a simple home-court-only baseline.
- Estimate game-winning probabilities.
- Forecast final standings and qualification probabilities.
- Quantify uncertainty rather than relying on a single prediction.

## Methodology

**Team ratings:** Ridge regression with home and away team indicators.

**Model inputs:** Scoring margins normalized per 100 possessions.

**Home-court advantage:** Approximately +3.77 points per 100 possessions.

**Regularization:** Alpha approximately 5.995, selected with RidgeCV.

**Game probabilities:** Predicted scoring margins converted to win
probabilities using a normal error distribution.

**Season forecasting:** 10,000 Monte Carlo simulations of the remaining
289 regular-season games.

The main forecast uses current-season data only.

## Model Validation

Leave-one-out cross-validation was used to compare Ridge against a
home-court-only baseline.

| Metric | Ridge | Baseline | Error Reduction |
|---|---:|---:|---:|
| RMSE | 15.1179 | 16.4201 | 7.9% |
| MAE | 12.6530 | 13.7708 | 8.1% |
| Brier Score | 0.2288 | 0.2547 | 10.2% |

The regularization parameter was selected using the full sample,
so these cross-validation results should be interpreted as indicative,
not as a fully independent prospective evaluation.

## Olympiacos Forecast

Based on the 91-game snapshot:

| Indicator | Forecast |
|---|---:|
| Expected Final Wins | 25.7 |
| Probability of 1st Place | 29.1% |
| Probability of Top 4 | 72.9% |
| Probability of Top 6 | 87.4% |
| Probability of Top 10 | 98.8% |

These are model-based probabilities, not guaranteed outcomes.

## Project Contents

- `EuroLeague_2026_27_Forecasting_Portfolio.ipynb` — analysis and visualizations
- `data/league_team_summary_2026_27.csv` — team-level summary
- `data/team_game_metrics_2026_27.csv` — game-level team metrics
- `data/monte_carlo_main_91games.csv` — stored simulation results
- `requirements.txt` — Python dependencies

## How to Run

1. Download or clone this repository.
2. Install the dependencies:

   `pip install -r requirements.txt`

3. Open the notebook using JupyterLab or Jupyter Notebook.
4. Run all cells from top to bottom.

The notebook reproduces team ratings, validation metrics and
visualizations from the included datasets. Monte Carlo results are
loaded from a saved simulation snapshot, rather than rerun.

## Data Source

EuroLeague game statistics, retrieved through the public
EuroLeague API using the `py-euroleague` Python package.

The dataset represents a historical snapshot of the 2026–27
season, not a continuously updated live forecast.

## Limitations

- Relatively small early-season sample.
- Team strength is assumed constant over the simulated games.
- Injuries, roster changes and coaching decisions are not modeled.
- Prediction errors are assumed normally distributed.
- Simulated game outcomes are conditionally independent.
- Official EuroLeague tie-breaking rules are not fully implemented.
- Cross-validation is not a chronological holdout test.

## Tools

Python, pandas, NumPy, scikit-learn, SciPy, Matplotlib,
SQLite and Jupyter Notebook.

## Project Status

Completed educational and portfolio case study.
Future improvements may include temporal validation,
roster-adjusted team strength and a fully reproducible
Monte Carlo simulation pipeline.
