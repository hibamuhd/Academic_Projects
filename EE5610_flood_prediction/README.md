# Random Forest for Early Flood Warning in Rural Catchments

A machine learning project for **flood-risk classification using historical meteorological data from Bangladesh**. The project develops an end-to-end preprocessing and Random Forest classification pipeline, with particular emphasis on **class imbalance, probability-threshold optimization, and minority-class recall**.

## Overview

Flood prediction is a challenging classification problem because extreme flood events are relatively rare compared with normal weather conditions. As a result, a model can achieve high overall accuracy while still failing to identify a significant proportion of actual flood events.

This project investigates whether a **Random Forest classifier** can learn nonlinear relationships between meteorological variables and flood occurrence while providing interpretable predictions.

The workflow includes:

* Data preprocessing and missing-value handling
* Numerical feature standardization
* One-hot encoding of categorical station/region information
* Cyclic encoding of wind-direction features
* Random Forest classification
* Class-imbalance-aware evaluation
* ROC-AUC and Precision–Recall analysis
* Probability-threshold optimization
* Confusion-matrix analysis
* Feature-importance analysis

The ultimate goal is to establish a foundation for a **low-cost, data-driven early-warning system** suitable for resource-constrained regions.

---

## Problem Statement

Traditional flood prediction approaches can struggle to capture complex nonlinear relationships between meteorological variables such as rainfall, humidity, temperature, and wind.

This project formulates flood prediction as a binary classification problem:

**Input:** Historical meteorological observations

**Output:**

* `0` → No Flood
* `1` → Flood

The key challenge is the severe imbalance between these two classes. Consequently, the project focuses not only on accuracy but also on whether the model can successfully detect the minority flood class.

---

## Dataset

The dataset was obtained from a publicly available Kaggle repository and originates from historical meteorological records of the **Bangladesh Meteorological Department (BMD)**. It combines observations from multiple weather stations and includes long-term climatic information spanning several decades.

### Key Features

| Feature        | Description                        |
| -------------- | ---------------------------------- |
| `Tn`           | Minimum temperature                |
| `Tx`           | Maximum temperature                |
| `RHavg`        | Average relative humidity          |
| `RR`           | Rainfall                           |
| `ffavg`        | Average wind speed                 |
| `dddx`         | Wind direction                     |
| `ss`           | Bright sunshine duration           |
| Station/Region | Geographic and station identifiers |

The dataset also contains spatial and station-related information that can help capture geographic differences in meteorological conditions.

### Source

Dataset: **65 Years of Weather Data Bangladesh (1948–2013)**

Source: Kaggle / Bangladesh Meteorological Department

---

## Data Preprocessing

### Missing Values

Missing numerical values were handled using **median imputation**.

### Numerical Features

Numerical variables were standardized using `StandardScaler`.

### Categorical Features

Station and region identifiers were transformed using **OneHotEncoder**.

### Wind Direction

Wind direction is a circular variable, meaning that directions near `0°` and `360°` are actually close to each other.

To preserve this relationship, wind direction was transformed using:

```text
sin(θ)
cos(θ)
```

This prevents the model from treating `0°` and `360°` as distant numerical values.

### Date

The original preprocessing excluded the date feature from the Random Forest model rather than directly modelling temporal dependencies.

---

## Model

### Random Forest Classifier

Random Forest was selected because it is well suited to heterogeneous meteorological data and can capture nonlinear relationships between environmental variables.

The model uses an ensemble of decision trees, with:

* Bootstrap aggregation
* Random feature selection
* Multiple decision trees
* Majority voting for classification
* Class-probability estimation

The implemented model used:

```text
n_estimators = 200
train/test split = 80/20
```

The model also provides feature-importance estimates that can be used to interpret which meteorological variables contribute most strongly to predictions.

---

## Why Accuracy Alone Is Not Enough

Flood events represent a minority class in the dataset.

This creates a major problem with relying solely on accuracy.

For example, a model could classify most observations as "No Flood" and still achieve high overall accuracy while missing many actual flood events.

Therefore, this project evaluates:

* ROC-AUC
* Average Precision
* Precision
* Recall
* F1-score
* Confusion Matrix
* Probability thresholds

This provides a more meaningful assessment of the model's ability to detect rare flood events.

---

## Key Findings

### 1. High accuracy does not necessarily imply good flood detection

The model achieved approximately **93% overall accuracy**, but the minority flood class remained substantially harder to detect.

### 2. Threshold tuning improves flood sensitivity

Reducing the classification threshold from the default `0.5` to approximately `0.078` substantially increased the model's ability to identify flood events.

### 3. There is a precision–recall trade-off

Increasing flood-event recall produced more false alarms. For an early-warning system, this trade-off needs to be considered carefully because missing a genuine flood event can have substantially greater consequences than issuing an unnecessary warning.

### 4. Meteorological variables provide meaningful predictive information

Rainfall emerged as the dominant feature, while humidity, temperature, wind and cloud-related variables also contributed to the model's predictions.

---

## Limitations

The project has several important limitations:

* Severe class imbalance limits minority-class prediction performance.
* The dataset is historical and may not fully represent current climate conditions.
* The Random Forest model does not explicitly model temporal dependencies.
* A relatively low classification threshold increases false positives.
* Feature importance from Random Forest should be interpreted as model-based importance rather than causal evidence.
* Further validation across independent geographical regions would be necessary before operational deployment.

---

## Technologies Used

* **Python**
* **Pandas**
* **NumPy**
* **Scikit-learn**
* **Matplotlib**
* **Random Forest**
* **Jupyter Notebook**
* **TensorFlow Lite** *(proposed deployment pathway)*

---

## Conclusion

This project demonstrates an end-to-end machine-learning approach to flood-risk classification using historical meteorological data.

While the Random Forest classifier achieved strong overall discrimination (**ROC-AUC = 0.808**), the severe class imbalance highlighted why accuracy alone is insufficient for rare-event prediction. Probability-threshold optimization improved flood-event recall to approximately **0.578**, demonstrating the importance of selecting operating thresholds based on the practical objective of the system.

The project provides a foundation for further work involving class-imbalance techniques, temporal and spatial modelling, ensemble methods, uncertainty estimation, and eventual real-time edge deployment.

---

## Disclaimer

This repository documents a **coursework-based machine learning project** developed as an academic exercise. The project was developed with reference to **multiple publicly available sources, prior work and similar machine-learning approaches**, and AI-assisted tools were also used during parts of the research, development, debugging, and documentation process.

The methodology, model choices, preprocessing pipeline, evaluation strategy, and interpretations should therefore be understood in the context of an **academic/coursework project rather than as entirely novel research**. AI tools and external references were used as supporting resources, while the final implementation, analysis, evaluation, and presentation were reviewed and adapted as part of the project.

**Please do not treat the repository as a standalone authoritative source or assume that every implementation choice or conclusion is independently validated.** For reproducibility and further study, readers are encouraged to consult the cited dataset, references, and underlying literature.

