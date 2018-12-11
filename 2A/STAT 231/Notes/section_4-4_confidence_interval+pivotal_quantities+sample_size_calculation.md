__STAT 231 |__ Section 4.4

# Confidence Intervals

A ==__100$p$% confidence interval__== for a parameter is an interval estimate $[L(y), U(y)]$ for which:

![image-20181210120011379](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210120011379-4461211.png)

and $p$, in this case, is known as a __confidence coefficient__ for the interval.

We say that for a sample, we are '$100p$% confident' that the true value of $\theta$ is in the interval that we constructed.

`Caution:` The true value of $\theta$ is __not__ a random variable - it is an unknown __constant__ and therefore does not have a distribution. This is why we _cannot define a confidence interval to be the probability that the true value of $\theta$ lies in the interval, since_ the __true value of $\theta$ is either in the interval or not in the interval. It's a constant.__



### Likelihood vs. Confidence Intervals

A 100$p$% likelihood interval tells us that values of $\theta$ inside the interval are at least $100p$% as plausible as the ml estimate $\hat \theta$ (that $R(\theta) \geq p$). 

A $100p$% confidence interval, tells us that, constructing multiple intervals from $[L(Y), U(Y)]$, we expect $100p$% of these intervals to contain the true (unknown) value of $\theta$ (and that $100(1-p)$% of the intervals are expected not to contain it).



### Calculating a Confidence Interval

Usually, we are only able to construct one interval (_think back to repeated sampling and why it's usually just a concept_), and we hope that the interval we construct is one that falls in the good $100p$%. 

To construct one, take the following for a Gaussian model as an example:

1. Get a random sample $(Y_1, Y_2, ..., Y_n)$ from a $G(\mu, 1)$ distribution where $E[Y_i] = \mu$ is our unknown parameter, and $sd(Y_i) = 1$ is known. 
2. For the random interval: ![image-20181210120514828](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210120514828-4461514.png), we have ![image-20181210120533744](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210120533744-4461533.png), since we expect that approx. 95% of a sample is within 2 s.d. of the mean $\bar Y$.

3. Then, the interval:![image-20181210120604539](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210120604539-4461564.png) with observed *sample* mean $\bar y$ is a $95$% confidence interval for the unknown mean $\mu$ of the *population.*



   `Caution`: Again, with this example, we illustrate the difference between $\bar Y$ and $\bar y$. Suppose that $n = 16$. Then, by calculation, a 95% confidence interval for $\mu$ is ![image-20181210121516352](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210121516352-4462116.png)but we cannot say that $P(\mu \in [9.91, 10.89]) = 0.95$. This is because $\bar Y$ is a random variable, and that allows us to say that repeatedly taking intervals resulting from $\bar Y$ will give us an overall probability $p$ that $\mu$ lies in all those intervals. $\bar y$ is a specific value, so the first `Caution` above applies.



### Relationship Between Sample Size, Confidence Level, and Variance

As confidence level increases, the confidence interval gets wider.

As sample size increases, the confidence interval gets narrower.

As sample standard deviation increases, the confidence interval gets wider.

As population variance increases, the confidence interval gets wider.

As the unknown parameter we are finding the interval for changes, the confidence interval __stays the same width.__



# Pivotal Quantities

A ==__pivotal quantity__== is a function of the data $Y$ and the unknown parameter $\theta$ such that the distribution of the random variable $Q$ is completely known. 

_For example..._

![image-20181210130917020](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210130917020-4465357.png)

![image-20181210130928635](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210130928635-4465368.png)

Pivotal quantities are useful for constructing 100$p$% confidence intervals. We can use them as follows:

1. Find numbers $a, b$ such that $P(a \leq Q(Y; \theta) \leq b) = p$.
   _For symmetric distributions, we want to find a number $a$ such that $P(-a \leq Q \leq a) = p$. This allows us to obtain the narrowest confidence interval, which is the best one._
2. Isolate for $\theta$ in $Q(Y; \theta)$ to get an inequality of the form $L(Y) \leq \theta \leq U(Y)$.
   Then, $p = P(a \leq Q(Y; \theta) \leq b) = P(L(Y) \leq \theta \leq U(Y))$, which means the coverage probability is $p$.
3. Using observed data $y$ in place of $Y$, the interval $[L(y), U(y)]$ is a 100$p$% confidence interval for the unknown parameter $\theta$.



_Algorithm to find confidence interval of $\mu$ for Gaussian data where $\sigma$ is known:_

1. Use normal tables or `R` to find $a$ such that $P(-a \leq Z \leq a) = p$ where $Z \sim G(0, 1)$. In otherwords, such that $P(Z \leq a) = \frac{1 + p}{2}$.
2. A 100$p$% confidence interval for $\mu$ is then $\bar y \pm a \frac{\sigma}{\sqrt{n}}$.



### Helpful `R` Functions

`pnorm(y, mu, sigma)`: gives us the $P(Y \leq y)$ where $Y \sim G(mu, sigma)$. `mu` and `sigma` default to 0 and 1.

`qnorm(y, mu, sigma)`: gives us $a$ where $P(Y \leq y) = a$, and $Y \sim G(mu, sigma)$. Same defaults as `pnorm`.



### Approximate Pivotal Quantities & Approximate Confidence Intervals

In a lot of models, it's hard or not possible to find exact pivotal quantities or confidence intervals for $\theta$.

However, we can find ==__approximate pivotal quantities__==, which are random variables $Q_n = Q_n(Y_1, Y_2, ..., Y_n; \theta)$ where as $n \rightarrow \infty $, distributions no longer depend on unknown information like $\theta$ or elsewise.

_see course notes for all approximations of different models_



### Sample Size Calculation

A sample size, as shown before, affects the confidence intervals for an unknown parameter. More specifically, as the sample size increases, the confidence intervals get narrower. So, oftentimes we will want to find the smallest sample size $n$ such that we have a 100$p$% confidence interval.

Suppose we want to estimate $\theta$ with a sample size of $n$. We want to use the 95% confidence interval, given by

![image-20181210135513596](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210135513596-4468113.png)

The width of this interval is 

![image-20181210135533559](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210135533559-4468133.png)

and if we want a width of $\leq  2l$, then 

![image-20181210135603396](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-4.assets/image-20181210135603396-4468163.png)

We just need the maximum value of $\hat \theta$ so we can calculate the worst case scenario to get a lower bound for $n$ in order to maintain the 95% confidence interval.

