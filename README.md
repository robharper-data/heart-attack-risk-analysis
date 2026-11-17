# Heart attack risk: a statistical analysis in R

Do age and sex affect heart attack risk? This project explores a public heart disease dataset with descriptive statistics and visualisation, then tests two hypotheses: whether risk differs between men and women, and whether it is associated with age group.

Written in R Markdown as a slide presentation. Completed in 2024 during my Master of Data Science at RMIT University.

## Data

[Heart Attack Prediction](https://www.kaggle.com/datasets/juledz/heart-attack-prediction) on Kaggle: 1,025 records and 14 clinical and demographic variables, derived from the 1988 heart disease databases from Cleveland, Hungary, Switzerland and Long Beach. The `target` variable is a heart attack risk score between 0 and 1.

The data is not included in this repository. Download `heart.csv` from the link above and place it in a `data` folder beside the R Markdown file.

## Method

- **Preparation:** variables converted to appropriate types and factor labels; age grouped into ten-year bands; risk recoded into a binary variable and three risk levels.
- **Descriptive statistics:** summary tables for age, cholesterol and resting blood pressure by sex, with boxplots, bar charts and scatter plots built in ggplot2.
- **Two-sample t-test:** mean risk score compared between men and women. Levene's test showed unequal variances, so Welch's t-test was used.
- **Chi-square test of association:** age group against low or high risk.

## Findings

- Women had a higher mean risk score than men (0.656 against 0.484). The difference was statistically significant: t(668.69) = 9.67, p < .001, 95% CI for the difference [0.137, 0.206].
- Risk was significantly associated with age group (chi-square test, p < .05).
- Cholesterol tended to rise with age, though the correlation was weak.
- Resting blood pressure was distributed similarly in men and women.

## Limitations

These matter more than the findings, and the result for sex should not be read as a clinical conclusion.

- **The result for women contradicts the evidence.** Population data consistently shows men at higher risk of heart attack. The pattern here reflects who is in this dataset, not the general population.
- **The records are not independent.** The file has 1,025 rows but only 302 distinct sets of patient measurements, so most rows repeat the same patients. The tests treat every row as a separate person, which overstates the sample size and the significance of both results.
- **The data is old and narrow.** It was collected in 1988 from four centres and includes 713 men and 312 women.
- **The risk score is not a clinical outcome.** It is a derived variable in this version of the dataset, clustered into low and high values.

## Running it

Requires R with `ggplot2`, `dplyr`, `knitr`, `readr`, `car`, `gridExtra` and `kableExtra`, plus a LaTeX installation for the PDF slides.

```
rmarkdown::render("heart_attack_risk_analysis.Rmd")
```

The illustrative images used in the original slides are not included because they are not mine to redistribute.
