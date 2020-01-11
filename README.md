# Bayesian Statistics the Fun Way
###### Will Kurt

[[@willkurt](https://twitter.com/willkurt)] [[https://www.countbayesie.com/](https://www.countbayesie.com/)]


[[https://nostarch.com/learnbayes](https://nostarch.com/learnbayes)]

*"Frequentist statistics is founded on the idea that probability represents the frequency with which something happens. ... Bayesian statistics, on the other hand, is concerned with how probabilities represent how uncertain we are about a piece of information"*

---

## PART I: INTRODUCTION TO PROBABILITY

### 1. Bayesian Thinking and Everyday Reasoning

#### Exercises

**Q1+A1.** *Rewrite the following statements as equations:*

* *The probability of rain is low* : **P(rain) = low**
* *The probability of rain given that it is cloudy is high* : **P(rain | cloudy) = high** 
* *The probability of you having an umbrella given it is raining is much greater than the probability of you having an umbrella in general* : **P(umbrella | raining) >> P(umbrella)** 

**Q2.** *Organize the data you observe in the following scenario into a mathematical notation. Then come up with a hypothesis to explain this data: [You come home from work and notice that your front door is open and side window is broken. Inside, you immediately notice that your laptop is missing]*

A2. **P(door, window, no-laptop | H1) = high** ...where H1 = burglary

**Q3.** *The following scenario adds data to the previous one. Demonstrate how this new information changes your beliefs and come up with a second hypothesis to explain the data: [A neighborhood child runs up and apologizes profusely for accidentally throwing a rock through your window. They claim that they saw the laptop and didn’t want it stolen, so it is safe at their house]*

A3. **P(door, window, no-laptop | H2, child)** ...where H2 = accident

**P(D | H2) >> P(D | H1)** ...where D = door open, window broken, laptop missing


---

### 2. Measuring Uncertainty

* ¬ symbol means “negation” or “not”. [ie. ¬P(X) == 1 - P(X)] ...P.14
* Ω indicates the set of all events ...P.15

#### Exercises

**Q1+A1.** *What is the probability of rolling two six-sided dice and getting a value greater than 7?* **{2+6, 3+5, 3+6, 4+4, 4+5, 4+6, 5+3, 5+4, 5+5, 5+6, 6+2, 6+3, 6+4, 6+5, 6+6} --> 15/36 --> 0.417**

**Q2+A2.** *What is the probability of rolling three six-sided dice and getting a value greater than 7?* **{1+1+6, 1+2+5, 1+2+6, 1+3+4, 1+3+5, 1+3+6, 1+4+3, 1+4+4, 1+4+5, 1+4+6, 1+5+2, 1+5+3, 1+5+4, 1+5+5, 1+5+6, 1+6+1, 1+6+2, 1+6+3, 1+6+4, 1+6+5, 1+6+6, 2+1+5, 2+1+6, etc etc} --> 181/216 --> 0.838**

**Q3.** *The Yankees are playing the Red Sox. You’re a diehard Sox fan and bet your friend they’ll win. You’ll pay your friend $30 if the Sox lose and receive only $5 if the Sox win. What is the probability you have intuitively assigned to the belief that the Red Sox will win?*

A3. **Odds of 30:5 or 6:1 --> P(win) = 6/7 or 0.857**


---

### 3. The Logic of Uncertainty

* **Product Rule** of probability : P(A,B) = P(A) × P(B) ...P.25
* **Sum Rule** of probability : P(A OR B) = P(A) + P(B) − P(A,B) ...P.29,30

#### Exercises

**Q1+A1.** *What is the probability of rolling a 20 three times in a row on a 20-sided die?* : **P(3 20s) = 1/20 * 1/20 * 1/20 --> 1/8000 or 0.000125**

**Q2+A2.** *There’s a 10% chance of rain tomorrow, and you forget your umbrella half the time you go out. What is the probability that you’ll be caught in the rain without an umbrella tomorrow?* : **P(rain, no-umbrella) = 1/10 * 1/2 --> 1/20 or 0.05**

**Q3+A3.** *Raw eggs have a 1/20,000 probability of having salmonella. If you eat two raw eggs, what is the probability you ate a raw egg with salmonella?* : **1/20000 + 1/20000 - 1/400,000,000 --> 39,999/400E6 or 0.0001**

**Q4+A4.** *What is the probability of either flipping two heads in two coin tosses or rolling three 6s in three six-sided dice rolls?* : **coins: 1/2 * 1/2 --> 1/4; dice: 1/6 * 1/6 * 1/6 --> 1/216; combination: 1/4 + 1/216 - 1/864 --> 219/864 or 0.253**


---

### 4. Creating a Binomial Probability Distribution

* '**binomial**' has 2 possible outcomes - an event happens or not. ('multinomial' has >2 possible outcomes) ...P.34
* '**binomial coefficient**' represents the ways [permutations] we can select k from n ...P.37
* **`choose(n,k)`** in R for binomial coefficient ...P.38
* '**Probability Mass Function**' (PMF) is the basis of the binomial distribution [B(k,n,p)] ...P.39
*  k outcomes we care about; n trials; and p probability of the individual outcome ...P.39
*  Σ is the summation symbol (for every value of k from 1 to n) ...P.42
* **`pbinom(k,n,p,lower.tail)`** in R (to sum up all these values for k in our PMF) ...P.42


#### Exercises

**Q1.** *What are the parameters of the binomial distribution for the probability of rolling either a 1 or a 20 on a 20-sided die, if we roll the die 12 times?*

A1. **outcomes k = 1 [1 time, out of n trials]; trials n = 12; probability p = 2/20**

**Q2.** *There are four aces in a deck of 52 cards. If you pull a card, return the card, then reshuffle and pull a card again, how many ways can you pull just one ace in five pulls?*

A2. **k = 1; n = 5; p = 4/52. We are interested in permutations : n!/k!(n-k)! --> 60/(1 x 12) --> 5 ways you can pull one ace in one pull (which can be reasoned without using formula)**

**Q3.** *For the example in Q2, what is the probability of pulling five aces in 10 pulls (remember the card is shuffled back in the deck when it is pulled)?*

A3. **k = 5; n = 10; p = 4/52**
**B(5;10,1/13) = (10!/5!5!) x (1/13)^5 x (12/13)^5 -->
(3628800/120x120) x 0.00000269329 x 0.67017692226 -->
252 * 0.00000180498 -->
0.00045485516 ... ~1/2199**

[Book answer (P.234) says B(5;10,1/13) is ~1/32000 --> 0.00003125 ...I don't see how]
[Using R, `choose(10,5)` is 252]
[Using R, `pbinom(5,10,1/13,lower.tail=TRUE)` minus `pbinom(4,10,1/13,lower.tail=TRUE)` --> 0.9999669 - 0.999512 --> 0.0004549. THIS AGREES WITH MY LONG CALC, above]
[Online solutions [https://nostarch.com/learnbayes](https://nostarch.com/learnbayes) incorrectly say p=1/23 ...but that would give/explain the answer 3.134986e-05. Cannot see a form/way to mention the error to publisher]

**Q4.** *When you’re searching for a new job, it’s always helpful to have more than one offer on the table so you can use it in negotiations. If you have a 1/5 probability of receiving a job offer when you interview, and you interview with seven companies in a month, what is the probability you’ll have at least two competing offers by the end of that month?*

A4. **k >= 2; n = 7; p = 1/5**

**B(2;7,0.2) = (7!/2!5!) x (0.2)^2 x (0.8)^5 ...need to also do for k=3,4,5,6,7 and total the probabilities**

**`pbinom(7,7,0.2,lower.tail=TRUE)` minus `pbinom(1,7,0.2,lower.tail=TRUE)` --> 0.4232832 ...[don't 'minus' k=2 here, as we want k=2 probabililty in our total]**

**`pbinom(1,7,0.2,lower.tail=FALSE)` --> 0.4232832 ...same result**

**Q5.** *You get a bunch of recruiter emails and find out you have 25 interviews lined up in the next month. Unfortunately, you know this will leave you exhausted, and the probability of getting an offer will drop to 1/10 if you’re tired. You really don’t want to go on this many interviews unless you are at least twice as likely to get at least two competing offers. Are you more likely to get at least two offers if you go for 25 interviews, or stick to just 7?*

A5. **k >=2 ; n = 25; p = 1/10**

**`pbinom(1,25,0.1,lower.tail=FALSE)` --> 0.7287941 ...More likely to get at least two offers if you go for 25 interviews. But less than twice as likely. So stick to just 7 interviews**


---

### 5. The Beta Distribution

* In a sense, statistics is probability in reverse [re. inference] ...P.46
* '**Probability Density Function**' (PDF) is similar to the PMF, but for continuous values ...P.50
* α + β is total number of trials [cf. k + (n-k) = n] ...P.50
* '**beta function**' (and subtract 1) to normalize our values ...P.51
* **beta distribution** [of k] is fundamentally different from the binomial distribution [of p] ...P.52
* `dbeta(p,α,β)` in R for PDF [Beta(α,β)] ...P.53
* `integrate()` in R (to sum up all these values for p in our PDF) ...P.53
* `integrate(function(p) dbeta(p,14,27),0,0.5)` ...P.53
* beta distribution is closely related to the binomial distribution, but behaves quite differently ...P.55
* Cannot sum results as we did for a discrete probability distribution. Instead, use calculus to sum ranges of values [integrate] ...P.55


#### Exercises

**Q1.** *You want to use the beta distribution to determine whether or not a coin you have is a fair coin — meaning that the coin gives you heads and tails equally. You flip the coin 10 times and get 4 heads and 6 tails. Using the beta distribution, what is the probability that the coin will land on heads more than 60 percent of the time?*

A1. **α = 4; β = 6**

**`integrate(function(p) dbeta(p,4,6),0.6,1)` --> 0.09935258 with absolute error < 1.1e-15**

**Q2.** *You flip the coin 10 more times and now have 9 heads and 11 tails total. What is the probability that the coin is fair, using our definition of fair, give or take 5 percent?*

A2. **α = 9; β = 11**

**`integrate(function(p) dbeta(p,9,11),0.45,0.55)` --> 0.30988 with absolute error < 3.4e-15**

**Q3.** *Data is the best way to become more confident in your assertions. You flip the coin 200 more times and end up with 109 heads and 111 tails. Now what is the probability that the coin is fair, give or take 5 percent?*

A3. **α = 109; β = 111**

**`integrate(function(p) dbeta(p,109,111),0.45,0.55)` --> 0.8589371 with absolute error < 9.5e-15**


---

## PART II: BAYESIAN PROBABILITY AND PRIOR PROBABILITIES

### 6. Conditional Probability

* 'Independent probabilities' often don’t reflect real life ...P.59
* Conditional probabilities allow us to demonstrate how information changes our beliefs ...P.60
* **Product rule** updated as : P(A,B) = P(A) × P(B | A). [This definition works for independent probabilities as well, because for those P(B) = P(B | A) ] ...P.62
* **Sum rule** updated as : P(A or B) = P(A) + P(B) − P(A) × P(B | A) ...P.62
* One of the most amazing things we can do with conditional probabilities is reversing the condition ...P.62
* **Bayes theorem** : P(A | B) = P(A) P(B | A) / P(B) ...P.64
*  Bayes’ theorem allows you to reverse P(observed | belief) and solve for the likelihood of your beliefs given what you’ve observed, P(belief | observed) ...P.64

#### Exercises

**Q1.** *What piece of information would we need in order to use Bayes’ theorem to determine the probability that someone in 2010 who had GBS also had the flu vaccine that year?*

A1. **P(A | B) = P(A) P(B | A) / P(B)**

**P(vaccine | GBS) = P(vaccine) x P(GBS | vaccine) / P(GBS)**

**From P.60 info, P(GBS | vaccine) is 3/100000 in 2010; P(GBS) is 2/100000. So we need to know P(vaccine) in the general population**

**Q2.** *What is the probability that a random person picked from the population is female and is not color blind?*

A2. **P(female, not color blind) = P(female) x P(not color blind | female) --> From P.61 info, 0.5 x (1 - 0.005) --> 0.4975**

**Q3.** *What is the probability that a male who received the flu vaccine in 2010 is either color blind or has GBS?*

A3. **P(color blind OR GBS | male,vaccine) = P(cb | male,vaccine) + P(GBS | male,vaccine) - P(cb,GBS | male,vaccine)**

**0.08 + 0.00003 - (0.08 x 0.00003) --> 0.0800276**

[Book answer (P.236) says P(cb | male) = 4/1000 ...but P.61 says differently, and is claimed to be the source(??)]
[Online solutions [https://nostarch.com/learnbayes](https://nostarch.com/learnbayes) say 4/1000. Cannot see a form/way to mention the error(??) to publisher]


---

### 7. Bayes' Theorem with LEGO

* **Bayes theorem** rearranged from Chapt6 : P(A | B) = P(B | A) P(A) / P(B) ...P.67

#### Exercises

**Q1.** *Kansas City, despite its name, sits on the border of two US states: Missouri and Kansas. The Kansas City metropolitan area consists of 15 counties, 9 in Missouri and 6 in Kansas. The entire state of Kansas has 105 counties and Missouri has 114. Use Bayes’ theorem to calculate the probability that a relative who just moved to a county in the Kansas City metropolitan area also lives in a county in Kansas. Make sure to show P(Kansas) (assuming your relative either lives in Kansas or Missouri), P(Kansas City metropolitan area), and P(Kansas City metropolitan area | Kansas)*

A1. **P(A | B) = P(B | A) P(A) / P(B)**

**P(Kansas | KCMA) = P(KCMA | Kansas) P(Kansas) / P(KCMA) --> 6/15 = (6/105) x (105/219) / (15/219) ...2/5**

**Q2.** *A deck has 52 cards with suits that are either red or black. There are four aces: two red and two black. You remove a red ace from the deck and shuffle the cards. Your friend pulls a black card. What is the probability that it is an ace?*

A2. **P(A | B) = P(B | A) P(A) / P(B)**

**P(Ace | Black) = P(Black | Ace) P(Ace) / P(Black)**

**If red ace replaced : 2/26 = (2/4) x (4/52) / (26/52) ...1/13**

**If red ace NOT replaced : 2/26 = (2/3) x (3/51) / (26/51) ...1/13 again**


---

### 8. The Prior, Likelihood, and Posterior of Bayes' Theorem

* Ratio : If we just want to compare hypotheses, we don’t need to know P(D) (ie. don't need to normalize) ...P.78
* Bayes' theorem (for ratio) : P(H | D) ∝ P(H) × P(D | H) ...'Posterior probability is proportional to Prior probability multiplied by the Likelihood'. (P(D) is notably absent) ...P.80

#### Exercises

**Q1.** *As mentioned, you might disagree with the original probability assigned to the likelihood: P(brokenwindow, openfrontdoor, missinglaptop | robbed) = 3/10. How much does this change our strength in believing H1 over H2?*

A1. **Likelihood : P(D | H1) = 3/10. Ratio of the two posteriors is proportional to this likelihood. So if likelihood is doubled (6/10) then our belief in H1 over H2 also doubles (13140)**

**Q2.** *How unlikely would you have to believe being robbed is — our prior for H1 — in order for the ratio of H1 to H2 to be even?*

A2. **Prior : P(H1). Assume that "ratio of H1 to H2 to be even" means 'to be 1'. Based on the P.80 calculation, (which used 1/1000 from P.75), P(H1) would need to be 6570 times smaller  --> P(robbed) would have to be 1/6,570,000**


---

### 9. Bayesian Priors and Working with Probability Distributions

* [HARD TO UNDERSTAND, based on previous Chapters, especially (only?) 'Likelihood' here]

#### Exercises

**Q1.** *A friend finds a coin on the ground, flips it, and gets six heads in a row and then one tails. Give the beta distribution that describes this. Use integration to determine the probability that the true rate of flipping heads is between 0.4 and 0.6, reflecting that the coin is reasonably fair*

A1. **Beta(α,β) ...where α = observed successes = 6; β = observed failures = 1**

**From Chapt5, for use with R : `integrate(function(p) dbeta(p,6,1),0.4,0.6)` --> 0.04256 with absolute error < 4.7e-16 ...Integrating the Beta function between 0.4 & 0.6**

**Q2.** *Come up with a prior probability that the coin is fair. Use a beta distribution such that there is at least a 95 percent chance that the true rate of flipping heads is between 0.4 and 0.6*

A2. **[SEE ANSWER on P.240]**

**Q3.** *Now see how many more heads (with no more tails) it would take to convince you that there is a reasonable chance that the coin is not fair. In this case, let’s say that this means that our belief in the rate of the coin being between 0.4 and 0.6 drops below 0.5*

A3. **[SEE ANSWER on P.240]**


---

## PART III: PARAMETER ESTIMATION

### 10. Intoduction to Averaging and Parameter Estimation

* Parameter : An unknown value that we want to estimate ...P.93
* Averaging (μ) is the most basic form of parameter estimation ...P.94
* Parameter estimation is the most common process for dealing with uncertainty ...P.95

#### Exercises

**Q1.** *It’s possible to get errors that don’t quite cancel out the way we want. In Fahrenheit, 98.6 degrees is the normal body temperature and 100.4 degrees is the typical threshold for a fever. Say a child feels warm and seems sick, but your repeated readings from the thermometer are all between 99.5 and 100.0 degrees: warm, but not quite a fever. You try the thermometer yourself and get several readings between 97.5 and 98. What could be wrong with the thermometer?*

A1. **The thermometer scale may be inaccurate ('biased'). If 'MY' normal temperature is 98.6 and I'm well, but the thermometer reads 97.5 to 98, then I'd assume this (~0.9F) inaccuracy to be in the child's readings as well**

**Q2.** *Given that you feel healthy and have traditionally had a very consistently normal temperature, how could you alter the measurements 100, 99.5, 99.6, and 100.2 to estimate if the child has a fever?*

A2. **Average of child's readings is 99.825. Average of my readings is (without frequency info) 97.75. Assumed 'systematic' error is 98.6 minus 97.75 --> 0.85F. So corrected average of child's readings is 99.825 + 0.85 --> 100.675 ...On average (and for 2 of the 4 readings), a fever is indicated**


---

### 11. Measuring the Spread of Our Data

* **Mean absolute deviation** (MAD) is the average distance of each observation from the mean. It is intuitive, but not as useful mathematically as the other options. ("For mathematicians, the absolute value function can be a bit annoying in practice") ...P.109, 106
* **Variance** is the squared difference of our observations. It is the mathematically preferred method, but we lose the intuitive feel for what our calculation means. (Squaring results in an '**exponential penalty**') ...P.109, 107
* **Standard deviation** (σ) is the square root of the variance. It is mathematically useful and also gives us results that are reasonably intuitive. (In most of the literature, variance is defined simply as σ2!) ...P.109, 108
* By far the most commonly used is the standard deviation, because we can use it, together with the mean, to define a '**normal distribution**' ...P.108

#### Exercises

**Q1.** *One of the benefits of variance is that squaring the differences makes the penalties exponential. Give some examples of when this would be a useful property*

A1. **Chapt11 gives an example of physical distance : "In other words, small differences aren’t nearly as important as big ones, as we would feel intuitively. If someone scheduled your meeting in the wrong room, for example, you wouldn’t be too upset if you ended up next door to the right room, but you’d almost certainly be upset if you were sent to an office on the other side of the country"**

**Q2.** *Calculate the mean, variance, and standard deviation for the following values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10*

A2. **sum = 55 --> mean = 5.5**

**variance = (4.5^2 + 3.5^2 + 2.5^2 + 1.5^2 +0.5^2) x 2 / 10 --> 8.25**

**standard deviation = variance^0.5 --> 2.872**


---

### 12. The Normal Distribution

*  The true goal of parameter estimation isn’t simply to estimate a value, but rather to assign a probability for a range ...P.111
*  To get the probability, integrate the probability density function (PDF) ...P.117
*  `integrate(function(x) dnorm(x,mean=20.6,sd=1.62),10,18)` ...P.118
*  If you have information about your problem besides the μ and σ, it is usually best to make use of that [eg. beta distribution] ...P.118
*  Only when you know nothing about the data other than its mean and variance is it safe to assume a normal distribution ...P.121
*  Normal distribution is important because it allows us to reason about the error in our measurements in a probabilistic way ...P.122


#### Exercises

**Q1.** *What is the probability of observing a value five sigma greater than the mean or more?*

A1. **From P.119 we know that -/+ 3 sigma is 99.7%. So the probability of 3 sigma or more than the mean is 0.0015 (ie. almost zero)**

**From P.120 the probability of 3sigma to 5sigma is 1:5000 (though I don't understand why the ratio increases between successive sigma increments, since slope gets shallower). So 0.0015 / 5000 --> 3.0e-7 (as an estimate)**

[Answers on P.242 suggest a better method, using R : `integrate(function(x) dnorm(x,mean=0,sd=1),5,100)` --> 2.88167e-07 with absolute error < 5.6e-07]

**Q2.** *A fever is any temperature greater than 100.4 degrees Fahrenheit. Given the following measurements, what is the probability that the patient has a fever? : 100.0, 99.8, 101.0, 100.5, 99.7*

A2. **sum = 501; mean = 100.2**

**variance = 0.2^2 + 0.4^2 + 0.8^2 + 0.3^2 + 0.5^2 --> 1.18/5 --> 0.236; variance = 0.4857983**

**`integrate(function(x) dnorm(x,mean=100.2,sd=0.4857983),100.4,110)` --> 0.340282 with absolute error < 3.8e-10**

**Q3.** *Suppose in Chapter 11 we tried to measure the depth of a well by timing coin drops and got the following values: 2.5, 3, 3.5, 4, 2. The distance an object falls can be calculated (in meters) with: distance = 1/2 × G × time^2 ...where G is 9.8 m/s/s. What is the probability that the well is over 500 meters deep?*

A3. **mean time = 15/5 --> 3s; mean distance = 1/2 x 9.8 x 9 --> 44.1m**

**variance time = (0.5^2 + 0 + 0.5^2 + 1 + 1) / 5 --> 0.5; variance distance = 1/2 x 9.8 x 0.5^2 --> 1.225; SD distance = 1.106797m**

**`integrate(function(x) dnorm(x,mean=44.1,sd=1.106797),500,1000)` --> 0 with absolute error < 0**

**This is as expected, even without the R function, as 500m would be (500 - 44.1) / 1.225 --> 372sigma**

[Answers on P.243 suggest a (better?) method, using R for the mean & SD and remaining in time units (but separately calculating a time value for 500m)] [Have I still made an error? (I corrected a typo that affected A3. & A4.)]

**Q4.** *What is the probability there is no well (ie. the well is really 0 meters deep)? There are two good (possible) explanations for this probability being higher than it should (given your observation that there is a well). The first is that the normal distribution is a poor model for our measurements; the second is that I made up values that you likely wouldn’t see in real life. Which is more likely to you?*

A4. **Probability of no well (0 meters deep) will be the same as the probability that the well is at least 88.2m deep (since the normal distribution is symmetrical) ...ie. much higher than the probability in A3, but still expected to be tiny**

**`integrate(function(x) dnorm(x,mean=44.1,sd=1.106797),-100,0)` --> 0 with absolute error < 0**

**Based on the wording in the question, would expect a small but "higher than it should" probability, (which is not what I got). If I'd got that, would expect normal distribution to be a reasonable model in this context, but that values look more widely spread than careful real-life measurements would be**

[Answers on P.244 remained in time units] [Have I still made an error? (I corrected a typo that affected A3. & A4.)]


---

### 13. Tools of Parameter Estimation: The PDF, CDF, and Quantile Function

#### Exercises

**Q1.** *Using the code example for plotting the PDF on P.127, plot the CDF and quantile functions*

A1. ****

**Q2.** *Returning to the task of measuring snowfall from Chapter 10, say you have the following measurements (in inches) of snowfall: 7.8, 9.4, 10.0, 7.9, 9.4, 7.0, 7.0, 7.1, 8.9, 7.4. What is your 99.9 percent confidence interval for the true value of snowfall?*

A2. ****

**Q3.** *A child has visited 30 houses and sold 10 candy bars. She will visit 40 more houses today. What is the 95 percent confidence interval for how many candy bars she will sell the rest of the day?*

A3. ****


---

### 14. Parameter Estimation with Prior Probabilities


---

## PART IV