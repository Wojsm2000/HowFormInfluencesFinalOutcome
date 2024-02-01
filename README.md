# HOW FORM INFLUENCES FINAL OUTCOME 
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
First step of every data-related project is obtaining required data. All neccessary information such as: team participating in a certain match, score and date were webscrapped from http://www.90minut.pl/liga/1/liga12330.html using Beautiful Soup package.

## Ideas for linking sports performance to team form 
