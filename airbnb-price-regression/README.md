# Airbnb Nightly Price Prediction

**Goal:** predict a listing's nightly `price` (USD) from host, location, property and review attributes.
**Metric:** MAE · **Result:** **≈ $96.6** on the held-out competition test set (course competition; see note on data). Beat the course's performance threshold.

## Data
- ~9,400 labeled listings across Chicago, Asheville and Kauai; ~57 raw columns. See [`data_dictionary.xlsx`](data_dictionary.xlsx).
- Raw CSVs are not included (competition data no longer available).

## Approach
1. **Cleaning:** dropped free-text columns; parsed percentages, price strings and bathroom counts; imputed missing values with training medians/modes; one-hot encoded location, room type, property type and neighbourhood (aligning test columns to train).
2. **Feature engineering:** bedroom-to-bathroom ratio.
3. **Models tried:** Ridge/Lasso and KNN baselines (kept as commented experiments), bagged trees (OOB error used to choose the number of trees), Random Forest, XGBoost.
4. **Key improvement — log-transforming the target.** Price is right-skewed; fitting XGBoost on `log(price)` and exponentiating predictions cut test MAE substantially:

| Model | MAE |
|---|---|
| Bagged trees (CV) | ≈ $102.5 |
| Random Forest (OOB) | ≈ $101.7 |
| XGBoost, raw price (test) | $104.8 |
| XGBoost, log price (test) | $97.0 |
| **XGBoost, log price, tuned (final, test)** | **$96.6** |

## Files
- [`price_regression.ipynb`](price_regression.ipynb) — full workflow with saved outputs.
- [`data_dictionary.xlsx`](data_dictionary.xlsx) — column definitions.
