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