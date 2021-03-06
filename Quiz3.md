# Statistical Inference Quiz 3
Ray Qiu  
October 21, 2015  

##### Question 1: In a population of interest, a sample of 9 men yielded a sample average brain volume of 1,100cc and a standard deviation of 30cc. What is a 95% Student's T confidence interval for the mean brain volume in this new population?

```r
n <- 9
m <- 1100
sd <- 30
round(m + c(-1, 1) * qt(.975, df = n-1) * sd / sqrt(n), 0)
```

```
## [1] 1077 1123
```

##### Question 2: A diet pill is given to 9 subjects over six weeks. The average difference in weight (follow up - baseline) is -2 pounds. What would the standard deviation of the difference in weight have to be for the upper endpoint of the 95% T confidence interval to touch 0?

```r
n <- 9
m <- -2
upper <- 0
# upper = m + qt(.975, df = n-1) * sd / sqrt(n)
sd <- round((upper - m) * sqrt(n) / qt(.975, df = n-1), 2)
sd
```

```
## [1] 2.6
```

##### Question 3: In an effort to improve running performance, 5 runners were either given a protein supplement or placebo. Then, after a suitable washout period, they were given the opposite treatment. Their mile times were recorded under both the treatment and placebo, yielding 10 measurements with 2 per subject. The researchers intend to use a T test and interval to investigate the treatment. Should they use a paired or independent group T test and interval?

* Paired Interval

##### Question 4: In a study of emergency room waiting times, investigators consider a new and the standard triage systems. To test the systems, administrators selected 20 nights and randomly assigned the new triage system to be used on 10 nights and the standard system on the remaining 10 nights. They calculated the nightly median waiting time (MWT) to see a physician. The average MWT for the new system was 3 hours with a variance of 0.60 while the average MWT for the old system was 5 hours with a variance of 0.68. Consider the 95% confidence interval estimate for the differences of the mean MWT associated with the new system. Assume a constant variance. What is the interval? Subtract in this order (New System - Old System).

```r
# sp^2 = {(nx − 1)sx^2 + (ny − 1)sy^2}/(nx + ny − 2)
nx <- 10
ny <- 10
vx <- 0.6
vy <- 0.68
sp <- sqrt(((nx - 1)*vx + (ny-1)*vy)/(nx + ny -2))
semd <- sp * sqrt(1 / nx + 1/ny)
md <- 3 - 5
round(md + c(-1, 1) * qt(.975, df = nx + ny - 2) * semd, 2)
```

```
## [1] -2.75 -1.25
```

##### Question 5: Suppose that you create a 95% T confidence interval. You then create a 90% interval using the same data. What can be said about the 90% interval with respect to the 95% interval?

* The interval will be narrower.

##### Question 6: To further test the hospital triage system, administrators selected 200 nights and randomly assigned a new triage system to be used on 100 nights and a standard system on the remaining 100 nights. They calculated the nightly median waiting time (MWT) to see a physician. The average MWT for the new system was 4 hours with a standard deviation of 0.5 hours while the average MWT for the old system was 6 hours with a standard deviation of 2 hours. Consider the hypothesis of a decrease in the mean MWT associated with the new treatment. What does the 95% independent group confidence interval with unequal variances suggest vis a vis this hypothesis? (Because there’s so many observations per group, just use the Z quantile instead of the T.)

```r
nx <- 100
ny <- 100
sx <- 0.5
sy <- 2
sp <- sqrt(((nx - 1)*sx^2 + (ny-1)*sy^2)/(nx + ny -2))
semd <- sp * sqrt(1 / nx + 1/ny)
md <- 6 - 4
round(md + c(-1, 1) * qt(.975, df = nx + ny - 2) * semd, 2)
```

```
## [1] 1.59 2.41
```

##### Question 7: Suppose that 18 obese subjects were randomized, 9 each, to a new diet pill and a placebo. Subjects’ body mass indices (BMIs) were measured at a baseline and again after having received the treatment or placebo for four weeks. The average difference from follow-up to the baseline (followup - baseline) was −3 kg/m2 for the treated group and 1 kg/m2 for the placebo group. The corresponding standard deviations of the differences was 1.5 kg/m2 for the treatment group and 1.8 kg/m2 for the placebo group. Does the change in BMI over the four week period appear to differ between the treated and placebo groups? Assuming normality of the underlying data and a common population variance, calculate the relevant 90% t confidence interval. Subtract in the order of (Treated - Placebo) with the smaller (more negative) number first.

```r
nx <- 9
ny <- 9
sx <- 1.5
sy <- 1.8
sp <- sqrt(((nx - 1)*sx^2 + (ny-1)*sy^2)/(nx + ny -2))
semd <- sp * sqrt(1 / nx + 1/ny)
md <- -3- 1
round(md + c(-1, 1) * qt(.90 + (1-.90)/2, df = nx + ny - 2) * semd, 3)
```

```
## [1] -5.364 -2.636
```

