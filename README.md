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


### Univariate Analysis
I decided to perform a univariate analysis on player dpm.

<iframe
  src="assets/q2aplot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The overall distribution is slightly right-skewed, suggesting that players in their game strategy are more likely to either use champions that on average deal a lower dpm, or utilize their champions and items to provide more support as opposed to dealing damage.

I also decided to perform a univariate analysis on player earned gold.

<iframe
  src="assets/q2bplot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The overall distribution is slightly right-skewed but overall balancedd, suggesting that in various game scenarios, players and teams are collecting "normal" amounts of gold across various game scenarios. In other words, no player/team is necessarily at an advantage/disadvantage when it comes to game farming.

### Bivariate Analysis
Next, I decide to perform a bivariate analysis on both the relationship between league and team kills, and league and team deaths. As shown by the scatterplots below, the relationship between kills and deaths are similar across leagues, signifying that both counts are proportional to each other per league.

<iframe
  src="assets/q2cplot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/q2dplot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Aggregate Analysis
Lastly I performed an aggregate analysis on game statstics in my cleaned dataframe as grouped by tier. When taking the average of the game statistics, there are discreptancies across tier level. While columns like `'kda'` seems to inc as tier level inc, the other columns in this table don't seem to have a clear relationship to tier.

| tier   |   gamelength |   kills |   deaths |   assists |     dpm |   earnedgold |      kda |
|:-------|-------------:|--------:|---------:|----------:|--------:|-------------:|---------:|
| A      |      1887.57 | 3.13511 |  3.14182 |   7.12248 | 512.852 |      7524.01 | 0.209174 |
| T1     |      1944.51 | 2.59009 |  2.59498 |   6.23349 | 477.543 |      7710.29 | 7.18998  |
| T2     |      1872.34 | 2.91205 |  2.91894 |   6.7142  | 514.77  |      7484.73 | 2.9989   |
| T3     |      1923.57 | 2.98807 |  2.9936  |   7.1064  | 493.924 |      7649.48 | 0.267264 |

## Assessment of Missingness
### NMAR Analysis
I believe that `'killsat25'`, `'assistsat25'`, `'deathssat25'`, `'opp_killsat25'`, `'opp_assistsat25'`, and `'opp_deathsat25'` are NMAR as it doesn't seem to be correlated with any other columns/ no specific missingness trends (even alongside columns like game length and game completion). I theorize that if a game doesn't reach that 25 time mark, there wouldn't be any kills, deaths, and assists statistics to record for a given team. A way to make it MAR would be to add a variable (post-game status) in which it could provide a proportional metric ([40,60]) to measure how far a team was close to winning a game based on tower damage, inhibitor damge, turret damage, etc.

### Missingness Dependency
This section will focus on testing if the missingness of the `'monsterkillsownjungle'` column is dependent on other columns. The two other columns used were `'league'` and `'minionkills'`. For `'league'`, total variation distance (TVD) was used as the test statistic, while for `'minionkills'` the KS statistic was used. Both permutation tests performed were tested at the 0.05 significance level.

First analysis compared `'monsterkillsownjungle'` and `'league'`, and I sought to determine that the missingness of `'monsterkillsownjungle'` values depends on league. The hypotheses tested were as follows:

**Null Hypothesis**: the distribution of `'league'` when `'monsterkillsownjungle'` is missing is the same as the distribution of league when `'monsterkillsownjungle'` is not missing.

**Alt Hypothesis**: the distribution of `'league'` when `'monsterkillsownjungle'` is missing is NOT the same as the distribution of league when `'monsterkillsownjungle'` is not missing.

The table displays the distribution of `'league'` when `'monsterkillsownjungle'` is missing vs not missing.

| league          |   mkills_missing = True |   mkills_missing = False |
|:----------------|------------------------:|-------------------------:|
| AC              |              0.00416023 |               0          |
| AL              |              0.0181861  |               0          |
| CBLOL           |              0.0312611  |               0          |
| CBLOLA          |              0.0328064  |               0          |
| CDF             |              0.00820159 |               0          |
| CT              |              0.00463568 |               0          |
| DCup            |              0          |               0.0129403  |
| EBL             |              0.0168786  |               0          |
| EBLPA           |              0.00297159 |               0          |
| EM              |              0.0474266  |               0          |
| EPL             |              0.0178295  |               0          |
| ESLOL           |              0.0345893  |               0          |
| EWC             |              0.00225841 |               0          |
| GLL             |              0.0181861  |               0          |
| GLLPA           |              0.00451682 |               0          |
| HC              |              0.0131939  |               0          |
| HM              |              0.0184239  |               0          |
| HW              |              0.00998455 |               0          |
| IC              |              0.00808273 |               0          |
| KeSPA           |              0.00582432 |               0          |
| LAS             |              0.0343516  |               0          |
| LCK             |              0.0572923  |               0          |
| LCKC            |              0.0607393  |               0          |
| LCO             |              0.0185427  |               0          |
| LCS             |              0.0228218  |               0          |
| LDL             |              0          |               0.406183   |
| LEC             |              0.0349459  |               0          |
| LFL             |              0.0281707  |               0          |
| LFL2            |              0.0204446  |               0          |
| LIT             |              0.0177107  |               0          |
| LJL             |              0.0175918  |               0          |
| LLA             |              0.025318   |               0          |
| LPL             |              0          |               0.515457   |
| LPLOL           |              0.018305   |               0          |
| LRN             |              0.0108166  |               0          |
| LRS             |              0.0121241  |               0          |
| LVP SL          |              0.028765   |               0          |
| MSI             |              0          |               0.0560748  |
| NACL            |              0.0580055  |               0          |
| NEXO            |              0.019137   |               0          |
| NLC             |              0.0247236  |               0          |
| NLC Aurora Open |              0.0091525  |               0          |
| PCS             |              0.0353025  |               0          |
| PRM             |              0.0286461  |               0          |
| PRMP            |              0.0159277  |               0          |
| TCL             |              0.0215143  |               0          |
| TSC             |              0.0127184  |               0          |
| UL              |              0.0188993  |               0          |
| USP             |              0.00451682 |               0          |
| VCS             |              0.0299536  |               0          |
| WLDs            |              0.0141448  |               0.00934579 |

After performing a permutation test calculating the TVD, the observed test statistic is **0.9906542056074766**, with a p-value of 0. The following plot shows the empirical distribution of the TVD for the test.

<iframe
  src="assets/q3aplot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Since the p-value is less than the 0.05 significance level we reject the null hypothesis. This means that `'monsterkillsownjungle'` depends on `'league'`.

The second analysis compared `'monsterkillsownjungle'` and `'minionkills'`, and I sought to determine that the missingness of `'monsterkillsownjungle'` values doesn't depend on `'minionkills'`. The hypotheses tested were as follows:

**Null Hypothesis**: the distribution of `'minionkills'` when `'monsterkillsownjungle'` is missing is the same as the distribution of league when `'monsterkillsownjungle'` is not missing.

**Alt Hypothesis**: the distribution of `'league'` when `'monsterkillsownjungle'` is missing is NOT the same as the distribution of league when `'monsterkillsownjungle'` is not missing.

After performing a permutation test calculating the KS statistic, the observed test statistic is **0.041330767154286824**, with a p-value of 1. The following plot shows the empirical distribution of the KS Statistic for the test.

<iframe
  src="assets/q3bplot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Since the p-value is greater than the 0.05 significance level we fail to reject the null hypothesis. This means that `'monsterkillsownjungle'` doesn't depend on `'earnedgold'`.

## Hypothesis Testing
In this section, I focused on analyzing the KDA statistic itself across tiers, and whether there is a correlation between the tier level and KDA. This hypothesis was fueled by a common assumption across levels within both sports and esports: *as tier level increases, the disparities between team performance decrease as teams are more closer to each other in terms of skill level and performance*. Testing the KDA statistic with a hypothesis test will reveal whether this assumption holds true, and if tier level is a good indicator of overall team performance and skill level.

**Null Hypothesis**: The difference in average normalized KDA for the best performing and worst performing teams within a given league tier does not decrease as league tier increases.

**Alt Hypothesis**: The difference in average normalized KDA for the best performing and worst performing teams within a given league tier decreases as league tier increases.

I analyzed this at the 0.05 significance level, and to measure correlation, the Spearman R statistic was used as the test statistic. To be able to measure the increase/decrease of league tier, the `'tier'` column was modified through an ordinal encoding function that assigned the following values to each tier: 

| **Tier**      | **Assigned Value** |
| ----------- | ----------- |
| A      | 1      |
| T3      | 2     |
| T2      | 3      |
| T1      | 4      |

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
