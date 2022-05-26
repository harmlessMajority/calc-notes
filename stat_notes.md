
  
## **Normal approximation for binomial distribution**

For a given random variable $X \sim Bin(n, p)$ we know that:

$$\mu = np,$$
$$\sigma^2 = np(1-p).$$

If $\mu \geq 10 \land \sigma^2 \geq 10$ we can make the following approximation:

$$Bin(n, p) \approx N(\mu, \sigma^2) = N(np, np(1-p)).$$

>Just remember that the parameters for our normal approximation have to be greater or equal to 10. The way in which to calculate these parameters can be easily found in the course formula sheet.

## **Method of moments (MM)**
The moment of a random variable X is defined as:

$$E(X^k), \text{where } k \in \{1,2,3,\dots\}.$$

$E(x)$ is approximated by:

$$\sum_{i=1}^n\frac{X_i}{n}.$$

The estimate of the $k^{th}$ for a random sample of size n is given by:

$$\sum_{i=1}^n\frac{X_i^k}{n}.$$

>If only one unknown parameter is present then $E(X) = \bar{x}$ suffices to solve the problem.

## **Maximum likelihood method (ML)**

## **Independent events** ##
Two evens A and B are said to be independent iff:

$$P(A \cap B ) = P(A) \cdot P(B).$$


## **Hypotheses testing**
>To find a suitable TS look in the same spots as for CI in the formula cheat.

The p-value for a null hypothesis $H_0$ is defined as the probability of UL being equal to or more extreme than the TS. Where UL is the underlying random variable for $H_0$. Roughly speaking UL will share the same distribution as TS.

Furthermore the p-value proves very useful because of this property:

$$H_0\text{ is rejected} \iff TS \in C \iff \text{p-value} < TS.$$

>Significance level (or sometimes just level), refers to $\alpha.$ When looking in the tables however remember to look for $1-\alpha$ to get the correct answer.

Power is defined as **TODO CHECK THIS**:

$$P(TS \in C | H_a \text{ is true})$$

## **Confidence intervals**











