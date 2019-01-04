__STAT 231 | __ Section 1.1, 1.2

# Empirical Studies

### Key Terms

An ==empirical study== is __a study in which we learn by observation or experimentation.__

A ==unit== is **an individual person, place, or thing which we can measure**.

A ==population== is **a collection of units**.

A ==process== is **a system by which units are produced.**

> Both _populations_ and _processes_ are collections of units, but population is static and processes occur over time.

==Variates== are __characteristics of the units,__ usually represented by variables like $x, y, z$. There are different types:

- ==continuous==: __numerical__ values that can be measured to an infinite degree of accuracy
- ==discrete==: __numerical__ values that can only be a certain number of values
- ==categorical==: __non-numerical__ values that put _variates_ in categories (_ex. hair colour, university choice_)
- ==ordinal==: **non-numerical** values that are categorical, but have an implied order
- ==complex==: __non-numerical__ and not necessarily values, like text or an image

Variates can be separated into two categories: 

1. The ==response variate==, which is the focus of the study; what we're trying to predict or explain
2. The ==explanatory variate==, which can be anything that may affect the response variate

An ==attribute== of a _population_ or _process_ is a __function of a variate which is defined for all units__ (_ex. if the population of interest is all persons aged 18-25 in Ontario, an attribute of interest might be the proportion of the population that owns a smartphone_).

### Types of Empirical Studies

There are three types of empirical studies:

#### Sample Surveys

==Sample surveys== are where information is obtained about a __finite__ population by selecting a __sample__ of units and determining variates of interest for each unit. Since it's finite, the survey is asking __specific questions__ to attempt to find answers about a __complete population__ (_ex. voters voting for a specific party in the next election_) and units usually only **complete the survey once**.

#### Observational Study

==Observational studies== are where information about a **general** population or process is collected without changing any variates. These studies usually try to __observe everything of interest__ to get a general sense of a population of theoretically infinite size, or a population that's conceptual (_ex. amount of people at risk of a disease_). These studies are also **conducted over time instead of at once**.

#### Experimental Study

==Experimental Studies== are where the people conducting the experiment __changes or sets the value of variate(s)__ for the units in the study. These studies are usually easy to distinguish from the above two since it's the **only one where variates are altered**.

> On an exam question, a study could be interpreted correctly as either one of the first two studies as long as reasonable justification is provided.



__STAT 231 | __ Section 1.3

# Empirical Studies (cont.)

### Percentiles, Quantiles, and Quartiles

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



__STAT 231 | __ Section 1.3

# Empirical Studies (cont.)

### Graphical Summaries

There are many different types of graphical summaries, including **histograms, boxplots, scatterplots, etc.**

#### 1. Relative Frequency Histogram

The== relative frequency histogram== is used to compare data to a _p.d.f._; after partitioning the data set into $k$ intervals, it shows the relative frequencies of each interval to each other (the proportion of values in the data set that appear in the interval vs another interval).

#### 2. Boxplot

The ==boxplot== allows us to get information that a histogram does not give us, like a median, the IQR, etc.

![image-20181209153411251](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_1-3-graphs.assets/image-20181209153411251-4387651.png)

It has the following features:

- The box extends from $q(0.25)$ to $q(0.75)$
- The line inside the box represents the **median**
- The upper and lower horizontal lines outside the box connected by tails represent:
  - The smallest observation inside $q(0.25) - 1.5 * IQR$
  - The largest observation inside $q(0.75) + 1.5 * IQR$
- The additional Xs represent **outliers** (values in the data set outside the range of the lines)

It can also tell us the following measures:

- A **longer right/upper tail** indicates **positive skewness** (long right tail), and a **longer left/lower tail** indicates **negative skewness** (long left tail).
- A **median line leaning towards one end of the box** indicates asymmetry!

#### 3. Scatterplot

A ==scatterplot== is used to plot **bivariate** data, with each pair in a value of the data set being represented as the xy-coordinates of the pot.

![image-20181209154114957](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_1-3-graphs.assets/image-20181209154114957-4388074.png)

We want to find if there is a relationship between IQ and brain size in the above chart. We introduce an additional measure to judge **correlation** between two variates: the **sample correlation**, given by:

![image-20181209154241279](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_1-3-graphs.assets/image-20181209154241279-4388161.png)



### Bivariate Categorical Data & Relative Risk

When we have two variates that are both categorical, we can't plot them on a scatterplot, since it would just be four solid points with a bunch of values at that point and categorical data does not have correlation. We introduce the idea of ==relative risk==, which can explain the propability of an occurrence in one category of a variate vs another category in the same variate. 

![image-20181209154957740](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_1-3-graphs.assets/image-20181209154957740-4388597.png)

![image-20181209155008612](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_1-3-graphs.assets/image-20181209155008612-4388608.png)

### Empirical c.d.f

The ==empirical c.d.f.== allows us to compare the distribution of a dataset with a c.d.f. of a random variable.

It is given by: $F(y) = \frac{\text{# of. values in the dataset which are}  \leq  y}{n}$, where $y$ is a variable.

You can use the empirical cdf to compare the same variate value of two or more groups, or you can even use it to check normality by comparing it to the e.c.d.f of a normal data set.

![image-20181209152405722](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_1-3-graphs.assets/image-20181209152405722.png)

__STAT 231 | __ Section 1.4, 1.5

# Data Analysis & Statistical Inference

There are two broad aspects of analysis and interpretation of data:

#### Descriptive Statistics

This is when we take data and portray it in numerical and graphical ways, so we can show the variates or features that we are interested in.

The graphs, charts, tables, in the previous section are all examples of this aspect of data analysis.

#### Statistical Inference

When we use this data to draw conclusions or say something about a population or process, this is ==statistical inference==.  Since we use data about a sample of the population/process, this is __inductive reasoning__ - we're using a specific set of data to infer things about the general population.

> There is also deductive reasoning, where we use general results to prove specific things (kinda the opposite), like using axioms to create proofs of specific theorems in math.

In this course, we examine **3 main types of problems**:

#### 1. Estimation Problems

We want to **estimate** the **attributes** of the population or process. 

Some examples include:

- Estimate the proprtion of STAT 231 students who like poutine
- Estimate the distribution of waiting times at a hospital's ER
- Find a distribution that makes the most sense for a process

#### 2. Hypothesis Testing Problems

After posing a question or hypothesis, we use the data to **assess the truth or validity of the question**.

Some examples include:

- Is it true that a higher proportion of math students than CS students like poutine?
- Will the introduction of a new computer system reduce waiting times at the hospital's ER?

#### 3. Prediction Problems

Use the data to predict a future value of a variate for a unite that is selected from the population or process.

Some examples include:

- Given the past performance of a stock and other data, predict the value of the stock at some point in the future
- Based on the results of a clinical trial, predict how much an individual’s blood pressure would drop for a given dosage of a drug



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

![image-20181209210206335](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-1to2-5.assets/image-20181209210206335-4407326.png)

We can find the ==maximum likelihood estimate==, a point estimate of $\theta$, by maximizimg the function according to the data. For example, if we want to find the maximum likelihood estimate of $\theta$ where we get 10 heads in 25 tosses, we maximize this function with known values substituted:

![image-20181209210428370](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-1to2-5.assets/image-20181209210428370-4407468.png)

We find that the value that maximizes this function is $\hat\theta = 0.4$, which means that **the data are most likely of all $\theta$ when $\theta = 0.4$.**  This is our maximum likelihood estimate, or _m.l. estimate._ Since the above function can help us find the _m.l. estimate,_we call the function a ==likelihood function for $\theta$.==

### Relative Likelihood

We care more about how two values of the parameter compare in terms of making the data more or less likely. This is the ==__relative likelihood__== of one value to another, and we can find a ==__relative likelihood function__== that tells us this:

![image-20181209210957998](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-1to2-5.assets/image-20181209210957998-4407798.png)

This function will always be less than one since the denominator is the **maximum** likelihood estimate, and you'll notice that the constants in the likelihood function will **cancel out**, since **multiplying the likelihood function by a constant will not change its shape.**

### Log Likelihood Function

The ==__log likelihood function__== is defined as:

![image-20181209211316943](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-1to2-5.assets/image-20181209211316943-4407996.png)

where $log = ln$, the natural log. The log likelihood function has the same shape as the likelihood function, plus this will make our algebra much easier when trying to solve for $\hat\theta$.

> Prof. Wallace says :speech_balloon:: easier algebra = happier times :smile:

### Log Relative Likelihood Function

The ==__log relative likelihood function__== is given by:

![image-20181210112554413](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-3.assets/image-20181210112554413-4459154.png)

It's often also easier to compute than the regular relative likelihood function. The maximum value of $r(\theta)$ is $0$.

### Likelihood Function of a Random Sample

If $Y = (Y_1, Y_2, ..., Y_n)$ are independent random variables with the same distribution and probability function $P(Y = y; \theta)$, then the likelihood function for observing a data set $y = (y_1, y_2, ..., y_n)$ from these variables is given by:

![image-20181209211734458](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-1to2-5.assets/image-20181209211734458-4408254.png)

### Invariance Property of Maximum Likelihood Estimates

We can use maximum likelihood estimates for estimating other properties of a data set and a distribution through the ==__invariance property __==:

![image-20181209212106642](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-1to2-5.assets/image-20181209212106642-4408466.png)

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



__STAT 231 |__ Section 2.6



# Q-Q Plots

It's hard for humans to deal with curves in terms of reading them and finding patterns or matching two curves together. By modelling _cumulative distribution functions_ with a ==__QQ plot__==, we can 'straighten' the curves and more easily work with them.

QQ plots are plots of the quantiles of data vs a Gaussian (normal) distribution. In theory, plotting the 1^st^, 2^nd^, ..., 99^th^ quantile of observed data on the $y$-axis and the _theoretical_ quantiles of the normal distributions on the $x$-axis should result in a linear relationship since they _should_ be similar, so we *should* get a straight line.

![image-20181209215120438](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-6.assets/image-20181209215120438-4410280.png)

### Reading a QQ Plot

Apart from a relatively straight QQ plot indicating normal data, we can have 4 main variations:

| Plot                                                         | Meaning                                        |
| ------------------------------------------------------------ | ---------------------------------------------- |
| ![image-20181209215431329](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209215431329-4410471.png) | __Symmetric, low kurtosis__ (less than 3)      |
| ![image-20181209215651007](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209215651007-4410611.png) | __Symmetric, high kurtosis__ (greater than 3)  |
| ![image-20181209215700427](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209215700427-4410620.png) | __Asymmetric, positive skew__ (greater than 0) |
| ![image-20181209215706515](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209215706515-4410626.png) | __Asymmetric, negative skew__ (less than 0)    |



# Checking Fit of a Model

There are multiple ways of checking the fit of a model compared to the observed data.

#### Comparing Expected Frequencies

One method is to calculate the expected frequencies of the data using the assumed model, and then comparing them with observe frequencies (which can be relative or absolute). 

Using a model that is suitable for the data **should yield similar expected frequencies of the data as the frequencies in the data themselves**.

#### Comparing Histograms with Probability Density Functions

This method deals with __continuous__ data, We can create a relative frequency histogram of the data and place the probability density function of the assumed model on top, and **see how well it matches**.

#### Comparing Cumulative Distribution Functions with Empirical Versions

This method also deals with **continuous data**. Recall the definition of the empirical cumulative distribution function:

![image-20181209214354742](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-6.assets/image-20181209214354742-4409834.png)

This is a cumulative distribution function calculated from the set of observed data, and we can compare it to the cumulative distribution function of the assumed model. A model that fits the observed data should have **the _c.d.f_ match the _e.c.d.f_ in terms of fit** pretty well.

#### Reading a QQ Plot

As explained above, QQ plots can indicate if observed data fits a normal distribution model.

![image-20181209220020636](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-6.assets/image-20181209220020636-4410820.png)

![image-20181209220029154](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_2-6.assets/image-20181209220029154-4410829.png)



__STAT 231 | __ Section 3.0 (all of Chapter 3)

# PPDAC Algorithm

The steps of this algorithm are:

- **Problem:** A clear statement of the study's objectives.
- **Plan:** The procedures used to carry out the study, including how the data will be collected, what steps to take to measure them, etc.
- **Data:** The physical collection of the data, as described in the **Plan** step.
- **Analysis**: The analysis of the data collected, taking into account the **Problem** and the **Plan**.
- **Conclusion**: The conclusions that are drawn about the **Problem** and their limitations.



### Error in Studies

![image-20181211111458568](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_3_PPDAC.assets/image-20181211111458568-4544898.png)



### Things To Consider for PPDAC

1. What **type of study** is this and why?

   > Think about if the researchers changed/controlled any variates. If so, then it's very likely observational. If there's a survey mentionef in the study, a sample survey is also very likely.

2. Define the **Problem** for this study.

   > What are the researchers themselves trying to find out? Look for a quote or a conclusion in the article.

3. Is the type of **Problem** descriptive, causative, or predictive? Explain why.

4. What are the $n$ most important **variates** in this study and what is their type?

   > What is being measured?

5. Define a suitable **target population** for this study.

   > Who are the researchers interested in studying? If nothing is explicitly stated, look at who the study consisted of and extrapolate to a larger population. Make sure you're being as specific as possible.

6. Define a suitable **study population** for this study.

   > Note that the __units in the study population may be systematically different to units in target population in terms of some attribute__!
   >
   > As well, the study population is always a subset of the target population (most of the time it's a strict subset).

7. Give a possible source of **study error** for this study in relation to your answers to to 5) and 6).

8. What information is given about the **sampling protocol** for this study?

   > You don't have to reshape the description with your own words; precision matters more so you can reuse the wording in the original article if it answers the question.

9. Give a possible source of **sample error** for this study based on the information you have stated in 8).

10. What type of **numerical summary** is `some number they mentioned`?



__STAT 231 |__ Section 4.1, 4.2

# Parameter Estimates and Estimators

When we take a sample of a population and find an _m.l._ estimate of a parameter, the sample we take is usually a random sampling. 

We can think of the sample we take, and its resulting sample estimate, as a concrete value of a __random variable__. If we take samples over and over, known as ==__repeated sampling__==, we'll keep getting different estimates. 

> Note that we can't really expect to do this in real life - this is just a concept.

The parameter we're estimating then itself can be modeled with a probability distribution that has its own mean and variance. _For example, if the parameter we are estimating is the sample mean of a model $Y \sim G(\mu, \sigma), i = 1, 2, ..., n$ independently, with observed data $y_1, y_2, ..., y_n$, the sample mean would follow a distribution, and the m.l. estimate of that distribution is $\bar y = \hat \mu$._ 

For large values of $n$, $\hat \mu$ would be very close to the true value of $\mu$ (but remember, they're very very likely not the same).

Recall that a ==point estimate of a parameter $\theta$==, denoted $\hat\theta$, is the value of a function $\hat\theta(y) = g(y_1, y_2,...,y_n)$ where $y$ is a set of observed data $(y_1, y_2, ..., y_n)$. So, varying sets $y$ will have different associated $\hat \theta$ values. This means that we can associate with the point estimate

![image-20181210003202483](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4.1+4.2.assets/image-20181210003202483-4419922.png)

a random variable 

![image-20181210003153680](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4.1+4.2.assets/image-20181210003153680-4419913.png)

where instead of observed values $y_1, ..., y_n$, we have random variables $Y_1, ..., Y_n$. This is known as a ==__point estimator__==, a random variable that processes data to give us an estimate of an unknown parameter $\theta$.

With this definition, the value $\hat \theta$ is a value obtained from $\tilde \theta$ by 'plugging in' the data set $(y_1, y_2, ..., y_n)$ obtained from $(Y_1, Y_2, ..., Y_n)$.

Since $\tilde \theta$ is a random variable, it has a distribution! This is known as the __sampling distribution of the estimator.__ To find this distribution, brute force often doesn't work - we can't just enumerate through all possible sets of $n$ size and compute the parameter for each and plot it to get the probability function for $Y$ in most cases. 

We need to __use the Central Limit Theorem__, which tells us:

![image-20181210001443789](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4.1+4.2.assets/image-20181210001443789-4418883.png)

We can apply this to the estimator, which takes in $Y_1, Y_2, ..., Y_n$ random variables, so by computing $\bar Y$, $\sigma, $ and $\mu$, we can compute a _new_ random variable that follows the $G(0, 1)$ distribution. 

Another fact is that __as $n$ gets larger and $\sigma $ gets smaller, the $sd(\bar Y)$ gets smaller.__ Since $sd(\bar Y)$ measures how close each value of $\bar Y$ is to the mean $\mu$,  the smaller it is, the more accurate our estimates obtained through $Y$ are!

Knowing these two pieces of information, we can calculate things like how large $n$ must be or how small $\sigma$ must be to ensure our estimate is at maximum some value off from the true $\mu$. 

> The true mean $\mu$ does not affect how many of the sample estimates are close to it, since they are all relative to the true $\mu$ - essentially, a change in position of $\mu$ will shift the estimates as well.



__STAT 231 |__ Section 4.3

# Interval Estimation

We know that our estimate of a parameter, $\hat \theta$, is likely not the true value of $\theta$. So, how good is our estimate and how can we quantify the uncertainty of our estimate?

We can give an interval of values for $\theta$ that are 'supported' by the observed data where we got $\hat \theta$. We use an __interval estimate__ of the form $[L(y), U(y)]$, where both values are functions of the observed data $y$. 

### Interval Estimates & Likelihood Intervals

An interval estimate that can give us 'reasonable' values of the unknown parameter is a __likelihood interval__. By using the relative likelihood function $R(\theta) = \frac{L(\theta)}{L(\hat\theta)}$, we can construct a ==__100p% likelihood interval__== for the parameter $\theta$ like so:

1. Define a set of values $A$ of $\theta$ where $R(\theta) \geq p$.

   - Recall that as $R(\theta)$ approaches 1, the values of $\theta$ that result in those large values of $R(\theta)$ are the most plausible. So, this set of values will contain values of $\theta$ that are _at least_ 100p% as likely as when $\theta = \hat\theta$.

     _Ex. For a 50% likelihood interval, the set will contain values that are at least 50% as likely as $\hat\theta$._

2. Find values of $\theta$ where $\theta \in A$. This is hard to do manually, and in general will be **computed by software** like `R`.  

3. **Graph the relative likelihood function*** and draw a line at $y = p$. The intersections of this line with the $R(\theta)$ curve will give us the lower ($L(\theta)$) and upper ($U(\theta)$) bounds of the likelihood interval.

   _*We can also do this with the log relative likelihood function ($r(\theta) $). Instead of drawing the line at $y = p$, we draw the line at $y = log(p)$. The rest of the steps are the same._

![image-20181210112433658](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-3.assets/image-20181210112433658-4459073.png)

### Interval Estimators & Coverage Probability

Much like a point estimate and a point estimat__or__, an interval estimator is a rule that allows for many different intervals of plausible values of $\theta$ to be constructed. If $Y = (Y_1, Y_2, ..., Y_n)$ is a random variable of all the data that can be observed, then $[L(Y), U(Y)]$ is an ==__interval estimator__== that can produce _interval estimates_ (note the difference in $Y$ vs $y$! ).

To determine how good our interval estimator is at finding plausible values of $\theta$, we use the ==__coverage probability__== of the interval estimator:

![image-20181210113601874](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-3.assets/image-20181210113601874-4459761.png)

We want to find interval estimators where:

1. The coverage probability is large (usually 0.9, 0.95, or 0.99)
2. The interval is as narrow as possible

It's hard to get these two criteria to agree, since **increasing the coverage probability will increase the size of the likelihood interval**; thus, we often fix the coverage probability at a set value and then try to find the narrowest interval by moving the lower and upper bounds around (as long as the probability doesn't drop below the set value).



__STAT 231 |__ Section 4.4

# Confidence Intervals

A ==__100$p$% confidence interval__== for a parameter is an interval estimate $[L(y), U(y)]$ for which:

![image-20181210120011379](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210120011379-4461211.png)

and $p$, in this case, is known as a __confidence coefficient__ for the interval.

We say that for a sample, we are '$100p$% confident' that the true value of $\theta$ is in the interval that we constructed.

`Caution:` The true value of $\theta$ is __not__ a random variable - it is an unknown __constant__ and therefore does not have a distribution. This is why we _cannot define a confidence interval to be the probability that the true value of $\theta$ lies in the interval, since_ the __true value of $\theta$ is either in the interval or not in the interval. It's a constant.__



### Likelihood vs. Confidence Intervals

A 100$p$% likelihood interval tells us that values of $\theta$ inside the interval are at least $100p$% as plausible as the ml estimate $\hat \theta$ (that $R(\theta) \geq p$). 

A $100p$% confidence interval, tells us that, constructing multiple intervals from $[L(Y), U(Y)]$, we expect $100p$% of these intervals to contain the true (unknown) value of $\theta$ (and that $100(1-p)$% of the intervals are expected not to contain it).



### Calculating a Confidence Interval

Usually, we are only able to construct one interval (_think back to repeated sampling and why it's usually just a concept_), and we hope that the interval we construct is one that falls in the good $100p$%. 

To construct one, take the following for a Gaussian model as an example:

1. Get a random sample $(Y_1, Y_2, ..., Y_n)$ from a $G(\mu, 1)$ distribution where $E[Y_i] = \mu$ is our unknown parameter, and $sd(Y_i) = 1$ is known. 
2. For the random interval: ![image-20181210120514828](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210120514828-4461514.png), we have ![image-20181210120533744](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210120533744-4461533.png), since we expect that approx. 95% of a sample is within 2 s.d. of the mean $\bar Y$.
3. Then, the interval:![image-20181210120604539](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210120604539-4461564.png) with observed *sample* mean $\bar y$ is a $95$% confidence interval for the unknown mean $\mu$ of the *population.*



   `Caution`: Again, with this example, we illustrate the difference between $\bar Y$ and $\bar y$. Suppose that $n = 16$. Then, by calculation, a 95% confidence interval for $\mu$ is ![image-20181210121516352](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210121516352-4462116.png)but we cannot say that $P(\mu \in [9.91, 10.89]) = 0.95$. This is because $\bar Y$ is a random variable, and that allows us to say that repeatedly taking intervals resulting from $\bar Y$ will give us an overall probability $p$ that $\mu$ lies in all those intervals. $\bar y$ is a specific value, so the first `Caution` above applies.



### Relationship Between Sample Size, Confidence Level, and Variance

As confidence level increases, the confidence interval gets wider.

As sample size increases, the confidence interval gets narrower.

As sample standard deviation increases, the confidence interval gets wider.

As population variance increases, the confidence interval gets wider.

As the unknown parameter we are finding the interval for changes, the confidence interval __stays the same width.__



# Pivotal Quantities

A ==__pivotal quantity__== is a function of the data $Y$ and the unknown parameter $\theta$ such that the distribution of the random variable $Q$ is completely known. 

_For example..._

![image-20181210130917020](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210130917020-4465357.png)

![image-20181210130928635](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210130928635-4465368.png)

Pivotal quantities are useful for constructing 100$p$% confidence intervals. We can use them as follows:

1. Find numbers $a, b$ such that $P(a \leq Q(Y; \theta) \leq b) = p$.
   _For symmetric distributions, we want to find a number $a$ such that $P(-a \leq Q \leq a) = p$. This allows us to obtain the narrowest confidence interval, which is the best one._
2. Isolate for $\theta$ in $Q(Y; \theta)$ to get an inequality of the form $L(Y) \leq \theta \leq U(Y)$.
   Then, $p = P(a \leq Q(Y; \theta) \leq b) = P(L(Y) \leq \theta \leq U(Y))$, which means the coverage probability is $p$.
3. Using observed data $y$ in place of $Y$, the interval $[L(y), U(y)]$ is a 100$p$% confidence interval for the unknown parameter $\theta$.



_Algorithm to find confidence interval of $\mu$ for Gaussian data where $\sigma$ is known:_

1. Use normal tables or `R` to find $a$ such that $P(-a \leq Z \leq a) = p$ where $Z \sim G(0, 1)$. In otherwords, such that $P(Z \leq a) = \frac{1 + p}{2}$.
2. A 100$p$% confidence interval for $\mu$ is then $\bar y \pm a \frac{\sigma}{\sqrt{n}}$.



### Helpful `R` Functions

`pnorm(y, mu, sigma)`: gives us the $P(Y \leq y)$ where $Y \sim G(mu, sigma)$. `mu` and `sigma` default to 0 and 1.

`qnorm(y, mu, sigma)`: gives us $a$ where $P(Y \leq y) = a$, and $Y \sim G(mu, sigma)$. Same defaults as `pnorm`.



### Approximate Pivotal Quantities & Approximate Confidence Intervals

In a lot of models, it's hard or not possible to find exact pivotal quantities or confidence intervals for $\theta$.

However, we can find ==__approximate pivotal quantities__==, which are random variables $Q_n = Q_n(Y_1, Y_2, ..., Y_n; \theta)$ where as $n \rightarrow \infty $, distributions no longer depend on unknown information like $\theta$ or elsewise.

_see course notes for all approximations of different models_



### Sample Size Calculation

A sample size, as shown before, affects the confidence intervals for an unknown parameter. More specifically, as the sample size increases, the confidence intervals get narrower. So, oftentimes we will want to find the smallest sample size $n$ such that we have a 100$p$% confidence interval.

Suppose we want to estimate $\theta$ with a sample size of $n$. We want to use the 95% confidence interval, given by

![image-20181210135513596](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210135513596-4468113.png)

The width of this interval is 

![image-20181210135533559](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210135533559-4468133.png)

and if we want a width of $\leq  2l$, then 

![image-20181210135603396](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-4.assets/image-20181210135603396-4468163.png)

We just need the maximum value of $\hat \theta$ so we can calculate the worst case scenario to get a lower bound for $n$ in order to maintain the 95% confidence interval.



__STAT 231 |__ Section 4.5

# Chi-squared Distributions

The Chi-squared distribution is parameterized by its __degrees of freedom__, often denoted $k$.

The value of $k$ affects the shape of the resulting probability density function:

![image-20181210140125209](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-5.assets/image-20181210140125209-4468485.png)

### Properties

==If $W_1, W_2, ..., W_n$ are independent random variables with $W_i \sim \chi^2_{k_i}$, then==

![image-20181210140242260](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-5.assets/image-20181210140242260-4468562.png)

_i.e. the sum of chi-squared random variables also follows a chi-squared distribution with its degrees of freeedom being the sum of the degrees of freedoms of itscomponent distributions._

_ex. if $W_1 \sim \chi^2_2, W_2 \sim \chi^2_3$, then $W_1 + W_2 \sim \chi^2_5$._

------

==If $Z \sim  G(0, 1)$, then $Z^2 = W \sim \chi^2_1$.==

_i.e. the square of a standard normal distribution has chi-squared distribution with 1 degree of freedom._

This means that if $W \sim \chi^2_1$, then

![image-20181210140708001](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-5.assets/image-20181210140708001-4468828.png)

allowing us to use standard normal tables and `R ` to compute probabilities with a $\chi^2_1$ distribution.

![image-20181210140839307](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-5.assets/image-20181210140839307-4468919.png)

![image-20181210141036488](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-5.assets/image-20181210141036488-4469036.png)



------

==If $W \sim \chi^2_2$, then $W \sim Exponential(2)$.==

_i.e. a chi-squared distribution with 2 degrees of freedom is the same as an exponential distribution with parameter 2._

So, if $W \sim \chi^2_2$, then

![image-20181210141015008](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-5.assets/image-20181210141015008-4469015.png)



__STAT 231 | __Section 4.6

# Relating Likelihood Intervals & Confidence Intervals

In Section 4.4, we were able to calculate confidence intervals using pivotal quantities or approximate pivotal quantities. Now we can show that likelihood intervals are also a form of confidence intervals.

If we replace the maximum likelihood estimate $\hat \theta$ in the relative likelihood function with a maximum likelihood estimator $\tilde \theta$ to define the random variable $\Lambda(\theta)$:

![image-20181210141905800](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-6.assets/image-20181210141905800-4469545.png)

This is the ==__maximum likelihood statistic__==. For large $n$, we can show that $\Lambda \sim \chi^2_1$, and by the second property in Section 4.4, we know this is a pivotal quantity; which means that it can be used to obtain confidence intervals for $\theta$.



### Approximating a Confidence Interval Using Likelihood

We can approximate a 100$q$% confidence interval for $\theta$ using likelihood with this:

![image-20181210142230731](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-6.assets/image-20181210142230731-4469750.png)

So, to **convert a confidence interval to a likelihood interval**:

==__Theorem:__ A 100$q$% confidence interval is an approximate 100$p$% likelihood interval where $p = e^{-c/2}$ and $q = P(|Z| \leq \sqrt{c}) = 2P(Z \leq \sqrt{c}) - 1 , Z \sim N(0, 1) $.==

1. Identify the appropriate $c$ for the desired confidence interval $p$ by choosing $c$ such that $p = P(W \leq c) = P(|Z| \leq \sqrt{c})$.
2. The likelihood interval is all $R(\theta) \geq e^{-c/2}$, so it is a 100$(e^{-c/2})$% confidence interval.

Inversely, to **convert a likelihood interval to a confidence interval**:

==__Theorem:__ A 100$p$% likelihood interval is an approximate 100$q$% confidence interval where $q = 2P(Z \leq \sqrt{-2log(p)}) - 1$ and $Z \sim N(0, 1)$.==



This gives us an additional technique to approximate confidence intervals for distributions like Binomial where we cannot find an exact pivotal quantity: **find the corresponding likelihood interval and convert it to a confidence interval**!



__STAT 231 | __Section 4.6

### Gaussian Data with Unknown $\mu, \sigma$

In our previous examples with calculating  confidence intervals for the mean $\mu$ of Gaussian data, $\sigma$ is always a known value. This is an assumption, and often we won't know this value.

Suppose $Y_1, Y_2,..., Y_n$ is a random sample from a $G(\mu, \sigma)$ distribution where both $\mu = E(Y_i)$ and $sd(Y_i) = \sigma$ are both __unknown.__

The maximum likelihood estimator $\tilde \mu = \bar Y$ can still be used to estimate $\mu$. We use a point estimator for $\sigma^2$ to be

![image-20181210151114532](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151114532-4472674.png)

beecause $E[S^2] = \sigma^2$.

So now, the pivotal quantity (which isn't a pivotal quantity anymore because $\sigma$ is unknown)

![image-20181210151151353](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151151353-4472711.png)

can be used again once we replace $\sigma$ with $S$ to get 

![image-20181210151226560](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151226560-4472746.png)

This is a new distribution: a ==__Student's $t$ distribution.__==



### Student's $t$ Distributions

A random variable $T$ is said to have a __Student's $t$ distribution__ (or simply a $t$ distribution) if its _pdf_ is

![image-20181210151333009](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151333009-4472813.png)

where the constant $c_k$ is (with $\Gamma$ being the gamma function):

![image-20181210151347828](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151347828-4472827.png)

The $t$ distribution is **symmetric about zero**. The parameter $k$ is also known as the __degrees of freedom__, and we denote $T \sim t(k)$, or $T \sim t_k$.



### Finding a Confidence Interval for $\mu$

We can use the distribution ![image-20181210151226560](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151226560-4472746.png)as a pivotal quantity to construct a confidence interval for $\mu$.

To find a 100$p$% confidence interval for $\mu$, when $\sigma$ is unknown:

1. Since the $t$ distribution is symmetric, we look for a value $a$ from $t$ tables such that

   ![image-20181210151710062](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151710062-4473030.png)

   where $T \sim t_{n-1}$. Since we also know ![image-20181210151819929](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151819929-4473099.png)by sustituting this into the above inequality, we have

   ![image-20181210151906981](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151906981-4473147.png)

2. Isolate for $\mu$ like we do when finding a normal confidence interval, to obtain

   ![image-20181210151949268](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151949268-4473189.png)

3. Then, ![image-20181210151959754](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210151959754-4473199.png) is a 100$p$% confidence interval for $\mu$.

==Compared to using the normal distribution, the confidence interval found with a $t$ distribution with unknown $\sigma$ is **wider** than an interval found with the normal.==



### Helpful `R` Functions

`pt(t, df)`: gives us the $P(T \leq t)$ where $T \sim t_{df}$. There is no default value for `df`.

`qt(t, df)`: gives us $a$ where $P(T \leq t) = a$, and $T \sim t_{df}$. No default value for `df`.



### Sample Size Calculation, $\sigma$ unknown

We solve this in the same way as calculating the sample size $n$ in Section 4.4: find the width of the interval, set it equal to our desired width, solve for $n$. However, since this is for Gaussian data, we have that $\sigma$ is estimated by $s$, our sample standard deviation.



### Finding a Confidence Interval for $\sigma^2, \sigma$

We can use the following theorem:

![image-20181210154417375](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210154417375-4474657.png)

Since this random variable is a function of the data $Y_1, Y_2, ..., Y_n$, and its distribution is completely known, this is a pivotal quantity and we can use it to construct a confidence interval.

To costruct a 100$p$% confidence interval for $\sigma^2$ when $\mu$ is unknown:

1. Find values $a, b$ such that $P(a \leq W \leq b) = p$, where $W \sim \chi^2_{n - 1}$.

   To find this, we need to find $P(W \leq a) = (1 - p)/2$  and $P(W \gt b) = (1-p)/2$ (or $P(W \leq b) = (1+p)/2$).

2. Since $W \sim \chi^2_{n - 1}$ and ![image-20181210155004932](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210155004932-4475005.png)we can write that

   ![image-20181210155041073](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210155041073-4475041.png)

3. Isolate for $\sigma^2 $ to get

   ![image-20181210155224309](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210155224309-4475144.png)

   This confidence interval is __not__ symmetric about $s^2$, the point estimate of $\sigma^2$.

4. To find a  confidence interval for $\sigma$ instead of $\sigma^2$, we have that

   ![image-20181210155551055](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_4-7.assets/image-20181210155551055-4475351.png)





### Helpful `R` Functions

`pchisq(w, df)`: gives us the $P(W \leq w)$ where $W \sim \chi^2_{df}$. There is no default value for `df`.

`qchisq(w, df)`: gives us $a$ where $P(W \leq w) = a$ and $W \sim \chi^2_{df}$. There is no default value for `df`.



__STAT 231 |__ Section 5.1

# Hypothesis Testing

In hypothesis testing, we aim to collect data to prove or disprove a hypothesis.

We usually begin by specifying a single default hypothesis - this is called the ==__null hypothesis__==, denoted $H_0$. There is also an ==__alternate hypothesis__==, denoted $H_A$ or $H_1$ (often, this is simply the statement that $H_0$ is not true).

_Example: testing if US coins are biased to one side when tossed._

![image-20181210160529728](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-1.assets/image-20181210160529728-4475929.png)

![image-20181210160557129](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-1.assets/image-20181210160557129-4475957.png)

However, it's hard to define how close is 'close enough'  to our $H_0$ to conclude that $H_0$ is true. To measure this, we have to use a ==__test statistic__==, also known as a ==__discrepancy measure__==.

==A test statistic or discrepancy measure is a function of the data $D = g(Y )$ that is constructed to **measure the degree of ‘agreement’** between the data $Y$ and the null hypothesis $H_0 $.==

Usually, $D=0$ represents the best possible agreement between the data and $H_0$, whereas large values of $D$ indicate poor agreement.



### P-values

We care more about the probability of observing a value of $D$ greater than or equal to that observed when we ran an experiment once, assuming the null hypothesis is true. The probability $P(D \geq d)$ is the $p$-value of the test of the hypothesis.

A small _p-value_ tells us that if the null hypothesis were true, it would be __unlikely__ to have observed **data as weird or more weird** than the data we actually observed.



### Hypothesis Testing for Binomial parameters

We can calculate $P(D \geq d)$ to get the $p$-value, or we can use the Normal approximation to the Binomial for large $n$.

![image-20181210163953155](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-1.assets/image-20181210163953155-4477993.png)





### Hypothesis Testing Recipe

![image-20181210161722543](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-1.assets/image-20181210161722543-4476642.png)

![image-20181210162205521](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-1.assets/image-20181210162205521-4476925.png)

### Notes About Hypothesis Testing

**Disproving vs. proving hypotheses:** While hypotheses can be disproved by showing a difference or small $p$-value from the null hypothesis, it hs not possible to do the same for proving it. You can only say that there is _no evidence against $H_0$ in light of the observed data._

**Magnitude of difference when disproving hypotheses:** A hypothesis could be wrong, but only off by a slight amount, or it could be wrong and off by miles. You should always have a measurement of magnitude in terms of how 'off' $H_0$ is from your observed results.

**Statistical Significance vs. Practical Significance**: While we might be able to find evidence of a *statistically* significant difference against a hypothesis, it doesn't mean in the real world that it would be *practically* significant. 
_ex. if insurance finds that values of policies sold in 2 years differ by $5.32, it would not mean a lot to them as the value of each policy is orders of magnitudes bigger, like \$1000._



__STAT 231 |__ Section 5.2

# Hypothesis Testing for $G(\mu, \sigma)$ parameters

We know we can estimate parameters in the $G(\mu, \sigma)$ distribution. 

Now, we can test $H_0: \mu = \mu_0$, that the true mean of the distribution equals some value $\mu_0$.

We can also conduct a similar test for the variance: $H_0: \sigma^2 = \sigma^2_0$.

### Hypothesis Testing & Confidence Intervals

The $p$-value for testing $H_0: \mu = \mu_0$ is greater than or equal to $p$ _iff_ the value $\mu = \mu_0$ is inside a 100$(1-p)$% confidence interval.

So, a $p$-value $\geq 0.05$ means that $\mu = \mu_0$ will not be in a 95% confidence interval, and vice versa.

### Testing $H_0: \mu = \mu_0$, $\sigma$ unknown

![image-20181210164955780](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-2.assets/image-20181210164955780-4478595.png)

![image-20181210165106142](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-2.assets/image-20181210165106142-4478666.png)

### Testing $H_0: \sigma^2 = \sigma^2_0$, $\sigma$ unknown

![image-20181211114634527](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-2_hypotest_gaussian_params.assets/image-20181211114634527-4546794.png)



__STAT 231 | __Section 5.3

# Likelihood Ratio Tests

### General Single Parameter $p$-value & Likelihood Ratio Test

![image-20181210173458722](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-3.assets/image-20181210173458722-4481298.png)

We can then calculate the observed value of $\Lambda(\theta_0)$, denoted by $\lambda(\theta_0)$:

![image-20181210175107807](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-3.assets/image-20181210175107807-4482267.png)

![image-20181210175004017](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-3.assets/image-20181210175004017-4482204.png)



### Binomial 

![image-20181210173201918](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_5-3.assets/image-20181210173201918-4481121.png)

### Other Distributions & Models

_follow the general model defined in the first part_



__STAT 231 |__ Section 6.1

### Gaussian Response Model

A ==__Gaussian response model__== allows for the parameters of the Gaussian distribution ($\mu, \sigma$) to depend on a vector of __covariates__ which are explanatory variates for the response variate $Y$. 

Formally:

![image-20181210231926047](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1.assets/image-20181210231926047-4501966.png)

Most of the time, we'll make $\sigma(x_i) = \sigma$ a constant, which makes the models easier to analyze. So, the value of $\mu(x)$ is determined by the function itself and the covariates $x$.



### Linear Regression Model

Often, we assume $\mu(x_i)$ is a linear function of the covariates; these are known as ==__linear regression models__== and can be written as:

![image-20181210232134601](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1.assets/image-20181210232134601-4502094.png)

where $x_i = (x_{i1}, x_{i2}, ..., x_{ik})$ is the vector of known covariate _constants_ associated with the $i^{th}$ random variable (a unit), and $\beta_0, \beta_1, ..., \beta_k$ are unknown parameters known as __regression coefficients.__

#### Example: STAT 230/231 Grades

Let's examine the plot of grades students received in STAT 230 vs the ones they received in STAT 231.

![image-20181210232551345](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1.assets/image-20181210232551345-4502351.png)

We can see that the relationship between $x, y$ don't vary as much when $x$ increases or decreases (it's a relatively linear relationship). 

Assume a model in which $\mu(x) =$ mean STAT 231 final grade, with $x$ being their final grade in STAT 230. Then, since the mean STAT 231 final grade of each final STAT 230 grade will form a line, we can say that

![image-20181210232909105](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1.assets/image-20181210232909105-4502549.png)

where $\alpha, \beta$ are unknowns and $x$ is a known constant (the STAT 230 final grade). To extend this to more than just one STAT 230 final grade, we look at multiple $x$ values.

![image-20181210232956086](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1.assets/image-20181210232956086-4502596.png)

$\sigma$, which we assumed to be the same for each $Y_i$, represents the variability in the response variate $Y$ in the study population for each value of the explanatory variate $x$.



__STAT 231 |__ Section 6.1

# Estimates of $\alpha, \beta$  

### Least Squares Estimate

__Question:__ which line is the best fitting line to this graph of data?

![image-20181210230232214](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230232214-4500952.png)

We define the distance between a fitted line and the data by __residuals.__ We try to find a fitted like $y = \alpha + \beta x$ which minimizes the sums of squares of the distances between the observed points and the fitted line. 

Estimates of $\alpha, \beta$, denoted $\hat \alpha, \hat \beta$, are called the ==__least squares estimate__==.

Formally, we find $\hat \alpha, \hat\beta$ which minimize:

![image-20181210230543506](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230543506-4501143.png)

![image-20181210230900028](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230900028-4501340.png)

![image-20181210230906775](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210230906775-4501346.png)

![image-20181210231015868](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210231015868-4501415.png)

![image-20181210231021251](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-2.assets/image-20181210231021251-4501421.png)

### Maximum Likelihood Estimate

We can also use maximum likelihood estimation.

Since our model is 

![image-20181210234504240](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210234504240-4503504.png)

and we know the likelihood function for a distribution is

![image-20181210234524909](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210234524909-4503524.png)

then we know that 

![image-20181210234547692](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210234547692-4503547.png)

and we want to maximize it by minimizing

![image-20181210234609724](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210234609724-4503569.png)

but then this is just the least squares problem, with the estimate being the **same as the least squares estimate** above:

![image-20181210234806609](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210234806609-4503686.png)





### Distribution of $\tilde \alpha, \tilde \beta$ Estimators

We have shown that the least squares and maximum likelihood estimate of $\beta$ is given by

![image-20181210234934347](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210234934347-4503774.png)

and so a corresponding estimat__or__ would be

![image-20181210234950511](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210234950511-4503790.png)

_note the change in uppercase $Y_i$, making it a random variable_



Then, a theorem tells us that if

![image-20181210235046146](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235046146-4503846.png)

independently, where the $x_i$ for $i = 1, 2, ..., n$ are known constants, then 

![image-20181210235113463](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235113463-4503873.png)

where $\tilde \beta$ is the equation above (second in this section).



### Pivotal Quantity of $\beta$

![image-20181210235234117](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235234117-4503954.png)



### Confidence Interval for $\beta$

Like mentioned in the previous part, we don't know $\sigma$, so we estimate $\sigma^2$ using

![image-20181210235437105](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235437105-4504077.png)

or more easily,

![image-20181210235448878](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235448878-4504088.png)

Note the following theorem:

![image-20181210235549374](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235549374-4504149.png)

![image-20181210235607270](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235607270-4504167.png)

So, a 100$p$% confidence interval for $\beta$ is given by:

![image-20181210235635632](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235635632-4504195.png)

where $P(T \leq a) = (1+p)/2$, and $T \sim t_{n - 2}$.



### Hypothesis Testing $\beta = \beta_0$ and the Hypothesis of No Linear Relationship

For testing $H_0: \beta = \beta_0$, the $p$-value is

![image-20181210235749284](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181210235749284-4504269.png)

where $T \sim t_{n -2}$. 

We can **test $H_0: \beta = 0$ to show that $\mu(x)$ does not depend on $x$,** since $\mu(x) = \alpha + \beta x$. This tells us that there is __no linear relationship__ between the variates $Y$ and $x$.



### Confidence Interval for $\mu(x) = \alpha  + \beta x$

By the Invariance Property, we know that the maximum likelihood estimator of $\mu(x)$ is the random variable

![image-20181211000039912](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211000039912-4504439.png)

and we can find a distribution for $\tilde \mu(x)$, which will let us construct a confidence interval for the mean response. It takes some effort, so we just give the confidence interval as follows.

A 100$p$% confidence interval for $\mu(x) = \alpha + \beta x$ is

![image-20181211000150547](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211000150547-4504510.png)

_Note that this is basically the same argument we had for deriving a confidence interval for $\beta$ above._



### Confidence Interval for the intercept $\alpha$

![image-20181211000241621](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211000241621-4504561.png)



### Confidence (Prediction) Interval for a new response variate $Y$ at $x$

The 100$p$% prediction interval for a new response variate $Y$ at $x$ is given as

![image-20181211000507500](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211000507500-4504707.png)





# Checking Model Assumptions

There are two main assumptions we make for Gaussian linear response models:

1. $Y_i$ (given covariates $x_i$) has a Gaussian distribution with standard deviation $\sigma$ which does not depend on any of the covariates.
2. $E[Y_i] = \mu(x_i)$ is a linear combination of known covariates $x_i = (x_{i1}, ..., x_{ik})$ and the known regression coefficients $\beta_0, \beta_1, ..., \beta_k$.

We can check these assumptions using graphical methods like:

### Scatterplot with data + fitted line

![image-20181211000902868](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211000902868-4504942.png)

To check the two assumptions with this method, respectively:

1. Are the points generally spread out to the same extent regardless of their $x$-position?
   This shows if $\sigma$, the standard deviation of the points, depends on $x$.
2. Do the points seem to fit reasonably along a straight line (the fitted line helps here)?
   This shows if $E[Y_i]$ is following $\mu(x_i)$, the linear function line of $x$



### Residual plots of $(x_i, \hat r_i)$

We can define $\hat r_i = y_i - \hat \mu_i$, where $\hat \mu_i = \hat \alpha + \hat \beta x_i$. These are called __residuals__ since they represent what is 'left over' after the estimate based on the model has been 'fitted' to the observed data ($y_i $).

 Also note:

![image-20181211001310114](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211001310114-4505190.png)

We see that...

![image-20181211001342796](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211001342796-4505222.png)

![image-20181211001643800](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211001643800-4505403.png)





### Standardized Residual Plots of $(x_i, \hat r^*_i)$

This plot can be interpreted in the same way, but we define the __standardized residuals__ to be

![image-20181211001534588](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211001534588-4505334.png)

so the plot will be 'scaled' compared to a normal residual plot. The $\hat r^*_i$ values should be in the range (-3, 3). The following plot is the same as the above, but standardized:

![image-20181211001635296](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211001635296-4505395.png)

### Standardized Residual Plots of $(\hat u_i, \hat r^*_i)$

There is also an __alternate__ form of this plot, where we plot the mean instead to check if the __assumed mean $\mu(x) = \alpha + \beta x$ is reasonable__. 

If it is, we should see a horizontal band around the like $\hat r^*_i = 0$.

![image-20181211001925573](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211001925573-4505565.png)

### QQ Plots of Standardized Residuals

A QQ plot of the $\hat r^*_i$ should give approximately a **straight line if the assumption of a Gaussian model holds**:

![image-20181211002027200](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211002027200-4505627.png)

![image-20181211002032568](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-1+6-2.assets/image-20181211002032568-4505632.png)



__STAT 231 | __Section 6.3

# Comparing Means of Two Populations

We sometimes are interested in comparing variates of two different populations. We can define 

![image-20181211003455716](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003455716-4506495.png)

and 

![image-20181211003501580](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003501580-4506501.png)

Note that we have defined $\sigma$ to be the same for both models.

This is known as a __two sample Gaussian problem__. It can be shown to be a special case of the Gaussian response model. 

### Point Estimators of Means $\mu_1, \mu_2$

The maximum likelihood estimator of $\mu_1$ is

![image-20181211003337976](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003337976-4506417.png)

and the equivalent for $\mu_2$ is

![image-20181211003356106](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003356106-4506436.png)

and also...

![image-20181211003408721](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003408721-4506448.png)



### Point Estimator of $\sigma$

We need to define the point estimator of $S_1^2$, which estimates $\sigma^2$ based only on $Y_{1i}$:

![image-20181211003636921](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003636921-4506596.png)

and another estimator for $S_2^2$, which estimates $\sigma^2$ based only on $Y_{2i}$:

![image-20181211003715246](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003715246-4506635.png)

and finally we can find the point estimator for $\sigma^2$:

![image-20181211003734028](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211003734028-4506654.png)



### Confidence Interval of Difference in Means (Equal Variances)

![image-20181211004017727](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211004017727-4506817.png)



### Confidence Interval of Difference in Means (Unequal Variances)

If the variance or standard deviation is not the same, but $n_1, n_2$ are large, we can use the approx. pivotal quantity:

![image-20181211004152628](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211004152628-4506912.png)

to construct confidence intervals and test hypotheses for the difference in means.

To find a 100$p$% confidence interval of the difference in means, we use:

![image-20181211004300788](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211004300788-4506980.png)

where $1.96$ is replaced by your $a$ value, where $P(T \leq a) = \frac{1+p}{2}$ and $T \sim t_{n_1 + n_2 - 2}$.





# Paired Data

Sometimes, the two samples we're studying won't be independent, like we've assumed them to be in all of the previous parts of this section.

We pair up observations, so that the value of the $i^{th}$ unit in the first sample is correlated with the second sample. This is __paired data.__

### Variance & Covariance

![image-20181211004836420](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211004836420-4507316.png)

This shows us that the variance of paired data is less, which is one of the benefits of using paired data.



### Working With Distributions in Paired Data

To make inferences about $\mu_1 - \mu_2$, we analyze the within-pair differences 

![image-20181211004942684](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211004942684-4507382.png)

by assuming 

![image-20181211005000999](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211005000999-4507401.png)

or, when working with Gaussian, that

![image-20181211005015023](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211005015023-4507415.png)

This can then be used to **find confidence intervals**, etc, just like a normal one sample Gaussian distributed random variable.



### When and Why Paired Experiments are Better than 2 independent random samples

Paired experiments reduce the variance of each individual sample's random variables, which is better than when they are two independent studies. 

This is better for estimating $\mu_1 - \mu_2$, since a smaller variance means a smaller confidence interval, which is more accurate. However, this is only the case when __there is a positive correlation or association between the two random variables (samples)__. 

To show this mathematically, if we say that the estimator of $\mu_1 - \mu_2$ is $\bar Y_1 - \bar Y_2$, and we have that $E(\bar Y_1 - \bar Y_2) = \mu_1 - \mu_2$, then

![image-20181211005658624](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_6-3.assets/image-20181211005658624-4507818.png)

We can see that $\sigma_{12} = Cov(Y_{1i}, Y_{2i})$, and so a **positive correlation** means $\sigma_{12} \gt 0$, **reducing** $Var(\bar Y_1 - \bar Y_2)$. On the other hand, a negative correlation between the two random variables means $\sigma_{12} \lt 0$, which increases the variance - not what we want and in that case pairing is a bad idea.



__STAT 231 |__ Section 7.1

# Multinomial Models

We might have a distribution that's not based on a single random variable, but **multiple random variables**. This is ==__multinomial distribution__.== Its probability function is given by:

![image-20181210184631802](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-all.assets/image-20181210184631802-4485591.png)

### Multinomial Likelihood Function

Just like likelihood functions with a single parameter, we can find the likelihood function of a multinomial model based on observed data $y_1, y_2, ..., y_n$ to be:

![image-20181210184739608](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-all.assets/image-20181210184739608-4485659.png)

### Multinomial Maximum Likelihood Estimates & Hypotheses of Interest

In general, we can find a maximum likelihood estimator $\tilde \theta_j$ to be $\frac{Y_j}{n}$ with a corresponding maximum likelihood estimate $\hat \theta_j = \frac{y_j}{n}$, for some observed multinomial data $y_1, ..., y_k$.

When we're trying to test hypotheses, we usually define our null hypothesis based on what we're testing, but keep in mind that now there's multiple parameters to define in our null hypothesis.

_ex. to test if a $k$-sided die is fair, we might define our null hypothesis to be  $\theta_0 = (\frac{1}{k},..., \frac{1}{k})$._



### Hypothesis Testing & Likelihood Ratio Test Statistic

Based on the information above, we would set up the likelihood ratio test statistic for multinomial data like so:

![image-20181210185438176](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-all.assets/image-20181210185438176-4486078.png)

if we're testing the null hypothesis $\theta_0$ defined above.

So, since $\theta_j = \frac{1}{k}$, we have that 

![image-20181210185735370](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-all.assets/image-20181210185735370-4486255.png)

![image-20181210185755274](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-all.assets/image-20181210185755274-4486275.png)

and finally,

![image-20181210185834454](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-all.assets/image-20181210185834454-4486314.png)

For the observed value, we simply replace $Y_j$ with an observed value of $y_j$ and $E_j = \frac{n}{k}$.

If $e_j \geq 5$ for all $j$, we can use a Chi-squared approximation to obtain the $p$-value. The $p$-value $= P(W \geq \lambda(\theta_0))$, where $W \sim \chi^2_{k - 1 - p}$, $p$ being the number of parameters estimated (number of unknown parameters).

So, the number of **degrees of freedom** is $k - 1 - p$.

What do we do when some of the expected frequencies are less than 5? We have to 'collapse' some of our adjacent categories with the smallest frequencies so that we can have every category be greater than 5.



__STAT 231 |__ Section 7.2

# Pearson Goodness of Fit Statistic

The ==__Pearson goodness of fit statistic__== is an alternative test statistic that was developed earlier before the likelihood ratio test statistic.

It's given by 

![image-20181210191007471](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-2.assets/image-20181210191007471-4487007.png)

For large values of $n$, $D$ and $\Lambda$ are equivalent and have the same Chi-squared distribution.



__STAT 231 |__ Section 7.3

# Two Way Tables & Independence Tests

When we have multiple possible values for both variates, we need to create a ==__two way table__.==

Suppose $n$ individuals are classified according to two different variates which have two possible values. The _two way table_ would look like this:

![image-20181210214009592](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210214009592-4496009.png)

where $\bar A$ means $\neg A$, or _'not A'_.

If we let $Y_{ij}$ be the number of outcomes in the $i^{th}$ row and $j^{th}$ column, then

![image-20181210214218038](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210214218038-4496138.png)





### Testing for Independence

We want to conduct a hypothesis test for independence of the two variates. So, our null hypothesis $H_0$ is that the variates $A, B$ are independent:

![image-20181210214405239](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210214405239-4496245.png)

![image-20181210214421718](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210214421718-4496261.png)

If we want to be more specific in terms of our hypothesis, since $\theta_{11} = \alpha\beta,$ then the likelihood function is

![image-20181210214837258](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210214837258-4496517.png)

and our maximum likelihood estimates and estimators are:

![image-20181210214901387](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210214901387-4496541.png)

and 

![image-20181210214910252](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210214910252-4496550.png)

respectively (these are because $\alpha$ represents the probability that $A$ is true and $\beta$ is the same for $B$, so we add up the corresponding row in the two way table).

Note that the likelihood ratio test statistic is as follows (similar to previous likelihood ratio test statistics:

![image-20181210215259535](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210215259535-4496779.png)

with the observed value being

![image-20181210215317028](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210215317028-4496797.png)

and the expected value of the first row/column spot being

![image-20181210215415344](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_7-3.assets/image-20181210215415344-4496855.png)

allowing us to **find the rest of the expected frequencies** by subtracting this value from the totals of each row and each column.

Then, we **calculate $\lambda$** (the observed value of the likelihood ratio test statistic above) from the expected values and the observed values $y_{ij}$ by plugging them in.

Almost done! We **find the $p$-value** by the fact that $p$-value $= P(W \geq \lambda)$ where $W \sim \chi^2_{k - 1 -p}$.

Finally, we are able to **conclude based on the $p$-value** whether or not our null-hypothesis is true; if the $p$-value is very small, there is evidence against the null hypothesis (_i.e. it is very likely that the two variates are NOT independent_), or the opposite might be true.



__STAT 231 |__ Section 8-all

# Causal Effect & Relationships

We want to say that $x$ __has a__ ==__causal effect__== on $y$ if, when all other factors that affect $Y$ are held constant, a change in $x$ induces a change in a property of the distribution of $Y$. 

This definition is impractical because we cannot hold all other factors that affect $y$ constant. Sometimes, we might not even know what all the factors that affect $y$ are! However, we use this as a baseline sort of ideal to use in a study to show that a causal relationship exists.



### Relating Two Variates

There are many reasons two variates can be related.

#### 1. The explanatory variate is the direct cause of the response variate.

Sometimes, like if were to measure intake of food as the explanatory variate and level of hunger as the response variate, we can **find a relationship** where the explanatory variate is the **direct cause** of the response variate.

However, even if one is a **direct cause** of the other, there **may not be a strong association**: for example, intercourse is the direct cause of pregnancy, but many occurrences of intercourse do not result in pregnance, so the **relationship between those two variates are not strong**.

#### 2. The response variate is causing a change in the explanatory variate.

This is the opposite of the causal connection we might expect, or want to make.

_For example:_

![image-20181210224151156](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_8-all.assets/image-20181210224151156-4499711.png)

![image-20181210224200604](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_8-all.assets/image-20181210224200604-4499720.png)

#### 3. The explanatory variate is a contributing but not sole cause of a change in the response variate.

This scenario occurs most often when the variates being studied are complex. It's easy to be misled into thinking you have found **a sole cause** for a response variate, but in reality you have just found one of many **contributors** to the outcome.

_For example, diet might have a causal connection with cancer, but it is highly unlikely that the cancer was caused solely by eating that type of diet._

#### 4. Both variates are changing with time.

This scenario can crate nonsensical associations since lots of variates change in similar ways over time, but it doesn't mean there's a causal connection.

_For example a strong correlation between number of women in the workforce and number of Christmas trees sold in Canada between 1930 and the present would be observed since both of these numbers are increasing with time._

#### 5. The association may be due to coincidence.

_Self explanatory, really_

#### 6. Confounding variates may exist.

Two variates are __confounded__ if their effects on a third variate cannot be separate. These variates might help cause change in the third variate, but there is no way to establish how much change is due to one and how much is due to another.

![image-20181210224749734](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_8-all.assets/image-20181210224749734-4500069.png)

#### 7. Both variates may result from a common cause.

![image-20181210224759420](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_8-all.assets/image-20181210224759420-4500079.png)

![image-20181210224805633](../../../../../Google%20Drive/University/2A/STAT%20231/Notes/section_8-all.assets/image-20181210224805633-4500085.png)

### Controlling Variates in an Experiment

When conducting an experiment, it's hard for variates that should not change to be held constant or controlled. We introduce **randomization** to help deal with this problem.

When you create a sample of randomized units, the **distribution of confounding variates will be the same** as in another sample with the same amount of randomization. This allows us to find a relationship between the variates we change and control and the response variate, since the randomization is equally prevalent for both groups!



### Controlling Variates in Observational Studies

In observational studies controlling variates and using randomization is not possible. Establishing causation in observational studies is much more difficult and requires at least the following four features:

1. The association between the two variates must be observed in many studies of different types among different groups. This reduces the chance that an observed association is due to a defect in one type of study or a peculiarity in one group of subjects.
2. The association must continue to hold when the effects of plausible confounding variates are taken into account.
3. There must be a plausible scientific explanation for the direct influence of one variate on the other variate, so that a causal link does not depend on the observed association alone.
4. There must be a consistent response, that is, one variate always increases (decreases) as the other variate increases.



==dis the end of STAT 231 :disappointed:==



