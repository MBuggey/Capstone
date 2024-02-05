## Project Overview 
---
This project was created as the capstone project for BrainStation's Data Science Diploma program.  The purpose of this project is to create a recommender algorithm for the Steam game store.  Specifically, this project seeks to create a recommender that is able to recognize early signs of success in the Indie (independent developer) game genre and predict whether a title will be successful, and if it is, recommend it.  

The issue in the gaming space is that indie developers often do not have strong budgets to market their games, often forced to spend it all on development.  This makes it difficult for them to reach potential buyers, often relying on free social media marketing and community influence to get the word out.  Despite this, indie games have had many examples of runaway success.  So much so that there has been a marked shift of trust of the gaming community from established game development studios to new indie studios, marking a gaming renaissance of sorts.  That being said there are all too many examples of game finishing development and lying dormant for long periods of time until a player with a strong community following plays it and revitalizes the entire project.  

The purpose of this algorithm is to hopefully streamline the discovery process. To boost games that it determines has strong potential for success in the market that may not otherwise receive any attention. 

## Data Source
---
The version of the dataset that was used for this project can be downloaded [here.](https://drive.google.com/file/d/1uAk0yDECBKfU1yI5PucsgsySShJ4tyFc/view?usp=sharing)

These datasets were sourced from Kaggle, the original poster specified a monthly update frequency so you can potentially source an updated dataset [here.](https://www.kaggle.com/datasets/antonkozyriev/game-recommendations-on-steam)

## Data Breakdown
---
The file consists of three separates csv's and a JSON file.  

games.csv features a breakdown of all the games available for sale in the Steam store.  The intial csv contains basic data that could create a base recommender system.  The JSON file included however contains additional, non tabular, information on games such as descriptions and tags.  For our purposes we will have to extract and connect at least some of that information to this file.  

Column breakdown of games.csv is as follows:

- **app_id:** Unique id for each individual game in the games.csv
- **title:**  Title of game
- **date_release:**  Release date of the game
- **win:** Game is playable on Windows 
- **mac:** Game is playable on Mac
- **linux:** Game is playable on Linux
- **rating:**  Overall user rating of game 
- **positive_ratio:**  The ratio of positive user reviews to negative user reviews by game
- **user_reviews:** Number of unique user reviews on a game
- **price_final:** Current price of game as of last data scrape 
- **price_original:** Original price of game on release (specifically on Steam store release) 
- **discount:**  Whether the game is discounted as of last data scrape (and by how much in %)
- **steam_deck:**  Whether game is playable on Steam's handheld device, the Steam Deck

| app_id | title                                | date_release | win  | mac  | linux | rating       | positive_ratio | user_reviews | price_final | price_original | discount | steam_deck |
|--------|--------------------------------------|--------------|------|------|-------|--------------|----------------|--------------|-------------|----------------|----------|------------|
| 13500  | Prince of Persia: Warrior Within™   | 2008-11-21   | true | false| false | Very Positive | 84             | 2199         | 9.99        | 9.99           | 0.0      | true       |


---





users.csv contains information on unique Steam users.  Though the information is sparse it could potentially be used to 'grade' recommendations based on whether the user is a notable one.  

Column breakdown of users.csv is as follows:

- **user_id:** Unique id for each individual user of the Steam store.  Useful for connecting back to recommendations.csv
- **products:**  Number of products owned by unique user
- **reviews:**  Number of reviews posted by unique user

| user_id | products | reviews |
|---------|----------|---------|
| 7360263 | 359      | 0       |

----

recommendations.csv is the largest file of the three and focuses on individual user recommendations for video games.  This will be the primary column in determinine whether a game is performing well and whether a review could be a good or bad indicator of game success.  


Column breakdown of recommendations.csv is as follows:

- **app_id:** Unique id of the game being reviewed, can be tied back to app_id in games.csv
- **helpful:**  How many users voted this review as 'helpful'
- **funny:**  How many users voted this review as 'funny'
- **date:** Date of review 
- **is_recommended:** Whether the user recommends the game or not
- **hours:** Hours of playtime the user has on the game
- **user_id:**  Unique user id that can be tied back to users.csv 
- **review_id:**  Auto-generated label for review number by row.  Could potentially be deleted.


| app_id | helpful | funny | date       | is_recommended | hours | user_id | review_id |
|--------|---------|-------|------------|-----------------|-------|---------|-----------|
| 975370 | 0       | 0     | 2022-12-12 | True            | 36.3  | 51580   | 0         |



## Steps to Complete 
---

- [x] Initial GitHub repository and project breakdown 
- [x] Preliminary EDA on the data, including cleaning and noting any problem areas
- [x] Extraction of JSON file and merging pertinent data into existing csv, cleaning data again once completed
- [x] Discover usable metrics which might lead to an initial model
- [x] Begin prototyping model
- [ ] Explore virtual collaborative filtering environments
- [ ] Build PySpark based model
