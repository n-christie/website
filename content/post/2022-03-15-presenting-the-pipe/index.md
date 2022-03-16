---
title: "Presenting the Pipe"
subtitle: ""
excerpt: ""
date: 2022-03-15T14:46:18+01:00
author: ""
draft: true
series:
tags:
categories:
layout: single # single or single-sidebar
---



It's a baffling thing at first.
And then,
once you get the hang of it,
you can't seem to imagine doing anything in another way.
The %>% in R is just darn nifty.


So what's the deal with the pipe?


In the process of working with data, you are going to have a series of steps you perform to get to the final product.
For example,
you might start out with some .csv files that first need to be combined.
Then you would perhaps deal with missing values, maybe do some renaming of variables, maybe create some new variables,
or remove a number of observations that meet certain conditions.
When we perform these tasks,
each one of these actions would probably be a line of code that takes the data,
does an action, 
then saves the output.

Here's the deal.

What?

Why?

How?

Often, what happens is the "Mulitple object option" which makes the data cleaning steps seemiingly straightword.
The output of each step is saved in an object where the following 

```{r, eval=FALSE, results='hide', error=FALSE, warning=FALSE, message=FALSE}

library(tidyverse)

df <- mtcars
df_1 <- filter(df, am == 1)
df_2 <- group_by(df_1, cyl)
df_3 <- summarise(df_2, "Average MPG" = mean(mpg))
df_final <- arrange(df_3, desc("Average MPG"))

df_final



```


```{r, eval=FALSE, results='hide', error=FALSE, warning=FALSE, message=FALSE}

df_final <- mtcars %>% 

```



