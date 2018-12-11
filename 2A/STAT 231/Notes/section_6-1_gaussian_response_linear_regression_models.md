__STAT 231 |__ Section 6.1

### Gaussian Response Model

A ==__Gaussian response model__== allows for the parameters of the Gaussian distribution ($\mu, \sigma$) to depend on a vector of __covariates__ which are explanatory variates for the response variate $Y$. 

Formally:

![image-20181210231926047](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1.assets/image-20181210231926047-4501966.png)

Most of the time, we'll make $\sigma(x_i) = \sigma$ a constant, which makes the models easier to analyze. So, the value of $\mu(x)$ is determinede by the function itself and the covariates $x$.



### Linear Regression Model

Often, we assume $\mu(x_i)$ is a linear function of the covariates; these are known as ==__linear regression models__== and can be written as:

![image-20181210232134601](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1.assets/image-20181210232134601-4502094.png)

where $x_i = (x_{i1}, x_{i2}, ..., x_{ik})$ is the vector of known covariate _constants_ associated with the $i^{th}$ random variable (a unit), and $\beta_0, \beta_1, ..., \beta_k$ are unknown parameters known as __regression coefficients.__

#### Example: STAT 230/231 Grades

Let's examine the plot of grades students received in STAT 230 vs the ones they received in STAT 231.

![image-20181210232551345](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1.assets/image-20181210232551345-4502351.png)

We can see that the relationship between $x, y$ don't vary as much when $x$ increases or decreases (it's a relatively linear relationship). 

Assume a model in which $\mu(x) =$ mean STAT 231 final grade, with $x$ being their final grade in STAT 230. Then, since the mean STAT 231 final grade of each final STAT 230 grade will form a line, we can say that

![image-20181210232909105](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1.assets/image-20181210232909105-4502549.png)

where $\alpha, \beta$ are unknowns and $x$ is a known constant (the STAT 230 final grade). To extend this to more than just one STAT 230 final grade, we look at multiple $x$ values.

![image-20181210232956086](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_6-1.assets/image-20181210232956086-4502596.png)

$\sigma$, which we assumed to be the same for each $Y_i$, represents the variability in the response variate $Y$ in the study population for each value of the explanatory variate $x$.

