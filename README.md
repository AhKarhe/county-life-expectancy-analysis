# Regression Analysis of County-Level Life Expectancy in the United States

A project exploring which socioeconomic, behavioral, environmental, and health-related factors drive life expectancy at the county level, using the **County Health Rankings** dataset.

**Final model**: multiple linear regression with 10 predictors — **adjusted R² = 0.792**, test RMSE = 1.876 years.

## Project Overview

Using ~1,150 U.S. counties and 15 candidate predictors, the project walks through a complete regression workflow:

1. **Exploratory Data Analysis** — marginal correlations, a correlation heatmap of all predictors, density plots for skewness checks, and scatter plots for nonlinearity screening
2. **Model Building** — multiple linear regression with backward elimination (dropping unemployment, PM2.5, primary care physicians, homeownership, and gender pay gap) plus removal of three highly influential outliers
3. **Diagnostics** — leverage and Bonferroni-adjusted studentized residual outlier checks, Cook's distance, Shapiro–Wilk normality test, Rain test for linearity, Breusch–Pagan test for heteroscedasticity (addressed via HC2 robust standard errors), and VIF for collinearity
4. **Model Comparison** — the final model is compared against a lasso-selected model (10-fold CV RMSE, adjusted R², AIC, BIC, test RMSE) and a random forest

### Key Findings

- **Diabetes prevalence, median income, severe housing cost burden, food insecurity, and income inequality** are the most important predictors
- The linear model is competitive with flexible methods: it slightly beats lasso on every criterion and is nearly matched by random forest (best CV RMSE 1.32 vs. 1.41), supporting the linearity assumption
- Inference is based on **HC2 robust standard errors** due to heteroscedasticity

## Repository Contents

| File | Description |
|---|---|
| `Regression Analysis of County-Level Life Expectancy in the United States.Rmd` | Full analysis in R Markdown (reproducible report) |
| `Regression-Analysis-of-County-Level-Life-Expectancy-in-the-United-States.pdf` | Knitted PDF report |
| `County_Health_Rankings_county_level_data.csv` | Raw data (County Health Rankings) |
| `data Analysis.Rproj` | RStudio project file |

## Reproducing the Analysis

**Requirements**: R (≥ 4.0) with packages `tidyverse`, `lmtest`, `caret`, `glmnet`, `leaps`, `MASS`, `faraway`, `patchwork`, `sandwich`, `randomForest`, `rmarkdown` (with a LaTeX distribution such as TinyTeX for PDF output).

```r
# from the repository root
rmarkdown::render("Regression Analysis of County-Level Life Expectancy in the United States.Rmd",
                  output_format = "pdf_document")
```

## Data Source

[County Health Rankings & Roadmaps](https://www.countyhealthrankings.org/) — county-level health and socioeconomic indicators for U.S. counties.

## Disclaimer

This is a course project completed for educational purposes. The analysis is not medical advice.
