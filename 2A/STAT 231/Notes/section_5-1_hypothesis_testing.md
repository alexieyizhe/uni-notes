__STAT 231 |__ Section 5.1

# Hypothesis Testing

In hypothesis testing, we aim to collect data to prove or disprove a hypothesis.

We usually begin by specifying a single default hypothesis - this is called the ==__null hypothesis__==, denoted $H_0$. There is also an ==__alternate hypothesis__==, denoted $H_A$ or $H_1$ (often, this is simply the statement that $H_0$ is not true).

_Example: testing if US coins are biased to one side when tossed._

![image-20181210160529728](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_5-1.assets/image-20181210160529728-4475929.png)

![image-20181210160557129](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_5-1.assets/image-20181210160557129-4475957.png)

However, it's hard to define how close is 'close enough'  to our $H_0$ to conclude that $H_0$ is true. To measure this, we have to use a ==__test statistic__==, also known as a ==__discrepancy measure__==.

==A test statistic or discrepancy measure is a function of the data $D = g(Y )$ that is constructed to **measure the degree of ‘agreement’** between the data $Y$ and the null hypothesis $H_0 $.==

Usually, $D=0$ represents the best possible agreement between the data and $H_0$, whereas large values of $D$ indicate poor agreement.



### P-values

We care more about the probability of observing a value of $D$ greater than or equal to that observed when we ran an experiment once, assuming the null hypothesis is true. The probability $P(D \geq d)$ is the $p$-value of the test of the hypothesis.

A small _p-value_ tells us that if the null hypothesis were true, it would be __unlikely__ to have observed **data as weird or more weird** than the data we actually observed.



### Hypothesis Testing for Binomial parameters

We can calculate $P(D \geq d)$ to get the $p$-value, or we can use the Normal approximation to the Binomial for large $n$.

![image-20181210163953155](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_5-1.assets/image-20181210163953155-4477993.png)





### Hypothesis Testing Recipe

![image-20181210161722543](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_5-1.assets/image-20181210161722543-4476642.png)

![image-20181210162205521](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_5-1.assets/image-20181210162205521-4476925.png)

###Notes About Hypothesis Testing

**Disproving vs. proving hypotheses:** While hypotheses can be disproved by showing a difference or small $p$-value from the null hypothesis, it hs not possible to do the same for proving it. You can only say that there is _no evidence against $H_0$ in light of the observed data._

**Magnitude of difference when disproving hypotheses:** A hypothesis could be wrong, but only off by a slight amount, or it could be wrong and off by miles. You should always have a measurement of magnitude in terms of how 'off' $H_0$ is from your observed results.

**Statistical Significance vs. Practical Significance**: While we might be able to find evidence of a *statistically* significant difference against a hypothesis, it doesn't mean in the real world that it would be *practically* significant. 
_ex. if insurance finds that values of policies sold in 2 years differ by $5.32, it would not mean a lot to them as the value of each policy is orders of magnitudes bigger, like \$1000._

