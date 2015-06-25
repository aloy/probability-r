### Defining a random variable

To begin, let's consider the random variable $$X$$ with PMF


$$P(X = k) = \begin{cases}
0.1 & \text{if }k=0\\
0.2 & \text{if }k=1\\
0.3 & \text{if }k=2\\
0.4 & \text{if }k=3 \end{cases}$$

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