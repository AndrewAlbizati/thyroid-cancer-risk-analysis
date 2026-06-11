# Thyroid Cancer Risk Analysis

This repository presents an end-to-end data science project on thyroid nodule diagnosis and risk assessment using the `thyroid_cancer_risk_data.csv` dataset. The work combines exploratory data analysis, preprocessing, feature engineering, visualization, and classical machine learning to study which patient characteristics are most useful for distinguishing benign and malignant cases.

The repository has been intentionally reduced to the three assets that matter most for review:

- `thyroid_cancer_risk_analysis.ipynb`: the full notebook with analysis, visualizations, and model evaluation
- `thyroid_cancer_risk_data.csv`: the dataset used by the notebook
- `README.md`: project overview, findings, and usage notes

## Project Summary

The notebook analyzes a thyroid cancer risk dataset with:

- `212,691` patient records
- `17` original columns
- a binary diagnosis target: `Benign` vs `Malignant`
- an ordinal risk label: `Low`, `Medium`, `High`

The project goal is to understand the dataset, identify useful predictive features, and compare several supervised learning models for diagnosis classification.

## Questions Explored

- How clean and complete is the dataset?
- How are demographic, behavioral, environmental, and clinical variables distributed?
- How severe is the class imbalance between benign and malignant cases?
- Do engineered thyroid-specific features improve predictive modeling?
- Which models perform best under class imbalance?

## Dataset

Source:

- Kaggle: <https://www.kaggle.com/datasets/bhargavchirumamilla/thyroid-cancer-risk-dataset>

Core variables used in the notebook:

- Demographic: `Age`, `Gender`, `Country`, `Ethnicity`
- Behavioral: `Smoking`, `Obesity`, `Diabetes`
- Environmental: `Radiation_Exposure`, `Iodine_Deficiency`
- Genetic: `Family_History`
- Clinical: `TSH_Level`, `T3_Level`, `T4_Level`, `Nodule_Size`
- Labels: `Thyroid_Cancer_Risk`, `Diagnosis`

## Workflow

The notebook follows a standard applied machine learning pipeline:

1. Load and inspect the dataset from the local CSV included in this repo.
2. Check shape, dtypes, missing values, summary statistics, and near-duplicate records.
3. Visualize categorical and numerical feature distributions.
4. Encode categorical variables and normalize numerical features.
5. Engineer domain-informed features:
   `Size_Age_Interaction`, `TSH_T3_Ratio`, and `Thyroid_Index`
6. Explore correlations and feature relationships.
7. Train and compare multiple classifiers.
8. Evaluate performance with stratified cross-validation and classification metrics that are appropriate for imbalanced data.

## Models Evaluated

The notebook compares several models for binary diagnosis prediction:

- Random Forest
- Random Forest with SMOTE applied inside cross-validation training folds
- Logistic Regression
- K-Nearest Neighbors
- Gradient Boosting
- AdaBoost
- Extra Trees
- Multi-Layer Perceptron
- XGBoost

## Results

The dataset is meaningfully imbalanced, so the notebook focuses on precision, recall, and F1-score rather than accuracy alone.

Selected results reported directly in the notebook:

| Model | Benign F1 | Malignant F1 | Notes |
| --- | ---: | ---: | --- |
| Logistic Regression | 0.76 | 0.46 | Higher malignant recall, but much weaker overall balance |
| K-Nearest Neighbors | 0.88 | 0.48 | Solid benign performance, limited malignant recovery |
| Random Forest | 0.89 | 0.54 | Strong baseline with cross-validated predictions |
| Random Forest + SMOTE | 0.88 | 0.53 | Rebalancing did not materially improve malignant F1 |
| Gradient Boosting | 0.89 | 0.55 | Best result highlighted in the notebook conclusion |
| AdaBoost | 0.89 | 0.55 | Comparable to Gradient Boosting |
| Extra Trees | 0.89 | 0.53 | Slightly lower malignant F1 |
| Neural Network (MLP) | 0.89 | 0.54 | Similar to Random Forest |
| XGBoost | 0.89 | 0.55 | Test-set result; mean 5-fold malignant F1 ≈ 0.5435 |

## Key Takeaways

- The analysis predicts benign cases reliably, but malignant detection remains materially harder.
- Class imbalance is the main modeling challenge across nearly every algorithm tested.
- More complex models modestly outperform linear baselines, but none fully solve the malignant-class gap.
- SMOTE did not create a meaningful improvement in malignant F1 without tradeoffs elsewhere.
- The notebook is strongest as a demonstration of a complete exploratory and comparative ML workflow, not as a production clinical model.

## Visual Analysis Included

The notebook includes:

- class distribution plots
- demographic breakdowns by gender, country, and ethnicity
- diagnosis and risk-level distributions
- binary risk-factor comparisons
- hormone-level and age distribution plots
- boxplots and histograms for major numerical variables
- correlation analysis
- confusion matrices
- feature-importance visualization for the Random Forest model

## Running The Notebook

The notebook now reads the local CSV directly, so no Kaggle download step is required.

Recommended environment:

```bash
pip install jupyter pandas numpy scipy matplotlib seaborn scikit-learn imbalanced-learn xgboost
jupyter notebook thyroid_cancer_risk_analysis.ipynb
```

Then open `thyroid_cancer_risk_analysis.ipynb` and run the cells in order.

## Repository Notes

- The notebook is preserved as the primary artifact because it shows the full analytical process, not just final conclusions.
- This project is for educational and portfolio purposes only. It is not suitable for clinical decision-making.
