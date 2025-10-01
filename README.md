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

### What are “rolling form” features?
We summarize a team’s **recent form** by averaging stats from its **previous 3 matches** (window=3), computed **before** the current match (shifted by 1 to avoid data leakage).

Feature names in the notebook: `rolling_sh`, `rolling_sot`, `rolling_gf`, `rolling_ga`, `rolling_dist`, `rolling_fk`, `rolling_pk`, `rolling_pkatt`.

- **gf** — Goals For (team goals scored)
- **ga** — Goals Against (opponent goals)
- **sh** — Shots
- **sot** — Shots on Target
- **dist** — Average shot distance
- **fk** — Shots from free kicks
- **pk** — Penalties scored
- **pkatt** — Penalties attempted

> Example: `rolling_sh` is the average number of shots the team took across its last 3 matches **prior** to this match.
