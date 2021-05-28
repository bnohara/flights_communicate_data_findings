# Project: Exploration of flight data from 1988 to 2007

## Project Intro

This was the last project in the Udacity Data Analyst Nanodegree program. The exploration_template Jupyter notebook and HTML file has the raw data analysis, and could be shared with a technical team. The slide_deck_template Jupyter notebook and HTML file polish the analysis and could be presented to a non-technical audience. Please see the rest of this readme for additional notes on the analysis.

## Dataset

This document explores a dataset containing flight delay information for approximately 18 million flights from 1988, 1998, and 2007. Time features in the dataset include the date, as well as the scheduled and actual departure and arrival times. Numerical columns indicate the length and distance of the flight, and the length of delays. Categorical variables indicate the type of delay, if any, and whether the flight was cancelled or diverted. Other features are the airline carrier, origin, and destination.

The original data source is here: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/HG7NV7

Definitions of the columns can be found here: http://stat-computing.org/dataexpo/2009/the-data.html

Each year's data has its own csv file. I concatenated the data for the 3 years to see if there were differences over time. Data for 2008 was only available through April of that year, so I chose 2007 instead.

Around 400k rows showed flight lengths with negative minutes, so I removed these as invalid data.

## Summary of Findings

### Univariate Exploration

When looking at data for delay times, I removed flights with a delay less than 10 minutes. My thinking was that flights with very short delay times wouldn't have much impact on the traveler.

The distribution of arrival delay times had a long tail. I used a log transform for the histogram. The transform showed a strong right skew, with most arrival delays under 60 minutes.

The top origin and destination cities by number of flights was the same. It's probably more practical to look at delays for destination cities, as people don't have as much choice about the origin city when planning a trip. Therefore I focused on destination city for the analysis.

The portion of delayed flights was around 27% in 1988 and 1998, but increased to around 30% in 2007.

### Bivariate Exploration

For the parts of the analysis involving delay times, I removed outliers with extremely high delays. This provided a clearer picture of the interactions between features in the dataset.

For the top 20 destination cities with the most flights, the median arrival delay time was fairly similar - between 20-30 minutes. Cities with higher median arrival delay time generally had a larger spread of values above the median though. The top 5 cities by median arrival delay time (EWR, SFO, ORD, BOS, LGA) had maximum delays between 110 and 150 minutes. The remaining cities generally had a maximum delay between 80 and 100 minutes.

Median arrival delay time increased over the 3 years in the data set, from around 20 minutes in 1988 to 30 minutes in 2007. The maximum delay times also doubled from 60 minutes in 1988 to 120 minutes in 2007.

The portion of flights with delays was higher in 2007 compared to 1988 for 16 of the top 20 cities.

### Multivariate Exploration

In most of the top cities, the length of delay increased over the years. The exception was SFO, which had shorter delays in 2007 compared to 1998.

## Key Insights for Presentation

The presentation contains all of the main findings from the exploration. I started with the histograms of arrival delay time, portion of delayed flights for top destination cities, and portion of delayed flights by year. This provides a base for the dataset's content.

Next, I showed boxplots of 1) arrival delay time for top destination cities, and 2) arrival delay time for each year. Rounding out the bivariate analyses, I included a clustered bar chart showing the portion of delayed flights for the top destination cities, clustered by year.

To close the presentation, I showed a heat map of arrival delay time by destination city and year. Longer delay times had a darker color. I decided not to use the clustered bar chart for this visualization, as it looked too similar to the bivariate chart of portion of delayed flights for top destination cities.

From the command line, this command can be used to run the slides:

jupyter nbconvert slide_deck_template.ipynb --to slides --post serve --no-input --no-prompt
