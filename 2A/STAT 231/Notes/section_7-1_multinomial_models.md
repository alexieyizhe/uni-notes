__STAT 231 |__ Section 7.1

# Multinomial Models

We might have a distribution that's not based on a single random variable, but **multiple random variables**. This is ==__multinomial distribution__.== Its probability function is given by:

![image-20181210184631802](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-all.assets/image-20181210184631802-4485591.png)

### Multinomial Likelihood Function

Just like likelihood functions with a single parameter, we can find the likelihood function of a multinomial model based on observed data $y_1, y_2, ..., y_n$ to be:

![image-20181210184739608](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-all.assets/image-20181210184739608-4485659.png)

### Multinomial Maximum Likelihood Estimates & Hypotheses of Interest

In general, we can find a maximum likelihood estimator $\tilde \theta_j$ to be $\frac{Y_j}{n}$ with a corresponding maximum likelihood estimate $\hat \theta_j = \frac{y_j}{n}$, for some observed multinomial data $y_1, ..., y_k$.

When we're trying to test hypotheses, we usually define our null hypothesis based on what we're testing, but keep in mind that now there's multiple parameters to define in our null hypothesis.

_ex. to test if a $k$-sided die is fair, we might define our null hypothesis to be  $\theta_0 = (\frac{1}{k},..., \frac{1}{k})$._



### Hypothesis Testing & Likelihood Ratio Test Statistic

Based on the information above, we would set up the likelihood ratio test statistic for multinomial data like so:

![image-20181210185438176](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-all.assets/image-20181210185438176-4486078.png)

if we're testing the null hypothesis $\theta_0$ defined above.

So, since $\theta_j = \frac{1}{k}$, we have that 

![image-20181210185735370](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-all.assets/image-20181210185735370-4486255.png)

![image-20181210185755274](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-all.assets/image-20181210185755274-4486275.png)

and finally,

![image-20181210185834454](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-all.assets/image-20181210185834454-4486314.png)

For the observed value, we simply replace $Y_j$ with an observed value of $y_j$ and $E_j = \frac{n}{k}$.

If $e_j \geq 5$ for all $j$, we can use a Chi-squared approximation to obtain the $p$-value. The $p$-value $= P(W \geq \lambda(\theta_0))$, where $W \sim \chi^2_{k - 1 - p}$, $p$ being the number of parameters estimated (number of unknown parameters).

So, the number of **degrees of freedom** is $k - 1 - p$.

What do we do when some of the expected frequencies are less than 5? We have to 'collapse' some of our adjacent categories with the smallest frequencies so that we can have every category be greater than 5.



