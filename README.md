# Kaggle-LCMS_Retention_Time

Machine learning project to predict LC-MS retention time of small molecules using molecular descriptors. Includes data cleaning, EDA, feature selection, regression model comparison, Extra Trees final model, feature importance analysis, error evaluation, and a deployment-ready prediction workflow from molecular descriptors.

## LC-MS Retention Time Prediction

This project uses machine learning to predict **LC-MS retention time** of small molecules from molecular descriptors. The dataset is based on METLIN retention time data with calculated molecular descriptors.

## Objective

The goal is to build a regression model that predicts retention time in minutes (`rt_min`) using molecular descriptor features.

## Dataset

**Source:** Kaggle - METLIN Retention Times with Molecular Descriptors

The original retention time column `rt` was provided in seconds and converted to minutes:

```python
df_clean["rt_min"] = (df_clean["rt"] / 60).round(3)
```

## Workflow

The project includes:

- Data loading and inspection
- Data cleaning and preprocessing
- Exploratory data analysis
- Feature selection
- Train-test split
- Regression model comparison
- Final model evaluation
- Feature importance analysis
- Model saving for future use

## Models Compared

The following models were tested:

- Linear Regression
- Ridge Regression
- Random Forest Regressor
- Extra Trees Regressor
- Hist Gradient Boosting Regressor
- XGBoost Regressor

## Best Model

The best-performing model was:

**Extra Trees Regressor with reduced features**

Final test performance:

| Metric | Value |
|---|---:|
| MAE | 0.9164 min |
| RMSE | 1.3776 min |
| R² | 0.7775 |

The model explains approximately **77.8%** of the variation in retention time.

## Feature Importance

The most important feature was **MolLogP**, which is chemically meaningful because hydrophobicity strongly affects retention in reversed-phase LC-MS.

Other important features included descriptors related to:

- Aromaticity
- Hydrogen bonding
- Molecular polarity
- Surface area
- Molecular complexity

## Deployment Concept

The final model can be used to estimate retention time for new molecules by following this workflow:

```text
SMILES → RDKit descriptors → selected features → trained model → predicted RT
```

The trained model and selected features can be saved using `joblib`:

```python
joblib.dump(final_model, "final_extra_trees_rt_model.pkl")
joblib.dump(selected_features, "selected_features.pkl")
```

## Limitation

Retention time depends strongly on chromatographic conditions such as column type, mobile phase, gradient, flow rate, temperature, and pH. Therefore, this model should be used as a decision-support tool, not as a replacement for experimental LC-MS analysis.

## Requirements

Main libraries:

- pandas
- numpy
- matplotlib
- scikit-learn
- xgboost
- joblib
- rdkit

## Conclusion

This project shows that molecular descriptors can be used to predict LC-MS retention time with good accuracy. Tree-based ensemble models outperformed linear models, and Extra Trees Regressor offered the best balance between performance and practical deployment.

---

> ## ***Author:*** Sam Pharmed  
> [Kaggle](https://www.kaggle.com/sampharmed) | [GitHub](https://github.com/Samb-pharmed)  
> **Date:** 19 April 2026  
> **Dataset:** [LCMS Retention Time Dataset](https://www.kaggle.com/datasets/satwikmurarka/meltin-retention-times-with-molecular-descriptors)
