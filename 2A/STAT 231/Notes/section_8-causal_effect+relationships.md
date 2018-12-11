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

![image-20181210224151156](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_8-all.assets/image-20181210224151156-4499711.png)

![image-20181210224200604](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_8-all.assets/image-20181210224200604-4499720.png)

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

![image-20181210224749734](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_8-all.assets/image-20181210224749734-4500069.png)

#### 7. Both variates may result from a common cause.

![image-20181210224759420](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_8-all.assets/image-20181210224759420-4500079.png)

![image-20181210224805633](/Users/alexieyizhe/Google Drive/University/2A/STAT 231/Notes/section_8-all.assets/image-20181210224805633-4500085.png)

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

