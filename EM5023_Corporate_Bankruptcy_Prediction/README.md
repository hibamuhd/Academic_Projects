# Corporate Bankruptcy Prediction Using Machine Learning

A machine learning project for **predicting corporate bankruptcy from financial ratios**, developed as part of the *Business Analytics Using Python* coursework.

The project compares four classification approaches — **Logistic Regression, Decision Tree, Random Forest, and Gradient Boosting** — on the Taiwan Bankruptcy Prediction Dataset, with particular emphasis on **class imbalance, model comparison, minority-class detection, and financial feature interpretation**.

---

## Project Overview

Corporate bankruptcy prediction is a highly imbalanced classification problem where accurately identifying the minority class is more important than maximizing overall accuracy.

This project investigates whether financial accounting ratios can be used to identify companies at risk of bankruptcy and evaluates multiple machine learning models using metrics beyond accuracy.

### Key Objectives

* Explore relationships between financial ratios and bankruptcy
* Handle severe class imbalance using **SMOTE**
* Compare four classification algorithms
* Evaluate models using **ROC-AUC, Precision, Recall and F1-score**
* Validate model stability using **5-fold stratified cross-validation**
* Identify the financial indicators most associated with bankruptcy risk
* Translate model outputs into potential business and financial-risk applications

---

## Dataset

The project uses the **Taiwan Bankruptcy Prediction Dataset**, originally constructed from the Taiwan Economic Journal (TEJ) database and available through the UCI Machine Learning Repository. The dataset contains financial information for companies listed on the Taiwan Stock Exchange during 1999–2009.

| Property                  |             Value |
| ------------------------- | ----------------: |
| Observations              |         **6,819** |
| Predictor variables       |            **95** |
| Total variables           |            **96** |
| Bankrupt observations     |    **220 (3.2%)** |
| Non-bankrupt observations | **6,599 (96.8%)** |
| Missing values            |          **None** |

The predictor variables represent financial dimensions including:

* Profitability
* Liquidity
* Solvency / leverage
* Efficiency
* Growth
* Cash flow
* Per-share metrics

This results in an approximately **30:1 class imbalance**, making conventional accuracy-based evaluation unsuitable.

---

## Data Preprocessing

### Missing Values

The dataset contained **no missing values**, so no imputation was required. A threshold-based mechanism for dropping features with excessive missingness was nevertheless included as a robustness measure.

### Outlier Treatment

Financial ratios can contain extreme values. A **1st–99th percentile clipping strategy** was used to reduce the influence of extreme observations while preserving the overall structure of the data.

### Class Imbalance

Only **3.2% of observations represented bankrupt companies**.

To prevent models from simply learning the majority class, **SMOTE (Synthetic Minority Oversampling Technique)** was applied **only to the training set** to avoid test-set leakage.

The resampled training data contained **5,279 observations per class**. The original class distribution was preserved in the stratified test set.

### Feature Scaling

`StandardScaler` was applied for Logistic Regression, while tree-based models were trained without scaling because Decision Trees, Random Forest and Gradient Boosting are invariant to feature scale.

---

## Exploratory Analysis

Correlation analysis identified several financial ratios with meaningful associations with bankruptcy, particularly:

* Net Worth / Assets
* Debt Ratio %
* Current Ratio
* Retained Earnings / Total Assets

The analysis also revealed substantial **multicollinearity** among related financial indicators, such as Current Ratio and Quick Ratio, and among different solvency and profitability measures.

This supported the use of multivariate models capable of capturing interactions across multiple financial dimensions.

---

## Models

Four classification models were evaluated.

### Logistic Regression

Used as an interpretable linear baseline with L2 regularization.

### Decision Tree

A depth-limited decision tree was used to capture nonlinear relationships while controlling overfitting.

### Random Forest

A **200-tree Random Forest** was trained using bootstrap aggregation and randomized feature selection, with maximum depth limited to 10.

### Gradient Boosting

A sequential tree ensemble using **150 estimators**, learning rate `0.1`, and maximum depth `4`.

The model configurations are documented in the coursework report.

---

## Model Evaluation

Because of the severe class imbalance, the primary evaluation metrics were:

* **ROC-AUC**
* **Precision**
* **Recall**
* **F1-score**
* Accuracy as a secondary metric
* Confusion matrices

Five-fold stratified cross-validation was additionally performed for Random Forest and Gradient Boosting to evaluate stability across different data splits.

---

## Key Findings

### Financial distress is multidimensional

No single financial ratio dominates the prediction problem. The model relies on information across several dimensions of financial health.

### Leverage and equity position are major signals

Net Worth / Assets and Debt Ratio % ranked as the two most important features, highlighting the importance of a company's equity buffer and leverage position.

### Liquidity matters

Current Ratio and Working Capital / Total Assets were among the strongest predictors, suggesting that liquidity indicators provide valuable early signals of financial distress.

### Model choice depends on the business objective

Logistic Regression achieved the highest recall (**84.1%**) but produced substantially more false positives, while Random Forest provided a better precision–recall balance. Gradient Boosting achieved the highest precision (**33.3%**) but lower recall (**52.3%**).

---

## Business Applications

The model can potentially support:

* Credit-risk screening
* Corporate financial monitoring
* Portfolio risk assessment
* Early-warning systems
* Risk-based credit decisions

The project proposes a two-stage screening framework in which a high-recall model initially identifies potentially distressed firms, followed by a more balanced ensemble model for further assessment.

---

## Limitations

* The dataset contains severe class imbalance.
* The analysis uses historical financial-statement ratios and may not capture real-time changes in company conditions.
* Feature importance represents model association, not causal relationships.
* The dataset covers Taiwanese listed companies and may not generalize directly to other countries, industries or company sizes.
* Additional temporal validation would be useful for assessing performance on future observations.

---

## Future Work

Potential extensions include:

* Industry-specific bankruptcy models
* Temporal modelling of changing financial ratios
* Alternative data sources such as market indicators and news
* SHAP-based model explainability
* Probability calibration
* Cost-sensitive classification
* XGBoost / LightGBM comparison
* Real-time financial risk monitoring

---

## Disclaimer

This is a coursework project developed using **multiple public sources, prior similar ML approaches, and AI-assisted tools** during research, implementation, debugging, and documentation. It should not be considered original research or independently validated; refer to the cited sources and literature for further verification.

---

## References

1. Taiwan Bankruptcy Prediction Dataset — UCI Machine Learning Repository.
2. Taiwan Economic Journal (TEJ) financial data.
3. Altman, E. I. — *Financial Ratios, Discriminant Analysis and the Prediction of Corporate Bankruptcy*.
4. Relevant machine-learning and financial distress literature cited in the accompanying coursework report.
