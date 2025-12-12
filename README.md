# The Culinary Guide to Popularity

## Introduction
This project aims to answer what types of recipes tend to have higher ratings on average than others. For avid chefs at home looking to share their recipes online for the world to follow, these results will come in handy to understand what recipe followers want most in their food! Using a subset of data from food.com, I utilized hundreds of thousands of recipes and ratings to find the factors of recipes that most heavily influence what give the recipe a high rating. The dataset I used was a merge of two datasets, one on recipes, and another one on ratings for those recipes, from food.com, as well as some new columns I added for analysis. The dataset has a total of 83782 rows and 20 columns. The columns I used are: 'id', which is the id of each recipe, 'n_steps', which is the number of steps to follow for the recipe, 'n_ingredients', which is the number of ingredients required by the recipe, 'average_rating', which is the average of all ratings corresponding to the same recipe ID, 'tag_count', which is the number of tags a recipe has on food.com such as "60-minutes-or-less" or "for-large-groups", and 'calories', which is the recipe's amount of calories and is a result of extracting the first item from the lists under the 'nutrition' column, which gives information about the recipe's nutritional value.

## Data Cleaning and Exploratory Data Analysis

In order to preprocess the data so that it was ready for analysis, I first had to combine the two original datasets, recipes and ratings, into one. Once I merged the two by matching with recipe_id's, I noticed many ratings were 0, which didn't make sense practically. Instead, I replaced those 0's with NaN's to indicate that no one has rated those particular recipes yet. The last thing I did was add a new column called `average_rating`, which was the target variable I intended to explore by seeing how other variables in other columns affected it. I did it by grouping the data by recipe_id, and taking the average rating of all ratings corresponding to the same recipe_id, so that each unique recipe would get an average rating. Additionally, I cleaned the 'nutrition' column. The original values in that column were strings that looked like lists, so I had to convert them into lists to be able to use them for future analysis. Additionally, since each value in the lists represented a different piece of information about the recipe's nutrition (first value was number of calories, second value was total fat (PDV), and so on for a total of 7 values), I expanded the dataset so that it included separate columns for each type of information, while still keeping the original nutrition list. The picture below shows what the cleaned data looks like:
<img width="847" height="164" alt="Screenshot 2025-12-09 at 12 01 23 PM" src="https://github.com/user-attachments/assets/fe6755da-4d11-4353-9daa-baa20d480926" />

I conducted three univariate analyses to see the distirbution of three variables: average rating, number of steps, and number of ingredients. The latter two were variables I believed were useful to accurately predict a recipe's average rating, so I wanted to include them in my initial analysis. The plot below shows the distribution of the number of steps, which appear to have a moderately strong skew to the right, meaning that most recipes don't require as many steps as the average number of steps required to follow in these recipes.
<img width="584" height="398" alt="Screenshot 2025-12-12 at 12 30 29 AM" src="https://github.com/user-attachments/assets/0542019b-1a07-446f-8a6e-a30c783889a7" />


The plot below displays the relationship between average rating and number of steps. It looks like the bulk of average ratings fall between the range of 4-5, and also typically require no more than 40 steps.
<img width="596" height="417" alt="Screenshot 2025-12-12 at 12 31 52 AM" src="https://github.com/user-attachments/assets/22b5d7d0-5846-4d5b-82e5-005dd7f7bbf5" />


I created a pivot table to explore the average number of tags given the number of ingredients for each unique number of steps. This is a useful way to quickly explore how recipes with different numbers of ingredients and different numbers of steps may fall into more or less categories for what the food can be used for, whether it's a quick source of protein, or a large family size meal to take to potlucks!
<img width="523" height="236" alt="Screenshot 2025-12-08 at 9 29 02 PM" src="https://github.com/user-attachments/assets/8da1c141-f4b9-43e7-87d4-b2168492e315" />

## Assessment of Missingness

I found out which columns in my dataset contained any missing values. There were three: name, description, and my aggregated column average_rating.

## Hypothesis Testing

I decided to test whether the average ratings for simple recipes (requiring <= 5 steps) and complex recipes (requiring > 5 steps) were the same. The p-value I got was 0.008 < 0.05, which tells us that the observed difference in means is statistically significant. We reject the null hypothesis, as there is sufficient evidence that simple recipes have a higher mean rating than complex recipes.

## Framing a Prediction Problem

To continue with the work I've done on exploring the relationship between average rating and other variables in the dataset, I decided to build a machine learning model that predicts the average rating of a recipe and chose to use root mean squared error (RMSE) as my metric to evaluate the model's performance.

## Baseline Model

To predict the average rating of a recipe, I used the two main features I've analyzed: number of steps and number of ingredients. Both features are numerical. I got an RMSE of about 0.636, which I think is a good start, but I can reduce it even further by including more features in my model.

## Final Model

To improve the model's performance, i.e. reduce the RMSE, I added several new features: tag_count, which represents the number of items in each list under the 'tags' column, and the seven new columns I created from expanding the list in the 'nutrition' column so that each type of nutrition information gets its own column. All these new features are numerical.

## Fairness Analysis

While the second model does have a lower RMSE than the first, I had to consider whether my model performed worse for simple recipes than complex recipes as I was initially exploring in my permutation test.
