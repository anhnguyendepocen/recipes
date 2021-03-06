# R Style Guide for Financial Recipes

The purpose of this document is to define a consistent style-guide for our R
code. Automatic tools may be employed to encourage the use of this style.

A good coding style is like a good writing style — it is good if it is easy for
the target audience to read. The target audience are:

1. **The intended readers of Financial Recipes**.
2. The writers of Financial Recipes.
3. The future maintainers of Financial Recipes.

A style guide helps a reader along by encouraging a consistent writer style.
This style may not suit your artistry, and in select, well-founded cases, you
*can* deviate from this *guideline*, but consider fixing the style guide
instead.

Furthermore, this style guide is likely to be incomplete.

As such, this style guide is written by the people, for the people, and while
suggestions for improvements are always welcome, please avoid
[bike-shedding](http://bikeshed.com/) the conversation.

## Inspiration

What readers of Financial Recipes might expect of our R code:

  1. [Google R Style Guide](https://google.github.io/styleguide/Rguide.xml).
  2. [Advanced R Style Guide](http://adv-r.had.co.nz/Style.html).
  3. [MSU, ZOL851 R Style Guide](https://www.msu.edu/~idworkin/ZOL851_style_guide.html).

An additional source of inspiration is the
[CRAN](https://cran.r-project.org/web/packages/).

## Line Length

Avoid long lines. Long lines are hard to wrap your head around. A good rule of
thumb is roughly 80 (monospaced) characters. See below for when to break your
lines.

## Indentation

Indent your code to make its structure visually apparent at first glance.

Use 2 spaces for indentation (tab defaults to 2 spaces in Jupyter).

## Spacing

Space out your code to make it feel less "cramped".

Place spaces around binary operators (`=`, `+`, `-`, `<-`, etc.).

~~~ .R
# Good
Btau <- (1 - exp(-kap * tau)) / kap

# Bad
Btau<-(1-exp(-kap*tau))/kap
~~~

Always place a space after a comma, but never before it.

~~~ .R
# Good
array(1:3, c(2, 4))
col1 <- sum(x[, 1])
rowl <- sum(x[1, ])

# Bad
array(1:3,c(2,4))
col1 <- sum(x[,1])
row1 <- sum(x[ ,1])
~~~

Place a space before a left parenthesis, except if in connection with a function
call.

~~~ .R
# Good
if (is.nan(x))

# Bad
if(is.nan(x))

# Good
for (x in 1:nQ)

# Bad
for(x in 1:nQ)
~~~

Add extra spacing to achieve more readable alignments.

~~~ .R
# Good
plot(x    = x,
     y    = y,
     type = 'l',
     col  = "blue",
     ylim = c(0.7,1),
     xlab = "time",
     ylab = "price")

# Bad
plot(x, y, type = 'l', col = "blue", ylim = c(0.7,1), xlab = "time", ylab = "price")
~~~

# Curly Braces

An opening curly brace goes on the same line. Do not omit curly braces, they
are easy to forget if you add another line in the future.

~~~ .R
# Good
if (opttype==1) {
  result <- spot * exp(-q * timetomat)
}

# Bad
if (opttype==1) result <- exp(-q * timetomat) * pnorm(d1)

# Bad
if (opttype==1)
  result <- exp(-q * timetomat) * pnorm(d1)

# Bad
if (opttype==1)
{
  result <- exp(-q * timetomat) * pnorm(d1)
}
~~~

An `else` statement should always be surrounded by curly braces.

~~~ .R
# Good
if (opttype==1) {
  result <- exp(-q * timetomat) * pnorm(d1)
} else {
  result <- (spot ^ 2) * exp((r + sigma ^ 2) * timetomat)
}

# Bad
if (opttype==1) {
  result <- exp(-q * timetomat) * pnorm(d1)
}
else {
  result <- (spot ^ 2) * exp((r + sigma ^ 2) * timetomat)
}
~~~

## Assignment

Use `<-`, not `=`, for assignment.

~~~ .R
# Good
x <- 5

# Bad
x = 5
~~~

## Function Definitions and Function Calls

A function definition should first list the argument without default values,
and then those with default values. Of what use is a default value which has to
be set?

If you need line breaks in your function definition or function call, break
them after commas, and indent until the opening brace.

~~~ .R
# Good
BlackScholesFormula  <- function (spot, timetomat, strike, r, sigma,
                                  q = 0, opttype = 1, greektype = 1) {

# Bad
BlackScholesFormula  <- function (spot, timetomat, strike, r, q = 0, sigma, opttype = 1, greektype = 1) {
~~~

## File Organization

### Layout

1. Author comment
2. File description comment
3. Function definitions
4. Executed statements (e.g., `plot`)
