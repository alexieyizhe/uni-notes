__STAT 231 |__ Section 4.5

# Chi-squared Distributions

The Chi-squared distribution is parameterized by its __degrees of freedom__, often denoted $k$.

The value of $k$ affects the shape of the resulting probability density function:

![image-20181210140125209](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-5.assets/image-20181210140125209-4468485.png)

### Properties

==If $W_1, W_2, ..., W_n$ are independent random variables with $W_i \sim \chi^2_{k_i}$, then==

![image-20181210140242260](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-5.assets/image-20181210140242260-4468562.png)

_i.e. the sum of chi-squared random variables also follows a chi-squared distribution with its degrees of freeedom being the sum of the degrees of freedoms of itscomponent distributions._

_ex. if $W_1 \sim \chi^2_2, W_2 \sim \chi^2_3$, then $W_1 + W_2 \sim \chi^2_5$._

---

==If $Z \sim  G(0, 1)$, then $Z^2 = W \sim \chi^2_1$.==

_i.e. the square of a standard normal distribution has chi-squared distribution with 1 degree of freedom._

This means that if $W \sim \chi^2_1$, then

![image-20181210140708001](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-5.assets/image-20181210140708001-4468828.png)

allowing us to use standard normal tables and `R ` to compute probabilities with a $\chi^2_1$ distribution.

![image-20181210140839307](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-5.assets/image-20181210140839307-4468919.png)

![image-20181210141036488](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-5.assets/image-20181210141036488-4469036.png)



---

==If $W \sim \chi^2_2$, then $W \sim Exponential(2)$.==

_i.e. a chi-squared distribution with 2 degrees of freedom is the same as an exponential distribution with parameter 2._

So, if $W \sim \chi^2_2$, then

![image-20181210141015008](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_4-5.assets/image-20181210141015008-4469015.png)