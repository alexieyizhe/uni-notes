__STAT 231 |__ Section 4.3

# Interval Estimation

We know that our estimate of a parameter, $\hat \theta$, is likely not the true value of $\theta$. So, how good is our estimate and how can we quantify the uncertainty of our estimate?

We can give an interval of values for $\theta$ that are 'supported' by the observed data where we got $\hat \theta$. We use an __interval estimate__ of the form $[L(y), U(y)]$, where both values are functions of the observed data $y$. 

### Interval Estimates & Likelihood Intervals

An interval estimate that can give us 'reasonable' values of the unknown parameter is a __likelihood interval__. By using the relative likelihood function $R(\theta) = \frac{L(\theta)}{L(\hat\theta)}$, we can construct a ==__100p% likelihood interval__== for the parameter $\theta​$ like so:

1. Define a set of values $A$ of $\theta$ where $R(\theta) \geq p$.

   - Recall that as $R(\theta)$ approaches 1, the values of $\theta$ that result in those large values of $R(\theta)$ are the most plausible. So, this set of values will contain values of $\theta$ that are _at least_ 100p% as likely as when $\theta = \hat\theta$.

     _Ex. For a 50% likelihood interval, the set will contain values that are at least 50% as likely as $\hat\theta$._

2. Find values of $\theta$ where $\theta \in A$. This is hard to do manually, and in general will be **computed by software** like `R`.  

3. **Graph the relative likelihood function*** and draw a line at $y = p$. The intersections of this line with the $R(\theta)$ curve will give us the lower ($L(\theta)$) and upper ($U(\theta)$) bounds of the likelihood interval.

   _*We can also do this with the log relative likelihood function ($r(\theta) $). Instead of drawing the line at $y = p$, we draw the line at $y = log(p)$. The rest of the steps are the same._

![image-20181210112433658](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-3.assets/image-20181210112433658-4459073.png)

### Interval Estimators & Coverage Probability

Much like a point estimate and a point estimat__or__, an interval estimator is a rule that allows for many different intervals of plausible values of $\theta$ to be constructed. If $Y = (Y_1, Y_2, ..., Y_n)$ is a random variable of all the data that can be observed, then $[L(Y), U(Y)]$ is an ==__interval estimator__== that can produce _interval estimates_ (note the difference in $Y$ vs $y$! ).

To determine how good our interval estimator is at finding plausible values of $\theta$, we use the ==__coverage probability__== of the interval estimator:

![image-20181210113601874](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-3.assets/image-20181210113601874-4459761.png)

We want to find interval estimators where:

1. The coverage probability is large (usually 0.9, 0.95, or 0.99)
2. The interval is as narrow as possible

It's hard to get these two criteria to agree, since **increasing the coverage probability will increase the size of the likelihood interval**; thus, we often fix the coverage probability at a set value and then try to find the narrowest interval by moving the lower and upper bounds around (as long as the probability doesn't drop below the set value).



