# League of Legends KDA Statistical Analysis
With a focus on the aggregated kills, deaths, and assists (KDA) variable, this UCSD project seeks to analyze the relevance of this statistic within League of Legends matches and its impact on in-game statistics and outcomes.

By: Odessa Castillo
## Introduction
### Project Overview
League of Legends (LoL), otherwise known as League, is an online multiplayer battle game that focuses on player-on-player combat in a team setting. With players controlling various characters, or "champions", players can utilize various methods such as gaining experience points, gold, or items in order to defeat the opposing team, and thus, its gameplay being popular with players worldwide. This analysis will focus on a dataset developed by Oracle's Elixir.

The dataset contains gameplay statistics spanning across various matches, detailing both player and team info across categories such as champion selection, overall performance, and overall progress towards securing a game win. While distinct from each other, these categories provide detailed context as to how player and team in-game choices and dynamics can vary and drastically impact overall results.

In LoL, kills, deaths, and assists (KDA) is a significant statistic in measuring player performance in-match. As calculated by the equation below, understanding KDA is essential to evaluating at a player's overall contributions to team results, with a higher KDA meaning a more impactful performance (players have a higher kills and assists ratio to deaths). With KDA varying across player roles, KDA plays a key part in analyzing team strategy, allowing us to get a glimpse into how effectively maxmizing player roles can lead to positive team outcomes.
                                                                                                  $$KDA = (Kills + Assists) / Deaths$$

I will be focusing on answering the central question: **How effective is KDA as a measure of player and team performance in-game?**. While KDA itself is a good baseline metric, with other factors such as skill of an overall league, and other metrics of performance such as dpm, KDA's effectivenss as a metric might not capture all factors that could lead to a team winning/losing. In conjunction with the predictive model used, insights gained can be used to optimize team strategy and decision making, leading to consistent and positive performance across games.

### Column Overview
The dataset contains information spanning various game matches within the 2024 year. In this dataset specifically, it contains 117648 amount of rows and 163 columns. The most relevant columns featured for my data analysis are explained below:

| **Column**      | **Description** |
| ----------- | ----------- |
| `'gameid'`      | unique identifier for each game played      |
| `'league'`  | the professional league a team belongs to/league tournament in which match happened        |
| `'gamelength'`      | the length of a game in minutes |
| `'kills'`      | the number of enemy champions a player or team eliminated in match |
| `'deaths'`      | the amount of times a player or team was elimated by enemy champions |
| `'assists'`     | the number of assists given to player or team (ie. when they helped eliminate enemy champion without getting kill recognition |
| `'earnedgold'`      | the amount of gold a player or team earns in match |
| `'monsterkills'`      | the amount of monsters a player or team eliminate in match |
| `'monsterkillsownjungle'`      | the amount of monsters elimated by player or team in their own jungle |
| `'dpm'`      | the amount of damage per minute a player deals on average in game |


## Data Cleaning and Exploratory Data Analysis
For convinence, only the `'gameid'`, `'league'`, `'gamelength'`, `'kills'`, `'deaths'`, `'assists'`, `'earnedgold'`, `'monsterkills'`, and `'monsterkillsownjungle'` columns were kept. Further, to prevent double counting values for both players and teams in the KDA analysis, rows where 'position' was team (row was an aggregate of a team's performance for each player column) were filtered out. To assist in the permutation test this project and staying true to my central question, two columns were created: 'tier' and 'KDA'. 

`'tier'` was assigned to each team using a helper function based on official league and tournament information found on Wikipedia and the Internet. Any team that didn't have an associated league/tournament identifier was placed in Tier A, or the ameteur league for purposes of a fair data analysis.`'KDA'` was created by normalizing the kills, deaths, and assists columns and plugging those values into the KDA equation to get the normalized KDA across all players. The normalization was necessary due to factors like game length that can impact the values of the kills, deaths, and assists columns for longer game durations. To maintain simplicity, the normalized columns were dropped after creating the `'KDA'` column.

| **Column**      | **Description** |
| ----------- | ----------- |
| `'tier'`      | the skill level group a team is placed in, is used for tournament play      |
| `'KDA'`   | the aggregate perfomance measured calculated using player kills, deaths, and assists        |

The resulting dataframe has 13 columns and 90840 rows.

| gameid             | teamname    | league   |   gamelength |   kills |   deaths |   assists |   monsterkills |   monsterkillsownjungle |     dpm |   earnedgold | tier   |       kda |
|:-------------------|:------------|:---------|-------------:|--------:|---------:|----------:|---------------:|------------------------:|--------:|-------------:|:-------|----------:|
| 10660-10660_game_1 | LNG Esports | DCup     |         1886 |       1 |        3 |         1 |             23 |                      16 | 225.62  |         6960 | A      | 132.461   |
| 10660-10660_game_1 | LNG Esports | DCup     |         1886 |       0 |        4 |         3 |            139 |                     111 | 234.178 |         4513 | A      |  -4.00307 |
| 10660-10660_game_1 | LNG Esports | DCup     |         1886 |       0 |        2 |         0 |              1 |                       1 | 318.293 |         6620 | A      |   5.02502 |
| 10660-10660_game_1 | LNG Esports | DCup     |         1886 |       2 |        4 |         0 |              4 |                       0 | 346.511 |         8101 | A      |  -3.85904 |
| 10660-10660_game_1 | LNG Esports | DCup     |         1886 |       0 |        3 |         3 |              0 |                       0 | 205.228 |         3098 | A      | 127.651   |



I decided to perform a univariate analysis on player dpm.

<iframe
  src="assets/q2aplot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The overall distribution is slightly right-skewed, suggesting that players in their game strategy are more likely to either use champions that on average deal a lower dpm, or utilize their champions and items to provide more support as opposed to dealing damage.

I also decided to perform a univariate analysis on player earned gold.

The overall distribution is slightly right-skewed but overall balancedd, suggesting that in various game scenarios, players and teams are collecting "normal" amounts of gold across various game scenarios. In other words, no player/team is necessarily at an advantage/disadvantage when it comes to game farming.

Next, I decide to perform a bivariate analysis on both the relationship between league and team kills, and league and team deaths.



## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
