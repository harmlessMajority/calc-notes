
  
## **Normal approximation for binomial distribution**

For a given random variable $X \sim Bin(n, p)$ we know that:

$$\mu = np,$$
$$\sigma^2 = np(1-p).$$

If $\mu \geq 10 \land \sigma^2 \geq 10$ we can make the following approximation:

$$Bin(n, p) \approx N(\mu, \sigma^2) = N(np, np(1-p)).$$

>Just remember that the parameters for our normal approximation have to be greater or equal to 10. The way in which to calculate these parameters can be easily found in the course formula sheet.

## **Method of moments (MM)**
The ***moment*** of a random variable X is defined as:

$$E(X^k), \text{where } k \in \{1,2,3,\dots\}.$$

$E(x)$ is approximated by:

$$\sum_{i=1}^n\frac{X_i}{n}.$$

The estimate of the ***$k^{th}$ moment*** for a random sample of size n is given by:

$$\sum_{i=1}^n\frac{X_i^k}{n}.$$

>If only one unknown parameter is present then $E(X) = \bar{x}$ suffices to solve the problem.

## **TODO: Maximum likelihood method (ML)**

## **Independent events** ##
Two evens A and B are said to be ***independent*** iff:

$$P(A \cap B ) = P(A) \cdot P(B).$$


## **Hypotheses testing**
>Remember: To find a suitable TS look in the same spots as for CI in the formula sheet.

The ***p-value*** for a null hypothesis $H_0$ is defined as the probability of UL being equal to or more extreme than the TS. Where UL is the underlying random variable for $H_0$. Roughly speaking UL will share the same distribution as TS.

Furthermore the ***p-value*** proves very useful because of the following property:

$$H_0\text{ is rejected} \iff TS \in C \iff \text{p-value} < TS.$$

***Significance level***, (or sometimes just ***level***), denoted by $\alpha$, can be defined as: 

$$\alpha = P(Z \geq z^*) \text{ for a one sided test } \land$$
$$\alpha = P(Z \geq \frac{z^*}{2}) \text{ for a two sided test},\text{where $z^*$ is the critical value.}$$

>When looking in the tables remember to look for $1-\alpha$ to get the correct answer since the tables refer to P(f(x) $\leq$ x).

For any given hypotheses test there are 4 possible outcomes:

$$\{"H_0 \text{is rejected}", "H_0 \text{is not rejected}"\}\times\{"H_a \text{ is true}", "H_a \text{ is false}"\}$$

A ***Type 1 error*** occurs when we reject the null hypothesis even thought in reality it was correct.

Therefore the probability of a type 1 error is given as:

$$P(\text{Reject } H_0 | H_0 \text{ is true})$$

A ***Type 2 error*** occurs when we do not reject the null hypothesis even thought in reality it was false.

Therefore the probability of a type 2 error is given as:

$$P(\text{Do not reject } H_0 | H_0 \text{ is false})$$

***Power*** is defined as: **TODO CHECK THIS**:


$$P(TS \in C | H_a \text{ is true})$$

## **Confidence intervals**

## **Point estimators**
There are two common attribute for point estimators.

1. A point estimator $\hat\theta_0$ is said to be ***unbiased*** iff

$$E(\hat\theta_0) = \theta$$

2. For two unbiased point estimators $\hat\theta_1 \text{ and } \hat\theta_2, \hat\theta_1$ is said to  me more ***efficient*** than $\hat\theta_2$ iff:
 
$$V(\hat\theta_1) < V(\hat\theta_2)$$












