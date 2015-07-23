### Simulating Discrete Random Variables

#### Example: Participation in the  First G.O.P. Debate

On July 21, [*The Upshot*](http://www.nytimes.com/interactive/2015/07/21/upshot/election-2015-the-first-gop-debate-and-the-role-of-chance.html?abt=0002&abg=1&_r=0) 
posted an article using simulation to explore the polling results that will 
determine the participants of the first G.O.P. debate of the 2016 presidential 
election cylce. Now that we understand how to define discrete random variables, 
we can replicate their results in R.

The writers averaged five recent polls, [the most recent ABC News/Washington Post poll](http://elections.huffingtonpost.com/pollster/polls/abc-post-22400) 
(which ended on July 17), to find the "true" probability that a randomly selected 
registered Republican will vote for candidate $X$. (This is a strong assumption, 
and certainly needs to be taken with a grain of salt!) This results in the below
PMF:

Candidate ($x$) | $P(X = x)$
--------------- | ----------
Trump           | .168
Bush            | .144
Walker          | .098
Rubio           | .064
Paul            | .064
Carson          | .06
Huckabee        | .056
Cruz            | .052
Christie        | .028
Perry           | .024
Santorum        | .02
Kasich          | .018
Jindal          | .014
Fortina         | .008
Graham          | .004
Pataki          | .004

```
X <- RV(outcomes = c("Trump", "Bush", "Walker", "Rubio", "Paul", "Carson",
                     "Huckabee", "Cruz", "Christie", "Perry", "Santorum",
                     "Kasich", "Jindal", "Fortina", "Graham", "Pataki"), 
        probs = c(.168, .144, .098, .064, .064, .06, .056, .052, .028,
                  .024, .02, .018, .014, .008, .004, .004))
```

Now that we have a random variable and PMF, we can simulate another poll. [The most recent ABC News/Washington Post poll](http://elections.huffingtonpost.com/pollster/polls/abc-post-22400)
polled 341 registered Republican voters, which seems like a reasonable hypothetical 
sample size for a poll conducted between July 21 and August 4 (the deadline Fox News set in the 
[rules](http://press.foxnews.com/2015/05/fox-news-and-facebook-partner-to-host-first-republican-presidential-primary-debate-of-2016-election/) for this debate). To simulate one
possible poll result, assuming that the PMF is correct, we can use the command

```
poll1 <- rsim(X, n = 341)
```

To display the results of this simulation we use the `table` command, divide by
the sample size (341) to obtain proportions, and round to three decimal places.

```
result1 <- round(table(poll1) / 341, 3)
result1
```

```
poll1
    Bush   Carson Christie     Cruz  Fortina   Graham Huckabee   Jindal   Kasich 
   0.150    0.111    0.023    0.044    0.009    0.006    0.053    0.012    0.029 
  Pataki     Paul    Perry    Rubio Santorum    Trump   Walker 
   0.015    0.076    0.026    0.076    0.026    0.243    0.100 
```

Fox News says that the top ten candidates will be invited to the debate. To 
more easily identify the top ten, we can `sort` the results

```
sort(result1, decreasing = TRUE)
```

```
poll1
   Trump     Bush   Carson   Walker     Paul    Rubio Huckabee     Cruz   Kasich 
   0.243    0.150    0.111    0.100    0.076    0.076    0.053    0.044    0.029 
   Perry Santorum Christie   Pataki   Jindal  Fortina   Graham 
   0.026    0.026    0.023    0.015    0.012    0.009    0.006 
```

Fox News will average the results from the five most recent polls, so in order
to complete a single *trial*, we must simulate five polls and find the average
level of support for each candidate. While we could do this manually, there is
a quicker way using the `replicate` function. 

```
polls <- replicate(5, rsim(X, n = 341))
```

Note that the first argument given to the replicate function is the number
of time you wish to replicate the function specified in the second argument. 
The above command results in a 341 $\times$ 5 matrix of results where each
column represents a simulated poll. To calculate the support for each candidate
for each poll, we can use a `for` loop to iterate through each column and use
the `table` command, similar to what we did above.

```
# Initialize the list for results
tallies <- matrix(0, nrow = 16, ncol = 5)
rownames(tallies) <- sort(outcomes(X))

# Iterate through each column of polls
for(i in 1:5) {
  calc <- table(polls[,i]) / 341
  
  # Note that we can use row names to index the matrix
  tallies[rownames(calc), i] <- calc
}

# Display rounded results
round(tallies, 3)
```

```
          [,1]  [,2]  [,3]  [,4]  [,5]
Bush     0.217 0.161 0.161 0.158 0.188
Carson   0.053 0.070 0.053 0.073 0.070
Christie 0.021 0.038 0.021 0.023 0.044
Cruz     0.076 0.067 0.070 0.065 0.065
Fortina  0.015 0.003 0.012 0.006 0.012
Graham   0.000 0.003 0.000 0.006 0.003
Huckabee 0.067 0.085 0.059 0.067 0.067
Jindal   0.012 0.032 0.012 0.006 0.012
Kasich   0.023 0.012 0.021 0.009 0.021
Pataki   0.006 0.006 0.006 0.003 0.000
Paul     0.073 0.079 0.097 0.123 0.076
Perry    0.021 0.035 0.053 0.023 0.032
Rubio    0.062 0.094 0.073 0.050 0.065
Santorum 0.023 0.032 0.015 0.029 0.032
Trump    0.223 0.164 0.217 0.232 0.173
Walker   0.109 0.117 0.132 0.126 0.141
```

Now that we have a nicely formatted matrix of results, it is easy to 
calculate a candidates average level of support by averaging across each row. 
This can easily be done in R using the `rowMeans` command.

```
avg.support <- rowMeans(tallies)
sort(round(avg.support, 3), decreasing = TRUE)
```

```
   Trump     Bush   Walker     Paul     Cruz Huckabee    Rubio   Carson    Perry 
   0.202    0.177    0.125    0.090    0.069    0.069    0.069    0.064    0.033 
Christie Santorum   Kasich   Jindal  Fortina   Pataki   Graham 
   0.029    0.026    0.017    0.015    0.009    0.004    0.002 
```

Thus, in our single simulation, we found that Trump, Bush, Walker, Paul,
Cruz, Huckabee, Rubio, Carson, Perry, and Christie will be invited to the debate.

It is important to note that our results (the averages) are in fact random 
variables, so they will change trial-to-trial. If you want a more stable result, 
then average over a large number of simulations of five polls is a good approach.
To do this, I recommend functionalizing the simulation code.

```
simulate5polls <- function() {
  polls <- replicate(5, rsim(X, n = 341))

  tallies <- matrix(0, nrow = 16, ncol = 5)
  rownames(tallies) <- sort(outcomes(X))

  for(i in 1:5) {
    calc <- table(polls[,i]) / 341
    tallies[rownames(calc), i] <- calc
  }

  return(rowMeans(tallies))
}
```

Notice now that simply typing `simulate5polls` into the console will run one 
simulation. In order to run many simulations, we again appeal to the `replicate`
function. Assume that we would like to run 1000 simulations, then we would run

```
polls1000 <- replicate(1000, simulate5polls())
```

which returns a 341 $\times$ 1000 matrix. Then we simply need to average over
the rows of the matrix to obtain the average of the 1000 simulated results.

```
avgs <- rowMeans(polls1000)
sort(round(avgs, 3), decreasing = TRUE)
```

```
   Trump     Bush   Walker     Paul    Rubio   Carson Huckabee     Cruz Christie 
   0.204    0.174    0.119    0.078    0.077    0.073    0.067    0.063    0.034 
   Perry Santorum   Kasich   Jindal  Fortina   Graham   Pataki 
   0.029    0.024    0.022    0.017    0.009    0.005    0.005 
```
