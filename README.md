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
must approve my recommendations, so they must be backed up with compelling data insights and professional data
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


## STEP 3: Process

As already mentioned, the software used for this analysis was RStudio. The following code and text chunks explain in detail all the steps taken during the process.





