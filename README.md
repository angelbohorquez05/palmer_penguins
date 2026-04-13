# Palmer Penguins — Statistical Models

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)

Exploratory data analysis and statistical inference on the [Palmer Penguins dataset](https://allisonhorst.github.io/palmerpenguins/), covering 333 penguins from three species in the Palmer Archipelago, Antarctica.

## Project Structure

```
palmer-penguins/
├── palmer_penguins_statistical_models.ipynb
├── penguins.csv
└── README.md
```

## Methodology

All tests are parametric. Normality was verified with Shapiro-Wilk stratified by species and sex before running any inference — the two variables used as dependent variables (body mass and flipper length) passed in all subgroups. Where three groups are compared, ANOVA is used instead of multiple t-tests to control the family-wise error rate, followed by Tukey HSD for pairwise post-hoc comparisons. The logistic regression uses only two predictors to avoid quasi-perfect separation, which would make coefficients numerically unstable. A global significance level of α = 0.05 is applied throughout.

## Contents

| Notebook section | Method |
|---|---|
| Exploratory Data Analysis | Descriptive statistics, KDE plots, scatter plots |
| Normality testing | Shapiro-Wilk, Q-Q plots |
| Confidence intervals | t-Student 95% CI by species and sex |
| Species-island association | Pearson chi-square |
| Island effect on body mass | One-way ANOVA, Levene's test, Tukey HSD |
| Simpson's Paradox | Pearson correlation, stratified vs. aggregated |
| Species classification | Logistic regression, ROC curve, confusion matrix |

## Dataset

File: `penguins.csv`

| Variable | Type | Description |
|---|---|---|
| `bill_length_mm` | continuous | Bill length (mm) |
| `bill_depth_mm` | continuous | Bill depth (mm) |
| `flipper_length_mm` | continuous | Flipper length (mm) |
| `body_mass_g` | continuous | Body mass (g) |
| `species` | categorical | Adélie, Chinstrap, Gentoo |
| `island` | categorical | Biscoe, Dream, Torgersen |

9 rows with missing sex values are dropped on load, leaving 333 complete observations.

## Requirements

```
numpy
pandas
matplotlib
seaborn
scipy
statsmodels
scikit-learn
```

Install with:

```bash
pip install numpy pandas matplotlib seaborn scipy statsmodels scikit-learn
```

## Usage

Place `penguins.csv` in the same directory as the notebook and run all cells in order.

## Key Findings

- Gentoo penguins are significantly heavier (~5,092 g mean) and have longer flippers than Adélie and Chinstrap, which are morphologically similar to each other.
- Species and island are strongly associated (chi-square p ~ 0), but island has no measurable effect on Adélie body mass (ANOVA p = 0.995).
- Bill length and bill depth show a negative global correlation (r = -0.23) that reverses to positive within each species — a textbook case of Simpson's Paradox.
- A logistic regression using only flipper length and bill depth achieves perfect classification of Gentoo vs. non-Gentoo on the test set (AUC = 1.000).

## Reference

Horst A.M., Hill A.P., Gorman K.B. (2020). *palmerpenguins: Palmer Archipelago (Antarctica) penguin data.* R package version 0.1.0.
