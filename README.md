# Motor Trend Car Road Test Analysis in R

This project presents an in-depth analysis of the Motor Trend Car Road Test dataset using R. In this analysis, Ordinary Least Squares (OLS) regression is employed to model the relationship between miles per gallon (mpg) and several predictors. The study evaluates the validity of the OLS assumptions, examines the statistical significance of each variable's contribution, applies backward elimination for variable selection, and uses cross validation to assess model robustness across multiple metrics (including R², AIC, SBIC, etc.).

---

## Data Overview

The dataset consists of motor trend car data with variables such as:
- **mpg**: Miles per gallon (the response variable)
- **cyl, disp, hp, drat, wt, qsec, vs, am, gear, carb**: Predictors describing engine configuration, transmission, and overall car design

This dataset is well-known in automotive analytics and provides a rich context for exploring regression techniques.

---

## Methodology

The analysis is structured into the following key steps:

1. **OLS Regression Modeling**  
   - Fit a full OLS model to predict mpg using all available predictors.
   - Examine the summary output for coefficients, standard errors, t-values, and p-values.
   - Example code:
     ```r
     full_model <- lm(mpg ~ cyl + disp + hp + drat + wt + qsec + vs + am + gear + carb, data = motorData)
     summary(full_model)
     ```
   
2. **Model Validity and Statistical Significance Checks**  
   - Conduct residual diagnostics to verify model assumptions.
   - Evaluate the overall significance of the model using ANOVA.
   - Check the individual p-values to assess the contribution of each predictor.

3. **Backward Elimination for Variable Selection**  
   - Apply backward elimination to remove non-significant predictors.
   - Use a stepwise selection method to refine the model.
   - Example code:
     ```r
     library(olsrr)
     final_model <- ols_step_backward_p(full_model, details = TRUE)
     summary(final_model)
     ```
   - The backward elimination procedure indicated that a reduced model (e.g., including predictors like `disp`, `hp`, `wt`, `qsec`, and `am`) better explains the variation in mpg.

4. **Cross Validation and Model Robustness**  
   - Implement cross validation to evaluate predictive performance.
   - Compare models using metrics such as adjusted R², AIC, SBIC, and R²CP.
   - Example code:
     ```r
     library(caret)
     train_control <- trainControl(method = "cv", number = 5)
     cv_model <- train(mpg ~ disp + hp + wt + qsec + am, data = motorData, method = "lm", trControl = train_control)
     print(cv_model)
     ```
   - This step confirms the robustness of the final model across different metrics (&#8203;:contentReference[oaicite:1]{index=1}).

---

## How to Run the Analysis

1. **Open the HTML Document:**  
   Simply open the `motorTrendCarRoadTest.nb.html` file in your web browser to view the static report.

2. **Reproduce the Analysis in R:**  
   - If you prefer an interactive session, open the corresponding R Markdown (`.Rmd`) file in RStudio.
   - Execute the code chunks sequentially to replicate the full analysis workflow—from data loading and model fitting to validation and cross validation.

---

## Requirements

- **R **
- Required R packages:
  - **olsrr** (for backward elimination and stepwise regression)
  - **caret** (for cross validation and model training)
  - **stats** (for OLS regression via `lm`, built-in in R)
  - **car**, **lmtest**, etc. (for additional diagnostic checks)
  
Install any missing packages using:
```r
install.packages(c("olsrr", "caret", "car", "lmtest"))

