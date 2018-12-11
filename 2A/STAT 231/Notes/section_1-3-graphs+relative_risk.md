__STAT 231 | __ Section 1.3

# Empirical Studies (cont.)

### Graphical Summaries

There are many different types of graphical summaries, including **histograms, boxplots, scatterplots, etc.**

#### 1. Relative Frequency Histogram

The== relative frequency histogram== is used to compare data to a _p.d.f._; after partitioning the data set into $k$ intervals, it shows the relative frequencies of each interval to each other (the proportion of values in the data set that appear in the interval vs another interval).

#### 2. Boxplot

The ==boxplot== allows us to get information that a histogram does not give us, like a median, the IQR, etc.

![image-20181209153411251](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_1-3-graphs.assets/image-20181209153411251-4387651.png)

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

![image-20181209154114957](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_1-3-graphs.assets/image-20181209154114957-4388074.png)

We want to find if there is a relatinship between IQ and brain size in the above chart. We introduce an additional measure to judge **correlation** between two variates: the **sample correlation**, given by:

![image-20181209154241279](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_1-3-graphs.assets/image-20181209154241279-4388161.png)



### Bivariate Categorical Data & Relative Risk

When we have two variates that are both categorical, we can't plot them on a scatterplot, since it would just be four solid points with a bunch of values at that point and categorical data does not have correlation. We introduce the idea of ==relative risk==, which can explain the propability of an occurrence in one category of a variate vs another category in the same variate. 

![image-20181209154957740](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_1-3-graphs.assets/image-20181209154957740-4388597.png)

![image-20181209155008612](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_1-3-graphs.assets/image-20181209155008612-4388608.png)

### Empirical c.d.f

The ==empirical c.d.f.== allows us to compare the distribution of a dataset with a c.d.f. of a random variable.

It is given by: $F(y) = \frac{\text{# of. values in the dataset which are}  \leq  y}{n}$, where $y$ is a variable.

You can use the empirical cdf to compare the same variate value of two or more groups, or you can even use it to check normality by comparing it to the e.c.d.f of a normal data set.

![image-20181209152405722](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_1-3-graphs.assets/image-20181209152405722.png)

