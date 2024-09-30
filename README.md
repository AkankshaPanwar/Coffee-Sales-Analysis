---
title: "Coffee Sales Analysis"
author: "Akanksha Panwar"
date: "2024-09-01"
output: html_document
---

# Business Task:

* This dataset contains detailed records of coffee sales from a vending machine.The dataset spans from March 2024 to Present time, capturing daily transaction data. And new information
continues to be added.
* The dataset has 6 columns and 1133 entries.

# Preparing the Data:
## Loading packages
```{r}
library(tidyverse)
library(janitor)
library(reshape2)
```

## Importing Datasets

```{r}
coffee_sales <- read_csv("Coffee sales.csv")
```

# Cleaning Process:

```{r}
glimpse(coffee_sales)
```
![glimpse](https://github.com/user-attachments/assets/023ee0a9-5c46-4fce-a9cf-2bc3fac99a1f)

```{r}
coffee_sales[duplicated(coffee_sales), ]
```
![dupdata](https://github.com/user-attachments/assets/0f8846c4-c1c3-482b-806e-a60eab1715c1)

```{r}
coffee_sales %>% filter(!complete.cases(.)) %>% na.omit(card)
```
![missingdata](https://github.com/user-attachments/assets/76808ecd-7169-436f-a192-849eb0e31f6d)

* The dataset seems to be perfectly clean. No duplicate data, nor missing values.
* All the columns are in the right format too.

# Analysing Data:

```{r}
summary(coffee_sales)
```
![summary](https://github.com/user-attachments/assets/7e651593-4b2e-4ece-900a-424dfaf0cbf6)

* People tend to spend 33 currency on average.
* The dataset contains entries till 31st of July, 2024.

```{r}
coffee_sales %>% select(coffee_name, money) %>% unique()
```
![unique](https://github.com/user-attachments/assets/7db613c4-a4e5-4415-9a2d-b1760a521124)

* The price of each kind of coffee isn't necessarily constant throughout.

# Creating Visualizations:

```{r}
coffee_sales %>% ggplot(aes(fct_infreq(coffee_name)))+
     geom_bar(fill = "#331900")+
     coord_flip()+
     theme_minimal()+
     labs(title = "Demand for each kind of coffee", x = "Kind of Coffee",  y = NULL)
```
![Coffee kinds](https://github.com/user-attachments/assets/6438b900-0df2-4818-9257-a69aeaef4c0b)

```{r}
coffee_sales %>% ggplot(aes(date, money, colour = coffee_name))+
     geom_point(size = 5, alpha = 0.5)+
     geom_smooth(method = lm, se = F)+
     facet_wrap(~cash_type)+
     theme_minimal()+
     labs(title = "Coffee prices", x = "Months", y = "Price")
```
![coffee prices](https://github.com/user-attachments/assets/d1de5241-f56c-4b92-8fd6-ffcb5d9d5501)

# Conclusion:

The insights I have drawn from the graphs above are as follows
* * Among the total beverages sold, the majority is 'Americano with milk'.
* Americano with milk, Latte, and Cappuccino are the most popular drinks.
* Over 5 months, the prices for all the beverages seemed to drop slightly.
* Cortado and espresso seemed the cheapest and Cappuccino, Latte, Hot chocolate, and Cocoa were among the most expensive.
* People tended to pay using cards over cash and since June, cash payment seems to have stopped altogether.

### Thank you for reading!
