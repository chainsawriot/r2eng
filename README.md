
<!-- README.md is generated from README.Rmd. Please edit that file -->

# {r2eng}

<!-- badges: start -->

[![Project Status: WIP – Initial development is in progress, but there
has not yet been a stable, usable release suitable for the
public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)
<!-- badges: end -->

The goal of the {r2eng} (as in ‘R to English’) package is to take an R
expression and ‘translate’ it to an English sentence. Make R speakable\!

The project inspired by [Amelia
McNamara](https://twitter.com/AmeliaMN)’s useR\! 2020 talk
([YouTube](https://www.youtube.com/watch?v=ckW9sSdIVAc),
[slides](https://www.amelia.mn/SpeakingR/#1)).

This project is a work in progress and highly opinionated.

## Installation

You can install the development version of {r2eng} from GitHub with:

``` r
remotes::install_github("matt-dray/r2eng")
```

This package depends on lintr and purrr.

## Example

There’s currently one function in the package: `r2eng()`.

Pass it an R expression like this:

Set speak to `TRUE` for a system call that will read the English
sentence out loud.

``` r
library(r2eng)
# Loading required package: lintr
# Loading required package: purrr
r2eng::r2eng("variable <- 1", speak = TRUE)
# Original expression: variable <- 1
# English expression: variable gets 1
```

``` r
obj <- r2eng::r2eng("hello <- c(TRUE, FALSE, 'banana' %in% c('apple', 'orange'))", speak = FALSE)
obj
# Original expression: hello <- c(TRUE, FALSE, 'banana' %in% c('apple', 'orange'))
# English expression: hello gets a vector of open paren TRUE , FALSE , string 'banana' matches a vector of open paren string 'apple' , string 'orange' close paren close paren
```

``` r
speak(obj)
```

``` r
r2eng::r2eng("mtcars %>% select(mpg > 22) %>% mutate(gear4 = gear == 4)")
# Original expression: mtcars %>% select(mpg > 22) %>% mutate(gear4 = gear == 4)
# English expression: mtcars then select of open paren mpg > 22 close paren then mutate of open paren gear4 = gear double equal 4 close paren
```

``` r
r2eng::r2eng("ggplot(diamonds, aes(x=carat, y=price, color=cut)) + geom_point() + geom_smooth()")
# Original expression: ggplot(diamonds, aes(x=carat, y=price, color=cut)) + geom_point() + geom_smooth()
# English expression: ggplot of open paren diamonds , aes of open paren x = carat , y = price , color = cut close paren close paren + geom_point of open paren close paren + geom_smooth of open paren close paren
```

It can understand the meaning of =

``` r
r2eng::r2eng("x = c(1, 2, 3)")
# Original expression: x = c(1, 2, 3)
# English expression: x gets a vector of open paren 1 , 2 , 3 close paren
```

``` r
r2eng::r2eng("plot(x = c(1, 2, 3), y = c(5, 6, 7))")
# Original expression: plot(x = c(1, 2, 3), y = c(5, 6, 7))
# English expression: plot of open paren x = a vector of open paren 1 , 2 , 3 close paren , y = a vector of open paren 5 , 6 , 7 close paren close paren
```

## Work in progress (WIP)

There is much to do. Most R expressions won’t currently work with the
`r2eng()` function.

  - [ ] Expand the dictionary
  - [x] Split out parentheses for evaluation
  - [ ] Ensure multi-line translation
  - [x] Smart check of expression structure (e.g. ‘=’ will be used as
    gets if used for assignment, but will be ‘is’ elsewhere)
  - [ ] Allow for variant opinions on translations
  - [ ] Account for dialects (dollar, formula, tidyverse, etc, notation)
  - [ ] Test\!
  - [ ] Add vignettes

## Code of Conduct

I welcome contributions.

Please note that the {r2eng} project is released with a [Contributor
Code of
Conduct](https://contributor-covenant.org/version/2/0/CODE_OF_CONDUCT.html).
By contributing to this project, you agree to abide by its terms.
