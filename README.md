# Data-Manipulation-Techniques-with-dplyr

Data manipulation techniques refer to the process of adjusting or rearranging data to make it organized and easier to read.

Data manipulation is a crucial function for all types of operations.

If you want to perform any kind of analysis like customer behavior, trend identification, prediction, etc… need to re-arrange the data in the way you need it.

As such, data manipulation techniques provides many benefits.


Data Manipulation Techniques Steps

Different steps involved in data manipulation, you’ll want to understand the general steps of operations.

    You need a database, which is created from your data sources.
    Need to cleanse your data, with data manipulation, you can clean, rearrange and restructure data.
    Develop the data frame for further analysis.
    Then analyze the data, to make all of this information and produce meaningful insights.

In this tutorial, we are going to explain data manipulation with dplyr package.

dplyr is the next iteration of plyr, focusing on only data frames. The main advantages of dplyr package is speed.


Load Library

library(dplyr)
library(readr)

Getting Data

mydata <- read_csv("D:/RStudio/Map/charts.csv")

In this dataset contains 327387 observations and 5 variables. You can download the dataset from here.


Piping %>%

head(mydata, 10)
    date     order Title                    Name                                         week
                                                                    
  1 8/4/1958     1 Poor Little Fool         Ricky Nelson                                    1
  2 8/4/1958     2 Patricia                 Perez Prado And His Orchestra                   1
  3 8/4/1958     3 Splish Splash            Bobby Darin                                     1
  4 8/4/1958     4 Hard Headed Woman        Elvis Presley With The Jordanaires              1
  5 8/4/1958     5 When                     Kalin Twins                                     1
  6 8/4/1958     6 Rebel-'rouser            Duane Eddy His Twangy Guitar And The Rebels     1
  7 8/4/1958     7 Yakety Yak               The Coasters                                    1
  8 8/4/1958     8 My True Love             Jack Scott                                      1
  9 8/4/1958     9 Willie And The Hand Jive The Johnny Otis Show                            1
 10 8/4/1958    10 Fever                    Peggy Lee                                       1
mydata %>% head(10)
10 %>% head(mydata, .)
    date     order Title                    Name                                         week
                                                                    
  1 8/4/1958     1 Poor Little Fool         Ricky Nelson                                    1
  2 8/4/1958     2 Patricia                 Perez Prado And His Orchestra                   1
  3 8/4/1958     3 Splish Splash            Bobby Darin                                     1
  4 8/4/1958     4 Hard Headed Woman        Elvis Presley With The Jordanaires              1
  5 8/4/1958     5 When                     Kalin Twins                                     1
  6 8/4/1958     6 Rebel-'rouser            Duane Eddy His Twangy Guitar And The Rebels     1
  7 8/4/1958     7 Yakety Yak               The Coasters                                    1
  8 8/4/1958     8 My True Love             Jack Scott                                      1
  9 8/4/1958     9 Willie And The Hand Jive The Johnny Otis Show                            1
 10 8/4/1958    10 Fever                    Peggy Lee                                       1



In dplyr the column operations are handled based on a select and mutate functions.
Select

mydata %>%   
select(date, order, Title, Name, 'week') 

Select function used for selecting the columns

date     order Title                    Name                                         week
                                                                    
  1 8/4/1958     1 Poor Little Fool         Ricky Nelson                                    1
  2 8/4/1958     2 Patricia                 Perez Prado And His Orchestra                   1
  3 8/4/1958     3 Splish Splash            Bobby Darin                                     1
  4 8/4/1958     4 Hard Headed Woman        Elvis Presley With The Jordanaires              1
  5 8/4/1958     5 When                     Kalin Twins                                     1
  6 8/4/1958     6 Rebel-'rouser            Duane Eddy His Twangy Guitar And The Rebels     1
  7 8/4/1958     7 Yakety Yak               The Coasters                                    1
  8 8/4/1958     8 My True Love             Jack Scott                                      1
  9 8/4/1958     9 Willie And The Hand Jive The Johnny Otis Show                            1
 10 8/4/1958    10 Fever                    Peggy Lee                                       1
mydata %>%
  select(date:Name, weeks_popular='week')
date     order Title                    Name                                        weeks_popular
                                                                            
  1 8/4/1958     1 Poor Little Fool         Ricky Nelson                                            1
  2 8/4/1958     2 Patricia                 Perez Prado And His Orchestra                           1
  3 8/4/1958     3 Splish Splash            Bobby Darin                                             1
  4 8/4/1958     4 Hard Headed Woman        Elvis Presley With The Jordanaires                      1
  5 8/4/1958     5 When                     Kalin Twins                                             1
  6 8/4/1958     6 Rebel-'rouser            Duane Eddy His Twangy Guitar And The Rebels             1
  7 8/4/1958     7 Yakety Yak               The Coasters                                            1
  8 8/4/1958     8 My True Love             Jack Scott                                              1
  9 8/4/1958     9 Willie And The Hand Jive The Johnny Otis Show                                    1
 10 8/4/1958    10 Fever                    Peggy Lee                                               1
mydata %>%
  select(-'order')
      date     Title                    Name                                         week
                                                                   
  1 8/4/1958 Poor Little Fool         Ricky Nelson                                    1
  2 8/4/1958 Patricia                 Perez Prado And His Orchestra                   1
  3 8/4/1958 Splish Splash            Bobby Darin                                     1
  4 8/4/1958 Hard Headed Woman        Elvis Presley With The Jordanaires              1
  5 8/4/1958 When                     Kalin Twins                                     1
  6 8/4/1958 Rebel-'rouser            Duane Eddy His Twangy Guitar And The Rebels     1
  7 8/4/1958 Yakety Yak               The Coasters                                    1
  8 8/4/1958 My True Love             Jack Scott                                      1
  9 8/4/1958 Willie And The Hand Jive The Johnny Otis Show                            1
 10 8/4/1958 Fever                    Peggy Lee                                       1

Mutate

mydata %>%
  select(date:Name, weeks_popular='week') %>%
  mutate(is_collab = grepl('Featuring', Name)) %>%
  select(Name, is_collab, everything())
    Name                                        is_collab date     order Title                    weeks_popular
                                                                                 
  1 Ricky Nelson                                FALSE     8/4/1958     1 Poor Little Fool                     1
  2 Perez Prado And His Orchestra               FALSE     8/4/1958     2 Patricia                             1
  3 Bobby Darin                                 FALSE     8/4/1958     3 Splish Splash                        1
  4 Elvis Presley With The Jordanaires          FALSE     8/4/1958     4 Hard Headed Woman                    1
  5 Kalin Twins                                 FALSE     8/4/1958     5 When                                 1
  6 Duane Eddy His Twangy Guitar And The Rebels FALSE     8/4/1958     6 Rebel-'rouser                        1
  7 The Coasters                                FALSE     8/4/1958     7 Yakety Yak                           1
  8 Jack Scott                                  FALSE     8/4/1958     8 My True Love                         1
  9 The Johnny Otis Show                        FALSE     8/4/1958     9 Willie And The Hand Jive             1
 10 Peggy Lee                                   FALSE     8/4/1958    10 Fever                                1



In dplyr row operations are handled based on filter, distinct and arrange functions
Filter

mydata %>%
  select(date:Name, weeks_popular='week') %>%
  filter(weeks_popular >= 20, Name == 'Drake' | Name == 'Taylor Swift')
       date       order Title                  Name         weeks_popular
                                             
  1 2/3/2007      43 Tim McGraw             Taylor Swift            20
  2 8/4/2007      39 Teardrops On My Guitar Taylor Swift            20
  3 8/11/2007     33 Teardrops On My Guitar Taylor Swift            21
  4 8/18/2007     34 Teardrops On My Guitar Taylor Swift            22
  5 8/25/2007     38 Teardrops On My Guitar Taylor Swift            23
  6 9/1/2007      49 Teardrops On My Guitar Taylor Swift            24
  7 9/8/2007      50 Teardrops On My Guitar Taylor Swift            25
  8 12/15/2007    44 Teardrops On My Guitar Taylor Swift            26
  9 12/22/2007    30 Teardrops On My Guitar Taylor Swift            27
 10 12/29/2007    24 Teardrops On My Guitar Taylor Swift            28

distinct

mydata %>%
select(date:Name, weeks_popular='week') %>%
filter(Name == 'Jack Scott') %>%
distinct(Title)

This function can be used to keep only unique/distinct rows from a data frame.

    Title                                         
  1 My True Love                     
  2 Leroy                            
  3 With Your Love                   
  4 Geraldine                        
  5 Goodbye Baby                     
  6 Save My Soul                     
  7 I Never Felt Like This           
  8 The Way I Walk                   
  9 There Comes A Time               
 10 What In The World's Come Over You
 11 Burning Bridges                  
 12 Oh, Little One                   
 13 Cool Water                       
 14 It Only Happened Yesterday       
 15 Patsy                            
 16 Is There Something On Your Mind  
 17 A Little Feeling (Called Love)   
 18 My Dream Come True               
 19 Steps 1 And 2                    

In dplyr group operations are handled based on group_by, summarise and count functions.
Group_by & Summarise

mydata %>%
  select(date:Name, weeks_popular='week') %>%
  filter(Name == 'Kalin Twins') %>%
  group_by(Title) %>%
  summarise(total_weeks_popular = max(weeks_popular))
    Title         total_weeks_popular
                          
 1 Forget Me Not                  15
 2 When                            9


Arrange

mydata %>%
  select(date:Name, weeks_popular='week') %>%
  filter(Name == 'Drake') %>%
  group_by(Title) %>%
  summarise(total_weeks_popular = max(weeks_popular)) %>%
  arrange(desc(total_weeks_popular), Title) %>%
  head(10)
     Title                   total_weeks_popular
                                     
  1 God's Plan                               36
  2 Hotline Bling                            36
  3 Controlla                                26
  4 Fake Love                                25
  5 Headlines                                25
  6 Nice For What                            25
  7 Best I Ever Had                          24
  8 In My Feelings                           22
  9 Nonstop                                  22
 10 Started From The Bottom                  22

Count

mydata %>%
  select(date:Name, weeks_popular='week')  %>%
  count(Name) %>%
  arrange(desc(n))
   Name              n
             
  1 Taylor Swift   1021
  2 Elton John      889
  3 Madonna         857
  4 Kenny Chesney   758
  5 Drake           742
  6 Tim McGraw      731
  7 Keith Urban     673
  8 Stevie Wonder   659
  9 Rod Stewart     657
 10 Mariah Carey    621

Conclusion

Based on dplyr package data can easily be modified the way we want and that too very easily.
