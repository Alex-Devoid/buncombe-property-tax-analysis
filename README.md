## Overview

This analysis aims to explore the potential relationship between unpaid property bills and gentrification in Buncombe County, with a focus on single-family homes. Specifically, it examines unpaid property bills from two perspectives:

- The rates of unpaid property bills among home-valuation quintiles and deciles.
- A logistics regression that looks for correlation between unpaid property bills and rising home valuations, among other factors, in different housing-valuation quintiles.

In addition to the README, the [Jupyter Notebook](unpaid_property_bills_analysis.ipynb) in this repositry contains comments on my methodology. 
## Highlighted Preliminary Findings

- The rates of unpaid property bills in 2022 were higher among groups with lower housing valuations.
- In the lowest housing-valuation decile, rates of unpaid property bills in 2022 were roughly three times higher than in the decile with the highst valuations.
## Rates of Unpaid Property Bills

Urban3 has already shown that homes in the bottom quintiles have experienced a sharper rise in valuations, likely contributing to gentrification. 

My analysis builds on this, by showing that the bottom quintiles are also shouldering more of the unpaid property bills, with higher rates of unpaid property bills across lower housing-valuation quintiles and deciles.

![quintiles](images/unpaid_property_bill_quintile_rates.png)
![deciles](images/unpaid_property_bill_decile_rates.png)

It should be noted that this analysis was conducted independently from Urban3's research and therefore the methodology may be different. Any comparisons or extrapolations should be made with caution.
## What factors lead to unpaid property bills?

Does a higher percent change in property value increase the probability of an unpaid bill? So far I haven't found a statistically significant relationship between the percent change of a home’s taxable value and the likelihood of the owner having an unpaid bill.

Further research is needed to fully understand the relationship between unpaid property bills and gentrification in Buncombe County.

However, unpaid bills could be an early-stage symptom of gentrification, as it becomes more expensive to pay taxes on homes.

I ran a logistic regression aimed at identifying the factors that influence the likelihood of a property owner having an unpaid bill. The dependent variable, `unpaid_bill`, is a binary variable indicating whether or not a property owner had an unpaid bill in 2022.

The independent variables include `total_value_pct_change`, `median_hh_income`, `income_gini`, `pct_white`, `pct_bachelor`, and `pct_rented`.  

The `total_value_pct_change` variable represents the percent change in taxable real estate value for a single-family home in Buncombe County from 2020 to 2021.

The remaining variables I pulled or calculated from the 2021 American Community Survey at the Census Tract level. The `median_hh_income` variable represents the median household income. The `income_gini` variable represents the Gini coefficient of income inequality. The `pct_white` variable represents the percent of the population that is white in a given tract. The `pct_bachelor` variable represents the percent of the population with a bachelor's degree in a given tract. The `pct_rented` variable represents the percent of the housing units that are rented in a given tract.

The results of the logistic regression suggest that there are several independent variables that are significantly associated with the likelihood of a property owner having an unpaid bill, however these results are only preliminary and more research is needed to fully understand these relationships. 

With that said, the results of this logistic regression suggest that higher median household income and a higher percentage of properties being rented are associated with a lower likelihood of a property owner having an unpaid bill, while a higher percentage of the population being white and having a bachelor's degree or higher are associated with a higher likelihood of a property owner having an unpaid bill.

The variables `total_value_pct_change` and `income_gini` are not statistically significant in their relationship with the likelihood of a property owner having an unpaid bill. 

 Logit Regression Results                           
==============================================================================
Dep. Variable:            unpaid_bill   No. Observations:                81885
Model:                          Logit   Df Residuals:                    81878
Method:                           MLE   Df Model:                            6
Date:                Mon, 30 Jan 2023   Pseudo R-squ.:                  0.1830
Time:                        02:20:23   Log-Likelihood:                -38052.
converged:                       True   LL-Null:                       -46574.
Covariance Type:            nonrobust   LLR p-value:                     0.000
==========================================================================================
                             coef    std err          z      P>|z|      [0.025      0.975]
------------------------------------------------------------------------------------------
const                     -2.7929      0.226    -12.353      0.000      -3.236      -2.350
total_value_pct_change  8.989e-05   9.59e-05      0.937      0.349    -9.8e-05       0.000
median_hh_income       -7.161e-05   1.07e-06    -66.865      0.000   -7.37e-05   -6.95e-05
income_gini               -0.2214      0.182     -1.218      0.223      -0.578       0.135
pct_white                  0.0760      0.002     38.660      0.000       0.072       0.080
pct_bachelor               0.4777      0.013     36.866      0.000       0.452       0.503
pct_rented                -0.0601      0.001    -58.163      0.000      -0.062      -0.058
==========================================================================================

