# Table of Contents

## Basic Statistics

| Function | What it calculates |
|------|----------|
|  mean(x)   |  Mean of the numbers in vector x.  |
|  median(x)  |  Median of the numbers in vector x  |
|  var(x)   |  Estimated variance of the population from which the numbers in vector x are sampled  |
|  sd(x)   |  Estimated standard deviation of the population from which the numbers in vector x are sampled  |
|  sd(x)   | Standard scores (z-scores) for the numbers in vector x  |

## Base R Statistical Functions for Relative Standing

| Function | What it calculates |
|------|----------|
|  sort(x)   |  The numbers in vector x in increasing order  |
|  sort(x)[n]  |  The nth smallest number in vector x  |
|  rank(x)   |  Ranks of the numbers (in increasing order) in vector x  |
|  rank(-x)   |  Ranks of the numbers (in decreasing order) in vector x  |
|  rank(x, ties.method= “average”)   |  Ranks of the numbers (in increasing order) in vector x, with tied numbers given the average of the ranks that the ties would have attained  |
| rank(x, ties.method=  “min”)   | Ranks of the numbers (in increasing order) in vector x, with tied numbers given the minimum of the ranks that the ties would have attained |
| rank(x, ties.method = “max”)   | Ranks of the numbers (in increasing order) in vector x, with tied numbers given the maximum of the ranks that the ties would have attained  |
| quantile(x)  | 	The 0th, 25th, 50th, 75th, and 100th percentiles (i.e, the quartiles) of the numbers in vector x. (That’s not a misprint: quantile(x) returns the quartiles of x.)  |


## T-test

| Function | What it calculates |
|------|----------|
|  t.test(x,mu=n, alternative = “two.sided”)   |  Two-tailed t-test that the mean of the numbers in vector x is different from n.  |
|  t.test(x,mu=n, alternative = “greater”)  |  One-tailed t-test that the mean of the numbers in vector x is greater than n.  |
|  t.test(x,mu=n, alternative = “less”)   | One-tailed t-test that the mean of the numbers in vector x is less than n.  |
|  t.test(x,y,mu=0, var.equal  = TRUE, alternative = “two.sided”)   |  Two-tailed t-test that the mean of the numbers in vector x is different from the mean of the numbers in vector y. The variances in the two vectors are assumed to be equal.  |
|  t.test(x,y,mu=0, alternative = “two.sided”, paired  = TRUE)   | Two-tailed t-test that the mean of the numbers in vector x is different from the mean of the numbers in vector y. The vectors represent matched samples.  |

### T-tests

#### Single Sample T-Tests
```
analysis1=t.test(caloriedata1$V1,mu=3000)
```

This command tells R to conduct a single sample t-test of calorie.data1$V1 against a known population mean of3000. By specifying mu, R will automatically know to treat this as a single sample t-test. To view the results of the
single sample t-test:

```
print(analysis1)
```
Note: for a single sample t-test, the degrees of freedom are: df = n -1.

#### Paired (Dependent) Sample T-Tests
In R, we need to first define factors (i.e. independent variables) as factors. We do this as follows:

```
caloriedata2$time=factor(caloriedata2$time)
```
Once the factor has been set, a paired sample t-test can be conducted:

```
analysis2=t.test(caloriedata2$calories~caloriedata2$time, paired=TRUE)
```

This command is essentially saying, “Let's run a t-test where we examine caloriedata2$calories as a function of caloriedata2$time and oh, by the way, it’s a paired/dependent samples ttest."
Note: for a dependent samples t-test, the degrees of freedom are: df = n -1.

#### Independent T-test
```
analysis3=t.test(caloriedata3$calories~caloriedata3$group)
```
#Note: for an independent samples t-test the degrees of freedom are: df = n1 - 1 + n2 - 1.

Finding Means of the Data (or Other Descriptives) for the Actual Conditions
```
mean(caloriedata2$calories[caloriedata2$time==1])
```

This command is use to find the mean calories for the subjects in the first condition.

```
mean(caloriedata2$calories[caloriedata2$time==2])
```
Conversely, this command allows you to find the mean calories for the subjects in the second condition.

## Analysis of Variance (ANOVA)

| Function | What is calculates |
|------|----------|
|  aov(y~x, data = d)   |  Single-factor ANOVA, with the numbers in vector y as the dependent variable and the elements of vector x as the levels of the independent variable. The data are in data frame d. |
|  aov(y~x + Error(w/x), data = d)   |  Repeated Measures ANOVA, with the numbers in vector y as the dependent variable and the elements in vector x as the levels of an independent variable. Error(w/x) indicates that each element in vector w experiences all the levels of x (i.e., x is a repeated measure). The data are in data frame d.  |
|  aov(y~x*z, data = d)   |  Two-factor ANOVA, with the numbers in vector y as the dependent variable and the elements of vectors x and z as the levels of the two independent variables. The data are in data frame d.  |
|  aov(y~x*z + Error(w/z), data = d)   |  Mixed ANOVA, with the numbers in vector z as the dependent variable and the elements of vectors x and y as the levels of the two independent variables. Error(w/z) indicates that each element in vector w experiences all the levels of z (i.e., z is a repeated measure). The data are in data frame d.  |


### Assumptions

1. **Assumption One:** Between Group Independence.
essentially, your groups cannot be related.

2. **Assumption Two:** Within Group Sampling and Independence.
The members of each groups are sampled randomly and are independent of each other

3. **Assumption Three:** Normality.
the sampling distribution of the mean of the population from which the data is drawn is normally distributed,
which approximately means the data for each group are drawn from a normally distributed population. 

    There are three ways to do this:
  * Plot Histograms for each group and assess this through visual inspection.

```
par(mfcol=c(1, 3))
hist(data$rt[data$group==1])
hist(data$rt[data$group==2])
hist(data$rt[data$group==3])
```

   * Examine the skew and kurtosis of the data for each group. Skewness assesses how much to the left or right the
    distribution is pulled (0 is perfectly normal) and kurtosis assesses how flat or peaked the distribution is (3 is
    perfectly normal).

```
library("moments")
skewness(data$rt[data$group==1])
kurtosis(data$rt[data$group==1])
skewness(data$rt[data$group==2])
kurtosis(data$rt[data$group==2])
```

   * Use QQ plots to assess normality. On a QQ plot the data is normal if it all falls on a line.
    
```
qqnorm(data$rt[data$group==1])
qqline(data$rt[data$group==1])
qqnorm(data$rt[data$group==2])
qqline(data$rt[data$group==2])
```

4. **Assumption Four:** Homogeneity of Variance.
ANOVA assumes that the variances of all groups are equivalent. There are three ways to test this:

* Plot Histograms and visually ensure a normal distribution.
* Compute the variances for each group:
```
var(data$rt[data$group==1])
var(data$rt[data$group==2])
var(data$rt[data$group==3])
```
A general rule of thumb is that if the smallest variance is within 4 magnitudes of the largest variance then the
assumption is met.

* Use a statistical test of the assumption i.e. Hartley’s rule of thumb or Bartlett’s test

```
bartlett.test(data$rt~data$group)
```

### Computing an ANOVA

```
data$condition=factor(data$condition)
analysis=aov(data$score~data$condition)
```
This command tells R to run an analysis of variance (aov) on data$rt with data$group as a factor.

```
Summary(analysis)
```

Typically, you would report an ANOVA as follows: Our analysis revealed that there was a difference between groups, F(2,147) = 17.58, p < 0.001.

An ANOVA simply tells you whether or not there is a difference between groups, it does not tell you where
the difference is. To find where the difference is, a test such as the TukeyHSD can be computed. 


### Methods for Performing a Post-Hoc Analysis

#### TukeyHSD
The TukeyHSD can be used to statistically test whether or not there are differences between specific groups

```
analysis=aov(data$score~data$condition)
TukeyHSD(analysis)
```

#### Bonferonni Analysis
Similar to the TukeyHSD test, you could also do pairwise t-tests with a Bonferonni correction by using:

```
pairwise.t.test(data$rt,data$group,p.adjust="bonf")
```

#### Contrast Analysis
```
summary.lm(analysis)
```

This command shows you the contrasts of groups 2 and 3 relative to group 1 - the default contrast.

To use a different contrast, you can define it through the contrast command and then re-execute the model.

```
contrasts(data$group)=contr.treatment(3,base=3)
modelnew=aov(data$rt~data$group)
summary.lm(modelnew)
```

The above code would conduct a contrast comparing the first two groups to the third.

```
contrasts(data$group) = contr.poly(3)
modelnew = aov(data$rt~data$group)
summary.lm(modelnew)
```

The above code would conduct a contrast examining the polynomial trends between the groups (linear, quadratic
etc).



### Repeated Measures ANOVA
```
data$subject = factor(data$subject)
data$condition = factor(data$condition)
model = aov(data$data~data$condition+Error(data$subject/data$condition))
summary(model)
```

Given the theory behind RM ANOVA, you are removing between participant variance from the overall error variance. The Error term accomplishes that.

#### Post-Hoc Analysis of RM ANOVA

To perform a post-hoc on data from a RM ANOVA, all you need to do is run a series of pairwise comparisons:

```
pairwise.t.test(data$data,data$condition,paired=TRUE)
```

### Computing a Factorial ANOVA
The linear model for a factorial ANOVA has to include both main effects (age, gender) and the interaction between age and gender.

```
rt=data$rt
age=factor(data$age)
gender=factor(data$gender)
model=aov(rt~age+gender+gender*age)
summary(model)
plot(rt ~ age)
plot(rt ~ gender)
interaction.plot(age,gender,rt)
```


To verify the results of the above, you need to do a posthoc analysis of the main effects of age and gender and the interaction.

```
TukeyHSD(model)
```
An even simpler way to post-hoc the ANOVA would be to do the following: 

Pick a direction: Age or Gender. If you pick Age, then you can run an independent samples t-test at each level of age to see where the difference lies.

```
age1 = subset(data,age==1)
t.test(age1$rt~age1$gender)
age2 = subset(data,age==2)
t.test(age2$rt~age2$gender)
age3 = subset(data,age==3)
t.test(age3$rt~age3$gender)
```

Then, you can look to see whether the tests are significant, and therefore, whether there is similarity between groups.

## Linear Regression

| Function | What it calculates |
|------|----------|
|  cor(x,y)   |  Correlation coefficient between the numbers in vector x and the numbers in vector y  |
|  cor.test(x,y)  |  Correlation coefficient between the numbers in vector x and the numbers in vector y, along with a t-test of the significance of the correlation coefficient.  |
|  lm(y~x, data = d)   |  Linear regression analysis with the numbers in vector y as the dependent variable and the numbers in vector x as the independent variable. Data are in data frame d.|
|  coefficients(a)   |  	Slope and intercept of linear regression model a. |
|  confint(a)   | 	Confidence intervals of the slope and intercept of linear regression model a |
|  lm(y~x+z, data = d)   | Multiple regression analysis with the numbers in vector y as the dependent variable and the numbers in vectors x and z as the independent variables. Data are in data frame d.  |


#### Testing the Assumptions of Multiple Regression
1. **Assumption of Independence of Errors**

```
library(car)
durbinWatsonTest(results)
```
You want the D-W value to be between 1 and 3 and as close to 2 as possible.

2. **Assumption of Normality, Linearity, & Homoscedasticity of Residuals**

One simple test of the assumptions in R is to examine the residuals. If the residuals are normally distributed then one can generally assume that all of the assumptions have been met.

```
res=resid(results)
```
This command puts all of the residuals (the difference between the actual and predicted y values) into a variable called res.

```
hist(res)
```

If the histogram is normally distributed, then one can assume the assumptions were met.

```
plot(results)
```
Input the return(results) command until you see Q-Q plot. The Q-Q plot in a multiple regression shows deviations from normality, thus, you want it to be straight.

3. **Assumption of Multi-Collinearity**
To test the Assumption of Multi-Collinearity, you typically examine variance inflation factors(vif).
Three criteria must be met:
  1. No VIF above 10 - check with vif(results).
  2. The average VIF should be close to 1- check with mean(vif(results))
  3. Ideally, the tolerance (1/vif) should be not be less than 0.1, and less than 0.2 may be a problem - check with

```
1/vif(results)
vif(results)
mean(vif(results))
1/vif(results)
```

4. **Testing for Outliers and Influential Cases**
A simple way to examine for multivariate outliers is to compute a Cook's Distance:
```
cooks=cooks.distance(results)
plot(cooks)
```
If the Cook’s Distance test reveals and outlier, you want to remove the outlier and redo the whole test.


#### Testing the Assumption of Homogeneity of Variance (Independent Ttest)

For an independent samples t-test, the assumption of homogeneity of variance needs to be tested. Hartley’s rule
of thumb is the easiest way to do this. The Bartlett and Levene’s tests are other ways to test this assumption.

##### Hartley's Rule of Thumb

```
vars=aggregate(caloriedata3$calories,list(caloriedata3$group),var)
vars
```

Essentially, you are looking to ensure that the variance of one group is no more than four times the variance of
the other group (or vice versa).

##### Bartlett Test
```
bartlett.test(caloriedata3$calories~caloriedata3$group)
```

##### Levene's Test
```
library(car)
leveneTest(caloriedata3$calories~caloriedata3$group)
```

The Levene Test is generally considered to be more reliable than the Bartlett test, especially for smaller sample sizes.

#### The Assumption of Sphericity
The assumption of sphericity is that the variances of the difference scores are equal. The reality is that in R the
test of this assumption is not as easy as one might think. Indeed, it is easier to just run the RM ANOVA using the ezANOVA package.

```
library("ez")
model = ezANOVA(data=data, dv = .(data), wid =.(subject), within =.(condition), detailed = TRUE, type =3)
```

This will give you a full RM ANOVA table plus the test of sphericity. Note, if you fail the test of sphericity you
should use one of the corrected p-values and correct the degrees of freedom. In general, the closer epsilon is to 1
then the more closely the assumption is met. For this design epsilon should have a range between 0.5 and 1. The
lower bound of epsilon is defined as 1 / (number of levels - 1). If epsilon is closer to the lower bound than 1 then
the assumption is definitely not met.

### Linear Regression

Here’s a selection of R statistical functions having to do with Analysis of Variance (ANOVA) and correlation and regression.
When you carry out an ANOVA or a regression analysis, store the analysis in a list. For example,

```
a <- lm(y~x, data = d)
```

Then, to see the tabled results, use the summary() function:

```
summary(a)
```



