# How can a wellness technology company play it smart?
## A Bellabeat data analysis case study

<img align="right" width="450" height="425" src="https://repository-images.githubusercontent.com/522069892/740a3949-ac89-4392-b167-194a026604ed">

[Bellabeat]( https://bellabeat.com/) is a high tech manufacturer of health-related products for women. They have a range of products including water bottles, as well as fashionable jewllery and watches. Each of these products collect data that can be accessed on the Bellabeat app. This was released in 2014 for the company's first wearable tracker, Leaf, which measured step-based movement, as well as sleep cycles, hydration and stress. In 2016 the app features were expanded to include guided meditations and breathing exercises. Additionally, in 2018 Bellabeat expanded its catalog with the Period Diary app. This is essentially a menstrual cycle tracking app that allows women to track the length of their mentral cycle, period duration and symptoms. 

**For the purpose of this case study a scenario has been constructed:**                                                                                           
You are a junior data analyst working on the marketing analyst team at Bellabeat. Urška Sršen, cofounder and Chief Executive Officer of Bellabeat, believes that analyzing smart device fitness data could help unlock new growth opporunities for the company. You have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices.

## Ask
### Key stakeholders

1. Urška Sršen: Bellabeat’s cofounder and Chief Creative Officer.

2. Sando Mu: Mathematician and Bellabeat’s cofounder.

3. The Bellabeat marketing analytics team: a team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy.

### Bellabeat products

* Bellabeat app: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.

* Leaf: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.

* Time: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.

* Spring: This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.

* Bellabeat membership: Bellabeat also offers a subscription-based membership program for users. Membership gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health and beauty, and mindfulness based on their lifestyle and goals.

### Business task

Analyze non-Bellabeat smart device data and compare with one Bellabeat product to discover insights to help guide marketing strategies for the company.

### Key Questions

1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers?
3. How could these trends help influence Bellabeat marketing strategy?

## Prepare 

### Data source: 

FitBit Fitness Tracker Data on [Kaggle]( https://www.kaggle.com/datasets/arashnic/fitbit) in 18 CSV files. The data contains smart health data from personal fitness trackers for thirty fitbit users. The data was collected via a survey of personal tracker data, including minute-level output for physical activity, hear rate, and sleep monitoring, through Amazon Mechanical Turk between March 12, 2016 and May 12, 2016. It was updated one year ago, approximately March 2024. The data includes information about daily activity, steps, and heart rate. The data dictionary can be found [here](https://www.kaggle.com/datasets/arashnic/fitbit/discussion/281341).

### Limitations: 

* The sample size is small as 33 individuals were considered, making it difficult to extrapolate results to a wider population.

* The data is about nine years old; the FitBit devices have likely evolved to deliver more accurate results. 

* Since the data was collected through a survey, the results may not be accurate as such participants may not provide honest and accurate answers.
* There are some significant gaps in the data. For instance, data relating to weight only has information from eight users

# Process

## Choosing Data Files

As `dailyActivity_merged.csv ` provides a good summary of steps and calories burned and the `sleepDay_merged.csv` file provides sleep data, these are good overall files to use to analyze patricipant usage. In addition, fitness devices are generally used to track overall health, weight and stress. Therefore, the file `weightLogInfo_merged.csv` containing weight data will be used, as well as the `heartrate_seconds_merged.csv` file.

## Applications
Excel will be used to load the data and initially look for any issues. R will then be used to transform and explore the data.

## Initial Pass Through 

1) Make sure there are no blank entries in the data by using filters.
2) Convert Id field to text data type as no numerical equations are needed for this field. 
3) Convert ActivityDate from Datetime to Date types as no times are given in the data. 
4) In the `weightLogInfo_merged` file, there are only two entries for the Fat field so this will not be used to draw insights.

## Transform and Explore 
All R code can be found [here](https://github.com/barrett203/CapstoneStudy_GoogleAnalytics/blob/main/R%20Script).

1) Load the tidyverse package and data files 
2) Check to see if the data has been loaded correctly
3) Convert the Id field to character data type 
4) Rename ActivityDate, SleepDay, and Date to convert to date data type 

```
activity <-activity %>%
  mutate_at(vars(Id), as.character) %>%
  mutate_at(vars(ActivityDate), as.Date, format = "%m/%d/%y") %>%
  rename("Day"="ActivityDate") 
```
  
  
5) Combine data frames using full joins
6) Add day of the week variable 

```
summary_data <-sleep_day %>%
  full_join(daily_activity, by=c("Id","Day")) %>%
  full_join(weight_info, by=c("Id", "Day")) %>%
  mutate(Weekday = weekdays(as.Date(Day, "m/%d/%Y")))
```

7) Filter and remove duplicate rows; count NAs and distinct entries using Id

```
summary_data <-summary_data[!duplicated(summary_data), ]
sum(is.na(summary_data))
n_distinct(summary_data$Id)
```

The final data frame has 940 variables with 25 variables. There are 33 distinct Id entries total. The number of distinct users in dailyActivity, sleepDay, and weightLogInfo are 33, 24, and 8, respectively. There are 6893 NAs in the combined data.

# Analyze 

## Select summary statistics and visualizations 

```
final_data %>%
  select(TotalSteps,TotalDistance,VeryActiveDistance,ModeratelyActiveDistance,LightActiveDistance,SedentaryMinutes, Calories, TotalMinutesAsleep, WeightKg, BMI, Value) %>%
  summary()
```
![Summary Statistics](https://github.com/barrett203/CapstoneStudy_GoogleAnalytics/blob/main/Summary%20statistics.png "Summary Statistics")

The average user weighs 72.04 kg, has a BMI of 25.19, and spent the most time doing light activities. On average, they also slept 6.9 hours, took 7638 steps, and traveled 5.49 km per day. 

```
# What's the relationship between minutes asleep and sedentary minutes?
ggplot(data=Data1, aes(x=TotalMinutesAsleep, y=SedentaryMinutes)) + geom_point()
```
![Summary Statistics](https://github.com/barrett203/CapstoneStudy_GoogleAnalytics/blob/main/TotalMinutes_Asleep%20and%20Sedentary_Minutes.png "Summary Statistics")









