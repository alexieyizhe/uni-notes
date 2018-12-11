__STAT 231 | __Section 4.6

### Gaussian Data with Unknown $\mu, \sigma$

In our previous examples with calculating  confidence intervals for the mean $\mu$ of Gaussian data, $\sigma$ is always a known value. This is an assumption, and often we won't know this value.

Suppose $Y_1, Y_2,..., Y_n$ is a random sample from a $G(\mu, \sigma)$ distribution where both $\mu = E(Y_i)$ and $sd(Y_i) = \sigma$ are both __unknown.__

The maximum likelihood estimator $\tilde \mu = \bar Y$ can still be used to estimate $\mu$. We use a point estimator for $\sigma^2$ to be

![image-20181210151114532](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151114532-4472674.png)

beecause $E[S^2] = \sigma^2$.

So now, the pivotal quantity (which isn't a pivotal quantity anymore because $\sigma$ is unknown)

![image-20181210151151353](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151151353-4472711.png)

can be used again once we replace $\sigma$ with $S$ to get 

![image-20181210151226560](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151226560-4472746.png)

This is a new distribution: a ==__Student's $t$ distribution.__==



### Student's $t$ Distributions

A random variable $T$ is said to have a __Student's $t$ distribution__ (or simply a $t$ distribution) if its _pdf_ is

![image-20181210151333009](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151333009-4472813.png)

where the constant $c_k$ is (with $\Gamma$ being the gamma function):

![image-20181210151347828](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151347828-4472827.png)

The $t$ distribution is **symmetric about zero**. The parameter $k$ is also known as the __degrees of freedom__, and we denote $T \sim t(k)$, or $T \sim t_k$.



### Finding a Confidence Interval for $\mu$

We can use the distribution ![image-20181210151226560](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151226560-4472746.png)as a pivotal quantity to construct a confidence interval for $\mu$.

To find a 100$p$% confidence interval for $\mu$, when $\sigma$ is unknown:

1. Since the $t$ distribution is symmetric, we look for a value $a$ from $t$ tables such that

   ![image-20181210151710062](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151710062-4473030.png)

   where $T \sim t_{n-1}$. Since we also know ![image-20181210151819929](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151819929-4473099.png)by sustituting this into the above inequality, we have

   ![image-20181210151906981](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151906981-4473147.png)

2. Isolate for $\mu$ like we do when finding a normal confidence interval, to obtain

   ![image-20181210151949268](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151949268-4473189.png)

3. Then, ![image-20181210151959754](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210151959754-4473199.png) is a 100$p$% confidence interval for $\mu$.

==Compared to using the normal distribution, the confidence interval found with a $t$ distribution with unknown $\sigma$ is **wider** than an interval found with the normal.==



### Helpful `R` Functions

`pt(t, df)`: gives us the $P(T \leq t)$ where $T \sim t_{df}$. There is no default value for `df`.

`qt(t, df)`: gives us $a$ where $P(T \leq t) = a$, and $T \sim t_{df}$. No default value for `df`.



### Sample Size Calculation, $\sigma$ unknown

We solve this in the same way as calculating the sample size $n$ in Section 4.4: find the width of the interval, set it equal to our desired width, solve for $n$. However, since this is for Gaussian data, we have that $\sigma$ is estimated by $s$, our sample standard deviation.



### Finding a Confidence Interval for $\sigma^2, \sigma$

We can use the following theorem:

![image-20181210154417375](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210154417375-4474657.png)

Since this random variable is a function of the data $Y_1, Y_2, ..., Y_n$, and its distribution is completely known, this is a pivotal quantity and we can use it to construct a confidence interval.

To costruct a 100$p$% confidence interval for $\sigma^2$ when $\mu$ is unknown:

1. Find values $a, b$ such that $P(a \leq W \leq b) = p$, where $W \sim \chi^2_{n - 1}$.

   To find this, we need to find $P(W \leq a) = (1 - p)/2$  and $P(W \gt b) = (1-p)/2$ (or $P(W \leq b) = (1+p)/2$).

2. Since $W \sim \chi^2_{n - 1}$ and ![image-20181210155004932](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210155004932-4475005.png)we can write that

   ![image-20181210155041073](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210155041073-4475041.png)

3. Isolate for $\sigma^2 $ to get

   ![image-20181210155224309](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210155224309-4475144.png)

   This confidence interval is __not__ symmetric about $s^2$, the point estimate of $\sigma^2$.

4. To find a  confidence interval for $\sigma$ instead of $\sigma^2$, we have that

   ![image-20181210155551055](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-7.assets/image-20181210155551055-4475351.png)





### Helpful `R` Functions

`pchisq(w, df)`: gives us the $P(W \leq w)$ where $W \sim \chi^2_{df}$. There is no default value for `df`.

`qchisq(w, df)`: gives us $a$ where $P(W \leq w) = a$ and $W \sim \chi^2_{df}$. There is no default value for `df`.