# Triangle Sports Analytics Competition — ACC Point Spread Model (Feb–Mar 2026)

Predicting **ACC men’s basketball point spreads** for the Triangle Sports Analytics Competition using a repeatable modeling pipeline:

**data → features → model training → evaluation → predictions (with intervals)**

> **Status:** Active / Iterating  
> **Built by:** Frank Thaingtham  
> **Stack:** Python, Pandas, scikit-learn, Jupyter

---

## What this project does

- Builds regression models to estimate point spreads for upcoming ACC matchups.
- Uses multiple seasons (2023–2026) to improve generalization and reduce overfitting.
- Produces:
  - **holdout evaluation** results across multiple model families
  - **predictions CSVs** for 2026 games
  - (optional) **prediction intervals** to express uncertainty

---

## Repository structure

    triangle-acc-spread-model/
      notebooks/
        main.ipynb
        all_years.ipynb
      data/
        raw/
          2023/
          2024/
          2025/
          2026/
        processed/
          all_years/
          2026_predictions/
      models/
        archive/
        holdout/
      reports/
        ACC_point_spread_intervals_writeup_2026.pdf
      .gitignore
      requirements.txt  (or pyproject.toml)
      LICENSE
      README.md

---

## Data

This repo contains season-level exports and derived datasets such as:

- `game_info_YYYY.csv` — game metadata
- `game_boxscores_YYYY.csv` — boxscore/team-level stats
- `team_stats_YYYY(_updated).csv` — engineered team features
- `pre_YYYY.csv`, `post_YYYY.csv` — pre/post snapshots
- `post_info_*_diff*.csv` — “diff” feature tables (performance deltas, etc.)

**Note:** If any data here is derived from external sources, treat it as research/competition use and follow the source’s terms.

---

## Modeling approach (high level)

### Problem framing
- Supervised regression: predict **spread** (or spread proxy) from team & matchup features.

### Feature design (examples)
- Team efficiency / rating deltas
- Recent form / rolling windows
- Home/away adjustments
- Pace / possessions proxies
- Opponent-adjusted stats (where available)

### Models tried
- Linear: `LinearRegression`, `Ridge`, `Lasso`, `ElasticNet`
- Robust: `HuberRegressor`
- Tree/ensemble: `RandomForestRegressor`, `GradientBoostingRegressor` (tuned)

### Evaluation
- Holdout testing by season / time split
- Metrics:
  - MAE (primary)
  - RMSE (secondary)
  - R² (context)

Add your final numbers here when ready:
- **Best holdout MAE:** `X.XX`
- **Best model:** `ModelName`
- **Training span:** 2023–2026

---

## How to run locally

### 1) Create an environment

    python -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt

### 2) Run notebooks

    jupyter lab

Start with:
- `notebooks/main.ipynb` (primary workflow / single-season focus)
- `notebooks/all_years.ipynb` (multi-year consolidation / experiments)

---

## Outputs

Common outputs you’ll see:
- `data/processed/all_years/` — combined datasets used for training + analysis
- `data/processed/2026_predictions/` — prediction tables for competition games
- `models/holdout/*.joblib` — saved models from holdout experiments
- `reports/ACC_point_spread_intervals_writeup_2026.pdf` — notes on interval estimation / methodology

---

## Notes / Known limitations

- Sports data is noisy; uncertainty matters. Intervals and calibration are a focus.
- Feature leakage is a constant risk — the pipeline attempts to separate pre-game vs post-game information.
- Model performance depends heavily on consistent preprocessing across years.

---

## Roadmap (next upgrades)

- Consolidate feature engineering into `src/` Python modules (instead of notebook-only)
- Add reproducible CLI pipeline: `python -m src.train` / `python -m src.predict`
- Add automated train/test split by date (no leakage)
- Add model tracking + experiment logs
- Add a small dashboard / report summary (plots + tables)

---

## License

MIT — see `LICENSE`.

---

## Contact

Frank Thaingtham  
- Website: https://frankthaingtham.com  
- GitHub: https://github.com/FrankThaingtham
