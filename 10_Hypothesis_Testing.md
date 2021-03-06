Chapter 10 - Hypothesis Testing
================

``` r
library(tidyquant)
library(tidyverse)
```

Lets create the decision table for hypothesis testing.

``` r
hyp_test <- data.frame(Null_is_true = c('Type_1_error', 'Correct_decision'),
                   Alternate_is_true = c("Correct_decision", "Type_2_erroe"))

row.names(hyp_test) <- c("Reject_Null", "Do_not_reject_Null")
hyp_test
```

    ##                        Null_is_true Alternate_is_true
    ## Reject_Null            Type_1_error  Correct_decision
    ## Do_not_reject_Null Correct_decision      Type_2_erroe

The mean of sampling distribution is equal to the population mean. The
standard error of mean is equal to population standard deviation divided
by the sample size.

``` r
x_values <- seq(40,160,1)
y_values <- seq(70,190,1)

tibble(x = x_values,
       y = y_values) %>%
  ggplot(aes(x = x_values, y = dnorm(x_values, mean = 100, sd = 15))) +
  geom_line() +
  geom_segment(aes(x = qnorm(0.975,100,15),
                   y = 0,
                   xend = qnorm(0.975,100,15),
                   yend = dnorm(qnorm(0.975,100,15), 100,15))) +
  geom_segment(aes(x = qnorm(0.025,100,15),
                   y = 0,
                   xend = qnorm(0.025,100,15),
                   yend = dnorm(qnorm(0.025,100,15), 100,15))) +
  geom_text(aes(x = 140, y = 0.006, label = '2.5%\nNull Hypothesis \nRejection area')) +
  geom_text(aes(x = 60, y = 0.006, label = '2.5%\nNull Hypothesis \nRejection area')) +
  annotate("segment", x = 100, xend = 100, y = 0.035, yend = 0.028, colour = "black", 
            alpha=0.6, arrow=arrow()) +
  geom_text(aes(x = 100, y = 0.04, label = 'H0 \nSampling Distribution')) +
  theme_classic() +
  scale_y_continuous(expand = c(0,0)) +
  labs(x = 'X',
       y = 'f(X)')
```

![](10_Hypothesis_Testing_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
x_values <- seq(40,160,1)
y_values <- seq(70,190, 1)
sd_x_values <- seq(40,160,15)
sd_y_values <- seq(80,200,15)

tibble(x = x_values,
       y = y_values) %>%
  ggplot(aes(x = x_values, y = dnorm(x_values, mean = 100, sd = 15))) +
  geom_line() +
  geom_line(data = tibble(y = y_values), aes(x = y_values, y = dnorm(y_values, mean = 130, sd = 15))) +
  geom_segment(aes(x = qnorm(0.95,100,15),
                   y = 0,
                   xend = qnorm(0.95,100,15),
                   yend = dnorm(qnorm(0.95,100,15), 100,15))) +
   annotate("segment", x = 165, xend = 135, y = 0.005, yend = 0.0005, colour = "black", 
            alpha=0.6, arrow=arrow()) +
  geom_text(aes(x = 100, y = 0.025, label = 'H0')) +
  geom_text(aes(x = 130, y = 0.025, label = 'H1')) +
  geom_text(aes(x = 181, y = 0.006, label = 'Null Hypothesis \nRejection area')) +
  theme_classic() +
  scale_y_continuous(expand = c(0,0)) +
  labs(x = 'X',
       y = 'f(X)')
```

![](10_Hypothesis_Testing_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->
