__STAT 231 |__ Section 4.1, 4.2

# Parameter Estimates and Estimators

When we take a sample of a population and find an _m.l._ estimate of a parameter, the sample we take is usually a random sampling. 

We can think of the sample we take, and its resulting sample estimate, as a concrete value of a __random variable__. If we take samples over and over, known as ==__repeated sampling__==, we'll keep getting different estimates. 

> Note that we can't really expect to do this in real life - this is just a concept.

The parameter we're estimating then itself can be modeled with a probability distribution that has its own mean and variance. _For example, if the parameter we are estimating is the sample mean of a model $Y \sim G(\mu, \sigma), i = 1, 2, ..., n$ independently, with observed data $y_1, y_2, ..., y_n$, the sample mean would follow a distribution, and the m.l. estimate of that distribution is $\bar y = \hat \mu$._ 

For large values of $n$, $\hat \mu$ would be very close to the true value of $\mu$ (but remember, they're very very likely not the same).

Recall that a ==point estimate of a parameter $\theta$==, denoted $\hat\theta$, is the value of a function $\hat\theta(y) = g(y_1, y_2,...,y_n)$ where $y$ is a set of observed data $(y_1, y_2, ..., y_n)$. So, varying sets $y$ will have different associated $\hat \theta$ values. This means that we can associate with the point estimate

![image-20181210003202483](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4.1+4.2.assets/image-20181210003202483-4419922.png)

a random variable 

![image-20181210003153680](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4.1+4.2.assets/image-20181210003153680-4419913.png)

where instead of observed values $y_1, ..., y_n$, we have random variables $Y_1, ..., Y_n$. This is known as a ==__point estimator__==, a random variable that processes data to give us an estimate of an unknown parameter $\theta$.

With this definition, the value $\hat \theta​$ is a value obtained from $\tilde \theta​$ by 'plugging in' the data set $(y_1, y_2, ..., y_n)​$ obtained from $(Y_1, Y_2, ..., Y_n)​$.

Since $\tilde \theta$ is a random variable, it has a distribution! This is known as the __sampling distribution of the estimator.__ To find this distribution, brute force often doesn't work - we can't just enumerate through all possible sets of $n$ size and compute the parameter for each and plot it to get the probability function for $Y$ in most cases. 

We need to __use the Central Limit Theorem__, which tells us:

![image-20181210001443789](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4.1+4.2.assets/image-20181210001443789-4418883.png)

We can apply this to the estimator, which takes in $Y_1, Y_2, ..., Y_n$ random variables, so by computing $\bar Y$, $\sigma, $ and $\mu$, we can compute a _new_ random variable that follows the $G(0, 1)$ distribution. 

Another fact is that __as $n$ gets larger and $\sigma $ gets smaller, the $sd(\bar Y)$ gets smaller.__ Since $sd(\bar Y)$ measures how close each value of $\bar Y$ is to the mean $\mu$,  the smaller it is, the more accurate our estimates obtained through $Y$ are!

Knowing these two pieces of information, we can calculate things like how large $n$ must be or how small $\sigma$ must be to ensure our estimate is at maximum some value off from the true $\mu$. 

> The true mean $\mu$ does not affect how many of the sample estimates are close to it, since they are all relative to the true $\mu$ - essentially, a change in position of $\mu$ will shift the estimates as well.