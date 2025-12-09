# The Culinary Guide to Popularity

## Introduction
This project aims to answer what types of recipes tend to have higher average ratings using data involving select recipes and their corresponding ratings by people trying to follow them step-by-step. I was interested in knowing what aspects of food in general might cause people to want to make their own food. Could it be financial reasons (not wanting to spend so much money on eating out), or do they believe following recipes themselves will make the food healthier? Or maybe, there's something about making your own food at home (even if it's other people's recipes) that makes the overall eating experience more satisfying. My mission was to get to the bottom of it once and for all. Using a subset of data from food.com, I utilized hundreds of thousands of recipes and ratings to find the factors of recipes that most heavily influence what give the recipe a high rating.

## Data Cleaning and Exploratory Data Analysis

In order to preprocess the data so that it was ready for analysis, I first had to combine the two original datasets, recipes and ratings, into one. Once I merged the two by matching with recipe_id's, I noticed many ratings were 0, which didn't make sense practically. Instead, I replaced those 0's with NaN's to indicate that no one has rated those particular recipes yet. The last thing I did was add a new column called `average_rating`, which was the target variable I intended to explore by seeing how other variables in other columns affected it. I did it by grouping the data by recipe_id, and taking the average rating of all ratings corresponding to the same recipe_id, so that each unique recipe would get an average rating. The picture below shows what the cleaned data looks like:
<img width="1279" height="169" alt="Screenshot 2025-12-08 at 8 58 52 PM" src="https://github.com/user-attachments/assets/3c1269ec-000a-4e8d-9aa4-7e2a6f4676da" />

I conducted three univariate analyses to see the distirbution of three variables: average rating, number of steps, and number of ingredients. The latter two were variables I believed were useful to accurately predict a recipe's average rating, so I wanted to include them in my initial analysis. The plot below shows the distribution of the number of ingredients, which appeared to be mostly uniform, slightly skewed right, meaning that most recipes required less than average number of ingredients, but the mean number of ingredients is higher than it would have been if the distribution was uniform.
<img width="627" height="403" alt="Screenshot 2025-12-08 at 9 22 06 PM" src="https://github.com/user-attachments/assets/d31b244d-2c5e-4894-a89f-4e12e6c9f94b" />

The plot below displays the relationship between average rating and number of ingredients.

I created a pivot table to explore the average number of tags given the number of ingredients for each unique number of steps.
<img width="523" height="236" alt="Screenshot 2025-12-08 at 9 29 02 PM" src="https://github.com/user-attachments/assets/8da1c141-f4b9-43e7-87d4-b2168492e315" />

## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
