# Clustering-Mixed-Data-types-in-R

Very often we need clustering method where the data types are a mixture of continuous variable, catogorical variables, and variables of binary type. In this project we would discuss an approach to address such situation. As an example we chose a dataset from ISLR package the publicly available "College" dataset.

Let's load the R packages required in this session.
```
set.seed(1680) # for reproducibility

library(dplyr) # for data cleaning
library(ISLR) # This packages has the college dataset
library(cluster) # for calculating gower similarity  matrix and pam
library(Rtsne) # for t-SNE plot
library(ggplot2) # for visualization
```

There are other packages to calculate dissimilarity matrix. We chose this cluster library and would run the daisy function.


Preprocessing the data before clustering.

```
college_clean <- College %>%
  mutate(name = row.names(.),
         accept_rate = Accept/Apps,
         isElite = cut(Top10perc,
                       breaks = c(0, 50, 100),
                       labels = c("Not Elite", "Elite"),
                       include.lowest = TRUE)) %>%
  mutate(isElite = factor(isElite)) %>%
  select(name, accept_rate, Outstate, Enroll,
         Grad.Rate, Private, isElite)
```
glimpse(college_clean)

