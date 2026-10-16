# coffee-production-forecasting-western-hararghe

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)

## Overview

This repository contains the dataset, source code, and analysis scripts for the study:

> **Machine Learning-Based Forecasting of Annual Coffee Production in Western Hararghe Zone, Ethiopia**
>
> Ketema Deresa, Hashim Siraj, Gadissa Nemomsa
> Oda Bultum University, Chiro, Oromia, Ethiopia

The study develops and evaluates six machine learning regression models (Ridge Regression, ElasticNet, Random Forest, Gradient Boosting, XGBoost, and Support Vector Regression) to predict annual coffee production in five coffee-producing districts of Western Hararghe Zone, Ethiopia, using agronomic, soil, and climatic data spanning 2000–2015 Ethiopian Calendar (approximately 2007/08–2022/23 Gregorian Calendar).

## Key Findings

- **Best model:** Ridge Regression (test R² = 0.8409, RMSE = 465.76 tons, MAE = 360.17 tons)
- **Dominant predictor:** Cultivated area (permutation importance = 1.1805 ± 0.1128)
- **Secondary predictors:** Soil type, fertilizer use, pH, exchangeable potassium
- **Negligible predictors:** All climatic variables in this dataset
- **Validation design:** Chronological, leakage-safe hold-out with in-fold preprocessing
- **Rolling-origin validation:** Mean R² = 0.8157 ± 0.0571
- **Calibration:** Slope = 0.988 ± 0.041, intercept = 55.49 tons


## Dataset

The dataset contains **N = 500 observations** from five coffee-producing districts:

- Boke
- Dara Labu
- Habro
- Shanan Dhugoo
- Tulo

**Variables:** 13 predictors (cultivated area, soil pH, total nitrogen, available phosphorus, exchangeable potassium, organic carbon, fertilizer use, soil type, annual temperature, precipitation, relative humidity, wind speed, solar radiation, soil wetness) and one target (annual coffee production in tons).

See [`data/README.md`](data/README.md) for the complete data dictionary.

## Installation

### Option 1: Using pip

```
git clone https://github.com/ketemaderesa/coffee-production-forecasting-western-hararghe.git
cd coffee-yield-forecasting-western-hararghe
pip install -r requirements.txt
```
ption 2: Using conda
```
git clone https://github.com/ketemaderesa/coffee-production-forecasting-western-hararghe.git
cd coffee-yield-forecasting-western-hararghe
conda env create -f environment.yml
conda activate coffee-yield
```
Methodology Summary
```
Data collection: Secondary data from district agricultural offices, Ethiopian National Meteorological Agency (ENMA), and NASA POWER

Data cleaning: Missing-value checks, duplicate checks, unit harmonization, IQR-based outlier flagging (no removal)

Chronological split: Training = 2000–2012 EC (N = 389); Test = 2013–2015 EC (N = 111)

In-fold preprocessing: Median/mode imputation, standardization, one-hot encoding — all fitted inside training folds only

Model training: Five-fold expanding-window TimeSeriesSplit with GridSearchCV

Model selection: Pre-specified one-standard-error (1-SE) plus parsimony rule

Final evaluation: Locked test set consulted once

Post-hoc diagnostics: Rolling-origin validation, calibration analysis, bootstrap confidence intervals, permutation importance
```
Requirements
```
Python 3.9+

scikit-learn

XGBoost

pandas

NumPy

Matplotlib

SciPy

Jupyter

See requirements.txt for exact versions.
