# NFL Draft Predictor

# Project Goals

The goal of this project is to use a classification algorithm to predict whether a player will be drafted in the top 2 rounds of the NFL draft given a players physical features, college statistics, and combine data. 

# Data Collection

I used BeautifulSoup and Selenium to scrape the following data for players in the last twenty NFL drafts:
- Average and Total Number of Receiving and Rushing Yards
- Rush Attempts
- Rushing and Receiving Touchdowns
- Total games Played
- School and Conference
- Height and Weight
- Year, Round Drafted
- Year of College when Drafted
- Position
- Forty Yard Dash

# EDA

Due to a lot of missing data for linemen and defensive players, I kept the data focused on offence and decided to use only wide receivers and running backs for a combined total of about 600 observations. As you can see from the graph below, the two positions have different relationships with the other variables, so when we use models such as Logistic Regression we need to create interaction terms between the position variable and some of the other variables.
<p align="center">
<img src="https://github.com/jmt0221/NFL-Draft-Predictor/blob/master/images/interaction.png" width="800" height="300">
</p>

I drop the total receiving and rushing yards since they were heavily correlated with average yards and rush attempts. After, the categorical variables are one hot encoded, but the continuous variables are left unscaled since it didn't improve performance. When I started modeling I realized that there was a heavy class imbalance since I was predicting if a player is in the top 2 rounds. To solve this I use SMOTE to upsample the data and rebalance the dataset so our models don't lean towards a single prediction.


# Models

## Model 1: Random Forest with Grid Search

With Random Forest, it was not needed to create interaction terms since it looks at each variable while weighing in previous splits, so it automatically separates the different positions. I used Grid Search to navigate the hyper parameters of the algorithm to create the best fit.

I took the Random Forest and looked at which features were used the most to classify each observation, this allowed me to create a graph and evaluate the feature importance in my dataset.

<p align="center">
<img src="https://github.com/jmt0221/NFL-Draft-Predictor/blob/master/images/feature_importance.png" width="600" height="500">
</p>

## Model 2: Logistic Regression

Like I mentioned above Logistic Regression requires us to create interaction terms to allow each position to have different weights for the other variables. I also attempted to use polynomial terms but it didn't help the model improve and only made it harder to derive inference from the model. This model has about the same accuracy as the previous Random Forest model, but catches much more of players that were drafted in the top rounds. In this experiment I deemed it was more important to catch potential top players than have a balanced mix missed on both sides.


<p align="center">
<img src="https://github.com/jmt0221/NFL-Draft-Predictor/blob/master/images/logistic_reg.png" width="900" height="250">
</p>
