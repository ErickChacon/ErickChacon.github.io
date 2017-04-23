---
title: "Visualizing extreme events with ggplot2"
date: 2017-04-22 23:27:59.00 +01:00
categories:
- data visualization
tags:
- ggplot2
- tidyverse
- R
---


When working with time series, sometimes, it is desired to highlight some events with some particular pattern. For example, highlight periods of time where the variable on interest exceed certain threshold or conversely. With this in mind, I extended an `stat` of `ggplot2` to allow easy visualization of those events. A will show how to use this `stat` using a simulated time series with exponential correlation function.

## Required packages

I will use the `tidyverse` collection of packages, `lubridate` and my package `day2day`. If you want to install `day2day`, you have to use `devtools::install_github("erickchacon/day2day")` to get it.


```r
library(tidyverse)
library(lubridate)
library(day2day)
```

## Simulating correlated time series

I use a exponential correlation function $c(d) = exp(-d/\phi)$ to represent the correlation between two random variables with temporal distance of $d$. Then, in order to simulate $Y \sim N(\mu, \Sigma)$, I use the Cholesky decomposition $\Sigma = LL^\intercal$. Defining $Z \sim N(0, I)$, it can be shown that $LZ \sim N(\mu, LU = \Sigma)$. Hence, I just have to simulate $Z$,`rnorm(n)`, and compute $LZ$.


```r
n <- 300
time <- seq(1, n, 3)
temporal_dist <- as.matrix(dist(time))
cov_matrix <- exp(-temporal_dist/7)
upper_chol <- chol(cov_matrix)
set.seed(1)
precipitation <- t(upper_chol) %*% rnorm(length(time))
time <- ymd("05-01-01") + weeks(time)
data <- data.frame(time, precipitation)
```

Then, the resulting data frame contains the time and the standardized precipitation under analysis as shown below. Note that most of the values are between -2 and 2.


```r
ggplot(data, aes(time, precipitation)) + geom_line()
```

![plot of chunk unnamed-chunk-3]({{site.baseurl}}/assets/images/2017-04-22-visualizing-extremes-unnamed-chunk-3-1.png)

## Visualizing positive and negative events

To start, I would like to highlight the difference between events that are constantly positive or negative. So, I made a try using `geom_area`.


```r
ggplot(data, aes(time, precipitation)) +
  geom_line() +
  geom_point(color = 2, alpha = 0.3) +
  geom_area(alpha = 0.3)
```

![plot of chunk unnamed-chunk-4]({{site.baseurl}}/assets/images/2017-04-22-visualizing-extremes-unnamed-chunk-4-1.png)

It makes the work, but the quality of the `geom_area` when the series change from positive to negative, or conversely, is not good. You can see that there is a difference between the `geom_line` and `geom_area` around these transitions. So, I created a `stat_events` that make the same thing as `geom_area`, but with better quality. Look in the next image how the `lines` and `areas` match perfectly.You can see that code to create `stat_events` in [my day2day package](https://github.com/ErickChacon/day2day/blob/5967cb0daa4e1237d6bcf73a0c3406e33bcf08f3/R/gg-adds.R#L143-L192).



```r
ggplot(data, aes(time, precipitation)) +
  geom_line() +
  geom_point(color = 2, alpha = 0.3) +
  stat_events(alpha = 0.3)
```

![plot of chunk unnamed-chunk-5]({{site.baseurl}}/assets/images/2017-04-22-visualizing-extremes-unnamed-chunk-5-1.png)

The geometry `area` only allow you to make a `ribbon` with a reference point of zero. However, maybe, you would like to differentiate two events using another reference point (e.g. $-0.5$ or $0.5$). This is allow in `stat_events` by defining the threshold of interest. In the next image, I have used `threshold = 0.5`.


```r
ggplot(data, aes(time, precipitation)) +
  geom_line() +
  geom_point(color = 2, alpha = 0.3) +
  stat_events(threshold = 0.5, alpha = 0.3)
```

![plot of chunk unnamed-chunk-6]({{site.baseurl}}/assets/images/2017-04-22-visualizing-extremes-unnamed-chunk-6-1.png)

## Differentiating events

Now it comes the fun part, the main reason I created this `stat` is because I wanted to differentiate two different events by coloring them and probably with a name for the legend. My first thought to highlight particular events (e.g. only positives) was using `subset` on `geom_area`.


```r
ggplot(data, aes(time, precipitation)) +
  geom_line() +
  geom_area(data = subset(data, precipitation > 0), alpha = 0.3)
```

![plot of chunk unnamed-chunk-7]({{site.baseurl}}/assets/images/2017-04-22-visualizing-extremes-unnamed-chunk-7-1.png)

It did not give me good results, because it just jump from one positive event to the next positive event, this jump make the polygons look different from the original time series. For this reason, I added the `event` aesthetics to `stat_events` such as it indicates the event of interest. It should be numeric variable taking $1$ (event), $0$ (no event) and `NA`. With this argument, we can easily identify and draw events exceeding or not certain threshold. Let's assume that flood events are detected when the standardized precipitation is greater than $>0.5$ and droughts when it is lower than $<-0.5$. They can be highlighted as follows.


```r
ggplot(data, aes(time, precipitation)) +
  geom_line() +
  stat_events(aes(event = I(1 * (precipitation > 0.5)), fill = "flood"),
              threshold = 0.5, alpha = 0.3) +
  stat_events(aes(event = I(1 * (precipitation < -0.5)), fill = "drought"),
              threshold = - 0.5, alpha = 0.3)
```

```
## Warning: Ignoring unknown aesthetics: event

## Warning: Ignoring unknown aesthetics: event
```

![plot of chunk unnamed-chunk-8]({{site.baseurl}}/assets/images/2017-04-22-visualizing-extremes-unnamed-chunk-8-1.png)

## Highlighting floods and droughts

McKee defined a drought as a period of time where the standardized precipitation index (SPI) is continuously negative falling down than $-1$ at least one time. Based on this definition, I created a function `find_flood_drought` to detect extreme events using the SPI. You can view the code [here](https://github.com/ErickChacon/day2day/blob/5967cb0daa4e1237d6bcf73a0c3406e33bcf08f3/R/spi-rain.R#L111-L131), Then a visualization of extreme events can be done using `find_flood_drought` and `stat_events` as follows. Note that the event is used as same as before, indicating with a value equals to $1$ that we want to highlight that corresponding value of the precipitation.


```r
data <- data %>% mutate(
  extremes = find_flood_drought(precipitation),
  floods = 1 * (extremes == "flood"),
  droughts = 1 * (extremes == "drought"))

ggplot(data, aes(time, precipitation)) +
  geom_line() +
  stat_events(aes(event = floods, fill = "flood"), alpha = 0.3) +
  stat_events(aes(event = droughts, fill = "drought"), alpha = 0.3)
```

```
## Warning: Ignoring unknown aesthetics: event

## Warning: Ignoring unknown aesthetics: event
```

![plot of chunk unnamed-chunk-9]({{site.baseurl}}/assets/images/2017-04-22-visualizing-extremes-unnamed-chunk-9-1.png)

I hope you have enjoyed this post about visualizing events in a time series and if you are asking yourself how I created the `stat_events` functions, take a view on this tutorial about [extending ggplot2](http://ggplot2.tidyverse.org/articles/extending-ggplot2.html).



