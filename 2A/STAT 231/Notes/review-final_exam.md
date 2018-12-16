__STAT 231 |__ Final Study Guide

# Final Study Guide

### 1. Review Notes

- [x] Empirical Studies (Sections ==1.1, 1.2==)
- [x] Numerical Summaries (Section ==1.3==)
- [x] Graphical Summaries (Section ==1.3==)
- [x] Data Analysis and Statistical Models (Sections ==1.4, 1.5, 2.1==)
- [x] Check the Fit of a Model (Section ==2.6==)
- [x] PPDAC (Chapter ==3==)
- [x] Estimation and Sampling Distributions (Sections ==4.1, 4.2==)
- [x] Likelihood Intervals (Section ==4.3==)
- [x] Confidence Intervals (Section ==4.4==)
- [x] Chi-squared and $t$ Distributions (Section ==4.5==)
- [x] Likelihood-based confidence intervals (Section ==4.6==)
- [x] Confidence Intervals for Parameters in the $G(\mu, \sigma)$ model (Section ==4.8==)
- [x] Hypothesis testing (Section ==5.1==)
- [x] Hypothesis testing for Parameters in the $G(\mu, \sigma)$ model (section ==5.2==)
- [x] Likelihood ratio tests (Section ==5.3==)
- [x] Gaussian Response Models (Sections ==6.1, 6.2==)
- [x] Comparing Means of Two Populations (Section ==6.3==)
- [x] Multinomial Models (Chapter ==7==)
- [x] Cause and Effect (Chapter ==8==)



### 2. Do Questions

- [ ] Finding relative risk
- [ ] *Finding sample correlation?*
- [ ] Find likelihood and log likelihood functions of a random variable
- [ ] Find ml estimate of random variables from different distributions
- [ ] Find relative likelihood functions of a random variable
- [ ] Use invariance property to find another property from the estimated property
- [ ] Calculate expected frequencies from a ml estimate
- [ ] Find correlation in scatterplot
- [ ] Answer PPDAC problems
  - type of problems
- [ ] Finding likelihood intervals from relative likelihood f'n and $log$ one
  - usually look at a graph to find intersection
- [ ] Finding confidence intervals 
- [ ] Finding confidence intervals using pivotal quantities
- [ ] Finding approximate pivotal quantities for  confidence intervals
- [ ] Know the difference between confidence and likelihood intervals (4.4)
  - ![image-20181211111936197](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/final_study_guide.assets/image-20181211111936197-4545176.png)
- [ ] Calculating minimum sample size required
- [ ] Converting between confidence and likelihood intervals
- [ ] finding confidence interval in Gaussian with unknown $\mu, \sigma$ for: `HIGH`
  - [ ] $\mu$ 
  - [ ] $\sigma^2$ 
- [ ] finding sample size for Gaussian with known $\sigma$ or estimated $\sigma$ by $s$ `HIGH`
- [ ] testing hypotheses of different distributions
  - [ ] tessting hypothesis of binomial through Normal approximation of Binomial
- [ ] Testing hypotheses of Gaussian parameters
- [ ] single parameter hypothesis tests with likelihood ratio test statistic (5.3, generic formula) 
  - [ ] binomial(n, $\theta$)
  - [ ] poisson($\theta$)
  - [ ] exponential($\theta$)
  - [ ] G($\theta, \sigma$) where $\sigma$ is known
- [ ] testing multinomial models with:
  - [ ] likelihood ratio test statistic
  - [ ] pearson goodness of fit statistic
- [ ] test for independence in two way table
- [ ] test for independence in larger two way table
- [ ] derive maximum likelihood estimates and least squares estimate
- [ ] finding confidence interval for $\beta$
- [ ] hypothesis testing for $\beta = \beta_0$ 
  - [ ] hypothesis of no linear relationship $\beta = 0$
- [ ] confidence interval for $\beta$ `Medium`
- [ ] Confidence Interval for $\mu(x) = \alpha  + \beta x$ `HIGH`
- [ ] Confidence (Prediction) Interval for a new response variate $Y$ at $x$ `HIGH`
- [ ] point estimators of means of two populations
- [ ] point estimators of $\sigma$ for two populations 
- [ ] confidence interval for difference in means in:
  - [ ] equal variance
  - [ ] unequal variance
  - [ ] paired data find new random variable $Y_i = Y_{1i} - Y_{2i} \sim N(\mu_1 - \mu_2, \sigma^2)$ which can be used for finding confidence interval



### 3. Create Cheat Sheet

- [x] Helpful `R` functions

  `pnorm(y, mu, sigma)`: gives us the $P(Y \leq y)$ where $Y \sim G(mu, sigma)$. `mu` and `sigma` default to 0, 1.

  `qnorm(y, mu, sigma)`: gives us $a$ where $P(Y \leq y) = a$, and $Y \sim G(mu, sigma)$. Same defaults as `pnorm`.

  `pt(t, df)`: gives us the $P(T \leq t)$ where $T \sim t_{df}$. No default value for `df`.

  `qt(t, df)`: gives us $a$ where $P(T \leq t) = a$, and $T \sim t_{df}$. No default value for `df`.

  `pchisq(w, df)`: gives us the $P(W \leq w)$ where $W \sim \chi^2_{df}$. There is no default value for `df`.

  `qchisq(w, df)`: gives us $a$ where $P(W \leq w) = a$ and $W \sim \chi^2_{df}$. There is no default value for `df`.

- [x] def'n of **variate**, types of variates, **attribute** ==Low==

- [x] 3 types of **studies, statistical inference** ==Low==

- [x] **kurtosis** and **skewness** and what each means graphically ==Low==

- [x] meaning of 5 number summary ==Low==

- [x] signs that data is Gaussian/normal `Medium`

  - mean = median
  - skewness close to 0
  - kurtosis close to 3
  - 95% of data $\in y \pm 2 s.d.$ 
  - data continuous, not truncated
  - graph is symmetric
  - ecdf matches cdf of normal
  - 5 num summary not all discrete
  - QQ plot is linear
  - relative frequency histogram is bell shaped

- [x] how to find expected frequencies `Medium`

- [x] meaning of **boxplot, QQ plots** `HIGH`

- [x] sample correlation ==Low==

- [ ] invariance property (space permitting) ==Low==

- [x] checking fit of model (2.6) `Medium`

- [x] steps of PPDAC, where error can occur, def'n of sampling protocol (3.0) `Medium`

- [x] relationship between properties and confidence interval width (4.4) ==Low==

- [x] steps to find confidence interval using pivotal quantity (4.4) `Medium`

- [x] how to find approximations of pivotal quantities `Medium`

  - take the central limit theorem equation of the distribution, sub in estimators in place of parameters

- [x] Central Limit Theorem `Medium`

- [x] distributions and their: maximum likelihood, variance, mean, standard deviation `HIGH`

- [x] sample size calculation (space permitting) ==Low==

- [x] properties of chi-squared (4.5) `Medium`

- [x] converting between likelihood and confidence interval `HIGH`

- [x] 15% likelihood interval is an approximate 95% confidence interval and a 10% likelihood interval is an approximate 97% confidence interval (NOTE IT IS APPROXIMATE **NOT** EXACT) ==Low==

- [ ] maximum likelihood statistic, how $\Lambda \sim \chi^2_1$ for large $n$ makes it a pivotal quantity `Medium`

- [ ] finding confidence interval in Gaussian with unknown $\mu, \sigma$ for: `HIGH`

  - [ ] $\mu$ 
  - [ ] $\sigma^2$ 

- [ ] finding sample size for Gaussian with known $\sigma$ or estimated $\sigma$ by $s$ `HIGH`

- [ ] point estimator $S^2$ for $\sigma^2$ (4.6) `Medium`

- [x] hypothesis testing recipe (5.1) `HIGH`

- [ ] hypothesis testing for Gaussian parameters `HIGH`

  - [ ] $\mu$ 
  - [ ] $\sigma$ 

- [ ] hypothesis testing relationship to confidence intervals (5.2) ==Low==

- [ ] single parameter hypothesis tests with likelihood ratio test statistic (5.3, generic formula) `HIGH`

- [ ] number of degrees of freedom of hypothesis test (7.1) `Medium`

  - [ ] what to do when expected frequencies are less than 5 (collapse them)

- [ ] pearson goodness of fit statistic ==Low==

- [ ] how to test for independence in two way tables `HIGH`

- [ ] definition of causation (space permitting) ==Low==

- [ ] linear regression model definition and terms `Medium`

- [ ] simplified steps to derive maximum likelihood estimates and least squares estimate `Medium`

- [ ] pivotal quantity of $\beta$ (6.2) ==Low==

- [ ] confidence interval for $\beta$ `Medium`

- [ ] Confidence Interval for $\mu(x) = \alpha  + \beta x$ `HIGH`

- [ ] Confidence (Prediction) Interval for a new response variate $Y$ at $x$ `HIGH`

- [ ] checking assumptions for linear regression models

  - [ ] residual and standardized residual plots
  - [ ] QQ plot of residuals

- [ ] point estimators of means of two populations

- [ ] point estimators of $\sigma$ for two populations 

- [ ] confidence interval for difference in means in:

  - [ ] equal variance
  - [ ] unequal variance
  - [ ] paired data find new random variable $Y_i = Y_{1i} - Y_{2i} \sim N(\mu_1 - \mu_2, \sigma^2)$ which can be used for finding confidence interval

- [ ] paired experiment is better when correlation is positive, relationship exists between the two random variables

  - [ ] this is because positive correlation = positive covariance which reduces variance which gives more accurate data and confidence intervals



### Additional Notes

- To find likelihood function and maximum likelihood estimate

  1. Find likelihood function, might need to do product if multiple random variables
  2. Take $ln(L(\theta))$
  3. Differentiate step 2
  4. Isolate for $\theta$, change to $\hat\theta$ 

- Finding expected frequencies

  1. Substitute your maximum likelihood estimate $\hat\theta $ and the value of $Y$ (which is $y$) into $P(Y = y; \theta)$ for a value $\hat p$
  2. Multiply $\hat p$ by the sample size $n$. This is your **expected frequency** for each value $y$ of $Y$.

- Use the invariance property!

- Central limit theorem says that for random variables $X_1, X_2, ..., X_n$ with the same distribution and mean $\mu$, standard deviation $\sigma$, as $n \rightarrow \infin$, then 

  $\mu_X = \mu$  (mean of the sample means)

  $\sigma_X = \frac{\sigma}{\sqrt n}$ (standard deviation of the sample standard deviations) 

  $X \sim G(\mu, \frac{\sigma}{\sqrt n})$.

- We can **standardize** a random variable $X$ by saying that $\frac{X -\mu}{\sigma} \sim G(0, 1)$

  this works with the Central Limit Theorem to allow us to standardize any random variable

- 

- ![image-20181211145953034](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/final_study_guide.assets/image-20181211145953034-4558393.png)

- changes that affect confidence interval width

- Constructing confidence intervals: 

  1. Find a pivotal quantity $Q( Y; \theta)$
  2. Find numbers $a, b$ such that $P(a \leq Q(Y; \theta) \leq b) = p$.
     _For symmetric distributions, we want to find a number $a$ such that $P(-a \leq Q \leq a) = p$. This allows us to obtain the narrowest confidence interval, which is the best one._
  3. Isolate for $\theta$ in $Q(Y; \theta)$ to get an inequality of the form $L(Y) \leq \theta \leq U(Y)$.
     Then, $p = P(a \leq Q(Y; \theta) \leq b) = P(L(Y) \leq \theta \leq U(Y))$, which means the coverage probability is $p$.
  4. Using observed data $y$ in place of $Y$, the interval $[L(y), U(y)]$ is a 100$p$% confidence interval for the unknown parameter $\theta$.

  **OR**

  1. Use the thing provided lol

- If a value $\theta$ is outside a confidence interval, it is outside the corresponding likelihood interval equivalent to the confidence interval as well

- When calculating sample size for Binomial, assume $\theta = 0.5$ to mazimize for worst case scenario, and round UP

- $P(|X| \geq a) = 2[1-P(X \leq a)]$ for any distribution $X$ and constant $a$

- Hypothesis testing:

  - if a custom test statistic (discrepancy measure) is defined (usually $D$), then calculate by

    $p-value = P(D \geq d)$

  - Otherwise, the $R(\theta)$ likelihood function should be defined, so use the likelihood ratio test statistic:

    $p-value = P(\Lambda \geq \lambda)$, and since $\Lambda \sim \chi^2_1$, we can say

    $p-value = P(W \geq \lambda)$, and by chi-squared properties since $W \sim \chi^2_1$, we can say

    $p-value = 2[1 - P(Z \leq \sqrt \lambda)]$ where $Z \sim G(0, 1)$ 

- ![image-20181211162605028](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/final_study_guide.assets/image-20181211162605028-4563565.png)

- 'a linear regression on $y$ of $x$' means $E[Y] = \alpha + \beta x$

- confidence interval is NOT ALWAYS symmetric around the maximum likelihood estimate

