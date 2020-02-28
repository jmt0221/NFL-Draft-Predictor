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

I also ended up dropping the total receiving and rushing yards since they were heavily correlated with average yards and rush attempts. Lasly I One Hot Encode all the categorical variables, but leave the continues variables as is since scaling didn't improve the models performance. 


# Model