# Assignment 04 Interpretation Memo

**Student Name:** Sam Weber
**Date:** 02/11/2026
**Assignment:** REIT Annual Returns and Predictors (Simple Linear Regression)

---

## 1. Regression Overview

You estimated **three** simple OLS regressions of REIT *annual* returns on different predictors:

| Model | Y Variable | X Variable | Interpretation Focus |
|-------|------------|------------|----------------------|
| 1 | ret (annual) | div12m_me | Dividend yield |
| 2 | ret (annual) | prime_rate | Interest rate sensitivity |
| 3 | ret (annual) | ffo_at_reit | FFO to assets (fundamental performance) |

For each model, summarize the key results in the sections below.

---

## 2. Coefficient Comparison (All Three Regressions)

**Model 1: ret ~ div12m_me**
- Intercept (β₀): [0.108196] (SE: [0.005987], p-value: [0.0000])
- Slope (β₁): [-0.068682] (SE: [0.032495], p-value: [0.0346])
- R²: [0.0018] | N: [2527]

**Model 2: ret ~ prime_rate**
- Intercept (β₀): [0.199799] (SE: [0.015764], p-value: [0.0000])
- Slope (β₁): [-0.019449] (SE: [0.002998], p-value: [0.0000])
- R²: [0.0164] | N: [2527]

**Model 3: ret ~ ffo_at_reit**
- Intercept (β₀): [0.097273] (SE: [0.009194], p-value: [0.0000])
- Slope (β₁): [0.577042] (SE: [0.567462], p-value: [0.3093])
- R²: [0.0004] | N: [2518]

*Note: Model 3 may have fewer observations if ffo_at_reit has missing values; statsmodels drops those rows.*

---

## 3. Slope Interpretation (Economic Units)

**Dividend Yield (div12m_me):**
- A 1 percentage point increase in dividend yield (12-month dividends / market equity) is associated with a -0.068682 change in annual return.
> According to this data, a higher dividend yield is associated with very slightly lower returns. This makes sense because, in general, high-growth firms offer less dividends than more stable firms.

**Prime Loan Rate (prime_rate):**
- A 1 percentage point increase in the year-end prime rate is associated with a -0.019449 change in annual return.
> The evidence suggests that the year-end prime rate is very slightly associated with annual returns. Higher interest rates generally lead to slightly lower returns.

**FFO to Assets (ffo_at_reit):**
- A 1 unit increase in FFO/Assets (fundamental performance) is associated with a 0.577042 change in annual return.
> The data does not support any correlation between REIT profitability and REIT returns. While the regression slope was slightly positive, a p-value of 0.3093 means that this is not significant at the 5% level.

---

## 4. Statistical Significance

For each slope, at the 5% significance level:
- **div12m_me:** Significant — A p-value of 0.0346 means that this slope is significant at the 5% level. This suggests that higher dividend REITs do generally have slightly lower returns.
- **prime_rate:** Significant — A p-value of 0.0000 means that this slope is significant at the 5% level. This suggests that higher interest rates do generally lead to slightly lower returns. 
- **ffo_at_reit:** Not significant — A p-value of 0.3093 means that this slope is not significant at the 5% level. This means that we cannot accurately discern a relationship between REIT profitability and returns from this data.

**Which predictor has the strongest statistical evidence of a relationship with annual returns?** Prime Loan Rate

---

## 5. Model Fit (R-squared)

Compare R² across the three models:
> The predictor with the highest R² was the Prime Loan Rate, which explained 1.6% of the variation in annual returns. Dividend Yield explained 0.18% and FFO to Assets explained 0.04% of the variation. In general, R²s for single predictors in economics tend to be low. This suggests that many different and independent factors drive REIT returns. In this case, 1.6% of the variation is explained by Prime Loan Rate, meaning the other 98.4% of variation is explained by factors not studied in this analysis.

---

## 6. Omitted Variables

By using only one predictor at a time, we might be omitting:
> REIT Size: Larger REITs are generally more diverse, meaning they likely provide more stability but less growth potential than smaller REITs. This difference could affect average returns

> Liquidity: REITs with more liquidity generally have quicker access to capital which could provide them with an advantage that translates to higher returns. Illiquid REITs might miss investment opportunities or be forced to sell at inopportune times due to their lack of quick access to capital.

> Risk: REITS with more risk will generally have more volatile returns. This volatility could potentially affect their average returns. Generally, REITs that take on more risk will have a higher revenue ceiling (and a lower revenue floor) than those playing it safe.

**Potential bias:** If omitted variables are correlated with both the X variable and ret, our slope estimates may be biased.
> For example, if larger firms are more likely to pay dividends and larger firms are more likely to have lower returns, our slope estimate might bias us into believing that dividends and returns are directly correlated with eachother instead of both being correlated with firm size. While this is not something that it is possible to entirely prevent (you can't analyze every single factor), it is something we can be aware of and think critically about.

---

## 7. Summary and Next Steps

**Key Takeaway:**
[2-3 sentences summarizing which predictor(s) show the strongest relationship with REIT annual returns and whether the evidence is consistent with economic theory]
> The predictor with the strongest relationship with REIT annual returns was Prime Loan Rate, with a slope of -0.019449, a p-value of 0.0000, and an R² of 0.0164. This evidence is consistent with economic theory in that higher interest rates generally lead to more competitive bonds, which generally leads to capital rotation out of REITs. Additionally, lower interest rates mean that REIT firms pay less in interest and thus have more capital for investments.

**What we would do next:**
- Extend to multiple regression (include two or more predictors)
- Test for heteroskedasticity and other OLS assumption violations
- Examine whether relationships vary by time period or REIT sector

---

## Reproducibility Checklist
- [YES] Script runs end-to-end without errors
- [YES] Regression output saved to `Results/regression_div12m_me.txt`, `regression_prime_rate.txt`, `regression_ffo_at_reit.txt`
- [YES] Scatter plots saved to `Results/scatter_div12m_me.png`, `scatter_prime_rate.png`, `scatter_ffo_at_reit.png`
- [YES] Report accurately reflects regression results
- [YES] All interpretations are in economic units (not just statistical jargon)
