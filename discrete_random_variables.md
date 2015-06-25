# Discrete Distributions

## General Discrete Distributions

A discrete probability distribution, also known as a probability mass function, 
consists of the possible outcomes and their associated probabilities. While we 
could write out own functions to calculate probabilities from PMFs, the
`discreteRV` package has already done this. 

### Defining a random variable

To begin, let's consider the random variable $X$ with PMF

$$P(X = x) = \begin{cases}
0.1 & \text{if }k=0\\
0.2 & \text{if }k=1\\
0.3 & \text{if }k=2\\
0.4 & \text{if }k=3
\end{cases} $$



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