# Working in the Console



# Utilizing Packages

When you open an R session you begin the "base" set of packages. While the base functionality of R is still quite nice, you will often want to utilize functionality that exists in a package that is not automatically loaded. 

One such package is the `discreteRV`, a package that makes working with discrete random variables more intuitive. To load this package, use the following command:

```{r}
library(discreteRV)
```

Note that you only need to load a package once during a session. I recommend loading all of the packages you think that you will use first, before continuing on with your work.

For most of you, the above command resulted in the error

```{r}
Error in library(discreteRV) : there is no package called ‘discreteRV’
```

indicating that you have not yet installed the package. To do so, enter the following command:

```{r}
install.packages("discreteRV")
```

Now that the `discreteRV` package is installed you can load the package. When I load this package on my machine I see the following message

```{r}
Attaching package: ‘discreteRV’

The following object is masked from ‘package:base’:

    %in%
```

Even though the letters are displayed in red in the console, don't worry, this is just an informational message. In R if something seriously breaks it will be labeled as an `Error`.

