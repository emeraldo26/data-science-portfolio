# Airbnb Superhost Classification

**Goal:** predict whether an Airbnb host is a *Superhost* (`host_is_superhost`) from listing and host attributes.
**Metric:** ROC-AUC · **Result:** **0.970** on the held-out competition test set (course competition; see note on data). Beat the course's performance threshold.

## Data
- ~10,500 labeled listings across three markets (Chicago, Asheville, Kauai); ~57 raw columns covering host profile, response/acceptance rates, availability, pricing, reviews, and listing text. See [`data_dictionary.xlsx`](data_dictionary.xlsx).
- Raw CSVs are not included (competition data no longer available).

## Approach
1. **Cleaning:** dropped free-text, location and other low-signal columns; converted percent/boolean strings to numbers; imputed review scores, response/acceptance rates and counts with the median (categoricals with the mode), using training statistics for both sets.
2. **Feature engineering**, motivated by Airbnb's Superhost criteria (rating, response rate, cancellation, occupancy): `occupancy_rate = 1 − availability_365/365`, `host_engagement = response_rate × acceptance_rate`, and a response × occupancy interaction.
3. **Model comparison** with cross-validated ROC-AUC and hyperparameter search:

| Model | Tuning | CV ROC-AUC |
|---|---|---|
| Bagged KNN | Grid search, repeated stratified 10-fold | 0.910 |
| Random Forest | Randomized search | 0.931 |
| Bagged decision trees | Randomized search | 0.951 |
| AdaBoost | Randomized search | 0.960 |
| CatBoost | Bayesian search (skopt) | 0.962 |
| XGBoost | Randomized search (50 iters) | 0.966 |
| **Gradient Boosting (final)** | Randomized search → manual refinement | **0.970 (test)** |

4. Inspected XGBoost feature importance to sanity-check which signals drive the prediction.

## Files
- [`superhost_classification.ipynb`](superhost_classification.ipynb) — full workflow with saved outputs.
- [`data_dictionary.xlsx`](data_dictionary.xlsx) — column definitions.

