# Google Data Analytics Capstone Project
###### Ilaria Bertoldi
###### April 2022

## Case Study: How Does a Bike-Share Navigate Speedy Success?

This case study was completed as part of the Google Data Analytics Professional Certificate capstone unit.
As described in the Google Sara Analytics Professional Certificate, this case study will follow the 6 steps of the Data analysis process: Ask, Prepare, Process, Analyse, Share and Act. 
The aforementioned steps were all accomplished by using Rstudio. 

### Scenario

I am a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director
of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore,
my team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights,
my team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives
must approve our recommendations, so they must be backed up with compelling data insights and professional data
visualizations.

### Goal

Driving question: How do annual members and casual riders use Cyclistic bikes differently?

Cyclistic Bike-Share wants to increase member subscriptions for their services because annual members are more profitable than casual riders. Therefore they would like to know how member and casual riders use Cyclistic services differently. The results from this analysis may be used to guide future marketing programs to increase member subscriptions.

## STEP 1 : Ask

Three questions will guide the future marketing program:

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

**This case study focuses on the first question.** 

The key tasks of this first step are the following:
* Identify the business task: analysing the difference in  usage patterns of casual riders and annualm members with the aim to convert casual riders into annual members
* Consider key stakeholders like the **director of marketing**, responsible for the development of campaigns and initiatives to promote the bike-sharing program, and the **Cyclistic's executive team**, which decides weather to approve the recommended marketing program.

## STEP 2: Prepare

This step allows to identify and collect the data from its location and determine its integrity, credibility and accessibility.

### Downloading data
The following files have been downloaded from Divvy Bike's trip data, available at the following [link](https://divvy-tripdata.s3.amazonaws.com/index.html):

* 202101-divvy-tripdata
* 202102-divvy-tripdata
* 202103-divvy-tripdata
* 202104-divvy-tripdata
* 202105-divvy-tripdata
* 202106-divvy-tripdata
* 202107-divvy-tripdata
* 202108-divvy-tripdata
* 202109-divvy-tripdata
* 202110-divvy-tripdata
* 202111-divvy-tripdata
* 202112-divvy-tripdata

Since Cyclistics is a fictional company, the 2021 data used for this project comes from Divvy, a bike-sharing company that operates in Chicago. 
Furthemore, the data used has been made available by Motivate International Inc, under this [license](https://ride.divvybikes.com/data-license-agreement).

Data includes monthly historical trip data from **January 2021** to **December 2021**, organized in csv files. Each csv files contains structured data with 13 colomuns and a variable number of rows. It also complies with ROCCC standards.

The data is credible and free of bias, does not contain private information of the riders, is open-source, it comes from a reliable source and it's original.

### Installing the packages 

Considering the size of the downloaded datasets, I decided to use RStudio as the working tool to complete the data analysis process.

After making sure the data is appropriate for our purpose, I installed the required packages on Rstudio and uploaded the datasets as shown below:

```
library(janitor) # for data cleaning
library(skimr) # summary statistics about variables
library(dplyr) # data manipulation 
library(lubridate) # date and time manipulation
library(tidyverse) # data analysis
library(ggplot2) # data visualization

setwd("C:/Users/ilari/Documents/COURSERA/R/case_study_1")
getwd() # it displays the working directory
```
### Uploading the files
```
Jan_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202101-divvy-tripdata/202101-divvy-tripdata.csv")
Feb_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202102-divvy-tripdata/202102-divvy-tripdata.csv")
Mar_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202103-divvy-tripdata/202103-divvy-tripdata.csv")
Apr_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202104-divvy-tripdata/202104-divvy-tripdata.csv")
May_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202105-divvy-tripdata/202105-divvy-tripdata.csv")
Jun_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202106-divvy-tripdata/202106-divvy-tripdata.csv")
Jul_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202107-divvy-tripdata/202107-divvy-tripdata.csv")
Aug_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202108-divvy-tripdata/202108-divvy-tripdata.csv")
Sep_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202109-divvy-tripdata/202109-divvy-tripdata.csv")
Oct_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202110-divvy-tripdata/202110-divvy-tripdata.csv")
Nov_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202111-divvy-tripdata/202111-divvy-tripdata.csv")
Dec_21 <- read.csv("C:/Users/ilari/Documents/COURSERA/R/case_study_1/trips_2021/202112-divvy-tripdata/202112-divvy-tripdata.csv")
```

### Checking column constistency
Then, before combining the dataset into one single file, the column consistency was checked by ensuring that the columns of the datasets matched perfectly with each other.

```
# making sure all the columns of the datasets match perfectly before combining the datasets into one single file
compare_df_cols_same(Jan_21, Feb_21, Mar_21, Apr_21, May_21, Jun_21, Jul_21, Aug_21, Sep_21, Oct_21, Nov_21, Dec_21)
```
```
[1] TRUE
```
### Joining data
As the result of the function is TRUE the datasets were joined into 'all_trips_21'.

```
# joining the datasets into one single file
all_trips_21 <- bind_rows(Jan_21, Feb_21, Mar_21, Apr_21, May_21, Jun_21, Jul_21, Aug_21, Sep_21, Oct_21, Nov_21, Dec_21)
```

### Inspecting data
```
summary(all_trips_21) # it returns a statistical summary of the data
head(all_trips_21) # it displays the first 6 rows of the dataframe
glimpse(all_trips_21) # returns a summary of each column in the dataframe
colnames(all_trips_21) # lists out all column names
skim_without_charts(all_trips_21) # checking the dataframe structure 
unique(all_trips_21$rideable_type) # to display all unique values of rideble_type
```

### Notes 
* There are 5595063 rows and 13 columns
* There are no duplicates of ride_id, as the number of ride_id unique values corresponds to the number of total rows
* The following columns have missing or empty values: start_station_name, start_station_id, end_station_name, end_station_id, end_lat, end_lng
* There are 3 unique values of rideble_type: "classic_bike", "elctric_bike" and "docked_bike"
* 2 unique values of member_casual: "member" and "casual" 

### What can be done to improve the data
* The columns "started_at" and "ended_at", containing datetime values, should be converted from character class to POSIXtc class
* We could add some additional columns containing different types of information (such as the duration of each ride, the time of the day in which the ride took place, and three columns separating day, month and year) in order to provide more opportunities to aggregate the data. 
* Some columns could be renamed to a more intuitive title

## STEP 3: Process
This step includes data manipulation and data cleaning processes

### Data manipulation
#### Renaming columns

```
all_trips_21 <- rename(all_trips_21, "user_type" = "member_casual") # renaming columns
```
#### Converting datetime values from character to POSIXtc

```
all_trips_21$started_at <- as.POSIXct(all_trips_21$started_at, format = "%Y-%m-%d %H:%M:%S", tz = "EST") # converting values of "started_at" column
all_trips_21$ended_at <- as.POSIXct(all_trips_21$ended_at, format = "%Y-%m-%d %H:%M:%S", tz = "EST") # converting values of "ended_at" column

```

#### Adding new columns 
Let's add the **ride_length** column by calculating the ride duration (in seconds)

```
all_trips_21$ride_length <- difftime(all_trips_21$ended_at, all_trips_21$started_at) # adding ride_length column
```

And now the **day_of_week**, **day**, **month** and **hour** columns by calculating the day of the week, the day, the month and the hour in which each ride started

```
all_trips_21$date <- as.Date(all_trips_21$started_at) # adding date column

#adding month, day, day_of_week and hour columns

all_trips_21 <- all_trips_21 %>%
  mutate(month = lubridate::month(all_trips_21$date),
         day = lubridate::day(all_trips_21$date),
         day_of_week = lubridate::wday(all_trips_21$date, label=TRUE, locale="English"),
         hour = lubridate::hour(all_trips_21$started_at)) 

```

Lastly we'll add the the **time_of_day** column

```
ll_trips_21 <- all_trips_21 %>%       # adding hour column
  mutate(time_of_day = case_when (
    hour >= 5 & hour < 12 ~ "Morning",
    hour >= 12 & hour < 18 ~ "Afternoon",
    hour >= 18 & hour < 22 ~ "Evening",
    hour < 5 | hour >= 22 ~ "Night" 
  ))                                   
```

#### Inspecting data

Let's inspect once again the dataframe

```
skim_without_charts(all_trips_21) # checking the dataframe structure 
```

#### Observations

* The maximum value of **ride_length** equals to 3356649 seconds, which corresponds to 932.4 hours. This value is an oulier and then considered invalid.
* The minimum value of **ride_length** is negative. Again, it is considered invalid.

#### In order to run calculation on the data we should convert "ride_length" from difftime to numeric class

```
all_trips_21$ride_length <- as.numeric(all_trips_21$ride_length) # converting ride_length from difftime to numeric
class(all_trips_21$ride_length) # checking if ride_length has successfully been converted to numeric
```

### Data cleaning
We must now remove all data that is incorrect, invalid or inaccurate from our dataframe, such as:

* rides with negative ride_length values
* rides with ride_length less than 60 seconds, as the company's website states that they potentially result from false starts or from user trying to re-dock a bike to ensure it is secured. 
* rides with ride_length greater that 24 hours
* rides with NA in end_lat or end_lng, which are considered invalid since the rides were not ended properly

#### Removing invalid rides
```
trips_v2 <- all_trips_21 %>%
  filter(!(ride_length < 60)) %>% # filtering rides with ride_length values greater than 60 seconds
  filter(!(ride_length > 86400)) %>% # filtering rides with ride_length values less than 24h
  filter (!(is.na(end_lat)) | !(is.na(end_lng))) # removing rides with NA values in end_lat or end_lng
```
#### Inspecting dataframe 

```
summary(trips_v2$ride_length) # checking the min and max value of ride_length

which(is.na(trips_v2$end_lng)) # checking if there still are NA values in end_lng or end_lat 
which(is.na(trips_v2$end_lat))
```

The results show that: 
* the min value of **ride_length** is now 60 seconds, as expected;
* the max value of **ride_length** is now 86391, or 23.99 hrs;
* all rides with NA values in the ending coordinates have been removed.


### Verifying Data Integrity
The data is now clean, accurate, consistent and complete.

* **Remove Duplicates**: Data does not have any duplicate values
* **Check for Outliers** : Outliers have been removed
* **Check for Missing Values**: Invalid data with missing values have been removed
* **Check Data Accuracy**: After removing bad data, all the remaining data is within its speculated range and hence accurate
* **Check Data Completeness** : All matrices are available to answer the Business Question
* **Check Data Consistency**: All 12 months of data have consistent format and structure, thus making it easier to combine into 1 single dataset
* **Check Data Relevance**: The dataset contains ridership data of past 12 months, thus the data is current and not outdated
* **Check Data Formats**: The columns have been typecast correctly and have appropriate data formats
* **Date-Time Format Consistency**: All throughout the dataset the date and time are in consistent format
* **Column Names**: All the column names are clear and meaningful
* **Overall sense of Data**: Given the knowledge of the business, the data makes sense


## STEP 4 : Analysis
Statistical summary of data about ride_length

```
summary(trips_v2$ride_length)
```
```
Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
     60     417     731    1181    1318   86391 
```

### Comparing ride_length data of casual riders and annual members 
```
# Descriptive analysis on ride_length (all figures in seconds)
trips_v2 %>% 
  group_by(user_type) %>% 
  summarise(avg_ride_length = mean(ride_length), #straight average (total ride length / rides)
            median_ride_length = median(ride_length), #midpoint number in the ascending array of ride lengths
            max_ride_length = max(ride_length), #longest ride
            min_ride_length = min(ride_length))  #shortest ride
```

Results:
```
 user_type avg_ride_length median_ride_length max_ride_length min_ride_length
  <chr>               <dbl>              <dbl>           <dbl>           <dbl>
1 casual              1625.                971           86391              60
2 member               813.                586           86024              60
```

Visualizing data:

```
trips_v2 %>%
  group_by(user_type) %>%
  summarise(avg_RL = mean(ride_length)) %>% 
  ggplot() + geom_col(mapping = aes(x = user_type, y = avg_RL, fill = user_type), width = 0.3) +
  labs(title= "Average ride length", subtitle= "Comparison between members and casual users", x = "User type", y = "Average ride length") +
  scale_fill_discrete(name = "User type:") # changing legend title
```


<img src="https://user-images.githubusercontent.com/104167965/171154790-9ff8070d-ac65-450b-aea2-923576404a17.png" width="700">


* **The average ride length of the casual rider is more than twice as long as the average ride duration of an annual member.**  

### Analyzing average ride length and total number of rides of annual and casual members by day of week

```
trips_v2 %>%
  group_by(user_type, day_of_week) %>% # groups by usertype and weekday
  summarise(number_of_rides = n(), avg_rl = mean(ride_length)) %>% # calculates the number of rides and the average duration
  arrange(user_type, day_of_week) # sort

```
Results:
```
# A tibble: 14 x 4
# Groups:   user_type [2]
   user_type day_of_week number_of_rides avg_rl
   <chr>     <ord>                 <int>  <dbl>
 1 casual    Sun                  514659  1851.
 2 casual    Mon                  295305  1693.
 3 casual    Tue                  265269  1505.
 4 casual    Wed                  268456  1434.
 5 casual    Thu                  275044  1400.
 6 casual    Fri                  344830  1482.
 7 casual    Sat                  526563  1737.
 8 member    Sun                  390835   931.
 9 member    Mon                  392944   797.
10 member    Tue                  448162   768.
11 member    Wed                  462267   764.
12 member    Thu                  444985   764.
13 member    Fri                  443811   785.
14 member    Sat                  430629   901.
```
Visualizing average ride length by weekday
```
trips_v2 %>%
  group_by(user_type, day_of_week) %>%
  summarise(avg_RL = mean(ride_length)) %>% 
  ggplot() + geom_col(mapping = aes(x = day_of_week, y = avg_RL, fill = user_type),position = "dodge", width = 0.7) +
  labs(title= "Average ride length by each day of week", subtitle= "Comparison between members and casual users", x = "Weekday", y = "Average ride length") +
  scale_fill_discrete(name = "User type:")
```

<img src = "https://user-images.githubusercontent.com/104167965/172907388-abb66fa2-b50c-48cc-a6bb-3ae464db726d.png" width="700">

* **Average ride length of casual riders reaches its highest point in the weekend**
* **Average ride length of annual members is fairly constant during all week**
* **Sunday is the day of week with longest average ride lenght for both user types**

Visualizing number of rides by weekday:
```
trips_v2 %>% 
  group_by(user_type, day_of_week) %>% 
  summarise(number_of_rides = n()) %>% 
  ggplot(aes(x = day_of_week, y = number_of_rides, fill = user_type)) + geom_col(position = "dodge", width = 0.7) +
  labs(title = "Number of rides for each user type by weekday", x = "Weekday", y = "Number of rides")
```

<img src="https://user-images.githubusercontent.com/104167965/172833589-b7826e93-5a82-4ae9-96e6-ac7026f2cf0c.png" width="700">

* **The number of rides for casual riders is higher during the weekend**
* **The number of rides for annual members is higher on weekdays**
* **Members rides are much more than casual rides on weekdays and less on weekends**


### Analyzing ridership data by type of bike and user type

```
trips_v2 %>% 
  group_by(user_type, rideable_type) %>% 
  summarise(number_of_rides = n()) %>% 
  ggplot() + geom_col(mapping = aes(x = user_type, y = number_of_rides, fill = rideable_type), width = 0.3)+
  labs(title = "Total number of rides by user type and type of bike", x = "User type", y = "Number of rides")+
  scale_fill_discrete("Type of bike")
```

<img src="https://user-images.githubusercontent.com/104167965/171154479-68bb4349-e128-4fef-aa89-4fdcc243be2b.png" width="700">

* **Total number of member rides is greater than the total number of casual rides**
* **Docked bikes are used only by casual riders**
* **The most used type of bike is the classic bike, both for members and casual riders**

### Analyzing total number of monthly rides for each user_type

```
# first, let's convert month numbers in "month" column into month names abbreviations
trips_v3 <- trips_v2 %>%
  mutate(month = month.abb[month]) 
```
```
# then let's make the plot
trips_v3 %>% 
  group_by(user_type, month) %>% 
  summarise(number_of_rides = n()) %>% 
  ggplot(aes(x = month, y = number_of_rides, group = user_type, color = user_type)) + 
  geom_line(size = 1.3) + geom_point(size = 2.5) + 
  labs(title = "Number of monthly rides for each user type", x = "Month", y = "Number of rides") +
  scale_x_discrete(limits = month.abb)
```

<img src="https://user-images.githubusercontent.com/104167965/172854121-273b3ba7-7195-420b-b69d-ee8c4ad86ddc.png" width="700">

* **The number of rides for casual riders is at its highest point during the summer, specifically in June, July and August**
* **The number of rides for annual members is at its highest in July, August, September and October**
* **Both casual riders and annual members reach their lowest number of rides in December, January and February**

### Analyzing total number of rides by time of day
```
trips_v3 <- trips_v3 %>% 
  mutate(time_of_day = factor(time_of_day, levels = c("Morning","Afternoon","Evening","Night")))
trips_v3 %>% 
  group_by(user_type, time_of_day) %>% 
  summarise(number_of_rides = n()) %>% 
  arrange(user_type)
```
Results:
```
# A tibble: 8 x 3
# Groups:   user_type [2]
  user_type time_of_day number_of_rides
  <chr>     <fct>                 <int>
1 casual    Morning              458648
2 casual    Afternoon           1127257
3 casual    Evening              596638
4 casual    Night                307583
5 member    Morning              836816
6 member    Afternoon           1289517
7 member    Evening              682416
8 member    Night                204884
```
Visualizing:
```
trips_v3 %>% 
  group_by(user_type, time_of_day) %>% 
  summarise(number_of_rides = n()) %>% 
  ggplot(aes(x = time_of_day, y = number_of_rides, group = user_type, color = user_type)) + 
  geom_line(size = 1.3) + geom_point(size = 2.5)+
  labs(title = "Number of rides for each user type by time of day", caption = "Morning: 5:00-12:00, Afternoon: 12:00-18:00, Evening: 18:00-22:00, Night: 22:00-5:00", x = "Time of day", y = "Number of rides")

```
<img src="https://user-images.githubusercontent.com/104167965/172930483-ad92e0e3-0d45-4f74-a6f2-8764e872c583.png" width="600">

* **Total number of rides of both annual members and casual riders reaches its peak in the afternoon**
* **On the contrary, as expected, night is the less busy time of the day for both user types**
* **In the morning member's number of rides are much more than casual riders's number of rides**

### Top starting and ending stations 

Top 5 **starting stations** for annual members and casual riders:
```
members_start <- trips_v3 %>% 
  filter(!(is.na(start_station_name) | start_station_name == "")) %>%
  filter(user_type == "member") %>%
  group_by(start_station_name) %>% 
  summarise(number_of_rides =n()) %>% 
  arrange(-number_of_rides) %>% 
  top_n(5)

casual_start <- trips_v3 %>% 
       filter(!(is.na(start_station_name) | start_station_name == "")) %>%
       filter(user_type == "casual") %>%
       group_by(start_station_name) %>% 
       summarise(number_of_rides =n()) %>% 
       arrange(-number_of_rides) %>% 
       top_n(5)
```
Results for annual members:
```
# A tibble: 5 x 2
  start_station_name       number_of_rides
  <chr>                              <int>
1 Clark St & Elm St                  24368
2 Wells St & Concord Ln              23398
3 Kingsbury St & Kinzie St           23235
4 Wells St & Elm St                  20740
5 Dearborn St & Erie St              19265
```
Results for casual riders:
```
# A tibble: 5 x 2
  start_station_name      number_of_rides
  <chr>                             <int>
1 Streeter Dr & Grand Ave           65445
2 Millennium Park                   33077
3 Michigan Ave & Oak St             29391
4 Shedd Aquarium                    22918
5 Theater on the Lake               21057
```
Visualizing:

```
members_start %>%
  ggplot () + geom_col(aes(x = number_of_rides, y = reorder (start_station_name, number_of_rides), fill = number_of_rides)) +
  labs(title = "Top 5 most popular starting stations for casual rides", x = "Start Station Name", y = "Number of rides")

casual_start %>%
  ggplot () + geom_col(aes(x = number_of_rides, y = reorder (start_station_name, number_of_rides), fill = number_of_rides)) +
  labs(title = "Top 5 most popular starting stations for annual members", x = "Start Station Name", y = "Number of rides")
```

<img src="https://user-images.githubusercontent.com/104167965/173118131-d261643c-0d90-4135-9b0c-218416a17328.png" width="700">

<img src="https://user-images.githubusercontent.com/104167965/173118230-1b34720b-864f-4bda-8573-8f9fa69a0e28.png" width="700">


Top 5 **ending** stations:
```
members_end <- trips_v3 %>% 
  filter(!(is.na(end_station_name) | end_station_name == "")) %>%
  filter(user_type == "member") %>%
  group_by(end_station_name) %>% 
  summarise(number_of_rides =n()) %>% 
  arrange(-number_of_rides) %>% 
  top_n(5)

casual_end <- trips_v3 %>% 
  filter(!(is.na(end_station_name) | end_station_name == "")) %>%
  filter(user_type == "casual") %>%
  group_by(end_station_name) %>% 
  summarise(number_of_rides =n()) %>% 
  arrange(-number_of_rides) %>% 
  top_n(5)

```
Results for annual members:
```
# A tibble: 5 x 2
  end_station_name         number_of_rides
  <chr>                              <int>
1 Clark St & Elm St                  24556
2 Wells St & Concord Ln              24092
3 Kingsbury St & Kinzie St           23335
4 Wells St & Elm St                  21370
5 Dearborn St & Erie St              19999
```
Results for casual riders:
```
# A tibble: 5 x 2
  end_station_name        number_of_rides
  <chr>                             <int>
1 Streeter Dr & Grand Ave           67912
2 Millennium Park                   34201
3 Michigan Ave & Oak St             30873
4 Theater on the Lake               22522
5 Shedd Aquarium                    21302
```
Visualizing:
```
members_end %>%
  ggplot () + geom_col(aes(x = number_of_rides, y = reorder (end_station_name, number_of_rides), fill = number_of_rides)) +
  labs(title = "Top 5 most popular ending stations for casual rides", x = "End Station Name", y = "Number of rides")

casual_end %>%
  ggplot () + geom_col(aes(x = number_of_rides, y = reorder (end_station_name, number_of_rides), fill = number_of_rides)) +
  labs(title = "Top 5 most popular ending stations for annual members", x = "End Station Name", y = "Number of rides")
```


<img src="https://user-images.githubusercontent.com/104167965/173118700-45b3db6e-fde8-411c-aab8-d79043a11929.png" width="700">

<img src="https://user-images.githubusercontent.com/104167965/173118751-752e4442-a139-42fd-82ce-b14744f6f61e.png" width="700">

## STEP 5 : Share
Create a csv file that we will visualize in Tableau
```
write.csv(trips_v3, file = "trips_v3.csv")
```
Link to the Interactive Tableau Dashboard


## STEP 6: Act

### Conclusions
The average ride length for casual rides is 30 minutes which is more than double of that of member rides - 13 minutes

No. of casual rides are highest in June, July and August with its peak in July and lowest in December, January and February
No. of member rides are highest in July, August and September with its peak in September and lowest in December, January and February
Casual rides are highest on weekends- Saturday and Sunday with the highest average ride lengths
Member rides are lowest on weekends
Both casual and member rides peak in the afternoon time ie. 12PM to 5PM

The top 5 ride starting and ending stations for casual users are- Streeter Dr & Grand Ave, Millennium Park, Michigan Ave & Oak St, Shedd Aquarium and Theater on the Lake

### Recommendations
To attract the maximum number of Casual riders, promotion with subscription offers shall be done during the months of June, July and August  

Subscription booth shall be set up on the top 5 docking stations for Casual riders during afternoon time ie. 12PM-5PM on weekends to give away “Weekend discounts” to membership subscriptions, leveraging the heavy weekend traffic

Marketing strategies should emphasize on “more number of trips and shorter trip lengths” for casual riders





