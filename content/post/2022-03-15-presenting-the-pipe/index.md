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


In the process of working with your data, you are going to have a series of steps you perform to get to the final product.
For example,
you might start out with a .csv file that first needs to be loaded.
Then you would perhaps filter out some data that you don't need, maybe calculate an avergage in every group you have, maybe rename a variable if needed,
and then sort the resulting data.
When we perform these tasks,
each one of these actions would probably be a line of code that takes the data,
does an action, 
then saves the output.

Often, this results in what is known as the "Multiple object option" which makes reading code a little tiresome and saves unnecessary objects in the environment.


Here's what that would look like:


```{r, eval=FALSE, results='hide', error=FALSE, warning=FALSE, message=FALSE}

library(tidyverse)

df <- mtcars
df_1 <- filter(df, am == 1)
df_2 <- group_by(df_1, cyl)
df_3 <- summarise(df_2, "Average MPG" = mean(mpg))
df_4 <- rename(df_3, "No. of Cylinders" = cyl)
df_final <- arrange(df_4, desc("Average MPG"))

df_final

```

Let's walk through that. First, we saved the built-in dataset, "mtcars" in the objef "df".
Then we executed a series of commands:

1. filtered out observations that do not meet the critereia "am == 1" (transmission type = manual)
2. group the dataset into groups based on "cyl" (number of cylinders)
3. calculate the "Average MPG" (miles per gallon) of each group.
4. rename the variable "cyl" to "No. of Cylinders"
5. sort the data by "Average MPG"

Here's the result:

```

  `No. of Cylinders` `Average MPG`
               <dbl>         <dbl>
1                  4          28.1
2                  6          20.6
3                  8          15.4

```

Ok, that doesn't look impossible to read or figure out once you are familiar with the commands.
But imagine if you had 300 steps in your analysis!
You would end up with 300 objects saved and it would be a mess to read through and troubleshoot errors if there were any.


So how does the pipe come into play?

Above we saved the result of each step into a new object,
with the subsequent step using that old saved object to do its thing and then save a new object.
What the pipe does is allow us to skip this saving part.

Here's how it works. we start off like we did before by saving the built-in dataset, "mtcars" into an object, "df_final".
At the end of the line, 
we enter the pipe operator, " %>% ", and hit enter.

```{r, eval=FALSE, results='hide', error=FALSE, warning=FALSE, message=FALSE}

df_final <- mtcars %>% 

```

Next we replicate the commands from above,
except we don't need to specify any data in the options,
it takes the output from the previous line and uses that!

I'll clarify a little bit.
Let's take a look:

```{r, eval=FALSE, results='hide', error=FALSE, warning=FALSE, message=FALSE}

df_final <- mtcars %>% 
  filter(am == 1) %>% 
  group_by(cyl) %>% 
  summarise("Average MPG" = mean(mpg)) %>% 
  arrange(desc("Average MPG"))

```

Think of the " %>% " operator as saying __"And then"__.


So, we take mtcars __and then__ we:

1. filter out obs that do not meet the critereia "am == 1" __and then__
2. group the dataset into groups based on "cyl" __and then__
3. calculate the "Average MPG" of each group. __and then__
4. rename the variable "cyl" to "No. of Cylinders" __and then__
5. sort the data by "Average MPG"

```{r, eval=FALSE, results='hide', error=FALSE, warning=FALSE, message=FALSE}

df_final 

  `No. of Cylinders` `Average MPG`
               <dbl>         <dbl>
1                  4          28.1
2                  6          20.6
3                  8          15.4


```

Hopefully, this gives some quick intuition of the pipe!  Give it a try, you won't go back!


