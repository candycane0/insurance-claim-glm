# Insurance Claim Frequency Modeling using Poisson GLM

This project develops a Poisson Generalized Linear Model (GLM) to predict insurance claim frequency using real-world policy data. The goal is to identify key risk drivers and improve model performance through feature engineering and model selection.

---

## Modeling Approach

A Poisson GLM with a log link function was used to model claim counts. Exposure was incorporated as an offset to account for differences in policy duration, allowing claim frequency to be modeled on a per-unit time basis.

Feature engineering was applied to:
- Capture nonlinear relationships (quadratic driver age)
- Handle skewed variables (log-transformed population density)
- Improve both interpretability and model fit

---

## Dataset

This project uses the **French Motor Third-Party Liability Claims dataset (freMTPL2)**, which contains policy-level information on claim counts, exposure, driver characteristics, vehicle attributes, and geographic factors.

- Kaggle source: https://www.kaggle.com/datasets/karansarpal/fremtpl2-french-motor-tpl-insurance-claims  
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

## Results

The final model achieved a reduction of **over 70 AIC points** compared to the baseline model, indicating a significantly improved fit.

Geographic area variables were removed, as they did not improve model performance after accounting for population density.

---

## Key Findings

- **BonusMalus** is the strongest predictor of claim frequency, with each one-unit increase associated with approximately a **2.4% increase** in expected claims  
- **Vehicle age** is negatively associated with claims, with each additional year corresponding to approximately a **4.2% decrease** in claim frequency  
- **Driver age** exhibits a nonlinear relationship with risk, with claim frequency peaking around age 60  
- **Vehicle power** is a significant predictor, with each unit increase associated with approximately a **1.7% increase** in claim frequency  
- **Fuel type** has a discrete effect, with regular fuel vehicles associated with approximately **7% higher** claim frequency than diesel vehicles  
- **Population density** is positively associated with risk, with denser areas exhibiting approximately **3% higher** claim frequency  

---

## Visualizations

The project includes visualizations of predicted claim frequency:

- Driver age vs predicted risk (nonlinear relationship)
- BonusMalus vs predicted risk (strongest driver)

---

## Skills Demonstrated

- Python (pandas, numpy, matplotlib)
- Statistical modeling with **statsmodels**
- Poisson regression and GLMs
- Feature engineering and transformation
- Model evaluation using AIC
- Interpretation of model coefficients

---

## Appendix

The notebook includes a simulation-based appendix demonstrating how the Poisson GLM recovers known parameters. This was used to validate understanding of the modeling framework.

---

## Project Structure

- `AutoPricingModel.ipynb` – Main notebook with modeling, analysis, and visualizations