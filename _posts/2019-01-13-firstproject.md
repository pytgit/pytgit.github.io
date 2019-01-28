---
layout: post
title: First Project- NYC MTA Data
---

*MTA Turnstile Data Analysis* is a group project where we are asked to provide recommendations to a non-profit organization to optimize street team positions at New York City MTA subway stations to gather emails and evangelize an upcoming gala event.

-----

### The Data Sources
- We found MTA turnstile data at [https://catalog.data.gov](https://catalog.data.gov/dataset/turnstile-usage-data-2018) with a quick google search. It's a pretty large data set, with ~10 million rows.
- We also grabbed the median income per zip codes in NYC from Census data for 2017.
- To figure out zip codes for the stations, we got a list of NYC MTA subway stations with names and corresponding geocodes, and then used Google API to find zip codes for the corresponding geocodes.

### Methodology
We dug into the MTA turnsile data, cleaned the data to remove duplicates, bad data, and various things to enable analysis, and then we were able to provide the following analysis:
- Top 10 Subway Stations by annual foot traffic volume for 2018, while also pointing out stations in zipcodes with median household income > 100K
  - Monthly pattern (which months are best)
  - Weekly pattern (which day of the week)
  - Daily pattern (time)

### Lessons Learned
As part of the Metis classes, design thinking and a MVP approach was encouraged. I loved that since it's an approach that is near and dear to my heart. It is something I've practiced daily in the past 5+ years at start up. At start up, any product features we can deliver as soon as possible while delivering value to the customers is critical to the survival of the company. However, even with the MVP approach, as a total noob in exploratory data analysis of real world data, of course there are some great lessons learned:

**1. Understand your data**

Despite the metadata descriptions that came along with the data, even though we know that the entries and exits are cumulative  and can get reset, HOW and WHEN the numbers get reset turns out to be quite unpredictable and causes a great deal of data that skew the counts and provide confusing results. A lot of effort was needed to figure out a way to filter out the "bad" data.

**2. Check results validity early!**

We didn't realize the data skew issue above till relatively late in the project since guess what, we didn't try to check if our initial results make sense until about half way through the project. It's only when we start questioning whether the top 10 stations could really have 100million+ visitors annually that we realize our data set has issues. When data set is large, it's not as straightforward to figure out obvious data issues until we do some quick estimation checks.
