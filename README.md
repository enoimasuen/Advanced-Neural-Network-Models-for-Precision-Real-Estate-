# Advanced Neural Network Models for Precision Real Estate

> Can a neural network predict home prices more accurately than traditional regression models?

This project analyzes the **King County, WA house-sales dataset (`kc_house_data`)** and compares a range of statistical and machine-learning models — linear regression, stepwise selection, ridge regression, a neural network, and logistic regression — to predict residential sale prices. It was built end-to-end in **R / R Markdown**.

## Overview

The goal is to estimate home sale price from property characteristics and to evaluate how well different modeling techniques capture the relationships in the data. Interpretable linear models serve as baselines; a neural network is introduced to capture nonlinear structure the linear models miss.

## Dataset

- **Source:** King County (Seattle area), Washington, USA — ~21,600 home sales.
- **Target:** `price` (continuous).
- **Features:** `bedrooms`, `bathrooms`, `sqft_living`, `sqft_lot`, `floors`, `waterfront`, `view`, `condition`, `grade`, `sqft_above`, `sqft_basement`, `yr_built`, `yr_renovated`, `zipcode`, `sqft_living15`, `sqft_lot15` (plus `id`, `lat`, `long`, which were dropped).

## Tools

- **Language:** R, documented in R Markdown (`.Rmd`) and rendered to PDF.
- **Packages:** `caret` (data partitioning), `MASS` (stepwise selection, Box-Cox), `glmnet` (ridge regression), `nnet` (neural network), `lmtest` / `sandwich` (heteroscedasticity testing), `pROC` (ROC / AUC).
- **Visualization:** base R graphics and `corrplot` (correlation matrix).

## Modeling Approach

### Preprocessing
- Converted `price` from formatted text to numeric.
- Dropped non-predictive columns (`id`, `lat`, `long`).
- **70/30 train/test split** using `createDataPartition()` with `set.seed(1023)`.
- Applied a **log transformation** to `price` to address right-skew and stabilize variance.
- For the neural network, **min-max normalized** all numeric features and the target to the [0, 1] range.
- For the logistic-regression experiment, binarized `price` into high/low around the median.

### Models
1. **Multiple linear regression** — all predictors, as an interpretable baseline.
2. **Stepwise selection** (`stepAIC`, both directions) — retained 14 predictors.
3. **Log-transformed linear model** — remedy for skew and heteroscedasticity.
4. **Ridge regression** (`glmnet`, `alpha = 0`) — lambda chosen by cross-validation to handle multicollinearity.
5. **Neural network** (`nnet`) — single hidden layer of 10 units, `linout = TRUE`, `maxit = 1000`, trained on normalized data.
6. **Logistic regression** (`glm`, binomial) — classification of above-/below-median price, for comparison.

### Diagnostics
- **Multicollinearity:** correlation matrix and VIF (`sqft_living` ≈ 8.5 and `sqft_above` ≈ 6.5 were the highest).
- **Heteroscedasticity:** Breusch-Pagan test (p < 2.2e-16 → significant).
- **Normality:** residual histogram and Q-Q plot (residuals were non-normal and heavy-tailed).
- **Remedies explored:** log transformation, Box-Cox (optimal λ ≈ 0.096), and weighted least squares.

## Results

| Model | Metric | Scale |
|---|---|---|
| Linear regression (full) | RMSE ≈ $223,244 · R² ≈ 0.66 | raw price ($) |
| Stepwise linear | RMSE ≈ $223,239 · R² ≈ 0.66 | raw price ($) |
| Log-transformed linear | RMSE ≈ 0.307 | log price |
| Ridge regression | ≈ 85% deviance explained | raw price ($) |
| Neural network (1×10) | RMSE ≈ 0.0199 (normalized) → **~$150K order of magnitude** | normalized [0, 1]; see note below |
| Logistic regression (price ≷ median) | Accuracy ≈ 0.79 · AUC ≈ 0.87 | binary class |

> **Note on scale.** The neural network was trained on min-max-normalized data, so its raw RMSE of `0.0199` is on the [0, 1] scale and is **not** directly comparable to the dollar-scale errors of the linear and ridge models. Because min-max scaling is linear, the error back-transforms as `RMSE_$ = RMSE_norm × (max − min)`. Over the King County price range (roughly $75,000 to $7.7M), this puts the network's error on the order of **$150,000** — meaningfully below the linear model's ≈ $223,244, rather than the thousand-fold gap the unscaled figures suggest. The exact value depends on the min and max of the training split.

## Key Takeaways
- Correlation analysis, stepwise selection, and regression significance (t-statistics) consistently identified **`grade`, `sqft_living`, `yr_built`, and `waterfront`** as among the strongest predictors of price. The neural network was not used to rank feature importance, consistent with its lower interpretability.
- Linear and stepwise models explained about **66% of price variance**; ridge regression explained roughly **85% of deviance** while reducing the impact of correlated predictors.
- Linear-model residuals showed **heteroscedasticity and non-normality**; log transformation and WLS were tested as remedies.
- The **neural network** captured nonlinear price structure and was selected as the project's champion model. Once its normalized error is expressed on the dollar scale, it sits **well below the linear baseline's ≈ $223,244 RMSE**. Reduced interpretability is the main trade-off.

## Repository
- `Advanced Neural Network Models for Precision Real Estate.Rmd` — full analysis in R Markdown
- `Advanced Neural Network Models for Precision Real Estate.pdf` — rendered report
- `README.md` — this file

## Authors
Zongmin Liu · Enoghayin Imasuen — Harvard Extension School

## 📬 Contact

**Enoghayin Jillient Imasuen**  
🔗 [GitHub](https://github.com/enoimasuen) | [LinkedIn](https://www.linkedin.com/in/enoghayin-jillient-imasuen-9080b2236?)

