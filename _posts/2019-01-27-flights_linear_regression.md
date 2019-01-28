---
layout: post
title: Flight Delay Prediction using Linear Regression
---

Delayed aircraft are estimated to have cost the airlines several billion dollars in additional expense <sup>[1]</sup>, not to mention the uncertainty it adds to a passenger's travels. The goals of this project is to  predict flight delay time using linear regression based on 2017 United States flights data. Through the analysis, it should also shine a light on factors that impact flight delay time, and help others to develop mitigating strategies.

-----

## Data Sources
* 2017 Flight delay and cancellation data from [Bureau of Transportation Statistics](https://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236)
* 2015 airport volume data scraped from Bureau of Transportation Statistics website: [Bureau of Transportation Statistics](https://www.transtats.bts.gov/airports.asp?pn=1)
* Historic airport weather data from Iowa State University website: [Iowa State Univerity Mesonet](https://mesonet.agron.iastate.edu/request/download.phtml?network=WA_ASOS)

## Methodology Used
As the data set is quite huge (~5.3 million rows), the data set is randomly sampled to 50,000 rows for quicker modeling time. Cross-validation with 5 folds is used on 80% of the data set to select features and model parameters.

Initially the following features were considered: 'Inbound Delay', 'Month', 'Airport Departure Volume', 'Plane Turnaround Time','Departure Time','Temperature', 'Wind Speed', 'Precipitation'.

Then some features get zero-ed out in Lasso regressions and are removed, specifically: 'Month', 'Airport Departure Volume', 'Plane Turnaround Time', 'Temperature'. 'Wind Speed' is further eliminated due to causing lower R2 score (indicating overfitting).

So three features remains to be used in model: 'Inbound Delay', 'Departure Time', 'Precipitation'.

No feature transform were needed when checking the residual plots, but y (Departure Delay) is noticed to be heavily left skewed and so is being log transformed before training.

RidgeCV, LassoCV, ElasticNet Models were used in training, and RidgeCV was seen to have slightly better R2 scoring, and therefore chosen.

## Results
* Ridge linear regression yielded a relatively low R2 score: 0.234
* Out of the 3 features used, "Inbound delay" had the best predictive power (coefficient=0.145), compared with "Departure Time (coefficient=0.068), and "Precipitation" (coefficient=0.016)

## Conclusions
* Three factors 'inbound delay', "departure time", "precipitation" are significant predictors of amount of departure delay, but are insufficient to reliably predict departure delay time (low R2 score)
* Given the low R2 score, further predictive features should be explored, for example:
    * Around airport volume or airport "busy-ness" should be explored, for example:
      * Timeframes around public holidays
      * Hourly volume of an airport around flight departure time
    * Further breakdown of how specific airline carrier can impact delay

## References
1. Airlines for America. http://airlines.org/dataset/per-minute-cost-of-delays-to-u-s-airlines/
