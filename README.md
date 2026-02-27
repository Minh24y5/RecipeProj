# Finding The Correlation Between Simplicity And Rating Of Recipes

Author: Minh Quang Pham

This data science project, conducted at UCSD, aims to discover the relationship between the amount of ingredients in a recipe on food.com and its average rating.

# Introduction

First launched in 1999, [food.com](https://www.food.com/) has become one of the biggest website to share recipes for any kind of dish you would think of, featuring over 500,000 user-generated recipes and millions of review. However, people find it harder than ever to prepare food due to many reasons, such as time, thus possibly making simpler recipes to be more popular. This raises a question: **Does simple recipes receive higher rating on average compared to other recipes?** To find this, I choose to analyze a subset of data in the report, containing recipes and reviews posted since 2008.

The first dataset, `recipes`, contains 83782 rows and 10 columns:

| Column | Description|
|---|---|
| `'name'` | Recipe name |
| `'id'` | Recipe ID |
| `'minutes'` | Minutes to prepare recipe |
| `'contributor_id'` | User ID who submitted this recipe |
| `'submitted'` | Date recipe was submitted |
| `'tags'` | Food.com tags for recipe |
| `'nutrition'` | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| `'n_steps'` | Number of steps in recipe |
| `'steps'` | Text for recipe steps, in order |
| `'description'` | User-provided description |

The second dataset, `interactions`, contains 731927 rows and 5 columns:

|Column |Description |
|---|---|
|`'user_id'` |User ID |
|`'recipe_id'` |Recipe ID |
|`'date'` |Date of interaction |
|`'rating'` |Rating given |
|`'review'` |Review text |

From these datasets, I will analyze whether people rate recipes with less ingredients higher than other recipes or not. To answer that, the most relevant columns in my research will be `'n_ingredients'`, `'rating'`, which will be the rating an user gave on their review, and `'average_rating'`, which is the average rating a recipe has.

From this research, I aim to inform the readers about a potential trend in people's preference to simple recipes, where they do not have to prepare many ingredients and save time and money. I hope the research can help [food.com](https://www.food.com/) improve their report on recipes and see how people react to different recipes based on their complexity.

# Data Cleaning and Exploratory Data Analysis

## Data Cleaning
In order to have the most effective analysis on this topic, I will clean the data in the following steps:
1. Left merge the recipes dataset with the ratings dataset on `'id'` and `'recipe_id'`, respectively.

2. In the merged dataframe, fill all ratings of 0 with `np.nan`. Because rating is on a scale of 1 to 5, which mean that 1 will be the lowest rating while 5 means the highest rating, I think that 0 indicates that the review did not include a rating or the rating was missing. Therefore, replacing 0 with np.nan can help avoid bias.

3. Use groupby method to find the average rating of each recipe as a Series.

4. Assign a new column `'average_rating'` to the dataframe.

5. Add column `'simple'` to the dataframe. From my data cleaning process, I discover that the average ingredients per recipe of the recipes dataset is 9. As a result, I assume that a simple ingredients would have less ingredients than this amount. `'simple'` is a boolean column that has True values for recipes with strictly less than 9 ingredients, and False values for other recipes.

6. Add column `'Year'` to the dataframe. I do this by convert the `'submitted'` column, which is in string, to pd.datetime, and then extract the year from that column.

The resulting dataframe has 234429 rows and 20 columns. Because of the large number of columns, I decided to only show the most relevant columns to my research. Below is the first 5 unique recipes of the cleaned dataframe:

|name|id|minutes|n_steps|n_ingredients|rating|average_rating|simple|Year|
|---|---|---|---|---|---|---|---|---|
|1 brownies in the world best ever|333281|40|10|9|4|4|False|2008|
|1 in canada chocolate chip cookies|453467|45|12|11|5|5|False|2011|
|412 broccoli casserole|306168|40|6|9|5|5|False|2008|
|millionaire pound cake|286009|120|7|7|5|5|True|2008|
|2000 meatloaf|475785|90|17|13|4|4|False|2012|

## Univarate Analysis
I analyzed the n_ingredients column to see the distribution of the amount of ingredients for each recipe.

<iframe src="assets/ing_dist.html" width="800" height="600" frameborder="0"></iframe>

From this histogram, we can observe that the distribution is right-skewed, showing that recipes on food.com tend to have less ingredients with 8 being the most common number of ingredients. There are also a decreasing trend that less recipes have many ingredients.
