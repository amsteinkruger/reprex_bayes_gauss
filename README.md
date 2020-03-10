
Mock up a posterior predictive from two artificial Gaussian
distributions.

# Packages

``` r
library(tidyverse)
library(ggpubr)
```

# Data

Generate some data, then find a posterior.

``` r
n = 1e+5 # Set a count of observations.
u0 = 0 # Set a mean for the prior probability distribution.
s0 = 10 # Set a standard deviation for "".
u1 = 50 # Set a mean for the likelihood function.
s1 = 5 # Set a standard deviation for "".

dat = tibble(Prior = rnorm(n, 
                           u0, 
                           s0),
             Likelihood = rnorm(n, 
                                u1, 
                                s1),
             Posterior = rnorm(n,
                                ((s0 ^ 2) ^ -1 + (s1 ^ 2) ^ -1) ^ -1 * (u0 / s0 ^ 2 + u1 / s1 ^ 2),
                                (((s0 ^ 2) ^ -1 + (s1 ^ 2) ^ -1) ^ -1 + s1 ^ 2) ^ (1 / 2))) %>%
  pivot_longer(cols = everything(),
               names_to = "Distribution",
               values_to = "Cheshire Cats Observed")
```

# Visualization

Get a neat illustration.

``` r
vis = 
  dat %>% 
  ggplot() +
  geom_density(aes(x = `Cheshire Cats Observed`,
                   color = `Distribution`)) + 
  theme_pubr()

print(vis)
```

![](reprex_bayes_gauss_files/figure-gfm/vis-1.png)<!-- -->
