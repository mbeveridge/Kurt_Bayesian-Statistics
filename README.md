# Bayesian Statistics the Fun Way
###### Will Kurt

[[@willkurt](https://twitter.com/willkurt)] [[https://www.countbayesie.com/](https://www.countbayesie.com/)]


[[https://nostarch.com/learnbayes](https://nostarch.com/learnbayes)]

*"Frequentist statistics is founded on the idea that probability represents the frequency with which something happens. ... Bayesian statistics, on the other hand, is concerned with how probabilities represent how uncertain we are about a piece of information"*

---

## PART I: INTRODUCTION TO PROBABILITY

### 1. Bayesian Thinking and Everyday Reasoning

#### Exercises

**Q1.** *Rewrite the following statements as equations:*

* *The probability of rain is low* : **P(rain) = low**
* *The probability of rain given that it is cloudy is high* : **P(rain | cloudy) = high** 
* *The probability of you having an umbrella given it is raining is much greater than the probability of you having an umbrella in general* : **P(umbrella | raining) >> P(umbrella)** 

**Q2.** *Organize the data you observe in the following scenario into a mathematical notation. Then come up with a hypothesis to explain this data: [You come home from work and notice that your front door is open and side window is broken. Inside, you immediately notice that your laptop is missing]*

**P(door, window, no-laptop | H1) = high** ...where H1 = burglary

**Q3.** *The following scenario adds data to the previous one. Demonstrate how this new information changes your beliefs and come up with a second hypothesis to explain the data: [A neighborhood child runs up and apologizes profusely for accidentally throwing a rock through your window. They claim that they saw the laptop and didn’t want it stolen, so it is safe at their house]*

**P(door, window, no-laptop | H2, child)** ...where H2 = accident

**P(D | H2) >> P(D | H1)** ...where D = door open, window broken, laptop missing


---

### 2. Measuring Uncertainty

* ¬ symbol means “negation” or “not”. [ie. ¬P(X) == 1 - P(X)] ...P.14
* Ω indicates the set of all events ...P.15

#### Exercises

**Q1.** *What is the probability of rolling two six-sided dice and getting a value greater than 7?* **{2+6, 3+5, 3+6, 4+4, 4+5, 4+6, 5+3, 5+4, 5+5, 5+6, 6+2, 6+3, 6+4, 6+5, 6+6} --> 15/36 --> 0.417**

**Q2.** *What is the probability of rolling three six-sided dice and getting a value greater than 7?* **{1+1+6, 1+2+5, 1+2+6, 1+3+4, 1+3+5, 1+3+6, 1+4+3, 1+4+4, 1+4+5, 1+4+6, 1+5+2, 1+5+3, 1+5+4, 1+5+5, 1+5+6, 1+6+1, 1+6+2, 1+6+3, 1+6+4, 1+6+5, 1+6+6, 2+1+5, 2+1+6, etc etc} --> 181/216 --> 0.838**

**Q3.** *The Yankees are playing the Red Sox. You’re a diehard Sox fan and bet your friend they’ll win. You’ll pay your friend $30 if the Sox lose and receive only $5 if the Sox win. What is the probability you have intuitively assigned to the belief that the Red Sox will win?*

**Odds of 30:5 or 6:1 --> P(win) = 6/7 or 0.857**


---

### 3. The Logic of Uncertainty

* **Product Rule** of probability : P(A,B) = P(A) × P(B) ...P.25
* **Sum Rule** of probability : P(A OR B) = P(A) + P(B) − P(A,B) ...P.29,30

#### Exercises

**Q1.** *What is the probability of rolling a 20 three times in a row on a 20-sided die?* : **P(3 20s) = 1/20 * 1/20 * 1/20 --> 1/8000 or 0.000125**

**Q2.** *There’s a 10% chance of rain tomorrow, and you forget your umbrella half the time you go out. What is the probability that you’ll be caught in the rain without an umbrella tomorrow?* : **P(rain, no-umbrella) = 1/10 * 1/2 --> 1/20 or 0.05**

**Q3.** *Raw eggs have a 1/20,000 probability of having salmonella. If you eat two raw eggs, what is the probability you ate a raw egg with salmonella?* : **1/20000 + 1/20000 - 1/400,000,000 --> 39,999/400E6 or 0.0001**

**Q4.** *What is the probability of either flipping two heads in two coin tosses or rolling three 6s in three six-sided dice rolls?* : **coins: 1/2 * 1/2 --> 1/4; dice: 1/6 * 1/6 * 1/6 --> 1/216; combination: 1/4 + 1/216 - 1/864 --> 219/864 or 0.253**


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

**outcomes k = 1 [1 time, out of n trials]; trials n = 12; probability p = 2/20**

**Q2.** *There are four aces in a deck of 52 cards. If you pull a card, return the card, then reshuffle and pull a card again, how many ways can you pull just one ace in five pulls?*

**k = 1; n = 5; p = 4/52. We are interested in permutations : n!/k!(n-k)! --> 60/(1 x 12) --> 5 ways you can pull one ace in one pull (which can be reasoned without using formula)**

**Q3.** *For the example in Q2, what is the probability of pulling five aces in 10 pulls (remember the card is shuffled back in the deck when it is pulled)?*

**k = 5; n = 10; p = 4/52**
**B(5;10,1/13) = (10!/5!5!) x (1/13)^5 x (12/13)^5 -->
(3628800/120x120) x 0.00000269329 x 0.67017692226 -->
252 * 0.00000180498 -->
0.00045485516 ... ~1/2199**

[Book answer (P.234) says B(5;10,1/13) is ~1/32000 --> 0.00003125 ...I don't see how]
[Using R, `choose(10,5)` is 252]
[Using R, `pbinom(5,10,1/13,lower.tail=TRUE)` minus `pbinom(4,10,1/13,lower.tail=TRUE)` --> 0.9999669 - 0.999512 --> 0.0004549. THIS AGREES WITH MY LONG CALC, above]
[Online solutions [https://nostarch.com/learnbayes](https://nostarch.com/learnbayes) incorrectly say p=1/23 ...but that would give/explain the answer 3.134986e-05. Cannot see a form/way to mention the error to publisher]

**Q4.** *When you’re searching for a new job, it’s always helpful to have more than one offer on the table so you can use it in negotiations. If you have a 1/5 probability of receiving a job offer when you interview, and you interview with seven companies in a month, what is the probability you’ll have at least two competing offers by the end of that month?*

**k >= 2; n = 7; p = 1/5**

**B(2;7,0.2) = (7!/2!5!) x (0.2)^2 x (0.8)^5 ...need to also do for k=3,4,5,6,7 and total the probabilities**

**`pbinom(7,7,0.2,lower.tail=TRUE)` minus `pbinom(1,7,0.2,lower.tail=TRUE)` --> 0.4232832 ...[don't 'minus' k=2 here, as we want k=2 probabililty in our total]**

**`pbinom(1,7,0.2,lower.tail=FALSE)` --> 0.4232832 ...same result**

**Q5.** *You get a bunch of recruiter emails and find out you have 25 interviews lined up in the next month. Unfortunately, you know this will leave you exhausted, and the probability of getting an offer will drop to 1/10 if you’re tired. You really don’t want to go on this many interviews unless you are at least twice as likely to get at least two competing offers. Are you more likely to get at least two offers if you go for 25 interviews, or stick to just 7?*

**k >=2 ; n = 25; p = 1/10**

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

**α = 4; β = 6**

**`integrate(function(p) dbeta(p,4,6),0.6,1)` --> 0.09935258 with absolute error < 1.1e-15**

**Q2.** *You flip the coin 10 more times and now have 9 heads and 11 tails total. What is the probability that the coin is fair, using our definition of fair, give or take 5 percent?*

**α = 9; β = 11**

**`integrate(function(p) dbeta(p,9,11),0.45,0.55)` --> 0.30988 with absolute error < 3.4e-15**

**Q3.** *Data is the best way to become more confident in your assertions. You flip the coin 200 more times and end up with 109 heads and 111 tails. Now what is the probability that the coin is fair, give or take 5 percent?*

**α = 109; β = 111**

**`integrate(function(p) dbeta(p,109,111),0.45,0.55)` --> 0.8589371 with absolute error < 9.5e-15**


---

## PART II: BAYESIAN PROBABILITY AND PRIOR PROBABILITIES

### 6. Conditional Probability

* 'Independent probabilities' often don’t reflect real life ...P.59
* Conditional probabilities allow us to demonstrate how information changes our beliefs ...P.60
* **Product rule** updated as : P(A,B) = P(A) × P(B | A). [This definition works for independent probabilities as well, because for those P(B) = P(B | A) ] ...P.62
* **Sum rule** updated as : P(A or B) = P(A) + P(B) − P(A) × P(B | A) ...P.62
* One of the most amazing things we can do with conditional probabilities is reversing the condition ...P.62
* **Bayes theorem** P(A | B) = P(A) P(B | A) / P(B) ...P.64
*  Bayes’ theorem allows you to reverse P(observed | belief) and solve for the likelihood of your beliefs given what you’ve observed, P(belief | observed) ...P.64

#### Exercises

**Q1.** *What piece of information would we need in order to use Bayes’ theorem to determine the probability that someone in 2010 who had GBS also had the flu vaccine that year?*

**P(A | B) = P(A) P(B | A) / P(B)**

**P(vaccine | GBS) = P(vaccine) x P(GBS | vaccine) / P(GBS)**

**From P.60 info, P(GBS | vaccine) is 3/100000 in 2010; P(GBS) is 2/100000. So we need to know P(vaccine) in the general population**

**Q2.** *What is the probability that a random person picked from the population is female and is not color blind?*

**P(female, not color blind) = P(female) x P(not color blind | female) --> From P.61 info, 0.5 x (1 - 0.005) --> 0.4975**

**Q3.** *What is the probability that a male who received the flu vaccine in 2010 is either color blind or has GBS?*

**P(color blind OR GBS | male,vaccine) = P(cb | male,vaccine) + P(GBS | male,vaccine) - P(cb,GBS | male,vaccine)**

**0.08 + 0.00003 - (0.08 x 0.00003) --> 0.0800276**

[Book answer (P.236) says P(cb | male) = 4/1000 ...but P.61 says differently, and is claimed to be the source(??)]
[Online solutions [https://nostarch.com/learnbayes](https://nostarch.com/learnbayes) say 4/1000. Cannot see a form/way to mention the error(??) to publisher]


---

### 7. Bayes' Theorem with LEGO
### 8. The Prior, Likelihood, and Posterior of Bayes' Theorem
### 9. Bayesian Priors and Working with Probability Distributions


---

## PART III
## PART IV