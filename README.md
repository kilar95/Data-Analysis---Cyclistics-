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
After making sure the data is appropriate for our purpose, I installed the required packages on Rstudio and uploaded the datasets as shown below:

```
library(janitor) # for data cleaning
library(skimr) # summary statistics about variables
library(dplyr) # data manipulation 
library(lubridate) # date and time manipulation
library(tidyverse) # data analysis
library(ggplot2) # data visualization

setwd("C://Users//ilari//Documents//COURSERA//R//case_study_1")
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
```


## STEP 3: Process

As already mentioned, the software used for this analysis was RStudio. The following code and text chunks explain in detail all the steps taken during the process.





