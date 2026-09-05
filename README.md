# Cooking Time Predictor

YumYumYumInMyTumTumTum  
By: Rishika Sahu and Natalie Wu

**Introduction**  

For our DSC 80 Final Project, we chose to work with the provided dataset from Food.com. With a busy lifestyle, it is critical that the recipes we choose to make are not only tasty but simple and quick to make as well. With that being said, we chose to focus our project on predicting the time it takes to make a recipe using features such as the number of steps, number of ingredients, and nutrition facts. In the merged dataset, there is a total of 234,429 rows and 17 columns. Out of the 17 columns, the ones most useful to us are 'minutes', 'n_steps', and 'ingredients' since they overall will be able to give us a good idea of the timing, steps, and the ingredients required.  


**Data Cleaning and Exploratory Data Analysis**   

For the data cleaning process, we started out by merging the interactions.csv with the RAW_recipes.csv on the 'recipe_id'/'id' columns in the corresponding datasets since those columns represented the identification of each recipe. An additional thing to note on the merging process is that we used a left merge to ensure that all of the listed recipes are being used in our project even if they have no ratings, reviews, or interactions in general.  
After merging the datasets together, we needed to fill any null values in 'rating' with a 0 (per the given project instructions). We then calculated the average rating for each recipe by grouping the DataFrame by 'id' and calculating the mean for the 'rating' column before merging it into our main dataset as a column called 'avg_rating'.  

**Assessment of Missingness**
