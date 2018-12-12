__STAT 231 | __ Section 1.3

# Empirical Studies (cont.)

###Percentiles, Quantiles, and Quartiles

These are used much like percentages, to measure the distribution of a fraction of the data.

The p^th^ ==quantile==, or equivalently, the 100p^th^ ==percentile==, is the value such that a fraction $p$ of the data set fall below or at this value (_ex. the 0.5^th^ quantile aka the 50^th^ percentile is also the median_).

To find the *p^th^ quantile*, denoted $q(p)$:

1. Let $m = (n + 1)p$, where $n$ is the sample size.
2. If $m$ is an integer, then take the _m^th^_ smallest value and $q(p) = y_{(m)}$.
3. Otherwise, determine the closest integer $j$ such that $j \lt m \lt j + 1$ and take $q(p) = \frac{1}{2}[y_{(j)} + y_{(j+ 1)}]$.

A ==quartile== is just one of the 25^th^, 50^th^, or 75^th^ percentiles:

- $q(0.25)$ or the 25^th^ percentile is known as the ==lower/first quartile==
- $q(0.5)$ or the 50^th^ percentile is known as the ==median==
- $q(0.75)$ or the 75^th^ percentile is known as the ==upper/third quartile==



### Numerical Summaries

Let the data be represented by $\{y_1, y_2, ..., y_n\}$ where $y_i$ is a real number and our sample size is $n$. First, note that the idea of an __ordered sample__ is a sorted version of the data set, and is denoted $y_{(1)}, y_{(2)},...,y_{(n)}$ where $y_{(1)} \leq y_{(2)} \leq ... \leq y_{(n)}$. 

There are **three types of numerical measures**:

#### 1. Measures of Location (or Central Tendency)

These are interpretations of the location of the 'centre' of the data, or where data is situated in the number system. There is the:

- ==Sample mean== or ==average==: $\bar{y} = \frac{1}{n} \sum\limits^n_{i=1} y_i$
- ==Sample median==: $\hat{m} = \frac{1}{2}[y_{\frac{n}{2}} + y_{(\frac{n}{2} + 1)}]$ (allows us to find a median when there are an even # of values) 
- ==Sample mode==: value that occurs the most in the data set (may not exist if multiple values occur the most)

#### 2. Measures of Variability (or Dispersion)

These measure the spread, or how clustered or dispersed the values in a data set are. There is the:

- ==Sample variance==: $s^2 = \frac{1}{n-1} \sum\limits^n_{i = 1} (y_i - \bar{y})^2 = \frac{1}{n-1}[\sum\limits^n_{i = 1}(y_i^2) - n\bar{y}^2]$
- ==Sample standard deviation==: $s = \sqrt{s^2}$ (square root of the variance)
- ==Range==: $\text{range} = y_{(n)} - y_{(1)}$ (largest value minus smallest value)
  - Very susceptible to outliers, not the best measurement
- ==Interquartile range (IQR)==: $IQR = q(0.75) - q(0.25)$
  - Much better than the range since it's not affected by outliers
  - 50% of the values in data set should lie in this IQR

#### 3. Measures of Shape

These describe the shape when plotting the data set. There is the:

- ==Sample skewness==: $\frac{\frac{1}{n} \sum\limits^n_{i = 1}(y_i - \bar{y})^3}{[\frac{1}{n}\sum\limits^n_{i = 1}(y_i - \bar{y})^2]^{\frac{3}{2}}}$ (measures the asymmetry of the data)
  - Does not have units
  - **Gaussian** (symmetric) data will have sample skewness close to 0
  - Data with a **long left tail** will have **negative** skewness
  - Data with a **long right tail** will have **positive** skewness
- ==Sample kurtosis==: $\frac{\frac{1}{n} \sum\limits^n_{i = 1}(y_i - \bar{y})^4}{[\frac{1}{n}\sum\limits^n_{i = 1}(y_i - \bar{y})^2]^{2}}$ (measures the concentration of the data in either the peak or the tails) 
  - **Gaussian** data will have sample kurtosis close to 3
  - Data with **larger tails**  will have kurtosis $\gt 3$
  - Data with **smaller tails** will have kurtosis $\lt 3$
  - **Uniform** data will have sample kurtosis close to 1.2



### Five Number Summary

A single value of a measure of the data set is usually not enough to meaningfully summarize it. So, we use the ==Five Number Summary==, usually seen in the form $ a \ \ b \ \ c \ \ d \ \ e$, where:

1. $a =$ the minimum value
2. $b = $ the lower quartile ($q(0.25) $)
3. $c = $ the median 
4. $d = $ the upper quartile ($q(0.75)$)
5. $e =$ the maximum value 



### Reasonability of Using a Gaussian Model

In order to assume that a Gaussian (normal) model distribution is reasonable for a given data set, most if not all of these should be satisfied:

1. The sample mean and median shoudl be approximately equal
2. The sample skewness should be close to 0 ($\pm 1$)
3. The sample kurtosis should be close to 3 ($\pm 1$)
4. Approx. 95% of the data should be in the interval $[\bar{y} - 2s, \bar{y} + 2s]$

Make sure to use words like 'reasonably' and 'approximately' and 'assume' when describing an approximation of data (_ex. ...so it does (not) seem reasonable to assume the data can be modelled by a Gaussian distribution._)!

> Even if one value of the four (or some more we'll learn later) is off, especially if it's off by a lot, it's sufficient usually to disqualify it from being Gaussian.