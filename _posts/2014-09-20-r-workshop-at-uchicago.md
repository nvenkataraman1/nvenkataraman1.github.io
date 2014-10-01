---
layout      : post
title       : R Basics Workshop (at UChicago)
subtitle    : Learning basic data munging and relevant packages
author      : Naveen Venkataraman
comments: True
permalink   : r-basics-workshop-uchicago
---

I conducted an R Workshop at the University of Chicago. This post contains the materials and code adapted from a Slidify presentation. The full presentation and code can be found [on this repo](https://github.com/nvenkataraman1/RBasics).


## Agenda

1. Installing and Loading Packages
2. Reading Data into R - using *jsonlite* package
3. Reshaping Data (Wide to Long format) - using *reshape2* package
4. Data Manipulation - using *dplyr* package
5. Data Visualization - using *ggplot2* package

---

## Installing Packages

* install.packages("packagename")
* library(packagename)

**Exercise 1:** Install and load these packages into the R environment

* httr
* jsonlite
* dplyr
* ggplot2

---

## Reading Data into R

* What is JSON 
    + [http://fx.priceonomics.com/v1/rates/](http://fx.priceonomics.com/v1/rates/)
    + [http://fantasy.premierleague.com/web/api/elements/1/](http://fantasy.premierleague.com/web/api/elements/1/)
    
**Exercise 2:** Fetch your IP address

* URL: [http://ip.jsontest.com/](http://ip.jsontest.com/)

---

## Data Manipulation

* dplyr
* Key features
    + tbl_df()
    + %>% chaining operator
    + Verbs
        + select
        + filter
        + arrange
        + mutate
        + summarise
        
**Exercise 3a:** Come up with a metric for the sports dataset and use dplyr to generate it

**Exercise 3b:** Explain why the metric is relevant

---

## Data Visualization

* ggplot2: Grammar of Graphics
    + Plots as objects
    + Layering aesthetics and options

 **Exercise 4:** Visualize the sports dataset metric

---

## Summary

* Installing and Loading packages in R
* Reading data
    + read.csv
    + jsonlite package
* Data munging using dplyr
* Visualization using ggplot2
* Metrics
    + Context
    + Relevance
    + Communication

---

## Resources

* R, Statistics
    + Basics
        + Coursera: [www.coursera.org](www.coursera.org)
        + R Programming: [https://www.coursera.org/course/rprog](https://www.coursera.org/course/rprog)
    + Advanced
        + [http://adv-r.had.co.nz/](http://adv-r.had.co.nz/)
    
    + R Studio: [www.rstudio.com](www.rstudio.com)
    
* Visualization: 
    + [R Graphics Cookbook](http://amzn.to/1wEDZG7) by Winston Chang
    + [rCharts](rcharts.io) by Ramnath Vaidya
    + [Shiny](http://shiny.rstudio.com/)
    + FlowingData: [www.flowingdata.com](www.flowingdata.com)
    + Tableau (free for UChicago students)
