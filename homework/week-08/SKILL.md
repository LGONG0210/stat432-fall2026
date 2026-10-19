---
name: lda-qda-analysis
description: When explicitly supplied by the user, compare LDA and QDA classifiers using training-only cross-validation and produce a one-page statistical report.
---

# LDA/QDA analysis

## Invocation and inputs

Keep this file outside automatically loaded skill folders. Apply it only when the user explicitly asks to use this file. Obtain the dataset, response, predictor list, coding instructions, and any split constraints from the invocation; do not hard-code a dataset or its results.

## Agent behavior

Use R unless the user requests another language. Execute the analysis and verify numerical results. Preserve the requested predictor coding. Ask for missing information only when it prevents a valid analysis. Explain findings in plain language and avoid claiming a model is best beyond the candidates evaluated.

## Analysis guidelines

1. Inspect class counts, missing values, predictor types, and dimensions. Record coding decisions and report any exclusions. Use a fixed random seed and report it.
2. Reserve a stratified 20% test set before model comparison, unless the user supplies another valid split. Keep test outcomes out of all preprocessing, model selection, and skill revisions. Adjust split and fold counts if class sizes require it, and explain why.
3. Compare ordinary LDA and ordinary QDA using the same numerical predictors and empirical training priors. Optional candidates may use PCA before LDA or QDA, or a weighted average of their posterior probabilities. All classifiers must remain based on LDA, QDA, or their combination. Specify a modest candidate grid before evaluation.
4. Use the same stratified five-fold cross-validation splits within the training set for every candidate. Fit means, priors, covariances, imputation, scaling, PCA, and any other learned preprocessing using only each fold's training observations; apply those fitted transformations to its validation observations. Select PCA dimensions or probability-blending weights only through this cross-validation.
5. Classify by the largest posterior probability, using a consistent tie rule. Compare candidates by total validation mistakes divided by total validation observations. Report cross-validation misclassification rates. Select the lowest-error valid candidate; prefer the simpler candidate in an exact tie.
6. Check for constant predictors, linear dependence, and singular class covariance matrices. Having more observations than predictors does not guarantee invertibility. Record failed fits and their causes; do not silently substitute a regularized model or omit failed folds from an average. Treat a candidate that fails in any fold as invalid.
7. Make any model or skill revisions using training and cross-validation results only. Freeze the selected configuration, refit it and its preprocessing on all training observations, then evaluate that selected classifier once on the reserved test set. Do not revise the model after seeing test results.

## Required report

Produce a readable analysis report of at most one printed page, containing all of the following:

- Setup: response, predictors and coding, sample and class counts, train/test sizes, seed, and any exclusions.
- Methods: candidate models, covariance assumptions, preprocessing, shared cross-validation folds, and selection rule.
- One compact table: candidate settings, cross-validation misclassification rates, fit failures if present, and the selected model clearly marked.
- One labeled figure: compare candidates' cross-validation misclassification rates; identify the selected candidate and display rates as percentages.
- Final numerical results: selected model, number of predictors or retained components, test mistakes and test sample size, and test misclassification rate.
- Interpretation: explain the main comparison using covariance assumptions and the bias-variance trade-off. Describe limitations, including sample size, model assumptions, and uncertainty from a single test split.

Keep executable code and supplementary output outside the one-page report. Render the report and inspect its page count and readability; shorten content without shrinking text to an unreadable size. Deliver reproducible code separately. Distinguish cross-validation results used for selection from the final test result.
