__STAT 231 |__ Section 2.1, 2.2, 2.3, 2.4

# Probability Models

Choosing a probability model is useful for a variety of reasons:

- Being able to measure variates in a quantitative manner
- How different or similar a population is in regards to a specific variate
- Measuring variate data itself

We usually choose a model based on some or all of the following:

- Background knowledge or assumptions about the population or process that can point at certain distributions
- Past experience with data sets from the population/process that show certain distributions are suitable
- Mathematical convenience when working with data from population/process
- A current data set against which the model can be assessed

> Remember that no statistical model is perfect in describing something, but we can learn a lot about a population/process from more accurate models.

# Maximum Likelihood Estimation

To determine how well a model fits a data set, we need a value for the probability $\theta$ obtained from the data. We can 'estimate' the value of $\theta$, denoted $\hat{\theta}$, and hope that it's close to the truth. 

 A ==point estimate of a parameter $\theta$==, denoted $\hat\theta$, is the value of a function of the observed data $y$ and other known quantities, like the sample size $n$. 

Sometimes, we can calculate $\hat{\theta}$ using reasonable methods, like taking the average of times to find one, but sometimes it's not so obvious. In that scenario, using the **Method of Maximum Likelihood** is useful to estimate the unknown parameter $\theta$. 

### Method of Maximum Likelihood & M.L. Estimates

When we have a model $M$, we have a function that describes the model. 

For example, the model for Binomial data when tossing 25 coin tosses with $Y$ being the number of heads is:

![image-20181209210206335](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-1to2-5.assets/image-20181209210206335-4407326.png)

We can find the ==maximum likelihood estimate==, a point estimate of $\theta$, by maximizimg the function according to the data. For example, if we want to find the maximum likelihood estimate of $\theta$ where we get 10 heads in 25 tosses, we maximize this function with known values substituted:

![image-20181209210428370](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-1to2-5.assets/image-20181209210428370-4407468.png)

We find that the value that maximizes this function is $\hat\theta = 0.4$, which means that **the data are most likely of all $\theta$ when $\theta = 0.4$.**  This is our maximum likelihood estimate, or _m.l. estimate._ Since the above function can help us find the _m.l. estimate,_we call the function a ==likelihood function for $\theta$.==

### Relative Likelihood

We care more about how two values of the parameter compare in terms of making the data more or less likely. This is the ==__relative likelihood__== of one value to another, and we can find a ==__relative likelihood function__== that tells us this:

![image-20181209210957998](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-1to2-5.assets/image-20181209210957998-4407798.png)

This function will always be less than one since the denominator is the **maximum** likelihood estimate, and you'll notice that the constants in the likelihood function will **cancel out**, since **multiplying the likelihood function by a constant will not change its shape.**

### Log Likelihood Function

The ==__log likelihood function__== is defined as:

![image-20181209211316943](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-1to2-5.assets/image-20181209211316943-4407996.png)

where $log = ln$, the natural log. The log likelihood function has the same shape as the likelihood function, plus this will make our algebra much easier when trying to solve for $\hat\theta$.

> Prof. Wallace says :speech_balloon:: easier algebra = happier times :smile:

### Log Relative Likelihood Function

The ==__log relative likelihood function__== is given by:

![image-20181210112554413](/Users/alexieyizhe/Google%20Drive/University/2A/STAT%20231/Notes/section_4-3.assets/image-20181210112554413-4459154.png)

It's often also easier to compute than the regular relative likelihood function. The maximum value of $r(\theta)$ is $0$.

### Likelihood Function of a Random Sample

If $Y = (Y_1, Y_2, ..., Y_n)$ are independent random variables with the same distribution and probability function $P(Y = y; \theta)$, then the likelihood function for observing a data set $y = (y_1, y_2, ..., y_n)$ from these variables is given by:

![image-20181209211734458](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-1to2-5.assets/image-20181209211734458-4408254.png)

### Invariance Property of Maximum Likelihood Estimates

We can use maximum likelihood estimates for estimating other properties of a data set and a distribution through the ==__invariance property __==:

![image-20181209212106642](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-1to2-5.assets/image-20181209212106642-4408466.png)

_As an example, if we wanted to estimate the variance of a random variable $Y$, since $Var(Y) = n\theta (1 - \theta)$, then the invariance property tells us that the maximum likelihood estimate of $Var(Y) = n \hat\theta (1 - \hat\theta)$._ 

### Steps For Finding Likelihood Function & M.L Estimate

To find the likelihood function and then the m.l. estimate of a distribution $X$ and data $y$:

1. Use the probability function of $X$ and substitute your known values like sample size $n$, and observed data (there can be multiple data sets, refer to __likelihood function of a random sample__).

2. Simplify. This is your __likelihood function__.

3. Take the log likelihood function of the likelihood function and isolate for $\theta$. After substituting and replacing $\theta$ with $\hat\theta$, you have your __maximum likelihood estimate__.

    

### Finding Expected Frequencies 

Assume you have a sample size of $n$ and you want to find the expected frequency of $y$, where $y$ is a value of a random variable $Y$ with probability function $P(Y = y; \theta)$. 

1. Substitute your maximum likelihood estimate $\hat\theta $ and the value of $Y$ (which is $y$) into $P(Y = y; \theta)$ for a value $\hat p$. 
2. Multiply this value by the sample size $n$. This is your **expected frequency** for each value $y$ of $Y$.