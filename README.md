# Boston Housing Predictor

This folder contains an R Markdown analysis of the Boston housing dataset. The report investigates which suburb-level characteristics are
most useful for predicting `medv`, the median value of owner-occupied homes in
thousands of dollars.

The main output is a PDF report generated from
`PDF_output_assignment1_boston.Rmd`.

## Project Files

| File | Purpose |
| --- | --- |
| `PDF_output_assignment1_boston.Rmd` | Main R Markdown source file for the final PDF report. |
| `PDF_output_assignment1_boston.pdf` | Rendered PDF output from the R Markdown file. |
| `my_boston.csv` | Training dataset used for the exploratory analysis and model fitting. |
| `boston.csv` | Full Boston housing dataset used to create the held-out test sample. |
| `PDF_output_assignment1_boston.log` | LaTeX/render log produced when building the PDF. |

Other files in the folder contain earlier drafts, generated outputs, helper
scripts, or supporting assignment material.

## Analysis Summary

The report follows a structured modelling workflow:

1. Explore the dataset structure, variable types, distributions, missingness,
   outliers, and correlations.
2. Fit a full multiple linear regression model for `medv`.
3. Evaluate predictive performance on a held-out test set.
4. Improve the model using backward stepwise selection with AIC and BIC.
5. Compare the full, stepwise, Ridge, and LASSO models using 10-fold
   cross-validation RMSE.
6. Add and evaluate interaction terms for the preferred stepwise model.
7. Review residual diagnostics and summarize the final model.

The analysis identifies `lstat`, `rm`, and `ptratio` as important predictors of
median home value, with additional contributions from variables such as `crim`,
`nox`, `dis`, `rad`, and `tax`. Both backward AIC and BIC remove `indus` and
`age`, indicating that these variables add little predictive value after the
other predictors are included.

## Requirements

The report is written in R Markdown and renders to PDF. You need:

- R
- RStudio or another R environment
- A working LaTeX installation, such as TinyTeX, MiKTeX, or TeX Live
- The following R packages:
  - `rmarkdown`
  - `knitr`
  - `kableExtra`
  - `ggplot2`
  - `gridExtra`
  - `broom`
  - `dplyr`
  - `caret`
  - `glmnet`

Install missing R packages with:

```r
install.packages(c(
  "rmarkdown", "knitr", "kableExtra", "ggplot2", "gridExtra",
  "broom", "dplyr", "caret", "glmnet"
))
```

If PDF rendering fails because LaTeX is missing, install TinyTeX from R:

```r
install.packages("tinytex")
tinytex::install_tinytex()
```

## How to Render

Open R in this folder, then run:

```r
rmarkdown::render("PDF_output_assignment1_boston.Rmd")
```

Alternatively, from a terminal in this folder:

```powershell
Rscript -e "rmarkdown::render('PDF_output_assignment1_boston.Rmd')"
```

The R Markdown file expects `my_boston.csv` and `boston.csv` to be available in
the same working directory, so render it from the `Ass_1` folder.

## Reproducibility Notes

- Random sampling and cross-validation steps use `set.seed(1494)`.
- The response variable is `medv`.
- The `chas` variable is converted to a factor with labels `No` and `Yes`.
- Model performance is reported using RMSE, MSE, R-squared, AIC, BIC, and
  10-fold cross-validation metrics.
- The PDF output uses LaTeX packages including `colortbl`, `xcolor`,
  `booktabs`, `float`, and `placeins`.
