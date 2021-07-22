# goalie-sentiment-analysis

Load required packages

```R
library(tidytext)
library(textdata)
library(ggplot2)
library(dplyr)
library(tidyverse)
```

Import data (code not shown). Data is: single column, header = 'word', rows = individual words spoken. Saved the data as `kelsey`.

Plot a chart of the top 50 most used words (change n to change chart). 

```R
kelsey %>%
  count(word, sort = TRUE) %>%
  top_n(50) %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(x = word, y = n)) +
  geom_col() +
  coord_flip() +
  ggtitle("Top 50 most used words")
```

<img width="779" alt="Screen Shot 2021-07-22 at 7 01 34 PM" src="https://user-images.githubusercontent.com/16511785/126719516-3c7395f6-b82c-4711-8c76-7af78c0af7df.png">


Assign each word spoken either a positive or negative sentiment

```R
new <- kelsey %>%
        inner_join(get_sentiments("bing")) %>%
        count(word, sentiment, sort = TRUE) %>%
        ungroup()
 ```
 Plot word sentiments
 
 ```R
 new %>%
  mutate(word = reorder(word, n)) %>%
  ggplot(aes(x = word, y = n, fill = sentiment)) +
  geom_col() +
  coord_flip() +
  ggtitle("Sentiment analysis of words")
```
<img width="864" alt="Screen Shot 2021-07-22 at 7 03 48 PM" src="https://user-images.githubusercontent.com/16511785/126719644-f89095b0-46ef-467a-8175-da15b93c899d.png">
 
  
