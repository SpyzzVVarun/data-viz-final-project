<h1 align = "center">Indian Air Quality Analysis</h1>
<p align = "center"><i>Data Visualization Report by Varun Nagpal (210150020)</i></p>

# Motivation

Data visualization serves as a powerful lens through which we can gain deeper insights into the complex dynamics of environmental phenomena. 

Why chose Air Quality analysis for the **Environment** theme?

1. **Direct Impact on Human Health:** Air quality significantly affects human health, with pollutants like particulate matter, ozone, sulfur dioxide, and nitrogen dioxide contributing to respiratory diseases, cardiovascular issues, and even premature death. Analyzing air quality data enables us to understand the extent of these health risks and formulate strategies to mitigate them.

2. **Environmental Indicator:** The quality of air serves as a crucial indicator of overall environmental health. Pollution in the air can originate from various sources such as industrial emissions, vehicular exhaust, biomass burning, and natural events. Monitoring air quality provides insights into the effectiveness of pollution control measures, the impact of human activities on the environment, and the health of ecosystems.

**Now, we will understand the data that we have collected. Next, we will try to formulate some questions and derive inferences from the data using visualizations.**

The sections are as follows:
1. Data
2. Understanding the Pollutants
3. Temporal Trends
4. Spatial Trends
5. Spatio-Temporal Trends
6. Conclusion

# Data

Data is the most important part of EDA/ Data Visualization. Good quality and bias-free data helps ensure good and reliable insights.

## Data Source
The data used in this project has been sourced from the Central Pollution Control Board (CPCB), which is the official portal of the Government of India. The CPCB has made the data publicly available and can be accessed at their website: https://cpcb.nic.in
The data was compiled from the CPCB website, which serves as the official body of the Government of India for monitoring and controlling pollution. 

## Data Cleaning & Processing

Initially we had hourly data from 450 Air Quality Monitoring stations across India. The dataset had 100+ features covering various air quality metrics and pollutant measurements. The data was also filled with missing values. We went through the data and finally selected the most influential pollutants based on some literature survey and also converted the data to daywise by averaging. We also created a single clean dataset by merging the data from all stations. The codes for data processing can be found in **data.ipynb** and **clean_data.ipynb**

## Data Description

The dataset contains air quality data for Indian cities from the year 2010 to 2023. This dataset is valuable for understanding and analyzing the air quality trends and patterns in Indian cities over a span of 13 years. 
The main pollutants we are covering are:
* SO2
* NO2, NO and NOx
* CO
* Ozone
* PM2.5
* PM10

We also consider the effects of Air Temperature and Relative Humidity.

# Air Quality Monitoring Stations

The number of Air Quality Monitoring Stations covered in my data is 450 and the data ranges from 2010 to 2022 (with some data till March 2023)

Here we have used the map of India along with the latitude and longitude information of the station locations to plot the location markers. The latitude and longitude information was extracted using Nominatim API 

<img src = "plots/Agency_Data.PNG" height = 500 width = 500>

The map clearly illustrates the extensive coverage of monitoring stations across India, effectively encompassing most regions except for certain areas in the extreme North and the South-East.

* An interactive HTML file for the above image is also provided as "map_of_locations.html"

# Understanding the Pollutants

## What is the distribution of each pollutant across the dataset?

To assess the distribution of each air pollutant in our dataset, two types of visualizations were employed: histograms and boxplots.

### Histograms
For each pollutant, a histogram was generated to visualize its frequency distribution across the dataset. These histograms are crucial as they show the spread and skewness of data points around the mean. To provide context regarding environmental standards, a vertical line representing the NAAQS threshold for each pollutant was included in the corresponding histogram. This demarcation helps in quickly identifying the proportion of observations that exceed the acceptable limits set by regulatory bodies.

<img src = "plots/SO2_histogram.png" height = 400 width = 500> <img src = "plots/PM2_histogram.png" height = 400 width = 500>

* More plots available in code notebook

Large number of instances when pollutant concentration crosses the set threshold for PM2.5 and PM10 is alarming and a cause for concern.
The high frequency of PM2.5 and PM10 concentration exceeding set thresholds can be expected to be due to urbanization, industrialization, combustion processes, natural sources, meteorological factors, and regional transport. These pollutants originate from various human activities and natural phenomena, leading to significant health risks and necessitating urgent air quality management actions.

### Boxplots
A composite figure comprising boxplots for each pollutant was also created. Boxplots summarize the central tendency and dispersion of data, while clearly marking outliers. This visualization allows for an easy comparison across pollutants, highlighting differences in their median levels and variability.

<img src = "plots/concentration_boxplot.png" height = 500 width = 700>


## Are there any strong correlations between different pollutants?

Correlation plots are the right choice for analyzing relationships between different pollutants because they provide a visual representation of the strength and direction of associations. By plotting correlation matrices, we can easily identify strong correlations between pollutants, which is crucial for understanding the underlying mechanisms driving air pollution. 

<img src = "plots/corr_plot.png" height = 500 width = 500>

Insights from correlation analysis highlight significant relationships between various pollutants and environmental factors:

1. **Strong correlation between Ozone and NO2:**
   This correlation indicates that the presence of NO2 in the atmosphere can contribute to the formation of ozone through photochemical reactions involving sunlight and other pollutants. Additionally, both ozone and NO2 are common pollutants associated with vehicular emissions, industrial activities, and combustion processes. 

2. **Strong correlation between CO and NOx:**
   This correlation suggests common emission sources such as vehicle exhaust, industrial processes, and biomass burning. CO is primarily emitted during incomplete combustion of carbon-containing fuels, while NOx is produced from combustion processes at high temperatures. 

3. **Correlation between Ozone and Air Temperature (AT)**

Understanding these correlations is crucial for policymakers, environmental scientists, and public health officials to develop targeted interventions and regulatory measures aimed at improving air quality and mitigating the adverse effects of pollution on human health and the environment.

## How do weather variables (temperature, humidity) correlate with pollutant levels?

Scatter plots, with or without regression lines, offer a concise and powerful method to analyze the relationships between weather variables (like temperature and humidity) and pollutant levels. They visually represent data points, helping to identify patterns and trends. Regression lines quantify the relationship, aiding in trend analysis and outlier detection.

<img src = "plots/ozone_AT.png" height = 300 width = 400>

This correlation seems to be primarily due to temperature's role in facilitating the formation of ozone through photochemical reactions involving precursor pollutants like volatile organic compounds (VOCs) and nitrogen oxides (NOx). As temperatures rise, these reactions accelerate, leading to higher ozone concentrations. 

<img src = "plots/SO2_AT.png" height = 300 width = 400> <img src = "plots/NO2_AT.png" height = 300 width = 400>

This pattern may be observed due to the optimal conditions for chemical reactions and pollutant dispersion at moderate temperatures. At ambient temperatures, industrial processes and vehicular emissions, which are major sources of SO2 and NO2, operate efficiently, leading to higher concentrations. As temperatures deviate from the ambient level, these emissions may decrease due to factors like reduced industrial activity or enhanced dispersion.

# Temporal Trends

Now lets look at some questions which help us understand the air quality trend over time

## How have pollution levels (CO, PM10, PM2.5, NOx, Ozone, SO2) changed over time? Are there noticeable trends in air quality improvement or deterioration? Are there any pollutants that consistently exceed regulatory limits?

Yearwise Boxplot with threshold lines is effective for analyzing pollution trends over time because it allows clear comparisons between years, identifies outliers exceeding regulatory limits, provides summary statistics for each year, offers visual clarity, and enables comparative analysis between pollutants.

<img src = "plots/NO2_box.png" height = 400 width = 500>

The increasing trend of NO2 concentrations yearwise is primarily driven by factors such as urbanization, industrial growth, vehicle emissions, combustion of fossil fuels, and meteorological conditions. This trend underscores the need for proactive measures to reduce emissions and improve air quality monitoring and enforcement.

* More plots available for other pollutants in code notebook


## How do pollution levels vary by season? Are certain pollutants more prevalent in winter compared to summer?

Monthwise lineplots are effective for analyzing how pollution levels vary by season because they provide a clear visualization of pollutant concentrations over the course of the year. They help us see Seasonal patterns and do comparative analysis.

<img src = "plots/SO2_season.png" height = 400 width = 500> <img src = "plots/Pollution_Season.png" height = 400 width = 500>

 Peaks observed in March-April and October-November in India are likely due to factors like crop residue burning, weather conditions, and increased industrial activity during those periods. The October-November peaks can also be explained by the Diwali season.

# Spatial Trends

## How does air quality differ across states and cities? Which areas consistently show higher or lower levels of pollution?

Lets look at the Top and Bottom 5 states/UTs in terms of PM2.5 and PM10 mean concentrations

<img src = "plots/most_state.png" height = 300 width = 400> <img src = "plots/most_state_10.png" height = 300 width = 400>
<img src = "plots/least_state.png" height = 300 width = 400> <img src = "plots/least_state_10.png" height = 300 width = 400>

Lets look at the Top and Bottom 5 cities in terms of PM2.5 and PM10 mean concentrations

<img src = "plots/most_city.png" height = 300 width = 400> <img src = "plots/most_city_10.png" height = 300 width = 400>
<img src = "plots/least_city.png" height = 300 width = 400> <img src = "plots/least_city_10.png" height = 300 width = 400>

The high pollution levels in Delhi and low pollution levels in northeastern states and cities can be attributed to several factors:

1. **Geographical Location and Topography:** Delhi's geographical location, combined with its flat terrain and lack of natural barriers, makes it susceptible to the accumulation of pollutants. Pollutants emitted from vehicular exhaust, industrial activities, construction, and biomass burning in and around Delhi tend to get trapped due to stagnant air masses, leading to poor air quality. In contrast, the northeastern states are characterized by hilly terrain and abundant vegetation, which promote better dispersion of pollutants and lower pollution levels.

2. **Population Density and Urbanization:** Delhi is one of the most populous and urbanized cities in India, with high population density and extensive industrial and vehicular activities. The concentration of emissions from various sources contributes to elevated pollution levels. In contrast, northeastern states have lower population densities and less industrialization, resulting in reduced pollution emissions and better air quality.

3. **Industrial and Agricultural Activities:** Delhi's proximity to industrial areas and agricultural regions where crop residue burning occurs exacerbates pollution levels. In contrast, the northeastern states have relatively fewer industrial activities and agricultural practices that contribute to air pollution, resulting in cleaner air.

4. **Transportation Infrastructure:** Delhi's extensive road network and high vehicular density lead to significant emissions of pollutants such as nitrogen oxides (NOx), particulate matter (PM), and volatile organic compounds (VOCs). In contrast, the northeastern states have less developed transportation infrastructure and lower vehicular density, resulting in lower emissions and better air quality.

5. **Government Policies and Initiatives:** Delhi has been grappling with air pollution for several years, leading to the implementation of various government policies and initiatives aimed at reducing pollution levels, such as the introduction of vehicle emission standards, restrictions on industrial activities, and measures to curb crop residue burning. In contrast, the northeastern states may have stricter environmental regulations and better enforcement mechanisms, contributing to lower pollution levels.

## Pollutant Distribution for the Top 6 Polluted States/UTs 

A boxplot with faceting is ideal for visualizing pollutant distributions across the top polluted states/UTs because it allows for easy comparison between regions, handles outliers well, represents skewed data effectively, and facilitates pattern recognition in a compact and informative manner.

<img src = "plots/top_6_poll.png" height = 500 width = 900> 


# Spatio-Temporal Trends

## Let's see a choropleth view of NO2 concentrations, over time and across regions

https://github.com/SpyzzVVarun/data-viz-final-project/assets/95134445/d3f165bb-8cda-4063-90fc-4340bede0891

## How often do levels of each pollutant exceed national health standards and how widespread is this? (Thresholds determined on the basis of National Ambient Air Quality Standards (NAAQS))

Lets look at some barplots for Nitric Oxide to help us answer this question.

<img src = "plots/NO_temp.png" height = 400 width = 500> <img src = "plots/NO_temp_1.png" height = 400 width = 500>

* More plots available for other pollutants in code notebook

The increasing trend indicates a rise in pollutant concentrations over time and across various regions, signaling worsening air quality conditions. This trend suggests growing emissions from various sources, such as industrial activities, vehicular traffic, and combustion processes. It highlights the need for immediate action to mitigate pollution, safeguard public health, and protect the environment.


# Possible Policy or Situational Effect

Certain cities like Delhi which have suffered due to Air Pollution for a long time have implemented various policies to curb air pollution
We can see here that mean PM2.5 concentration had been steadily decreasing for Delhi over the years, especially going into the lockdown period. Although we do see an increasing trend again post COVID.

<img src = "plots/delhi_pm.png" height = 400 width = 500> 

# Conclusion

In this comprehensive analysis of Indian air quality, we delved into the complexities of environmental dynamics through the lens of data visualization. By exploring various pollutants, their spatial and temporal trends, and correlations with weather variables, we gained valuable insights into the state of air quality across different regions and time periods.

Our findings underscore the critical importance of monitoring and managing air quality, given its direct impact on human health and its role as an environmental indicator. Through rigorous data cleaning and processing, we transformed raw data into actionable insights, enabling informed decision-making and policy formulation.

Spatial analyses helped us understand air quality across states and cities. Temporal trends highlighted both improvements and deteriorations in air quality over time, emphasizing the need for sustained efforts to mitigate pollution and safeguard public health.

Correlation analyses illuminated complex relationships between pollutants and weather variables, shedding light on the underlying mechanisms driving air pollution. These insights can inform targeted interventions and regulatory measures aimed at reducing emissions and improving air quality standards.

Overall, this data storytelling project offers a comprehensive understanding of Indian air quality dynamics. As we continue to grapple with the challenges of pollution and climate change, data-driven approaches will play a pivotal role in shaping a healthier and more sustainable future for generations to come.






