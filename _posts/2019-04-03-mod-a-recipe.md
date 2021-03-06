---
layout: post
title: Mod-a-Recipe
subtitle:   "Fun with recipes (an NLP Project)"
date:       2019-04-03
author:     "Po-Yan Tsang"
header-img: "img/posts/ingredients.jpg"
comments: true
tags: [ machineLearning ]
---

Mod-a-Recipe is developed as my capstone project at Metis data science immersive bootcamp, to combine my passions for cooking and natural language processing. The idea came from my own experience of always reviewing more than one recipe for a dish I had in mind to figure out what ingredients I can modify or swap out to suit my taste. Using natural language and machine learning techniques, similar recipes are found given a selected recipe, and suggestions on modifications are provided to make a recipe your own.

## Data Source
Recipe data was scraped by [Eight Portions](https://eightportions.com/datasets/Recipes/) (~80,000 recipes used here) from [Epicurious](https://www.epicurious.com/), [AllRecipes](https://www.allrecipes.com/), and [FoodNetwork](https://www.foodnetwork.com/).

Also, tagged ingredients data is used from the NYTimes Ingredients Phrase Tagger project [see Github](https://github.com/NYTimes/ingredient-phrase-tagger).

## Code at Github
Here is the github repo for this project: [link](https://github.com/pytgit/mod-a-recipe).

## Tools Used
Python is used for data acquisition, cleaning and modeling. Specific python libraries used include:
* Modeling: scikit-learn
* Natural language processing: spaCy
* Web application: Flask, PostgreSQL, Heroku

## Methodology Used
1. Data set from the three data sources (Epicurious, AllRecipes, Foodnetwork) are merged into one, and data cleaned to remove irrelevant information. (refer to code [here](https://github.com/pytgit/mod-a-recipe/blob/master/src/data/make_dataset.py))

2. Using 2000 rows of tagged ingredients list data from the [NYTimes Ingredients Phrase Tagger project](https://github.com/NYTimes/ingredient-phrase-tagger) and 200 rows of manually tagged data from the [Eight Portions](https://eightportions.com/datasets/Recipes/) data set, the spaCy NER model is trained to recognize ingredients from ingredients list text.

3. Using the trained spaCy NER model, ~40,000 unique ingredients were extracted from the ingredients list of the recipes data. (refer to code [here](https://github.com/pytgit/mod-a-recipe/blob/master/src/models/train_model-nlp.py and src/features/build_features.py))

4. Topic modeling technique (TFIDF word vector with non-negative matrix factorization) is then used to reduce dimensionality such that similar recipes can be calculated using cosine similarity. The NMF yielded 50 topics were seemed to be representative of certain types of recipes. For example:
   > Topic 1 (Asian recipes): soy sauce, sesame oil, green onion, ginger, sesame seed, rice vinegar, ginger root, scallion, rice wine vinegar, peanut oil

   > Topic 2 (baking): unsalted butter, pure vanilla extract, whole milk, light brown sugar, fine salt, nutmeg, shallot, kosher salt and freshly ground pepper, extra-large egg, semisweet chocolate

   (refer to code [here](https://github.com/pytgit/mod-a-recipe/blob/master/src/models/train_model.py))

5. Similar recipes were found as a result, and differences in ingredients lists are highlighted as possible substitutions or enhancements to the selected recipe. 

## Resources
1. NYTimes Ingredients Phrase Tagger [Github](https://github.com/NYTimes/ingredient-phrase-tagger).
2. Eight Portions (for recipes data) [Data set](https://eightportions.com/datasets/Recipes/).
