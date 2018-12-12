__poinSTAT 231 | __Section 6.3

# Comparing Means of Two Populations

We sometimes are interested in comparing variates of two different populations. We can define 

![image-20181211003455716](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003455716-4506495.png)

and 

![image-20181211003501580](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003501580-4506501.png)

Note that we have defined $\sigma$ to be the same for both models.

This is known as a __two sample Gaussian problem__. It can be shown to be a special case of the Gaussian response model. 

### Point Estimators of Means $\mu_1, \mu_2$

The maximum likelihood estimator of $\mu_1$ is

![image-20181211003337976](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003337976-4506417.png)

and the equivalent for $\mu_2$ is

![image-20181211003356106](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003356106-4506436.png)

and also...

![image-20181211003408721](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003408721-4506448.png)



### Point Estimator of $\sigma$

We need to define the point estimator of $S_1^2$, which estimates $\sigma^2$ based only on $Y_{1i}$:

![image-20181211003636921](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003636921-4506596.png)

and another estimator for $S_2^2$, which estimates $\sigma^2$ based only on $Y_{2i}$:

![image-20181211003715246](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003715246-4506635.png)

and finally we can find the point estimator for $\sigma^2$:

![image-20181211003734028](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211003734028-4506654.png)



### Confidence Interval of Difference in Means (Equal Variances)

![image-20181211004017727](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211004017727-4506817.png)



###Confidence Interval of Difference in Means (Unequal Variances)

If the variance or standard deviation is not the same, but $n_1, n_2$ are large, we can use the approx. pivotal quantity:

![image-20181211004152628](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211004152628-4506912.png)

to construct confidence intervals and test hypotheses for the difference in means.

To find a 100$p$% confidence interval of the difference in means, we use:

![image-20181211004300788](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211004300788-4506980.png)

where $1.96$ is replaced by your $a$ value, where $P(T \leq a) = \frac{1+p}{2}$ and $T \sim t_{n_1 + n_2 - 2}$.





# Paired Data

Sometimes, the two samples we're studying won't be independent, like we've assumed them to be in all of the previous parts of this section.

We pair up observations, so that the value of the $i^{th}$ unit in the first sample is correlated with the second sample. This is __paired data.__

### Variance & Covariance

![image-20181211004836420](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211004836420-4507316.png)

This shows us that the variance of paired data is less, which is one of the benefits of using paired data.



### Working With Distributions in Paired Data

To make inferences about $\mu_1 - \mu_2$, we analyze the within-pair differences 

![image-20181211004942684](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211004942684-4507382.png)

by assuming 

![image-20181211005000999](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211005000999-4507401.png)

or, when working with Gaussian, that

![image-20181211005015023](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211005015023-4507415.png)

This can then be used to **find confidence intervals**, etc, just like a normal one sample Gaussian distributed random variable.



### When and Why Paired Experiments are Better than 2 independent random samples

Paired experiments reduce the variance of each individual sample's random variables, which is better than when they are two independent studies. 

This is better for estimating $\mu_1 - \mu_2$, since a smaller variance means a smaller confidence interval, which is more accurate. However, this is only the case when __there is a positive correlation or association between the two random variables (samples)__. 

To show this mathematically, if we say that the estimator of $\mu_1 - \mu_2$ is $\bar Y_1 - \bar Y_2$, and we have that $E(\bar Y_1 - \bar Y_2) = \mu_1 - \mu_2$, then

![image-20181211005658624](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-3.assets/image-20181211005658624-4507818.png)

We can see that $\sigma_{12} = Cov(Y_{1i}, Y_{2i})$, and so a **positive correlation** means $\sigma_{12} \gt 0$, **reducing** $Var(\bar Y_1 - \bar Y_2)$. On the other hand, a negative correlation between the two random variables means $\sigma_{12} \lt 0$, which increases the variance - not what we want and in that case pairing is a bad idea.



