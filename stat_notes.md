
# **Viktor TAMS42 brief summery**

## **Don't forget basic set theory ya dummy**
* $P(A\cup B) = P(A) + P(B) - P(A \cap B)$
* $P(A\cup B \cup C) = P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap C) - P(B \cap C) + P(A \cap B \cap C)$

## **Independent events** ##
Two evens A and B are said to be ***independent*** iff

$$P(A \cap B ) = P(A) \cdot P(B).$$

## **Normal approximation for binomial distribution**

For a given random variable $X \sim Bin(n, p)$ we know that

$$\mu = np,$$
$$\sigma^2 = np(1-p).$$

If $\mu \geq 10 \land \sigma^2 \geq 10$ we can make the following approximation:

$$Bin(n, p) \approx N(\mu, \sigma^2) = N(np, np(1-p)).$$

>Just remember that the parameters for our normal approximation have to be greater or equal to 10. The way in which to calculate these parameters can be easily found in the course formula sheet.

# **Point estimators**
## **General**
*  Population mean $\mu$ is usually estimated by the sample mean $\bar X$.
*  Population variance $\sigma^2$ is usually estimated by the sample variance $S^2$.

If the population is normal $X \sim N(\mu,\sigma^2)$, then it follows that

$$\frac{\bar X - \mu}{\sigma / \sqrt{n}} \sim N(0,1) \land\frac{(n-1)S^2}{\sigma^2} \sim X^2(n-1).$$

>These and more can be found in the CI-section of the course formula sheet.


## **Method of moments (MM)**
The ***moment*** of a random variable X is defined as

$$E(X^k), \text{for some } k \in \{1,2,3,\dots\}.$$

The estimate of the ***$k^{th}$ moment*** for a random sample of size n is given by

$$\sum_{i=1}^n\frac{X_i^k}{n}.$$

Unknown parameters $\theta$ in a random pdf can be estimated by solving the following equations:

$$E(X) = \bar x ,\; E(X^2) = \sum_{i=1}^n\frac{X_i^2}{n}, \; E(X^3) = \sum_{i=1}^n\frac{X_i^3}{n}, \; \dotsc .$$

One equation is needed for each unknown variable.

If only one unknown parameter is present then $E(X) = \bar{x}$ suffices to solve the problem.

## **Maximum likelihood method (ML)**

Unknown parameters $\theta$ can be estimated by maximizing the following likelihood function

$$L(\theta) = f(x_1)\cdot f(x_2) \cdot \dotsc \cdot f(x_n), \text{ if the population is continuous,}$$
$$L(\theta) = p(x_1)\cdot p(x_2) \cdot \dotsc \cdot p(x_n), \text{ if the population is discrete.}$$

>To find the maximum do the good ole fashion taking the derivative  and setting it equals to 0.

## **Common attributes for point estimators**

 A point estimator $\hat\theta_0$ is said to be ***unbiased*** iff

$$E(\hat\theta_0) = \theta.$$

 For two unbiased point estimators $\hat\theta_1 \text{ and } \hat\theta_2, \hat\theta_1$ is said to  me more ***efficient*** than $\hat\theta_2$ iff

$$V(\hat\theta_1) < V(\hat\theta_2).$$

# **Confidence intervals**
For a given two sided confidence interval of some population mean
$$I_\mu = (a, b).$$
We can calculate the sample mean as

$$\bar x = b - \frac{b - a}{2}.$$

Furthermore the sample variance $S^2$ can be easily computed from the interval-delta divided by two by equating it to the term added/subtracted to the sample mean in the course formula sheet.

# **Hypotheses testing**
>Remember: To find a suitable TS look in the same spots as for CI in the formula sheet. #TODO some extra information to "de-pseudo" this might  be in order!

## **Significance level**
***Significance level***, (or sometimes just ***level***), denoted by $\alpha$, can be defined as 

$$\alpha = P(Z \geq z^*) \iff z^*  = Z_\alpha\text{ for a one sided test },$$
$$\alpha = P(Z \geq \frac{z^*}{2}) \iff z^*  = Z_\frac{\alpha}{2} \text{ for a two sided test}.$$


>When looking in the tables remember to look for $1-\alpha$ to get the correct answer since the tables refer to P(f(x) $\leq$ x).

## **Critical region**
To find the critical region $C$ of a HT given it's critical value $z^{*}$, simply look at the hypothesis:
$$C= (-\infty , -z^* ) \text{, when } H_a: \theta > x,$$
$$C= (z^*, \infty) \text{, when } H_a: \theta < x,$$
$$C= (-\infty , -z^*) \cup (z^*, \infty) \text{, when } H_a: \theta \neq x.$$

## **P-value**
The ***p-value*** for a null hypothesis $H_0$ is defined as the probability of UL being equal to or more extreme than the TS. Where UL is the underlying random variable for $H_0$. Roughly speaking UL will share the same distribution as TS.

Furthermore the ***p-value*** proves very useful because of the following property:

$$H_0\text{ is rejected} \iff TS \in C \iff \text{p-value} < TS.$$

For any given hypotheses test there are 4 possible outcomes:

$$\{H_0 \text{is rejected, } H_0 \text{is not rejected}\}\times\{H_a \text{ is true, } H_a \text{ is false}\}$$

## **Type 1 error**
A ***Type 1 error*** occurs when we reject the null hypothesis even thought in reality it was correct.

The probability of a type 1 error can be written as as

$$P(\text{Reject } H_0 | H_0 \text{ is true}).$$

>Remember that a type 1 error is the  same as the significance level denoted by $\alpha$. 

## **Type 2 error**
A ***Type 2 error*** occurs when we do not reject the null hypothesis even thought in reality it was false.

The probability of a type 2 error can be written as as

$$P(\text{Do not reject } H_0 | H_0 \text{ is false}).$$

A type 2 error is generally denoted by $\beta$.

## **Power**
The ***Power*** of a test is defined as

$$P(\text{Reject } H_0 | H_0 \text{ is false}).$$

In general it can be described as a measure for how good our test is.

If $H_a$ is not an equality but rather simply the negation of $H_0$ such as

$$H_a < x, H_0 \geq x  \lor H_a < x, H_0 \geq x .$$
Then power cannot be calculated unless probabilities are known for all possible values of the parameter that violate the null hypothesis. Thus one generally refers to a test's power against a specific alternative hypothesis.




