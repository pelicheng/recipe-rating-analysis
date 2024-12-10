# Exploring Recipe Ratings: What Contributes to Higher Average Ratings?
Author: Peiling Cheng
## Introduction
Sharing recipes has created opportunities for creativity in the kitchen. With the connections through the internet, recipes from different cultures are just a click away. [Food.com](https://www.food.com/) is one of the many websites that have built a community around recipes. From this website, I obtained two datasets, one with information about the recipe and the other about ratings given by users. Using the information obtained, I am interested in **what types of recipes tend to have higher average ratings.** Exploring this question would provide those from restaurants to small business entrepreneurs and home cooks with valuable insights when making recipe decisions.

`recipe` is the first dataset we have. It contains 83782 rows and the following columns:

| Column         | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| `name`         | Recipe name                                                                 |
| `id`           | Recipe ID                                                                   |
| `minutes`      | Minutes to prepare recipe                                                   |
| `contributor_id` | User ID who submitted this recipe                                          |
| `submitted`    | Date recipe was submitted                                                   |
| `tags`         | Food.com tags for recipe                                                   |
| `nutrition`    | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| `n_steps`      | Number of steps in recipe                                                   |
| `steps`        | Text for recipe steps, in order                                              |
| `description`  | User-provided description                                                   |

`interactions` contain 731927 rows and the following columns: 

| Column      | Description              |
|-------------|--------------------------|
| `user_id`   | User ID                  |
| `recipe_id` | Recipe ID                |
| `date`      | Date of interaction      |
| `rating`    | Rating given             |
| `review`    | Review text              |

## Data Cleaning
To be able to use these datasets, the following steps were applied.
1. Left merge the recipes and interactions on `id` and `recipe_id`.
2. Dropped one of the columns representing recipe id and keeping `recipe_id`.
3. Fill all ratings of 0 with `np.nan` because ratings range from 1 to 5.
4. The average rating per recipe is added as the column `average_rating`.
5. Checked the data types of all the columns and cast when needed.
    - Changed `submitted` from a string to a `datetime` object.
    - Changed `tags` from a string to a list.
    - Changed `nutrition` from a string to a list.
    - Changed `steps` from a string to a list.
    - Changed `ingredients` from a string to a list.
    - Changed `date` from a string to a `datetime` object.
6. Extracted columns that I will be using.

### First Five Rows

| name                                 |   recipe_id |   minutes |   n_steps | submitted   | nutrition                                    |   n_steps |   n_ingredients |          user_id | date       |   rating |   average_rating |
|:-------------------------------------|------------:|----------:|----------:|:------------|:---------------------------------------------|----------:|----------------:|-----------------:|:-----------|---------:|-----------------:|
| 1 brownies in the world    best ever |      333281 |        40 |        10 | 2008-10-27  | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        10 |               9 | 386585           | 2008-11-19 |        4 |                4 |
| 1 in canada chocolate chip cookies   |      453467 |        45 |        12 | 2011-04-11  | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        12 |              11 | 424680           | 2012-01-26 |        5 |                5 |
| 412 broccoli casserole               |      306168 |        40 |         6 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 |  29782           | 2008-12-31 |        5 |                5 |
| 412 broccoli casserole               |      306168 |        40 |         6 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 |      1.19628e+06 | 2009-04-13 |        5 |                5 |
| 412 broccoli casserole               |      306168 |        40 |         6 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 | 768828           | 2013-08-02 |        5 |                5 |

> While looking through the dataset, I found recipes that weren't real recipes such as 'how to preserve a husband' mentioning tips to keep a good relationship. Since its data weren't that different from real recipes, they were not removed.

As I explored the dataset, I added more columns to simplify the analysis process.
1. `is_simple`: `True` or `False` indicating if the recipe has less than or equal to 10 steps
2. `calories`: the number of calories extracted from `nutrition` list
3. `calories_range`: Bins that the number of calories fall into
4. `cal_low_mid_high`: `low` is less than or equal to 300 calories, `medium` is less than or equal to 800 calories, and anything above that is `high`

### First Five Rows

| name                                 |   recipe_id |   minutes |   n_steps |   n_ingredients |   rating |   average_rating | is_simple   |   calories | calorie_range   | cal_low_mid_high   |
|:-------------------------------------|------------:|----------:|----------:|----------------:|---------:|-----------------:|:------------|-----------:|:----------------|:-------------------|
| 1 brownies in the world    best ever |      333281 |        40 |        10 |               9 |        4 |                4 | True        |      138.4 | 101-200         | low                |
| 1 in canada chocolate chip cookies   |      453467 |        45 |        12 |              11 |        5 |                5 | False       |      595.1 | 501-600         | medium             |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |

## Exploratory Data Analysis

- Embed at least one plotly plot you created in your notebook that displays the distribution of a single column (see Part 2: Report for instructions).

<iframe
  src="assets/uni_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/uni_ingredients.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

- Embed at least one plotly plot that displays the relationship between two columns.

<iframe
  src="assets/bi_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/bi_is_simple.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

- Embed at least one grouped table or pivot table in your website and explain its significance.

| calorie_range   |    steps |   count |
|:----------------|---------:|--------:|
| 0-100           |  7.40371 |   26435 |
| 1000+           | 12.5791  |   12707 |
| 101-200         |  8.60998 |   46305 |
| 201-300         |  9.53788 |   44056 |
| 301-400         | 10.244   |   34883 |
| 401-500         | 11.165   |   25884 |
| 501-600         | 11.2582  |   16192 |
| 601-700         | 11.9804  |   10938 |
| 701-800         | 12.8463  |    8080 |
| 801-900         | 12.4846  |    5237 |
| 901-1000        | 12.17    |    3712 |

- Embed a plotly plot related to your missingness exploration; ideas include:

<iframe
  src="assets/missingness_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/missingness_minutes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<!-- | name                                 |   recipe_id |   minutes |   n_steps |   n_ingredients |   rating |   average_rating | is_simple   |   calories | calorie_range   | cal_low_mid_high   |
|:-------------------------------------|------------:|----------:|----------:|----------------:|---------:|-----------------:|:------------|-----------:|:----------------|:-------------------|
| 1 brownies in the world    best ever |      333281 |        40 |        10 |               9 |        4 |                4 | True        |      138.4 | 101-200         | low                |
| 1 in canada chocolate chip cookies   |      453467 |        45 |        12 |              11 |        5 |                5 | False       |      595.1 | 501-600         | medium             |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                | -->


- Permutation:

<iframe
  src="assets/perm_steps.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/perm_ingredients.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/perm_calories.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>