library(lubridate)
library(dplyr)

name <- c(rep("joe", 7), rep("lulu", 6), rep("abhi",8))
dates <- c("01/12/17","01/11/17","01/10/17","01/9/17","01/08/17","01/07/17","01/06/17",
           "01/12/17","01/11/17","01/10/17","01/9/17","01/8/17","01/07/17","01/12/17",
           "01/11/17","01/10/17","01/9/17", "01/12/17","01/11/17","01/10/17","01/9/17")

df <- data.frame(name, dates)

df1 <- df %>% mutate(dates2 = as.Date(dates, format = "%m/%d/%y")) %>%
  mutate(wday2 = wday(dates2, label = TRUE))

df1 %>% select(name, wday2) %>% group_by(name) %>% summarise(n_days = n_distinct(wday2)) %>% filter(n_days == 7)


# this tells us that Joe has logged on all 7 weekdays, but Lulu and Abhi have not

# good resource for date formats - https://www.r-bloggers.com/date-formats-in-r/
