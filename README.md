# R2-Portfolio
This is my second repository for github, for my R2 Bioinformatics class at LaTech.

# GGPlot
## Barplots
Now lets take a look at some ggplot2 barplots

We'll start with making a dataframe based on the tooth data.

```{r}

df <- data.frame(dose= c("DO.5", "D1", "D2"),
                 len = c(4.2, 10, 29.5))

df
```


And now lets make a dataframe

```{r}

df2 <- data.frame(supp=rep(c("VC", "OJ"), each = 3),
                  dose = rep(c("DO.5", "D1", "D2"), 2),
                  len = c(6.8, 15, 33, 4.2, 10, 29.5))

df2
```
Lets load up ggplot2

```{r}

library(ggplot2)
```

Lets set our parameters for ggplot
```{r}
theme_set(
  theme_classic() +
    theme(legend.position = "top")
)
```

Lets start with some basic barplots using the tooth data

```{r}

f <- ggplot(df, aes(x = dose, y = len))

f + geom_col()


```

Now lets change the fill, and add labels to the top

```{r}

f + geom_col(fill = "darkblue") +
  geom_text(aes(label = len), vjust = -0.3)

```

Now lets add the labels inside the bars

```{r}

f + geom_col(fill = "darkblue") +
  geom_text(aes(label = len), vjust = 1.6, color = "white")

```

Now lets change the barplot colors by group

```{r}

f + geom_col(aes(color = dose), fill = "white") +
  scale_color_manual(values = c("blue", "gold", "red"))

```
This is kinda hard to see, so lets change the fill.

```{r}
f + geom_col(aes(fill = dose)) +
  scale_fill_manual(values = c("blue", "gold", "red"))

```

ok how do we do this with multiple groups

```{r}

ggplot(df2, aes(x = dose, y = len)) +
  geom_col(aes(color = supp, fill = supp), position = position_stack()) +
  scale_color_manual(values = c("blue", "gold")) +
  scale_fill_manual(values = c("blue", "gold"))
  
```

```{r}

p <- ggplot(df2, aes(x = dose, y = len)) +
  geom_col(aes(color = supp, fill = supp), position = position_dodge(0.8), width = 0.7) +
  scale_color_manual(values = c("blue", "gold")) +
  scale_fill_manual(values = c("blue", "gold"))
```

```{r}
p

```


Now lets add those labels to the dodged barplot

```{r}

p + geom_text(
  aes(label = len, group = supp),
  position = position_dodge(0.8),
  vjust = -0.3, size = 3.5
)
```

Now what if we want to add labels to our stacked barplots? for this we need dplyr

```{r}
library(dplyr)

df2 <- df2 %>%
  group_by(dose) %>%
  arrange(dose, desc(supp)) %>%
  mutate(lab_ypos = cumsum(len) - 0.5 * len)

```
```{r}
df2
```

Now lets recreate our stacked graphs

```{r}

ggplot(df2, aes(x=dose, y = len)) +
  geom_col(aes(fill = supp), width = 0.7) +
  geom_text(aes(y = lab_ypos, label = len, group = supp), color = "white") +
  scale_color_manual(values = c("blue", "gold")) +
  scale_fill_manual(values = c("blue", "gold"))


```
## Boxplots













































































  
  
  





