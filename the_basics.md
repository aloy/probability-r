# Working in the Console



# Utilizing Packages

When you open an R session you begin the "base" set of packages. While the base functionality of R is still quite nice, you will often want to utilize functionality that exists in a package that is not automatically loaded. 

One such package is the `discreteRV`, a package that makes working with discrete random variables more intuitive. To load this package, use the following command:

```{r}
library(discreteRV)
```

Note that you only need to load a package once during a session. I recommend loading all of the packages you think that you will use first, before continuing on with your work.

```{r}
install.packages("discreteRV")
```
