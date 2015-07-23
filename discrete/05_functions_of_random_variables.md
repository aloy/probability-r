### Functions of a random variable

Using the `discreteRV` functionality you can also look at functions of your random variable. For example, we might be interested in $$Y = e^X$$. 

To define PMF of $$Y$$ we can simply apply the `exp` function to `X`

```
Y <- exp(X)
```

Once `Y` is defined, we can proceed as before with our calculations.

Sometimes it will be quicker to simply apply the function rather than define
a new random variable. For examples, if we just wanted to calculate $$E\left(e^X \right)$$, then we can simply use the command