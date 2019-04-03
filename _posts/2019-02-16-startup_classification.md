---
layout: post
title: Startups- Billion Dollars or Bust?
subtitle:   "Fun with startups"
date:       2019-02-16
author:     "Po-Yan Tsang"
header-img: "img/posts/startup.jpg"
comments: true
tags: [ machineLearning ]
---
As a potential investor or hire, how can you assess whether to further invest or join a startup? This project predicts type of status (acquisition, IPO, close, operating) for a company given current funding and company information. This can help potential investors or employees to look out factors to assess a startup and the potential exit path.

## Data Source
[Crunchbase 2013 Snapshot © 2013](https://data.crunchbase.com/docs/2013-snapshot)

## Code at Github
Here is the github repo for this project: [link](https://github.com/pytgit/startup-classification)

## Methodology Used
From the [Crunchbase 2013 snapshot data](https://data.crunchbase.com/docs/2013-snapshot) site:
* [MySql backup files](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) are downloaded
* Backup files are restored as MySQL databases
* MySQL database is migrated to local Postgres DB for further processing and analysis using [pgloader utility](https://pgloader.io/)

Initially I tried to run model on data including all funding rounds information known now for a particular company. For example, for company A, I would have a row with total raised amount, and number of total rounds, and number of investors thus far. The prediction accuracy were really good too!

But then, I thought, what the model is trained on is similar to saying, hey I know this company is going to get acquired and here's what we know at time of acquisition. This is not really what I want to predict: I want to know given what we know *so far* for a company, if it's likely to get acquired or not in the future.

So, I ended up wrangling the data such that training data represent yearly snapshot of a company’s funding information, so that the model is more about predicting status based on current known yearly status: [(code here)](https://github.com/pytgit/startup-classification/blob/master/Clean%20data%20and%20feature%20engineering.ipynb)

<p align="center">
  <img width="1000" height="300" src="../img/posts/data_wrangling.png">
</p>

After getting the data into shape, I noticed the predictor classes are highly imbalanced, so I further resampled the data for better model fitting. Different sampling methods were experimented with, including random undersampling, random oversampling. SMOTEENN was selected to in the end because it yielded best results.

I tried multiple classifiers: KNN, Logistic Regression, Gradient Boosting, Naive Bayes, Random Forest. Gradient Boosting yielded the best initial results, so further parameter tweaking was attempted on training set.

In the end, the following features were used:

| Feature (Yearly Snapshots)    | Type                   |
|-------------------------------|------------------------|
| Days active                   | Numerical              |
| Number of investors           | Numerical              |
| Total funding raised          | Numerical              |
| Number of funding rounds      | Numerical              |
| Category                      | Categorical            |
| Region                        | Categorical            |

## Results
Gradient Boosting yielded the best F1-macro score of 0.43 on test data set.

The model, however, heavily biased towards ‘operating’ status prediction.

See Jupyter notebook for steps to get to results [(code here)](https://github.com/pytgit/startup-classification/blob/master/Model%20training.ipynb)

## Conclusions
Funding information have some but not strong predicting power for predicting close, IPO, or acquired statuses.

For future work, I'd like to explore having more heavy weights on predicting “closed” status correctly during training to help perspective employees and investors to especially avoid companies heading to closure.

Also, expanding data set size, and using data sources beyond Crunchbase with additional predictive features may help improve results: e.g. company growth and performance data such as company revenue and number of employees.
