# Exploring Gender Pay Gaps in the United States

![R](https://img.shields.io/badge/R-276DC3?logo=r&logoColor=white) ![tidyverse](https://img.shields.io/badge/tidyverse-1A162D?logo=tidyverse&logoColor=white) ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white) ![Hypothesis Testing](https://img.shields.io/badge/Hypothesis%20Testing-z--test-4B8BBE) ![Bootstrapping](https://img.shields.io/badge/Bootstrapping-95%25%20CI-2E8B57)

A statistical inference study testing whether women are underrepresented in higher-paying jobs, using U.S. Census income data.

**Result:** 32.1% of men earned over $50,000, compared with 11.5% of women, a gap of **20.7 percentage points** (95% CI: 19.7 to 21.6). The gap held in every job sector tested.

## Question
Are women less likely than men to hold jobs paying more than $50,000 a year?

## Data
[Census Income (Adult) dataset](https://archive.ics.uci.edu/dataset/2/adult) from the UCI Machine Learning Repository, based on the 1994 U.S. Census: 32,561 records with education, occupation, work class, gender and income.

The analysis keeps U.S. workers only, since the dataset includes several countries at very different stages of economic development. That leaves 27,511 workers: 18,577 men and 8,934 women.

Income is only recorded as **$50K or less** or **more than $50K**, so the analysis compares the proportion of men and women in the higher bracket.

## Method
1. **Exploratory analysis:** compared income brackets for men and women across work classes (government, private, self-employed, no income).
2. **Confidence interval:** estimated the difference in proportions earning over $50K, with a 95% confidence interval built two ways:
   - using the Central Limit Theorem, after checking that the sampling distributions were approximately normal
   - using bootstrapping, to confirm the CLT result without relying on its assumptions
3. **Hypothesis test:** one-sided two-sample z-test.
   - H₀: the proportion of men and women earning over $50K is the same
   - Hₐ: a higher proportion of men than women earn over $50K
4. **Checking for confounding:** repeated the test within each work class, since job sector could explain part of the gap.

## Results

| | Men | Women |
|---|---|---|
| Workers | 18,577 | 8,934 |
| Earning over $50K | 32.1% | 11.5% |

| Estimate | Value |
|---|---|
| Difference in proportions | 20.7 percentage points |
| 95% CI (CLT) | 19.7 to 21.6 points |
| 95% CI (bootstrap) | 19.7 to 21.6 points |
| z statistic | 36.9 |
| p-value | < 0.001 |

The CLT and bootstrap intervals agree almost exactly, and the null hypothesis is rejected at the 5% level.

### By work class

| Work class | Men over $50K | Women over $50K | Gap | z |
|---|---|---|---|---|
| Private | 29.4% | 9.6% | 19.8 points | 31.9 |
| Government | 39.0% | 16.7% | 22.2 points | 14.9 |
| Self-employed | 39.2% | 22.6% | 16.6 points | 6.9 |

The gap is significant in every sector (all p < 0.001), so it isn't explained by men and women working in different types of jobs.

## Limitations
- **Income is only two categories.** "Over $50K" covers everyone from $50,001 to millions, so this measures a gap in access to higher-paying jobs, not the full size of the pay gap.
- **The data is from 1994.** The gap has narrowed since then, so the numbers describe that period, not today.
- **This is observational data.** The analysis shows a gap exists but doesn't explain why. Education, occupation, hours worked and experience could all play a part, and only work class was checked.

## How to run
The analysis is in `project_18.ipynb`, written in R. The dataset (`adult.data`) is included in the repository.

You need R, Jupyter and the R kernel for Jupyter (IRkernel). Install the packages from R:

    install.packages(c("tidyverse", "infer", "broom", "cowplot", "gridExtra", "repr"))

Then open the notebook in Jupyter and run all cells.

## Authors
Shahrukh Islam Prithibi, Anne Nguyen, Chuxuan Zhou

Built as a group project for STAT 201 (Statistical Inference for Data Science) at the University of British Columbia, 2023.

## References
- Kochhar, R. (2023). *The enduring grip of the gender pay gap.* Pew Research Center. https://www.pewresearch.org/social-trends/2023/03/01/the-enduring-grip-of-the-gender-pay-gap/
- Kohavi, R., & Becker, B. (1996). *Adult* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5XW20
- United Nations (2017). *Policy Brief #53: Reflection on development policy in the 1970s and 1980s.* UN Department of Economic and Social Affairs.
