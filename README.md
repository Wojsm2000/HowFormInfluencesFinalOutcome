# How form may inflence final outcome? 
The idea for this project emerged after the conclusion of the Ekstraklasa (Polish top-tier football league) in the 2022/23 season. In those competition, several teams had a similar pattern throughout the season, with one part of their season performance being very good and the other quite poor. This situation affected teams such as Widzew Łódź, Piast Gliwice, Korona Kielce, Górnik Zabrze and Wisła Płock. In the case of the latter, a disastrous second part of the season resulted in relegation from the league despite the fact that the team had been the leader for the first 9 rounds. Polish Ekstraklasa teams are requried to obtain more points per game to avoid relegation than top 5 european league teams.

## How many points per game need team to avoid relegation?
|Season|Premier League|La Liga|Ligue 1|Seria A|Bundesliga|Ekstraklasa|
| :-------------: |:-------------:| :-----:|:-----:|:------:|:----:|:----:|
| 2022/23      |0.89|1.07|0.94     |    0.81 |1.00     |    1.11 |
| 2021/22      |0.94|1.02|0.86     |    0.81 |0.97     |    0.97 |
| 2020/21      |0.76|0.92|1.07     |    0.89 |1.00      |    0.86 (1.00)|
| 2019/20      |0.92|0.97|0.85      |    0.94 |0.94      |   1.1|
| 2018/19      |0.92|1.00|0.92      |    1.00 |0.85     |    1.1 |
| Mean      |0.89|0.99|0.93      |    0.89 |0.95     |    1.03 (1.06) |

Note: In 2020/21 Ekstraklasa season only 1 instead of 2, teams were relegated due to expension of league from 16 to 18 teams in season 2021/22. 
The number of points that would be needed if two teams were relegated is given in brackets.

## Data
First step of every data-related project is obtaining required data. All neccessary information such as: team participating in a certain match, score and date were webscrapped from http://www.90minut.pl/liga/1/liga12330.html using Beautiful Soup library.

##  Standard way to score a football match
The standard scoring system in football matches typically follows the structure:

Win: 3 points for the winning team

Draw: 1 point for each team

Loss: 0 points for the losing team

## Idea to involve form of teams into scoring system
The idea for this project appeared when I have read an online article. Unfortunately I was not able to find it now (as of 5.02.2024, if I come across it, it will be linked here). Article dealt with the small differences between the relegated teams from the Polish Ekstraklasa and the teams that took the last safe places. Moreover there was shown that in comparison to top 5 leagues, Polish Ekstraklasa is exceptionally hard for lower tier teams which usually fight to avoid relegation. This exceptional difficulty comes from high amount of points needed to avoid relegation. Team, on average, needs over 1 point per game to avoid relegation.

Knowing the above correlations, it is easy to conclude that the outcome of a single match can have a major impact on the final result of certain team. If only one match can have huge impact there is always question about how luck influences the result.

Obviously it is nearly impossible to estimate influence of luck in just one single match. One fortuitous on-field event can decide the number of points scored by a team in a match. This can confuse the less attentive spectator as to the quality of a team's play in a particular match. On the other hand, if a team regularly performs poorly it may mean that either the quality of individual players is unsatisfactory or the coach's way of playing is not working.         
What if the coach makes changes to the formation and team's form improves, or puts in substitiute players and they bring more quality to the game? What if current coach gets fired and under rule of new menager team performs much better? What if the team we were playing against just happens to be in a few game crisis       or, conversely, is on an upswing. What if there is a team in the league that just happens to always play against teams which are in poor or good form at that time? They may find themselves much higher or much lower in final league table in relation to their real abilities. 

That is why I wanted check if including form of every team into scoring system will change final results.

## Rulebook 
To check how form may change final outcome, I decided to follow couple of diffrent strategies:

### First set of regulations

First idea assumes that first four matches of new season and four first matches after winter break are scored as usual.
Then for each team participating in a game, we calculate how well they performed in last 4 matches. Then the final amount of points for a particular game for each team is calculated as:

Final score = Standard points + Accumulated points from rival

where:
Accumulated points from rival are calculated as sum of form index from four last matches.
Let us take a closer look how does it look in practice:
![image](https://github.com/Wojsm2000/HowFormInfluencesFinalOutcome/assets/95697097/cb8d656c-5f33-4fcb-8b26-a5f5e62c48d6)

We would like to calculate form of each teams prior to that particular match because we can get the standard points with ease.
In that particular situation 3 points go to Widzew Łódź and 0 to Wisła Płock.
Next we have to take a look at last 4 matches of each team.
Wisła Płock recorded:

![image](https://github.com/Wojsm2000/HowFormInfluencesFinalOutcome/assets/95697097/058e93c1-24aa-4cf6-bc6d-d63a6b683c23)

3 wins and 1 draw. 

Widzew Łódź recorded:

![image](https://github.com/Wojsm2000/HowFormInfluencesFinalOutcome/assets/95697097/489c14f1-2bea-4413-8a61-67bafad45b34)

1 win, 1 draw and 2 defeats.

For each win in this set of regulations I decided to give each team 0.25 points for win, 0 for draw and -0.25 for defeat.

In this case final score for each team is as follows:

Widzew Łódź: 3 points from win + (0+0.25+0.25+0.25) from index form of a rival = 3.75

Wisła Płock: 0 points from deafeat + (0.25+0-0.25-0.25) from index form of a rival = -0.25
 
This algorithm is applied to all matches in the season (apart from first 4 matches of the season and 4 first games after winter break for each team).

#### Final table and conclusions 

