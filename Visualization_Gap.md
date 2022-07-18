Data Visualization -Gapminder dataset
================
Eric Anje
2022-07-17

``` r
#calling libraries
library(gapminder)
library(dplyr, warn.conflicts = F)
library(ggplot2)
library(tidyverse)
```

## Looking at the first six observations

``` r
gapminder %>% head()
```

    ## # A tibble: 6 × 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.
    ## 6 Afghanistan Asia       1977    38.4 14880372      786.

``` r
filter(gapminder, year == 1962) %>%
  ggplot(aes(lifeExp, gdpPercap,color=continent)) +
  geom_point()
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
g1 <- ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, color = continent, size =pop)) +
  geom_point() + scale_x_log10()
g1 + theme(legend.position = "top")+ggtitle("GDP vs Life Expectancy")
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
g2 <- ggplot(gapminder, aes(x = continent, y = gdpPercap, fill = continent))+
geom_boxplot(alpha = 0.5) 
g2 + labs(x = 'Continent', y = 'GDP per Capita [in USD]', title = "GDP per capita per continent")
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
filter(gapminder, year %in% c(1962, 2002)) %>%
   ggplot(aes(pop, gdpPercap, col = continent)) +
    geom_point() +
    facet_grid(. ~ year)
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
filter(gapminder, year %in% c(1962, 2002)) %>%
    ggplot(aes(pop, gdpPercap, col = continent)) +
    geom_point() +
    facet_grid(continent ~ year)
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
gapminder %>%
    filter(country %in%  c("Kenya","Uganda","Tanzania")) %>%
    ggplot(aes(year, pop,col=country)) +
    geom_point()+ggtitle("East Africa Population Trend",subtitle = "Erc scatter")
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
gapminder %>%
    filter(country %in%  c("Kenya","Uganda","Tanzania")) %>%
    ggplot(aes(year, pop,col=country)) +
    geom_line()+ggtitle("East Africa Population Trend",subtitle = "Erc scatter")
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot(data = gapminder) +
  geom_smooth(mapping = aes(x = log(gdpPercap), 
                            y = lifeExp, 
                            colour = continent))+ggtitle("Scatter: Life expectancy vs GDP by continent")
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

### composite plots

``` r
ggplot(data = gapminder) +
  geom_point(mapping = aes(x = log(gdpPercap), y = lifeExp,colour=continent)) +
  geom_smooth(mapping = aes(x = log(gdpPercap), y = lifeExp,colour=continent))
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
ggplot(data=gapminder, aes(x=lifeExp)) + 
    geom_density(size=1.5, fill="yellow", alpha=0.5) +
    geom_histogram(aes(y=..density..), binwidth=4, color="black", fill="purple", alpha=0.5)
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
ggplot(data=gapminder, aes(x=lifeExp, fill=continent)) +
    geom_density(alpha=0.6)
```

![](Visualization_Gap_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->
