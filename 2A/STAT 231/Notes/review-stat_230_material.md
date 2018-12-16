**STAT 231 |** Oct 4, 2018

# STAT 230 Concepts Review
## Random Variables And Their Functions
A __random variable__ is a variable that represents _outcomes in an experiment or random process_.
  - denoted by capital letters
  - possible values for them are denoted by lowercase letters

The __probability function__ of a _discrete_ random variable $X$ with range $A$ is the function:
$$f(x) = P(X = x), \forall x \in A$$
  1. $f(x) \geq 0, \forall x \in A$
  2. $\sum_{x \in A} f(x) = 1$

> Measuring the probability of a single value for continuous random variables is useless as that probability is always 0.

The __cumulative distribution function__ of a random variable $X$ is the function:
$$F(x) = P(X \leq x), \forall x \in A$$
  1. $F(x)$ is a non-decreasing function
  2. $0 \leq F(x) \leq 1, \forall x \in \R$
  3. $\lim\limits_{x \rightarrow -\infty} F(x) = 0$  and $\lim\limits_{x \rightarrow \infty} F(x) = 1$

> You can get one function from the other by summing up all _p.f.s_ to get the _c.d.f_, or subtracting the _c.d.f._ of $x$ from the _c.d.f_ of $x-1$ to get the _p.f._.

The __probability density function__ of a _continuous_ random variable $X$ with _c.d.f_ $F(x)$ is the function:
$$f(x) = \frac{dF(x)}{dx}$$
  1. $P(a \leq X \leq b) = F(b) - F(a) = \int_a^b f(x)dx$
  2. $f(x) \geq 0$

> The _p.d.f_ represents the approximate probability $X$ is inside a very small interval centered around $x$, so it is similar to the _p.f._ but _not_ the same.




## Probability Distributions
### Hypergeometric
  - Choosing $n$ objects _without replacement_ (dependent)
  - Measuring # of successes
  - Discrete

### Binomial
$X \sim Binomial(n, p)$
  - $n$ is _number of trials_
  - $p$ is _probability of success_
  - _Repeated_ trials
  - Each trial is _independent_ with _two outcomes_
  - Discrete

### Poisson
$X \sim Poisson(\mu)$
  - $\mu$ is:
    - $np$ if approximating _Binomial_
    - $\lambda t$ if events follow a _Poisson process_
      - $\lambda$ is rate per time interval
      - $t$ is number of time intervals
  - _Poisson process_ requires:
    - Independence: events are independent
    - Individuality: P(2 or more events in same time interval) = 0
    - Uniformity: events occur at a uniform rate
  - Discrete

> It is not Poisson if we can specify the maximum value of $X$ in advance and/or if we can calculate how often the event did _not_ occur.

### Exponential
$X \sim Exponential(\theta)$
  - $\theta$ is $\frac{1}{\lambda}$, where $\lambda$ is average rate of occurrence
  - Measures _time until_ some event occurs or _time between_ events in a Poisson process
  - Continuous

### Normal
$X \sim N(\mu, \sigma^2)$
  - $\mu$ is the mean, $\sigma$ is the standard deviation
  - $Var(X) = \sigma^2$ (_square of standard deviation_)
  - Continuous

__Probability function__: use tables
> The __Gaussian__ distribution is the same model, but the parameters specified are $\mu$ and $\sigma$, _not_ $\sigma^2$.

### Multinomial
$(X_1, X_2,...,X_k) \sim (n, p_1, p_2,...,p_k)$
  - $n$ is number of _independent_ trials
  - $p_i$ is probability of outcome $X_i$

__Probability function__: $\Sigma \frac{n!}{x_1!x_2!...x_k!} p_1^{x_1}p_2^{x_2}...p_k^{x_k}$


## Linear Combinations of Independent Normal Random Variables
  1. Let $X \sim N(\mu, \sigma^2)$ and $Y = aX + b$, where $a$ and $b$ are constant real numbers. Then, $Y \sim N(a\mu + b, a^2\sigma^2)$.
  2. Let $X \sim N(\mu_1, \sigma_1^2)$ and $Y \sim N(\mu_2, \sigma_2^2)$ independently, and let $a, b \in \R$. Then, $aX + bY \sim N(a\mu_1 + b\mu_2, a^2 \sigma_1^2 + b^2 \sigma_2^2)$. This can be generalized to $n$.
  3. Let $X_1, X_2,...,X_n$ be independent $N(\mu, \sigma^2)$ random variables. Then, $\Sigma X_i \sim N(n\mu, n\sigma^2)$ and $\bar{X} \sim N(\mu, \frac{\sigma^2}{n})$.


# Central Limit Theorem (CLT)
The __Central Limit Theorem__ is used to approximate non-Normal distributions with the Normal distribution.

__Theorem__: If $X_1, X_2,...,X_n$ are independent random variables with the same distribution, mean $\mu$, and variance $\sigma^2$, then as $n \rightarrow \infty$, the _c.d.f_ of the random variable
$$\frac{\Sigma_{i=1}^n X_i - n\mu}{\sigma \sqrt{n}} = \frac{S_n - n\mu}{\sigma \sqrt{n}}$$
approaches the $N(0, 1)$ _c.d.f_.

  - Use for large $n$
