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
The spatial distribution of the index shows high heterogeneity across the five boroughs. Manhattan exhibits the highest accessibility conditions in the whole city, just having some zones in the southwest with some lag. Neighborhoods around downtown Brooklyn are well connected, however the outer parts of the borough show a lower performance. The Bronx seems to have two clear patterns. The closest part to Manhattan seems to be more connected, while there are very low accessibility conditions along the border zone with Queens. Queens has massive mobility limitations especially in the east and given the socio-economic limitations and their dependence on MTA services, a clear intervention is needed.

Comparing the spatial distribution of the estimated essential workers’ participation and the value in the index per taxi zone, we can see some correlation between the variables. We got a Pearson correlation coefficient of 0.254, usually classified as low/intermediate correlation. Depending on the zone in the city, the relationship is more or less clear.

![result](https://user-images.githubusercontent.com/47055092/138021764-d027e825-d865-4c4c-8bbf-7588263a993f.png)