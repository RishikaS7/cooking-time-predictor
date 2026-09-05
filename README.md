# Cooking Time Predictor

YumYumYumInMyTumTumTum  
By: Rishika Sahu and Natalie Wu

**Introduction**  
For our DSC 80 Final Project, we chose to work with the provided dataset from Food.com. With a busy lifestyle, it is critical that the recipes we choose to make are not only tasty but simple and quick to make as well. With that being said, we chose to focus our project on predicting the time it takes to make a recipe using features such as the number of steps, number of ingredients, and nutrition facts. In the merged dataset, there is a total of 234,429 rows and 17 columns. Out of the 17 columns, the ones most useful to us are `minutes`, `n_steps`, and `ingredients` since they overall will be able to give us a good idea of the timing, steps, and the ingredients required.  


**Data Cleaning and Exploratory Data Analysis**   
For the data cleaning process, we started out by merging the interactions.csv with the RAW_recipes.csv on the `recipe_id`/`id` columns in the corresponding datasets since those columns represented the identification of each recipe. An additional thing to note on the merging process is that we used a left merge to ensure that all of the listed recipes are being used in our project even if they have no ratings, reviews, or interactions in general.  
After merging the datasets together, we needed to fill any null values in `rating` with a 0 (per the given project instructions). We then calculated the average rating for each recipe by grouping the DataFrame by `id` and calculating the mean for the 'rating' column before merging it into our main dataset as a column called `avg_rating`.  

|     id | name                                 |   minutes |   n_steps |   n_ingredients |   avg_rating |
|-------:|:-------------------------------------|----------:|----------:|----------------:|-------------:|
| 333281 | 1 brownies in the world    best ever |        40 |        10 |               9 |            4 |
| 453467 | 1 in canada chocolate chip cookies   |        45 |        12 |              11 |            5 |
| 306168 | 412 broccoli casserole               |        40 |         6 |               9 |            5 |
| 306168 | 412 broccoli casserole               |        40 |         6 |               9 |            5 |
| 306168 | 412 broccoli casserole               |        40 |         6 |               9 |            5 |
  
  
<iframe
  src="assets/distribution_of_steps.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>
*This plot represents univariate analysis using the distribution of the number of steps throughout each recipe, with `n_steps` on the horizontal axis and the vertical axis representing the density. The graph is very strongly right skewed which is a representation of the more complex and elaborate dishes in comparison to the simple recipes that are more commonly made.*

<iframe
  src="assets/ing_steps.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>
*This plot represents the bivariate analysis between `n_ingredients` and `n_steps` with `n_steps` on the horizontal axis and `n_ingredients` on the vertical axis. In this scatterplot, there is some clustering in the bottom left where the number of steps range from 0 to 30 and the number of ingredients from 0 to 15. Because there is a slight positive association, there is a trend showing that recipes with more ingredients tend to require more steps.*

| n_step_group   |     1-5 |     6-10 |    11-15 |    16-20 |      21+ |
|:---------------|--------:|---------:|---------:|---------:|---------:|
| 1-10           | 135.403 |  69.9325 |  80.5614 |  91.9591 |  135.319 |
| 11-20          | 565.024 |  85.6878 |  83.585  | 116.612  |  123.245 |
| 21-30          | 512.816 | 146.249  | 122.258  | 314.958  |  168.814 |
| 31-40          | 339.691 | 251.076  | 130.076  | 190.704  |  277.705 |
| 41+            | 238.114 | 350.005  | 168.005  | 325.993  | 1010.45  |
  
  
*This pivot table is used to show the recipe's complexity using `n_steps` and `n_ingredients` and how it relates to the recipe's cooking time using `minutes`. In general, the data reveals an upward moving trend which relates with the question that we are exploring on how recipes with a greater amount of steps and ingredients require more time to make. Additionally, this pivot table also highlights some of the outliers we had which were recipes that had little ingredients but took a very long time to prepare (such as fermentation processes).*

**Assessment of Missingness**  
A column that we suspected may be MNAR (missing not at random) was the `description` column because it is dependent on whether or not the authors of the recipes wanted to write it. It is possible that they felt like the recipe didn't need one because of the simplicity or they just did not feel like doing it. One piece of additional information that could help explain the missingness (make it MAR) is the activity of each recipe author. This way, if we see that an author is typically not very active, it could explain the missing description.   
We performed a permutation test to see if the missingness in `description` was because of `n_ingredients`. One rationale behind this was if the recipe itself had a lot of ingredients and therefore a lot to type out, the recipe author may be less willing to write the description. 
For the permutation test, our **null hypothesis** was: The distribution of `n_ingredients` is the same for recipes with missing descriptions and recipes with non-missing descriptions and our **alternative hypothesis** was: The distribution of `n_ingredients` is different for recipes with missing descriptions versus those with non-missing descriptions.  
As a result of our 1,000 simulations, we got a p-value of 0.001 which led us to reject the null hypothesis. This strongly indicates that the missingness of `description` is dependent on `n_ingredients` which means that the missingness is MAR rather than MCAR. 
