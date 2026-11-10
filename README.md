# econ3916-lab15-bias-variance

# The Bias-Variance Tradeoff: Choosing How Flexible a Model Should Be

## Objective
I used a simulated world with a known true curve to show how polynomial degree trades bias against variance, and to compare ways of choosing the degree.

## Methodology
- Split the error of polynomial fits into bias squared and variance, using 200 fresh samples at each of six degrees.
- Compared training error with error on 2,000 new points for degrees 1 to 15, and found the degree with the lowest held-out error.
- Chose a degree by 5-fold cross-validation and looked at how much the error varied from fold to fold.
- Used nested cross-validation to check whether the smallest CV error is a fair estimate of the error on new data.
- Wrote a function, `kfold_mse()`, that gives the k-fold CV error for any degree and number of folds, and used it to run 10-fold CV.
- Take-home challenge: fit a degree-40 polynomial, then fit minimum-norm models far past the point where the coefficients outnumber the 60 training points, and plotted training and held-out error on a log axis.

## Key Findings
- Variance was 0.0180 at degree 5 and 0.0994 at degree 15. Bias squared was already near zero by degree 5, so the extra flexibility mostly added variance.
- Training error fell with every added degree. Held-out error was lowest at degree 5.
- 5-fold CV chose degree 4 with a CV MSE of 0.1401. The spread across folds was small at degrees 4 and 5 (0.02 to 0.03) and 0.10 or more at the other degrees.
- The nested CV estimate was 0.2070, higher than the smallest CV error of 0.1401. The smallest CV error is optimistic because it is the minimum over several candidate degrees scored on the same folds. The degrees chosen in the five outer folds were 8, 8, 4, 4 and 6.
- 10-fold CV MSE was 0.1409 for degree 4 and 0.1457 for degree 5. Degree 4 has the lower error under both 5-fold and 10-fold CV, so the ranking did not change.
- Held-out error past the interpolation point: it spiked by more than 20 orders of magnitude near degree 60, where the number of coefficients equals the number of points. It then fell and levelled off as the degree grew, while training error stayed near zero. The plateau was still well above the error of a well-chosen low degree such as 4 or 5.
