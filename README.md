# How form may inflence final outcome? 
The idea for this project was born after the end of the 2022/23 season of the Ekstraklasa (Polish Premier League). In that competition, several teams had a similar pattern throughout the season, with one part of the season being very good and the other quite poor. This situation affected teams such as Widzew Łódź, Piast Gliwice, Korona Kielce, Górnik Zabrze and Wisła Płock. In the case of the latter, a disastrous second half of the season saw them relegated from the league despite leading the table for the first 9 rounds. Polish Ekstraklasa teams have to score more points per game to avoid relegation than the top 5 teams in the European leagues.

## How many points per game need team to avoid relegation?
|Season|Premier League|La Liga|Ligue 1|Seria A|Bundesliga|Ekstraklasa|
| :-------------: |:-------------:| :-----:|:-----:|:------:|:----:|:----:|
| 2022/23      |0.89|1.07|0.94     |    0.81 |1.00     |    1.11 |
| 2021/22      |0.94|1.02|0.86     |    0.81 |0.97     |    0.97 |
| 2020/21      |0.76|0.92|1.07     |    0.89 |1.00      |    0.86 (1.00)|
| 2019/20      |0.92|0.97|0.85      |    0.94 |0.94      |   1.1|
| 2018/19      |0.92|1.00|0.92      |    1.00 |0.85     |    1.1 |
| Mean      |0.89|0.99|0.93      |    0.89 |0.95     |    1.03 (1.06) |

Note: In the 2020/21 Ekstraklasa season only 1 instead of 2 teams were relegated due to the expansion of the league from 16 to 18 teams in the 2021/22 season. 
The number of points needed for two relegations is given in brackets.

## Data
The first step in any data-related project is to get the data you need. All the necessary information, such as the team playing in a particular match, the score and the date, was web-scraped from http://www.90minut.pl/liga/1/liga12330.html using the Beautiful Soup library.

##  Standard way to score a football match
The standard scoring system in football matches typically follows the structure:

Win: 3 points for the winning team

Draw: 1 point for each team

Loss: 0 points for the losing team

## Idea to involve form of teams into scoring system
The idea for this project came to me when I read an online article. Unfortunately, I have not been able to find it now (as of 5.02.2024, if I come across it, it will be linked here). The article was about the small differences between the relegated teams from the Polish Ekstraklasa and the teams that took the last safe places. It was also shown that in comparison to the top 5 leagues, the Polish Ekstraklasa is exceptionally difficult for the lower league teams, which usually fight to avoid relegation. This exceptional difficulty is due to the high number of points needed to avoid relegation. On average, a team needs more than 1 point per match to avoid relegation.

Knowing the above correlations, it is easy to conclude that the outcome of a single match can have a huge impact on a team's final result. If a single match can have a huge impact, then the question arises as to how luck affects the result.

Of course, it is almost impossible to estimate the influence of luck in a single match. A random event on the pitch can determine the number of points a team scores in a match. This can confuse the less attentive spectator as to the quality of a team's play in a particular match. On the other hand, if a team is performing poorly on a regular basis, it may mean that either the quality of individual players is unsatisfactory, or the coach's style of play is not working.         
What if the manager changes the formation and the team's form improves, or brings in substitutes and they bring more quality to the game? What if the current manager is sacked and the team performs much better under the new manager? What if the team we are playing against happens to be in crisis or on the up? What if there is a team in the league that happens to always play teams that are in bad or good form? They could find themselves much higher or much lower in the final league table in relation to their actual ability. 

This is why I wanted to see if the inclusion of each team's form in the scoring system would have any effect on the final results.

## Rulebook 
To check how form may change final outcome, I decided to follow couple of diffrent strategies:

### Set of regulations

Idea assumes that first four matches of new season and four first matches after winter break are scored as usual.
Then for each team participating in a game, we calculate how well they performed in last 4 matches. Then the final amount of points for a particular game for each team is calculated as:

Final score = Standard points + Accumulated points of rival's index form

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

There is also one important disclamer. Team is not allowed to get points from defeat. That situation could arise when, despiate being defeated, team X played team Y which had positive value of index form from 4 last matches. 

#### Final table and conclusions 
Ekstraklasa 2022/23 official final standings:

![image](https://github.com/Wojsm2000/HowFormInfluencesFinalOutcome/assets/95697097/133ce8f6-351a-4ec6-9aa9-2860e66726f5)

Ekstraklasa 2022/23 standings according to presented algorithm:

![image](https://github.com/Wojsm2000/HowFormInfluencesFinalOutcome/assets/95697097/45209715-60a1-45fc-a2e8-7b7dfafc65b8)

What is suprising only 2 out of 18 teams received less points in official table than in algorithm table. Both of these teams are top tier clubs in Polish Ekstraklasa: Pogoń Szczecin and Legia Warszawa. The biggest difference between official and algorithm score comes form Jagielonia Białystok. Jagielonia reached 41 points in official table and only 36 in algorithm table. 

There are two important diffrences between these two final standings. 

Lech Poznań(3.) and Pogoń Szczecin(4.) swapped places in the unofficial table. I don not feel need to explain why finishg fourth, especially when one is close to the third place, is worst feeling for any sport team/athlete. 

The most important switch came in relegation zone. According to algorithm table the 16th place should have been occupied by Śląsk Wrocław contrary to official table where Wisła Płock finished 16th and was relegated from top Polish division.

![image](https://github.com/Wojsm2000/HowFormInfluencesFinalOutcome/assets/95697097/3ce93b52-bcea-498c-8fdf-c98a0852d3d9)

In above shown Figure we can clearly see that Pogoń Szczecin has highest Accumulated Rival Points score. It means that, suming up all teams form points that certain team played against, team from Szczecin played against teams in the best form overall. On the other hand Raków Częstochowa (2022/23 champions) happend to play against teams when their were in worst from overall. 
