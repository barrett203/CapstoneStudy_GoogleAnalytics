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

FitBit Fitness Tracker Data on [Kaggle]( https://www.kaggle.com/datasets/arashnic/fitbit) in 18 CSV files. The data contains smart health data from personal fitness trackers for thirty fitbit users. The data was collected via a survey of personal tracker data, including minute-level output for physical activity, hear rate, and sleep monitoring, through Amazon Mechanical Turk between March 12, 2016 and May 12, 2016. It was updated one year ago, approximately March 2024. The data includes information about daily activity, steps, and heart rate. 

### Limitations: 

* The sample size is small as only 30 individuals were considered, making it difficult to extrapolate results to a wider population.

* The data is about six years old; the FitBit devices have likely evolved to deliver more accurate results. 

* Since the data was collected through a survey, the results may not be accurate as such participants may not provide honest and accurate answers.

# Process

## Choosing Data Files

As `dailyActivity_merged.csv ` provides a good summary of steps and calories burned and the `sleepDay_merged.csv` file provides sleep data, these are good overall files to use to analyze patricipant usage. In addition, fitness devices are generally used to track overall health, weight and stress. Therefore, the file `weightLogInfo_merged.csv` containing weight data will be used, as well as the `heartrate_seconds_merged.csv` file.

## Applications
Excel will be used to load the data and initially look for any issues. R will then be used to transform and explore the data.








