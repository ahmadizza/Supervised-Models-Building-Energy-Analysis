
# **Building Energy Consumption Analysis Using Supervised Learning**

## **Overview**

This project performs a supervised learning analysis on building-level energy consumption data. The goal is to explore structural and environmental factors that influence energy usage and to build interpretable models that support energy-efficiency decision-making. The work includes preprocessing, exploratory data analysis (EDA), regression modeling with Decision Trees, model evaluation, regularization, cross-validation, and insights for real-world energy management.

---

## **Business Objective**

Evaluating energy efficiency improvements is challenging because it is impossible to observe the true counterfactual: how much energy a building would have consumed without the upgrade. The closest approach is to build a counterfactual prediction model.

After retrofitting, the new (reduced) energy consumption is compared with the model-estimated baseline for the original building. More accurate models support better market incentives and enable lower-cost financing for energy-efficiency projects.

The purpose of this study is not to achieve the most accurate model, but to gain meaningful insights and produce an interpretable model.

---

## **Technical Objective**

The dataset represents average (non–time-series) electricity consumption for various buildings. The objectives are:

* Perform complete Data Mining processes using appropriate methods.
* Identify as many non-trivial insights as possible.
* Obtain an optimal and interpretable model (not necessarily the most accurate).
* Understand how building characteristics and environmental factors affect energy usage.

---

## **Data Description**

The dataset includes the following features:

* **building_id**: Unique building identifier.
* **meter_reading**: Target variable; energy consumption in kWh or equivalent (site 0 uses kBTU).
* **primary_use**: Main function of the building (EnergyStar categories).
* **square_feet**: Gross floor area.
* **year_built**: Year the building was constructed.
* **floor_count**: Number of floors.
* **air_temperature**: Outdoor temperature (°C).
* **cloud_coverage**: Cloudiness (oktas).
* **dew_temperature**: Dew point temperature (°C).
* **precip_depth_1_hr**: Hourly precipitation (mm).
* **sea_level_pressure**: Atmospheric pressure (mbar/hPa).
* **wind_direction**: Wind direction (0°–360°).
* **wind_speed**: Wind speed (m/s).

---

## **Preprocessing**

Standard preprocessing steps were performed, including handling missing values, formatting numeric variables, removing erroneous entries, and preparing data for EDA and modeling. Methods are consistent with previous projects.

---

## **Exploratory Data Analysis (EDA)**

### **Average Meter Reading by Temperature Category**

* Lowest energy consumption occurs at **mild temperatures (10°C–20°C)**.
* Consumption increases significantly in **cold (0°C–10°C)** and **warm (20°C–30°C)** ranges due to heating and cooling demands.
* No data in extreme ranges (< 0°C or > 30°C), suggesting the dataset represents moderate climates.

### **Meter Reading by Primary Use Category**

* **Healthcare** buildings have the highest energy consumption.
* **Religious worship** buildings have the lowest.
* Energy allocation strategies should prioritize sectors with high operational demand.

### **Correlation Heatmap Insights**

* **wind_speed vs wind_direction**: Strong positive correlation (0.84).
* **wind_direction vs air_temperature**: Strong negative correlation (-0.76).
* **wind_speed vs air_temperature**: Strong negative correlation (-0.60).
  These indicate atmospheric pattern tendencies, not causation.

---

## **Modeling: Decision Tree Regressor**

### **Model 1: Baseline Decision Tree**

**R² Score**

* Train: 0.6465
* Test: 0.3379

**MAE**

* Train: 36.16
* Test: 51.27

**MSE**

* Train: 3005.33
* Test: 6099.66

**Conclusion**: Strong overfitting. A large gap between train and test metrics indicates poor generalization.

---

## **Model 2: Decision Tree with Hyperparameter Tuning**

Grid search was applied to find the optimal combination of parameters.

**R² Score**

* Train: 0.4895
* Test: 0.3380

**MAE**

* Train: 46.17
* Test: 51.87

**MSE**

* Train: 4340.33
* Test: 6099.45

**Conclusion**: Regularization reduced overfitting. Differences between training and test metrics are smaller and more stable.

---

## **Cross-Validation**

* Cross-validation MAE: **59.07**
* Higher than train/test MAE, indicating mild overfitting and that the model may not generalize perfectly to unseen data.
* Nevertheless, performance remains acceptable for an interpretable baseline model.

---

## **Feature Importance**

* **square_feet (83.05%)**: Primary predictor. Larger buildings consume more energy.
* **dew_temperature (14.45%)**: Influences humidity-related HVAC usage.
* **sea_level_pressure (2.49%)**: Minor atmospheric influence.
* Other environmental features contribute negligibly, indicating low impact on average energy consumption.

---

## **Insights and Recommendations**

### Key Insights:

* Building size overwhelmingly determines energy usage.
* Dew point temperature affects HVAC load.
* Atmospheric conditions have limited influence.

### Recommendations:

* Focus energy optimization strategies on large buildings.
* Improve humidity and temperature control systems to reduce dew point sensitivity.
* Environmental variables like cloud coverage and wind do not need prioritized monitoring for average energy usage modeling.

---

## **Decision Tree Visualization Interpretation**

* The root node consistently splits by **square_feet**, confirming its dominant importance.
* Secondary splits involve **dew_temperature** (smaller buildings) and **sea_level_pressure** (larger buildings), showing environmental effects depend on building size.

---

## **Residual Analysis**

* Residuals center around zero → no strong bias.
* Some large errors on high meter readings → potential outliers or unmodeled nonlinear effects.

---

## **Learning Curve Analysis**

* Training error increases as more data is added.
* Validation error decreases then stabilizes.
* Curve pattern indicates mild overfitting but acceptable performance for a tree-based model.

---

## **Conclusion**

This project demonstrates how building structure, particularly **square_feet**, is the most influential factor in energy consumption. Decision Trees provide interpretability and reasonable performance after tuning. The model is suitable for generating insights and supporting energy management strategies rather than achieving state-of-the-art accuracy.

---

