# Premier League Match Prediction
Binary **Win vs. Not-Win (Draw/Loss)** prediction for Premier League matches using fixtures + shooting stats aggregated from FBref.

## Files
- **prediction.ipynb** — end-to-end feature engineering, training, and evaluation.
- **matches.csv** — prepared match-level dataset used by the notebook.

## What’s inside the notebook

**Target**
- `target = 1` if `result == "W"`, else `0` (Draw/Loss combined).

**Features**
- Categorical/temporal:
  - `venue_code` (home/away encoded)
  - `opp_code` (opponent encoded)
  - `hour` (match start hour extracted from `time`)
  - `day_code` (day of week from `date`)
- Rolling form features (per team, window=3, prior matches only):
  - Rolling means of `gf, ga, sh, sot, dist, fk, pk, pkatt`.

**Model**
- `RandomForestClassifier(n_estimators=50, min_samples_split=10, random_state=1)`

**Train/Test split (time-based)**
- Train: matches **before `2022-01-01`**
- Test: matches **after `2022-01-01`**

**Result**
- **Precision (Win as positive class): 67.5%**
