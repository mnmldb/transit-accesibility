# Transit Accessibility of Essential Workers in NYC

## Overview

In the first month of the COVID-19 pandemic lockdown, all non-essential travel came to a halt. For essential workers, however, the commute never stopped. While some of these workers pivoted to bike-share or FHV to avoid crowds, many continued to rely on public transit.

While New York City is one of the most connected cities in the world, this connectivity varies greatly in different parts of the city. Through this study, we intend to highlight the areas where essential workers have been impacted by lack of transit access.

We first set out to map the essential worker distributions across the city by using census data. We also mapped the declining transit trends over the initial lockdown period in 2020 as compared to 2019 and used this metric to predict population distribution through polynomial regression. We then calculated the transit accessibility index and finally overlaid the indices to our population distribution. We have found evidence that several zones across the city with high essential worker activity have low access to public transportation.

## Dataset
- [Longitudinal Employment Household Dynamics (LEHD)](https://lehd.ces.census.gov/)
- [American Community Survey (ACS)](https://www.census.gov/programs-surveys/acs)
- NYC Yellow Taxi, Green Taxi, FHV, and High Volume FHV in [NYC Open Data](https://opendata.cityofnewyork.us/data/)
- [MTA Turnstile](http://web.mta.info/developers/turnstile.html)
- Location of subway stations, rail train and bus stops

## Methods

1. Predict the essential worker population (taxi zone level)  by the decrease in the number of subway and taxi/FHV users in the lockdown and verify with multivariate regression analysis
2. Calculate [the accesibility index](https://ctr.utexas.edu/wp-content/uploads/pubs/0_5178_P3.pdf) per taxi zone

## Result

### 1. Estimated Essential Worker Population

We calculated the total number of turnstile entries at each subway station during the first two weeks of the lockdown (March 23rd to April 5th in 2020) and for the same two weeks of the previous year (March 25th to April 7th in 2019). We aggregated the number of turnstile entries at the taxi zone level and calculated the % decrease in the number of entries. We also got the total number of yellow taxis, green taxis, FHV, and high-volume FHV pickups in each taxi zone in the same period of time as the subway. We calculated the % decrease in the number of pickups.

The below maps show the ratio of essential workers to the working population estimated by census, a % decrease in the number of subway and taxi/FHV users. We can see the same trend in all three maps: the zones with a high essential worker ratio have a less decrease in the number of subway and taxi/FHV users and vice versa.

![population](https://user-images.githubusercontent.com/47055092/138023721-e0d0c3f0-c9f2-4d5f-bb6a-0d4ed7bb422f.png)

#### Verify by Multivariate Regression

We predicted the ratio of essential workers to the working population by a % decrease in the number of subway (yoy_sub) and taxi/FHV users (yoy_tf). To deal with the missing values in subway data, we created the dummy variable (yoy_sub_na) in those zones and filled missing values with an average. We tried several polynomial regression models from 1st to 4th degrees. We found that the best model was the 2nd-degree polynomial (yoy_sub2, yoy_tf2) with 0.685 of the adjusted R-Squared. The coefficients of a % decrease in the number of taxi/FHV were statistically significant, as seen in the p-value. However, those of the subway were not.

![regression](https://user-images.githubusercontent.com/47055092/138023953-4e39ddee-53e3-4fba-ace8-2febb9fcf479.png)

### 2. Accessibility Index
We wanted to measure how easy it is for essential workers to access public transportation. As input, we used the geospatial information of subway stations, bus stops, and citibike stations.
 
The first step was to calculate the closest distance to each mode of transportation, having as origin the centroid of each city's census block group . The next step was to compute a weighted average on each distance by the proportion of trips made for each mode of transportation in each census block group, according to the ACS estimation.

The final step was to do another weighted average by population across different census blocks for the same taxi zone, to be able to compare the essential workers prediction. The following equation calculates the index for a taxi zone j:

![index](https://user-images.githubusercontent.com/47055092/138024279-2b83c9cc-cdec-45da-8149-9bb672043e2f.png)

where
- *d(ci,bi)*:Distance from centroid of census block i and closest bus stop.
- *d(ci,si)*:Distance from centroid of census block i and closest subway station.
- *Pbi*:Proportion of bus rides in census block i
- *Psi*:Proportion of subway rides in census block i.
- *Total population j*: Total population in taxi zone j
- *Popi*: Population in census block i

The spatial distribution of the index shows high heterogeneity across the five boroughs. Manhattan exhibits the highest accessibility conditions in the whole city, just having some zones in the southwest with some lag. Neighborhoods around downtown Brooklyn are well connected, however the outer parts of the borough show a lower performance. The Bronx seems to have two clear patterns. The closest part to Manhattan seems to be more connected, while there are very low accessibility conditions along the border zone with Queens. Queens has massive mobility limitations especially in the east and given the socio-economic limitations and their dependence on MTA services, a clear intervention is needed.

Comparing the spatial distribution of the estimated essential workers’ participation and the value in the index per taxi zone, we can see some correlation between the variables. We got a Pearson correlation coefficient of 0.254, usually classified as low/intermediate correlation. Depending on the zone in the city, the relationship is more or less clear.

![result](https://user-images.githubusercontent.com/47055092/138021764-d027e825-d865-4c4c-8bbf-7588263a993f.png)

## Conclusion
We can state with relative confidence that our essential workers identification strategy predicts their spatial distribution across the city. The methodology provides an alternative way of mapping essential workers. Our prediction is close to the most recent picture of their location (ACS 2019), but is also slightly different, capturing the changing patterns brought on by the pandemic.

The global pandemic has demonstrated the vital importance of essential workers to urban systems, and with that, the importance of sustainable and affordable transportation infrastructure for those workers. We have provided evidence of the difficulties that densely-populated essential worker zones face in accessing public transportation infrastructure, and identified areas in most need of better service. Equipped with this information, New York City has an opportunity to prioritize affordable transportation for these populations beyond COVID-19.