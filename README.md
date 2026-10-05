# Data Science Portfolio — Emerald Ouyang

MS Business Analytics · Python · Machine Learning · Statistical Modeling

Three end-to-end projects from my graduate coursework: two predictive-modeling competitions on Airbnb listings and one statistical analysis (OLS inference) of wine quality. Each folder has its own README with the problem, approach, results and how to read the notebook.

| Project | Type | Task | Key methods | Result |
|---|---|---|---|---|
| [Airbnb Superhost Classification](airbnb-superhost-classification/) | Machine learning · classification | Predict whether a host is a Superhost | Feature engineering, XGBoost, Gradient Boosting, CatBoost, AdaBoost, Bagging, RF, KNN, randomized/Bayesian tuning | **Test ROC-AUC 0.970** |
| [Airbnb Price Regression](airbnb-price-regression/) | Machine learning · regression | Predict nightly listing price | Log-target modeling, Random Forest, Bagging, tuned XGBoost | **Test MAE ≈ $96.6** (from $104.8 baseline XGBoost) |
| [Wine Quality — OLS & Inference](wine-quality-ols-analysis/) | Statistics · data analysis | Predict and explain wine quality (red + white) | OLS (statsmodels), polynomial + interaction terms, LassoCV, hypothesis testing | **Test RMSE 0.722**, R² 0.28; alcohol and free SO₂ are the key drivers |

Both Airbnb competition entries beat the course's performance threshold.

## Skills demonstrated
- **Modeling:** logistic/linear regression, Ridge/Lasso, KNN, decision trees, bagging, random forest, AdaBoost, gradient boosting, XGBoost, CatBoost
- **Evaluation & tuning:** stratified / repeated K-fold CV, grid, randomized and Bayesian hyperparameter search, out-of-bag error, ROC-AUC, MAE, RMSE, R²
- **Data prep:** missing-value imputation (without test-set leakage), text/percent parsing, one-hot encoding, engineered features, log-transforming skewed targets
- **Statistical inference:** OLS, interpreting coefficients and p-values, non-linear and interaction effects, multicollinearity diagnostics
- **Communication:** stakeholder framing, written reports with recommendations
- **Tools:** Python, pandas, NumPy, scikit-learn, XGBoost, CatBoost, statsmodels, matplotlib, seaborn, Jupyter

## Repository layout
```
├── airbnb-superhost-classification/   notebook + data dictionary
├── airbnb-price-regression/           notebook + data dictionary
├── wine-quality-ols-analysis/         proposal → code → final report (ipynb + html), data/
├── requirements.txt
└── .gitignore
```

## Notes on data
The two Airbnb projects were course competitions whose data and leaderboards are no longer available; the raw `train.csv`/`test.csv` are therefore **not** included (the data dictionaries are). The notebooks keep their saved outputs so results can be read without re-running. The wine datasets are public ([UCI Wine Quality](https://archive.ics.uci.edu/dataset/186/wine+quality)) and included, so that project runs end-to-end:

```bash
pip install -r requirements.txt
jupyter notebook wine-quality-ols-analysis/02_analysis_code.ipynb
```
