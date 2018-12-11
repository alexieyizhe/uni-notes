__STAT 231 |__ Section 6.1

# Estimates of $\alpha, \beta$  

### Least Squares Estimate

__Question:__ which line is the best fitting line to this graph of data?

![image-20181210230232214](/Users/alexieyizhe/Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230232214-4500952.png)

We define the distance between a fitted line and the data by __residuals.__ We try to find a fitted like $y = \alpha + \beta x$ which minimizes the sums of squares of the distances between the observed points and the fitted line. 

Estimates of $\alpha, \beta$, denoted $\hat \alpha, \hat \beta$, are called the ==__least squares estimate__==.

Formally, we find $\hat \alpha, \hat\beta$ which minimize:

![image-20181210230543506](/Users/alexieyizhe/Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230543506-4501143.png)

![image-20181210230900028](/Users/alexieyizhe/Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230900028-4501340.png)

![image-20181210230906775](/Users/alexieyizhe/Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230906775-4501346.png)

![image-20181210231015868](/Users/alexieyizhe/Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210231015868-4501415.png)

![image-20181210231021251](/Users/alexieyizhe/Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210231021251-4501421.png)

### Maximum Likelihood Estimate

We can also use maximum likelihood estimation.

Since our model is 

![image-20181210234504240](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210234504240-4503504.png)

and we know the likelihood function for a distribution is

![image-20181210234524909](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210234524909-4503524.png)

then we know that 

![image-20181210234547692](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210234547692-4503547.png)

and we want to maximize it by minimizing

![image-20181210234609724](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210234609724-4503569.png)

but then this is just the least squares problem, with the estimate being the **same as the least squares estimate** above:

![image-20181210234806609](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210234806609-4503686.png)





### Distribution of $\tilde \alpha, \tilde \beta$ Estimators

We have shown that the least squares and maximum likelihood estimate of $\beta$ is given by

![image-20181210234934347](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210234934347-4503774.png)

and so a corresponding estimat__or__ would be

![image-20181210234950511](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210234950511-4503790.png)

_note the change in uppercase $Y_i$, making it a random variable_



Then, a theorem tells us that if

![image-20181210235046146](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235046146-4503846.png)

independently, where the $x_i$ for $i = 1, 2, ..., n$ are known constants, then 

![image-20181210235113463](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235113463-4503873.png)

where $\tilde \beta$ is the equation above (second in this section).



### Pivotal Quantity of $\beta$

![image-20181210235234117](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235234117-4503954.png)



### Confidence Interval for $\beta$

Like mentioned in the previous part, we don't know $\sigma$, so we estimate $\sigma^2$ using

![image-20181210235437105](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235437105-4504077.png)

or more easily,

![image-20181210235448878](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235448878-4504088.png)

Note the following theorem:

![image-20181210235549374](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235549374-4504149.png)

![image-20181210235607270](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235607270-4504167.png)

So, a 100$p$% confidence interval for $\beta$ is given by:

![image-20181210235635632](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235635632-4504195.png)

where $P(T \leq a) = (1+p)/2$, and $T \sim t_{n - 2}$.



### Hypothesis Testing $\beta = \beta_0$ and the Hypothesis of No Linear Relationship

For testing $H_0: \beta = \beta_0$, the $p$-value is

![image-20181210235749284](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181210235749284-4504269.png)

where $T \sim t_{n -2}$. 

We can **test $H_0: \beta = 0$ to show that $\mu(x)$ does not depend on $x$,** since $\mu(x) = \alpha + \beta x$. This tells us that there is __no linear relationship__ between the variates $Y$ and $x$.



### Confidence Interval for $\mu(x) = \alpha  + \beta x$

By the Invariance Property, we know that the maximum likelihood estimator of $\mu(x)$ is the random variable

![image-20181211000039912](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211000039912-4504439.png)

and we can find a distribution for $\tilde \mu(x)$, which will let us construct a confidence interval for the mean response. It takes some effort, so we just give the confidence interval as follows.

A 100$p$% confidence interval for $\mu(x) = \alpha + \beta x$ is

![image-20181211000150547](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211000150547-4504510.png)

_Note that this is basically the same argument we had for deriving a confidence itnerval for $\beta$ above._



### Confidence Interval for the intercept $\alpha$

![image-20181211000241621](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211000241621-4504561.png)



### Confidence (Prediction) Interval for a new response variate $Y$ at $x$

The 100$p$% prediction interval for a new response variate $Y$ at $x$ is given as

![image-20181211000507500](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211000507500-4504707.png)





# Checking Model Assumptions

There are two main assumptions we make for Gaussian linear response models:

1. $Y_i$ (given covariates $x_i$) has a Gaussian distribution with standard deviation $\sigma$ which does not depend on any of the covariates.
2. $E[Y_i] = \mu(x_i)$ is a linear combination of known covariates $x_i = (x_{i1}, ..., x_{ik})$ and the known regression coefficients $\beta_0, \beta_1, ..., \beta_k$.

We can check these assumptions using graphical methods like:

### Scatterplot with data + fitted line

![image-20181211000902868](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211000902868-4504942.png)

To check the two assumptions with this method, respectively:

1. Are the points generally spread out to the same extent regardless of their $x$-position?
   This shows if $\sigma$, the standard deviation of the points, depends on $x$.
2. Do the points seem to fit reasonably along a straight line (the fitted line helps here)?
   This shows if $E[Y_i]$ is following $\mu(x_i)$, the linear function line of $x$



### Residual plots of $(x_i, \hat r_i)$

We can define $\hat r_i = y_i - \hat \mu_i$, where $\hat \mu_i = \hat \alpha + \hat \beta x_i$. These are called __residuals__ since they represent what is 'left over' after the estimate based on the model has been 'fitted' to the observed data ($y_i $).

 Also note:

![image-20181211001310114](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211001310114-4505190.png)

We see that...

![image-20181211001342796](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211001342796-4505222.png)

![image-20181211001643800](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211001643800-4505403.png)





### Standardized Residual Plots of $(x_i, \hat r^*_i)$

This plot can be interpreted in the same way, but we define the __standardized residuals__ to be

![image-20181211001534588](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211001534588-4505334.png)

so the plot will be 'scaled' compared to a normal residual plot. The $\hat r^*_i$ values should be in the range (-3, 3). The following plot is the same as the above, but standardized:

![image-20181211001635296](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211001635296-4505395.png)

###Standardized Residual Plots of $(\hat u_i, \hat r^*_i)$

There is also an __alternate__ form of this plot, where we plot the mean instead to check if the __assumed mean $\mu(x) = \alpha + \beta x$ is reasonable__. 

If it is, we should see a horizontal band around the like $\hat r^*_i = 0$.

![image-20181211001925573](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211001925573-4505565.png)

### QQ Plots of Standardized Residuals

A QQ plot of the $\hat r^*_i$ should give approximately a **straight line if the assumption of a Gaussian model holds**:

![image-20181211002027200](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211002027200-4505627.png)

![image-20181211002032568](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1+6-2.assets/image-20181211002032568-4505632.png)

