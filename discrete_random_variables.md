# Discrete Distributions

## General Discrete Distributions

A discrete probability distribution, also known as a probability mass function, 
consists of the possible outcomes and their associated probabilities. While we 
could write out own functions to calculate probabilities from PMFs, the
`discreteRV` package has already done this. 

### Defining a random variable

To begin, let's consider the random variable $$X$$ with PMF

$$P(X = x) = \begin{cases}
0.1 & \text{if }k=0\\
0.2 & \text{if }k=1\\
0.3 & \text{if }k=2\\
0.4 & \text{if }k=3
\end{cases}$$

After loading the `discreteRV` package, we can define the random variable X 
using the command

```
X <- RV(outcomes = c(0, 1, 2, 3), probs = c(0.1, 0.2, 0.3, 0.4))
```

In the above command I have explicitly labeled the inputs, `outcomes` and `probs`,
but this is not necessary if you always enter them in that order. That is, 

```
X <- RV(c(0, 1, 2, 3), c(0.1, 0.2, 0.3, 0.4))
```

is an equivalent command.

Remember that noting printed here because we have simply *defined* the object 
(our random variable) `X`, we haven't asked R to do anything else. Typing `X` into
the console will print the PMF

```
Random variable with 4 outcomes

Outcomes    0    1    2    3
Probs    1/10  1/5 3/10  2/5
```

Once a random variable has been defined, the commands needed to calculate
probabilities, expected values, and variances are much like what you would
write in your notes. 

### Calculating probabilities

To calculate a probability based on a random variable, we use the `P` function
and define the event of interest. Below is a guide for defining these events.

Probability Statement | R Code
--------------------- | ------------
$P(X = 0)$            | `P(X == 0)`
$P(X < 2)$            | `P(X < 2)`
$P(X \le 2)$          | `P(X <= 2)`
$P(X > 2)$            | `P(X > 2)`
$P(X \ge 2)$          | `P(X >= 2)`





## Named Discrete Distributions

Having explored how to work with general discrete random variables in R, it's time 
to discuss how to work with *named* discrete distributions in R. In class we 
discuss some of the most commonly used discrete distributions. Because these distributions  are so commonly used R provides functions to work with their PMFs, 
CDFs, and functions for simulation. To distinguish between the functions different 
prefixes are attached to distribution's name, or an abbreviation of the name.
For example, there are four functions associated with the binomial distribution:

### Binomial

### Poisson

### Geometric

### Negative Binomial

### Hypergeometric