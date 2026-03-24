
# Early Prediction of Clinical Deterioration Risk in ICU Patients

## Overview

This project focuses on early prediction of clinical deterioration risk in ICU patients using physiological measurements collected during the initial hours of admission.

The task is framed as a **prognostic modelling problem**, where the goal is to estimate the probability of **future in-hospital mortality** using early time-series clinical data.

---

## Dataset

The dataset used is from the PhysioNet 2012 Challenge:

* Source: https://physionet.org/content/challenge-2012/1.0.0/
* 4,000 ICU patient stays (Set A)
* Includes:

  * Static features (Age, Gender, ICUType, etc.)
  * 37 time-series physiological variables
* Target:

  * In-hospital mortality (binary classification)


---

## Methodology

### Preprocessing

* Converted timestamps (HH:MM → hours)
* Replaced missing values (-1 → NaN)
* Filtered data based on observation windows (6h, 12h, 24h, 48h)

### Feature Engineering

Time-series data was transformed into interpretable summary features:

* Mean, Min, Max
* Last observed value
* Standard deviation
* Linear trend (slope)

### Models

* Random Forest
* XGBoost (best performing)
* Multi-Layer Perceptron (MLP)

---

## Results

| Model         |   ROC-AUC |
| ------------- | --------: |
| Random Forest |     0.873 |
| XGBoost       |     0.890 |
| Tuned XGBoost | **0.897** |
| MLP           |     0.756 |

Cross-validation:

* Mean AUC: 0.850
* Std: 0.007

### Time-Window Analysis

| Window |   AUC |
| ------ | ----: |
| 6h     | 0.763 |
| 12h    | 0.791 |
| 24h    | 0.807 |
| 48h    | 0.867 |

---

## Key Insights

* Early ICU data (within 6–12 hours) already provides useful predictive signal.
* XGBoost performs best for structured clinical data.
* Neurological, renal, and respiratory variables are strong predictors.

---

## Limitations

* High missingness in some variables (>90%)
* Loss of temporal detail due to feature summarisation
* No external validation dataset

---

## Future Work

* Use sequence models (LSTM / Transformers)
* Incorporate missingness-aware modelling
* Validate on external ICU datasets

---

## How to Run

1. Download dataset from PhysioNet
2. Place data in `/data/` directory
3. Run the notebook:

```bash
jupyter notebook notebooks/ICU_Prediction_Final.ipynb
```

---

## References (Harvard Style)

Goldberger, A.L. et al. (2000) *PhysioBank, PhysioToolkit, and PhysioNet*. Circulation.

Silva, I. et al. (2012) *Predicting in-hospital mortality of ICU patients: The PhysioNet/Computing in Cardiology Challenge 2012*.

Chen, T. and Guestrin, C. (2016) *XGBoost: A Scalable Tree Boosting System*. arXiv.

---

## Author

Gowtham Vaddanam
MSc Data Science
University of Hertfordshire

