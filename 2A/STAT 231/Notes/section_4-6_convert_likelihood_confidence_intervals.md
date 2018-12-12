__STAT 231 | __Section 4.6

# Relating Likelihood Intervals & Confidence Intervals

In Section 4.4, we were able to calculate confidence intervals using pivotal quantities or approximate pivotal quantities. Now we can show that likelihood intervals are also a form of confidence intervals.

If we replace the maximum likelihood estimate $\hat \theta$ in the relative likelihood function with a maximum likelihood estimator $\tilde \theta$ to define the random variable $\Lambda(\theta)$:

![image-20181210141905800](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-6.assets/image-20181210141905800-4469545.png)

This is the ==__maximum likelihood statistic__==. For large $n$, we can show that $\Lambda \sim \chi^2_1$, and by the second property in Section 4.4, we know this is a pivotal quantity; which means that it can be used to obtain confidence intervals for $\theta$.



### Approximating a Confidence Interval Using Likelihood

We can approximate a 100$q$% confidence interval for $\theta$ using likelihood with this:

![image-20181210142230731](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-6.assets/image-20181210142230731-4469750.png)

So, to **convert a confidence interval to a likelihood interval**:

==__Theorem:__ A 100$q$% confidence interval is an approximate 100$p$% likelihood interval where $p = e^{-c/2}$ and $q = P(|Z| \leq \sqrt{c}) = 2P(Z \leq \sqrt{c}) - 1 , Z \sim N(0, 1) $.==

1. Identify the appropriate $c$ for the desired confidence interval $p$ by choosing $c$ such that $p = P(W \leq c) = P(|Z| \leq \sqrt{c})$.
2. The likelihood interval is all $R(\theta) \geq e^{-c/2}$, so it is a 100$(e^{-c/2})$% confidence interval.

Inversely, to **convert a likelihood interval to a confidence interval**:

==__Theorem:__ A 100$p$% likelihood interval is an approximate 100$q$% confidence interval where $q = 2P(Z \leq \sqrt{-2log(p)}) - 1$ and $Z \sim N(0, 1)$.==



This gives us an additional technique to approximate confidence intervals for distributions like Binomial where we cannot find an exact pivotal quantity: **find the corresponding likelihood interval and convert it to a confidence interval**!