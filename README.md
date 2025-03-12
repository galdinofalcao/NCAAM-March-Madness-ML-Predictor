# NCAAM-March-Madness-ML-Predictor

## **Description of the Problem:**
March Madness in the NCAA is a high-stakes knockout tournament where top collegiate teams compete in a single-elimination format. The unpredictable nature of the tournament and the pressure of each elimination game create a unique challenge for forecasting match outcomes. Predict outcomes in the NCAAM tournament by leveraging a dataset filtered to include the top 64 teams (ranked by ESPN’s BPI) alongside game data from the 2024–25 season sourced from Kaggle.

## **Project Goal:**
Historical data from ESPN and Kaggle was leveraged to build a machine learning model for predicting matchup outcomes during the high-pressure knockout phase of March Madness. Accuracy was used as the primary performance metric, with F1 score serving as a secondary metric.

## **Tools and Libraries:**
- Python: Primary language for data cleaning, manipulation, and analysis.
- Pandas: Efficient data manipulation and preprocessing.
- NumPy: Numerical operations and array-based computations.
- Seaborn: Statistical data visualization and exploratory analysis.
- Matplotlib: Creation of detailed visualizations and custom charts.
- Scikit-Learn (Sklearn): Preprocessing, model training, data splitting, evaluation and cross-validation.
- CatBoost: Gradient boosting model training, particularly with categorical features.
- BeautifulSoup (bs4): HTML parsing and web scraping.
- Selenium: Browser automation and web scraping using Chrome WebDriver.

## **Data Preparation:**
1) The top 64 teams from ESPN were extracted based on the Basketball Power Index Rank (BPI RK).
   
2) The Kaggle dataset was filtered to include only these 64 teams for the 2025 season.
   
3) BeautifulSoup and Selenium were utilized to scrape the ESPN website for the scoreboard of the 2024–25 NCAA Men’s Basketball games, capturing each matchup (team_1 vs team_2) along with the game scores.
   
4) The 'winner' column, derived from the scraping process, served as the target variable, indicating whether team_1 won (class 1) or lost (class 0).
   
5) Features were engineered by calculating, for each matchup, the difference between the statistics of team_1 and team_2, resulting in a total of 26 features per game.
    
6) Features underwent selection and aggregation across two primary categories: Team Stats and General Info. The Team Stats category is divided into three subcategories: (A) Efficiency & Shooting, (B) Game Dynamics & Possession, and (C) Overall Team Performance & Experience. The General Info category comprises contextual columns that do not directly reflect in-game performance but remain significant for modeling or identification. Below is an overall description of all features and the applied aggregation methods:

## **Team Statistics for Features:**
### ***1. Efficiency & Shooting Metrics***


| Metric                                    | Description                                                                                                                                   |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| Adjusted Offensive Efficiency             | Points scored per 100 possessions, adjusted for opponent strength. Higher values indicate a more efficient offense.                           |
| Adjusted Defensive Efficiency             | Points allowed per 100 possessions, adjusted for opponent strength. Lower values indicate a stronger defense.                                |
| eFGPct (Effective Field Goal Percentage)  | Adjusts field goal percentage to account for the extra value of three-point shots.                                                            |
| FTRate (Free Throw Rate)                  | Ratio of free throw attempts to field goal attempts, indicating how frequently the team gets to the line.                                      |
| FG2Pct (2-Point Field Goal Percentage)    | Success rate on two-point shots inside the arc.                                                                                             |
| FG3Pct (3-Point Field Goal Percentage)    | Success rate on shots taken from beyond the arc.                                                                                            |
| FTPct (Free Throw Percentage)             | Conversion rate on free throws.                                                                                                               |
| BlockPct (Block Percentage)               | Percentage of opponent two-point shots blocked by the team.                                                                                   |
| OppFG2Pct (Opponent 2-Point Field Goal Percentage) | Opponents’ success rate on shots inside the arc, reflecting the team’s ability to defend close-range attempts.                               |
| OppFG3Pct (Opponent 3-Point Field Goal Percentage) | Opponents’ success rate on shots from beyond the arc, reflecting the effectiveness of the perimeter defense.                                 |
| OppFTPct (Opponent Free Throw Percentage) | Conversion rate on opponents’ free throws.                                                                                                  |
| OppBlockPct (Opponent Block Percentage)   | Percentage of the team’s own two-point attempts that are blocked by opponents.                                                                |


### ***2. Game Dynamics & Possession Metrics***

| Metric                                    | Description                                                                                                                                   |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| Adjusted Tempo                            | Estimated number of possessions per 40 minutes, adjusted for opponent, indicating the pace of play.                                              |
| TOPct (Turnover Percentage)               | Percentage of possessions that end in turnovers; lower values are preferable.                                                                  |
| ORPct (Offensive Rebound Percentage)      | Percentage of available offensive rebounds secured by the team.                                                                               |
| ARate (Assist Rate)                       | Percentage of made field goals that are assisted, reflecting team ball movement.                                                               |
| StlRate (Steal Rate)                      | Percentage of defensive possessions that result in a steal by the team.                                                                         |
| OppStlRate (Opponent Steal Rate)          | Percentage of the team’s offensive possessions that end in a steal by the opponent.                                                             |


### ***3. Overall Team Performance & Experience***

| Metric                          | Description                                                                                                                         |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Net Rating                      | Difference between offensive and defensive ratings (points scored minus points allowed per 100 possessions).                           |
| Experience                      | A measure of the team’s overall experience, often weighted by minutes played.                                                        |
| W-L                             | Overall win-loss record, serving as a straightforward indicator of team success.                                                     |
| BPI (Basketball Power Index)    | ESPN’s comprehensive power metric for the team, combining aspects of offense, defense, and pace.                                        |


### ***4. General Info***

| Metric                                    | Description                                                                                                                         |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Active Coaching Length                    | Indicates the duration of the current coach’s tenure.                                                                               |
| SOS RK (Strength of Schedule Rank)        | Rank that reflects the overall difficulty of the team’s schedule; lower rankings denote more challenging schedules.                   |
| NC SOS (Non-Conference Strength of Schedule) | Reflects the difficulty of non-conference games, which can differ significantly from conference play.                          

## **Datasets:**
The DataSet is prepared from ESPN and Kaggle and is compiled in the files:
- NCAA_mens_data - Feature Engineered Data
  - 509 rows representing possible matchups in the season
  - 34 columns representing Team stats provided above
  - Data wrangling and aggregation done through Microsoft Excel
- raw_ncaa_mens_data - Raw data scrubbed from the websites with Team1 and Team2 statistics without any aggregation

The Data wrangling and aggreation were done through Excel Spreadsheet.

## **Workbook Preview:**
| Feature Correlation Heatmap | Feature Correlation Heatmap |
|:---------------------------:|:---------------------------:|
| ![download](https://github.com/user-attachments/assets/65b57df2-eed3-47ff-9e78-aac8851fc73b) | ![download](https://github.com/user-attachments/assets/65cfa8ff-73f5-4b36-99dd-3123cace1e53) |


| **Counts of Team1 and Team2** | **Net Rating Differences Between Top 20 Teams** |
|:-----------------------------:|:-----------------------------------------------:|
| ![download](https://github.com/user-attachments/assets/783b96e4-5cea-4b4b-bb79-a7ea7f893420) | ![download](https://github.com/user-attachments/assets/898dcd16-d2b5-4959-ad8b-583898a05eae) |


| **Comparison of Models** | **Feature of Importance** |
|:-----------------------------:|:-----------------------------------------------:|
| ![download](https://github.com/user-attachments/assets/f74b9f2f-1c4c-4b5d-9d75-ad6ec7e6cff4) | ![download](https://github.com/user-attachments/assets/8b737e60-0a09-42c0-85b1-78e085e782a9) |














