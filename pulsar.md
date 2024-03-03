pulsar
================

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(tidyr)

# Ajustar parâmetros
vertical_margin <- 20
horizontal_margin <- 100
x_size <- 28
y_size <- 25
linewidth <- 4
src <- 'https://gist.githubusercontent.com/borgar/31c1e476b8e92a11d7e9/raw/0fae97dab6830ecee185a63c1cee0008f6778ff6/pulsar.csv'
plot_name <- 'plot.png'


pulsar <- read.csv(src, header = FALSE) %>%
  mutate(row = row_number()) %>%
  gather(col, height, -row) %>%
  mutate(
    col = sub("^V", "", col) %>% as.integer()
  )
```

Plotando o gráfico

``` r
library(ggplot2)
library(ggridges)

ggplot(pulsar, aes(x = col, y = row, height = height, group = row)) +
  geom_ridgeline(min_height = min(pulsar$height),
                 scale= 0.2,
                 size = 1,
                 fill = "black",
                 colour = "white") +
  scale_y_reverse() +
  theme_void() +
  theme(
    panel.background = element_rect(fill = "black"),
    plot.background = element_rect(fill = "black", color = "black"),
  )
```

    ## Warning in geom_ridgeline(min_height = min(pulsar$height), scale = 0.2, :
    ## Ignoring unknown parameters: `size`

![](pulsar_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->
