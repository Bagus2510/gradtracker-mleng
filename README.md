# GradTracker ML Engineering 🧠

![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter)
![XGBoost](https://img.shields.io/badge/XGBoost-1.7-blue?style=for-the-badge)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.3-F7931E?style=for-the-badge&logo=scikit-learn)

This repository contains the end-to-end Machine Learning pipeline for the GradTracker project. It is dedicated to predicting the probability of students graduating late based on their academic trajectories and demographic backgrounds.

## 🔬 Methodology Overview
The pipeline handles raw dataset ingestion, complex feature engineering, model training, and rigorous evaluation. 

### Key Techniques:
- **Feature Engineering**: Deriving macro indicators such as `Rata-rata IPS` and `IPS Drop` (semester-over-semester GPA deltas) from sparse transcript data.
- **Class Imbalance Handling**: Utilizing **SMOTE** (Synthetic Minority Over-sampling Technique) to balance the ratio between on-time and late graduates.
- **Hyperparameter Tuning**: Using `GridSearchCV` to find the optimal estimators and learning rates.
- **Model Explainability**: Integrating SHAP (SHapley Additive exPlanations) to interpret model decisions and output personalized student recommendations.

## 🏆 Models Evaluated
- Logistic Regression
- Random Forest Classifier
- **XGBoost Classifier (Selected for Production)**

*XGBoost achieved the highest ROC-AUC score and recall for the minority class (Late graduates).*

## 📂 Repository Structure
- `/notebooks`: Jupyter notebooks containing EDA (Exploratory Data Analysis), modeling pipelines, and SHAP visualizations.
- `/data`: Raw and processed dataset storage.
- `/models`: Serialized `.pkl` models ready to be deployed to the FastAPI backend.
- `future_roadmap.md`: Strategic plan for implementing **Course-Level Analysis** (V2) using Association Rule Mining to pinpoint specific subjects causing GPA drops.

## 🚀 Usage
1. Navigate to the directory:
   ```bash
   cd gradtracker-mleng
   ```
2. Install data science dependencies:
   ```bash
   pip install jupyter pandas scikit-learn xgboost imbalanced-learn matplotlib seaborn shap
   ```
3. Launch Jupyter Notebook to explore the training pipeline:
   ```bash
   jupyter notebook
   ```
