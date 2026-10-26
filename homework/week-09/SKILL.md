---
name: svm-analysis
description: Compare SVM models and choose the best settings using cross-validation.
---

Use this skill only when I explicitly ask for it.

Check if there are missing values and whether the response is categorical.
Decide if the data is suitable for SVM.

Compare linear, polynomial and radial kernels.
Linear is a simple baseline, while polynomial and radial can fit nonlinear relationships.

Tune C for all kernels, degree for polynomial, and gamma for radial.
Use C and gamma values spaced by factors of 10 or 100.
State other settings held fixed.

Use the same five folds for all candidates.
Standardize using only training data in each fold and apply the same scaling to validation data.
Choose the model with the lowest mean CV misclassification rate.

Include a compact table showing kernels, parameter settings and mean CV errors.
Include a plot showing how CV error changes with C and gamma.

Report the final kernel, parameters and mean CV error.
Explain the choice and limitations.
Keep the report within one printed page at 11-point font.
