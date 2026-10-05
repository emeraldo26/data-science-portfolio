# Wine Quality: Prediction & Inference with OLS

**Question:** which physicochemical properties drive wine quality, and how well can we predict it, for red and white wines combined?
**Data:** [UCI Wine Quality](https://archive.ics.uci.edu/dataset/186/wine+quality) — 1,599 red + 4,898 white wines (6,497 total), 11 continuous predictors plus a wine-colour indicator. Included in [`data/`](data/).
**Stakeholders:** winemakers, vineyards, retailers, food scientists.

## Approach
- **Prediction:** built OLS models by adding predictors incrementally (starting from alcohol, the most correlated), then tuned a **LassoCV on degree-2 polynomial features** to capture non-linearities and interactions.
- **Inference:** refit OLS in `statsmodels` on the ten most informative terms and interpreted coefficients, p-values and multicollinearity.

## Results (held-out test set)
| Model | RMSE | MAE | R² |
|---|---|---|---|
| Alcohol only | 0.767 | 0.602 | 0.187 |
| All linear predictors | ≈ 0.72–0.73 | ≈ 0.56 | ≈ 0.27 |
| **LassoCV, degree-2 polynomial** | **0.722** | **0.558** | **0.281** |

- **Alcohol** has a significant non-linear effect (alcohol², p < 0.001) and **free sulfur dioxide** matters both on its own, squared and through its interaction with alcohol (all p < 0.001).
- Sulphates and volatile acidity terms were not individually significant once the other terms were included; the large condition number signals multicollinearity, noted as a limitation.
- Recommendation: monitor and tune alcohol and free-SO₂ levels in production; investigate the factors behind density.
- Modest R² reflects that quality scores are subjective and only partly explained by chemistry.

## Files (read in order)
| File | What it is |
|---|---|
| [`01_proposal`](01_proposal.html) | Project proposal (`.ipynb` / `.html`) |
| [`02_analysis_code`](02_analysis_code.html) | Full modeling code (`.ipynb` / `.html`) |
| [`03_final_report`](03_final_report.html) | Final stakeholder report (`.ipynb` / `.html`) |

Tip: GitHub doesn't render the `.html` files in-browser; open the `.ipynb` versions on GitHub, or download the HTML to view.
