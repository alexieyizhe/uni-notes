__STAT 231 |__ Section 7.3

# Two Way Tables & Independence Tests

When we have multiple possible values for both variates, we need to create a ==__two way table__.==

Suppose $n$ individuals are classified according to two different variates which have two possible values. The _two way table_ would look like this:

![image-20181210214009592](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210214009592-4496009.png)

where $\bar A$ means $\neg A$, or _'not A'_.

If we let $Y_{ij}$ be the number of outcomes in the $i^{th}$ row and $j^{th}$ column, then

![image-20181210214218038](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210214218038-4496138.png)





### Testing for Independence

We want to conduct a hypothesis test for independence of the two variates. So, our null hypothesis $H_0$ is that the variates $A, B$ are independent:

![image-20181210214405239](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210214405239-4496245.png)

![image-20181210214421718](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210214421718-4496261.png)

If we want to be more specific in terms of our hypothesis, since $\theta_{11} = \alpha\beta,$ then the likelihood function is

![image-20181210214837258](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210214837258-4496517.png)

and our maximum likelihood estimates and estimators are:

![image-20181210214901387](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210214901387-4496541.png)

and 

![image-20181210214910252](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210214910252-4496550.png)

respectively (these are because $\alpha$ represents the probability that $A$ is true and $\beta$ is the same for $B$, so we add up the corresponding row in the two way table).

Note that the likelihood ratio test statistic is as follows (similar to previous likelihood ratio test statistics:

![image-20181210215259535](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210215259535-4496779.png)

with the observed value being

![image-20181210215317028](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210215317028-4496797.png)

and the expected value of the first row/column spot being

![image-20181210215415344](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_7-3.assets/image-20181210215415344-4496855.png)

allowing us to **find the rest of the expected frequencies** by subtracting this value from the totals of each row and each column.

Then, we **calculate $\lambda$** (the observed value of the likelihood ratio test statistic above) from the expected values and the observed values $y_{ij}$ by plugging them in.

Almost done! We **find the $p$-value** by the fact that $p$-value $= P(W \geq \lambda)$ where $W \sim \chi^2_{k - 1 -p}$.

Finally, we are able to **conclude based on the $p$-value** whether or not our null-hypothesis is true; if the $p$-value is very small, there is evidence against the null hypothesis (_i.e. it is very likely that the two variates are NOT independent_), or the opposite might be true.

