# Exploring Recipe Ratings: What Contributes to Higher Average Ratings?
Author: Peiling Cheng
- Show the head of your cleaned DataFrame (see Part 2: Report for instructions).
- Embed at least one plotly plot you created in your notebook that displays the distribution of a single column (see Part 2: Report for instructions).
- Embed at least one plotly plot that displays the relationship between two columns.
- Embed at least one grouped table or pivot table in your website and explain its significance.
- Embed a plotly plot related to your missingness exploration; ideas include:


# Exploring Recipe Ratings: What Contributes to Higher Average Ratings?
Author: Peiling Cheng
## Overview
### Heading 3 Text
Normal Test

## Introduction

- Show the head of your cleaned DataFrame (see Part 2: Report for instructions).

| name                                 |   recipe_id |   minutes |   n_steps | submitted   | nutrition                                    |   n_steps |   n_ingredients |          user_id | date       |   rating |   average_rating |
|:-------------------------------------|------------:|----------:|----------:|:------------|:---------------------------------------------|----------:|----------------:|-----------------:|:-----------|---------:|-----------------:|
| 1 brownies in the world    best ever |      333281 |        40 |        10 | 2008-10-27  | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        10 |               9 | 386585           | 2008-11-19 |        4 |                4 |
| 1 in canada chocolate chip cookies   |      453467 |        45 |        12 | 2011-04-11  | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        12 |              11 | 424680           | 2012-01-26 |        5 |                5 |
| 412 broccoli casserole               |      306168 |        40 |         6 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 |  29782           | 2008-12-31 |        5 |                5 |
| 412 broccoli casserole               |      306168 |        40 |         6 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 |      1.19628e+06 | 2009-04-13 |        5 |                5 |
| 412 broccoli casserole               |      306168 |        40 |         6 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 |               9 | 768828           | 2013-08-02 |        5 |                5 |

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

| name                                 |   recipe_id |   minutes |   n_steps |   n_ingredients |   rating |   average_rating | is_simple   |   calories | calorie_range   | cal_low_mid_high   |
|:-------------------------------------|------------:|----------:|----------:|----------------:|---------:|-----------------:|:------------|-----------:|:----------------|:-------------------|
| 1 brownies in the world    best ever |      333281 |        40 |        10 |               9 |        4 |                4 | True        |      138.4 | 101-200         | low                |
| 1 in canada chocolate chip cookies   |      453467 |        45 |        12 |              11 |        5 |                5 | False       |      595.1 | 501-600         | medium             |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |
| 412 broccoli casserole               |      306168 |        40 |         6 |               9 |        5 |                5 | True        |      194.8 | 101-200         | low                |


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