__STAT 231 |__ Section 2.6



# Q-Q Plots

It's hard for humans to deal with curves in terms of reading them and finding patterns or matching two curves together. By modelling _cumulative distribution functions_ with a ==__QQ plot__==, we can 'straighten' the curves and more easily work with them.

QQ plots are plots of the quantiles of data vs a Gaussian (normal) distribution. In theory, plotting the 1^st^, 2^nd^, ..., 99^th^ quantile of observed data on the $y$-axis and the _theoretical_ quantiles of the normal distributions on the $x$-axis should result in a linear relationship since they _should_ be similar, so we *should* get a straight line.

![image-20181209215120438](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209215120438-4410280.png)

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

### Comparing Cumulative Dstribution Functions with Empirical Versions

This method also deals with **continuous data**. Recall the definition of the empirical cumulative distribution function:

![image-20181209214354742](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209214354742-4409834.png)

This is a cumulative distribution function calculated from the set of observed data, and we can compare it to the cumulative distribution function of the assumed model. A model that fits the observed data should have **the _c.d.f_ match the _e.c.d.f_ in terms of fit** pretty well.

### Reading a QQ Plot

As explained above, QQ plots can indicate if observed data fits a normal distribution model.

![image-20181209220020636](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209220020636-4410820.png)

![image-20181209220029154](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_2-6.assets/image-20181209220029154-4410829.png)





