# Kidney Disease Risk Analysis Using Ordinal Logistic Regression

A group project for the **Categorical Data Analysis** course at **BINUS University**.

The project explores clinical and lifestyle variables associated with kidney disease risk categories using ordinal logistic regression in R.

## Dataset

`kidney_disease_dataset.csv` contains **20,538 observations**, with **42 predictors** and one target variable.

| Target category | Records |
| --- | --- |
| No Disease | 16,432 |
| Low Risk | 2,054 |
| Moderate Risk | 821 |
| High Risk | 821 |
| Severe Disease | 410 |

Predictors include age, blood pressure, urine measurements, medical history, lifestyle factors, and laboratory indicators.

## Methods

- Check for duplicate records and missing values.
- Explore variables using bar charts, box plots, and a correlation heatmap.
- Standardize selected numerical variables and encode categorical predictors.
- Fit an ordinal logistic regression model using `MASS::polr()`.
- Examine individual coefficients using Wald tests.
- Compare the full model with an intercept-only model using a likelihood-ratio test.
- Evaluate fitted classifications using a confusion matrix.

## Results

### Individual Predictor Tests

The saved model output reports four predictors with Wald p-values below **0.05**:

| Predictor | Coefficient | Wald p-value |
| --- | --- | --- |
| Specific gravity of urine | 5.044546 | 2.19 × 10⁻²⁴⁵ |
| Pus cells in urine | 0.131237 | 0.000159 |
| Appetite | 0.094469 | 0.006517 |
| Estimated glomerular filtration rate (eGFR) | −0.001171 | 0.024389 |

These are results from the submitted model. Their interpretation is limited by the category-ordering issue described below.

### Overall Model Evaluation

| Measure | Recorded result |
| --- | --- |
| Likelihood-ratio statistic | 55.6083 |
| Degrees of freedom | 42 |
| Likelihood-ratio p-value | 0.0778 |
| Classification accuracy | 80.01% |
| Majority-class baseline | 80.01% |
| Cohen's kappa | 0 |

The full model did not significantly improve on the intercept-only model at the **0.05** significance level.

The classifier predicted **No Disease for every observation**. Its accuracy therefore matched the majority-class baseline, and it did not identify observations in the other four categories.

## Important Limitations

- The notebook converts the target with `as.factor()` without specifying its intended order. The fitted model uses `High_Risk → Low_Risk → Moderate_Risk → No_Disease → Severe_Disease`, rather than increasing disease severity. The model needs to be refitted with the intended ordering before interpreting effects on severity.
- Evaluation uses the same observations used to fit the model; no separate test set is included.
- Results are taken from saved notebook outputs and have not been independently reproduced.

## Tools

**R**, with MASS, ggplot2, reshape2, dplyr, and caret.

## Project Files

| File | Description |
| --- | --- |
| `AOL_CategoricalDataAnalysis_Group_7.ipynb` | R notebook containing exploration, preprocessing, modeling, and evaluation |
| `kidney_disease_dataset.csv` | Dataset used in the analysis |
| `model_summary.csv` | Optional exported coefficients and model thresholds |
| `LRT_Table.csv` | Optional exported likelihood-ratio test results |

## How to Run

Open the notebook with an **R kernel**, install the required packages, and place `kidney_disease_dataset.csv` in the working directory.

Run the cells in order to reproduce the analysis workflow. Correcting the target order will produce a revised model, whose results may differ from those recorded above.

## Authors

**Group 7 — BINUS University**

- Marcell Prasetyo
- Nusantara Kusuma
- Ricardo Xavier Rinzi
