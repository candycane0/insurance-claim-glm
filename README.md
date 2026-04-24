# Insurance Pricing Model using Poisson & Gamma GLMs

This project develops a Poisson Generalized Linear Model (GLM) to predict insurance claim frequency using real-world policy data. The goal is to identify key risk drivers and improve model performance through feature engineering and model selection.

---

## Modeling Approach

The pricing model is built in three stages:

### 1. Frequency Model (Poisson GLM)

A Poisson GLM with a log link function was used to model claim counts. Exposure was incorporated as an offset to account for differences in policy duration.

This models:
> “How often does a policyholder file a claim?”

---

### 2. Severity Model (Gamma GLM)

A Gamma GLM with a log link function was used to model claim size, using only policies with observed claims.

This models:
> “How large is a claim when it occurs?”

---

### 3. Expected Loss & Pricing

The two components were combined:

Expected Loss = Predicted Frequency × Predicted Severity

A 30% loading factor was applied:

Premium = Expected Loss × (1 + 0.30)

---

## Dataset

This project uses the **French Motor Third-Party Liability Claims dataset (freMTPL2)**, which contains policy-level information on claim counts, exposure, driver characteristics, vehicle attributes, and geographic factors.

- Kaggle source: 
https://www.kaggle.com/datasets/karansarpal/fremtpl2-french-motor-tpl-insurance-claims  
https://www.kaggle.com/datasets/floser/fremtpl2sev

- Original dataset: https://www.openml.org/d/41214  

---

## Model Development

### Baseline Model
A baseline Poisson GLM was first constructed using linear predictors.

### Model Improvements
The model was improved by:
- Adding a quadratic term for driver age to capture nonlinear risk patterns  
- Log-transforming population density to address skewness and model proportional effects  
- Evaluating variables using AIC and removing redundant predictors (e.g., geographic area)

---

## Severity Model Selection

Although several variables (vehicle age, fuel type, and BonusMalus) were not individually statistically significant in the severity model, removing them led to a substantial increase in AIC.

Therefore, these variables were retained, as they improve overall model fit. This highlights that model selection should consider overall performance rather than relying solely on individual p-values.

---

## Results

- The frequency model achieved a reduction of **over 70 AIC points** compared to the baseline model  
- The severity model exhibited weaker explanatory power, reflecting the high variability of claim sizes  
- Removing variables from the severity model increased AIC significantly, so the full model was retained  

The combined model produces realistic expected losses and premiums for each policy.

---

## Key Findings

- **BonusMalus** is the strongest predictor of claim frequency, with each one-unit increase associated with approximately a **2.4% increase** in expected claims  
- **Vehicle age** is negatively associated with claims, with each additional year corresponding to approximately a **4.2% decrease** in claim frequency  
- **Driver age** exhibits a nonlinear relationship with risk, with claim frequency peaking around age 60  
- **Vehicle power** is a significant predictor, with each unit increase associated with approximately a **1.7% increase** in claim frequency  
- **Fuel type** has a discrete effect, with regular fuel vehicles associated with approximately **7% higher** claim frequency than diesel vehicles  
- **Population density** is positively associated with risk, with denser areas exhibiting approximately **3% higher** claim frequency  
- **Claim severity** is significantly more variable and less predictable than frequency, consistent with real-world insurance data  

---

## Visualizations

The project includes visualizations of:

- Driver age vs predicted claim frequency  
- BonusMalus vs predicted claim frequency  
- Premium distribution (log scale), showing heavy-tailed risk behavior  

---

## Skills Demonstrated

- Python (pandas, numpy, matplotlib)
- Statistical modeling with **statsmodels**
- Poisson regression and GLMs
- Feature engineering and transformation
- Model evaluation using AIC
- Interpretation of model coefficients
- Gamma regression (severity modeling)
- Data merging across different granularities (policy vs claim level)
- End-to-end insurance pricing pipeline

---

## Appendix

The notebook includes a simulation-based appendix demonstrating how the Poisson GLM recovers known parameters. This was used to validate understanding of the modeling framework.

---

## Project Structure

- `AutoPricingModel.ipynb` – Main notebook with modeling, analysis, and visualizations