# **Multi-/Individual-Target Regression and Risk Assessment of POPs**

## **Overview**
This repository contains Python implementations for analyzing Persistent Organic Pollutants (POPs) using machine learning regression techniques and Monte Carlo simulations. The goal of the study was twofold:
1. To predict the concentrations of various POPs (`TEQ_PCDDFs`, `TEQ_dlPCBs`, `TEQ_total`, `mPCBs_total`, and `PBDEs_total`) and identify key predictors using machine learning.
2. To assess the dietary exposure risk for POPs using a probabilistic Monte Carlo simulation framework.

---

## **Contents**
This repository includes two main analyses:
1. **Multi-/Individual-Target Regression Analysis**  
   _(See: [`Analysis of Regression&SHAP.ipynb`](Analysis%20of%20Regression&SHAP.ipynb))_
2. **Risk Assessment Using Monte Carlo Simulation**  
   _(See: [`Monte_Carlo-HQ&MOE.ipynb`](Monte_Carlo-HQ&MOE.ipynb))_

---

## **1. Multi-/Individual-Target Regression Analysis**
This analysis develops machine learning models to predict pollutant concentrations and identify key predictors. 

### **Highlights**
- **Dataset**: 
  - Categorical features: `Province`, `Food type`.  
  - Continuous features: `Urbanization Rate`, `Population Density`, `GDP per capita`, `Temperature`, `Latitude`, etc.  
- **Preprocessing**:
  - Removal of zero values and outliers using the interquartile range (IQR) method.
  - One-hot encoding for categorical variables.
  - Splitting the dataset into 90% training and 10% testing subsets.
- **Machine Learning**:
  - **Multi-Target Regression**: Predict all pollutants simultaneously using `MultiOutputRegressor` wrapped around:
    - Random Forest
    - Gradient Boosting
    - Ridge Regression
    - Linear Regression
    - Support Vector Regression (SVR)
  - **Individual-Target Regression**: Each pollutant is modeled independently using algorithms such as Ridge Regression, Random Forest, Huber Regressor, and Lasso Regression.
- **Evaluation Metrics**:
  - `R²`: Explained variance.
  - `Mean Squared Error (MSE)`: Prediction error.
- **Feature Importance**:
  - Feature importance and predictors' impact analyzed using **SHAP (SHapley Additive exPlanations)**.
- **Outputs**:
  - Consolidated predictions and evaluation metrics.
  - SHAP-derived feature importance values for the top 15 predictors.
  - True vs Predicted scatter plots for each pollutant.

---

## **2. Risk Assessment Using Monte Carlo Simulation**
The Monte Carlo simulation framework evaluates dietary exposure risks to PCDD/Fs, dl-PCBs, and PBDEs across three food categories: `eggs`, `fish`, and `meat`.

### **Highlights**
- **Input Parameters**:
  - **Food Consumption Rates**: From studies conducted by the Chinese Center for Disease Control and Prevention (Zhang et al., 2024).
  - **Body Weight**: Based on the Dietary Guidelines for Chinese Residents (2022).
  - **Analyte Concentrations**: Modeled using statistical distributions (e.g., gamma, lognormal, Weibull, Pareto).
- **Modeling Approach**:
  - **Food Consumption and Body Weight**: Modeled using normal distributions.
  - **Analyte Concentrations**: Best-fit distributions determined using the Akaike Information Criterion (AIC).
  - **Simulation**:
    - Conducted for 10,000 iterations to account for variability and uncertainty.
- **Risk Metrics**:
  - **Hazard Quotient (HQ)**: For PCDD/Fs and dl-PCBs based on tolerable daily intake (TDI) of 0.3 pg WHO2005-TEQ/kg b.w. (EFSA, 2018).
  - **Margin of Exposure (MOE)**: For PBDEs based on chronic human dietary intake values from EFSA (2011).
  - **Risk Thresholds**:
    - `HQ > 1`: Potential health risk for PCDD/Fs and dl-PCBs.
    - `1/MOE > 0.4`: Potential health risk for PBDEs.
- **Outputs**:
  - Best-fit distributions and parameters for analyte concentrations.
  - Risk metrics (`HQ` and `1/MOE`) summarized by food category and gender.
  - Probability density plots for visualization.

---

## **Files and Notebooks**
- **[`Analysis of Regression&SHAP.ipynb`](Analysis%20of%20Regression&SHAP.ipynb)**:
  - Implements the multi-/individual-target regression analysis.
  - Includes data preprocessing, machine learning model development, evaluation, and feature importance analysis.
- **[`Monte_Carlo-HQ&MOE.ipynb`](Monte_Carlo-HQ&MOE.ipynb)**:
  - Implements the Monte Carlo simulation framework for dietary risk assessment.
  - Includes probabilistic modeling, risk metric calculations, and visualization.

---

## **Getting Started**

### **Requirements**
- Python 3.8 or above
- Required libraries:
  - `pandas`, `numpy`, `seaborn`, `matplotlib`
  - `PyCaret`
  - `scipy`, `shap`
  - `tqdm` (for progress tracking)

### **Setup**
```bash
# Clone this repository
git clone https://github.com/yourusername/POPs_Analysis.git
cd POPs_Analysis

# Install dependencies
pip install -r requirements.txt

# Open the notebooks in Jupyter or your preferred environment
jupyter notebook
