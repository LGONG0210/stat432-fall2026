---
id: w05-lugong2-knn-candidate-search
title: "Choosing candidate k values for KNN"
author: lugong2
---

When tuning KNN with cross-validation, we first need to decide which candidate values of $k$ to evaluate. Testing every integer provides finer coverage within a chosen range, while using larger gaps reduces the number of candidates but may skip better-performing values. However, searching a narrow range very carefully could still miss useful values outside that range. How should we choose the range, spacing, and number of candidate $k$ values to balance search coverage and computational cost?
