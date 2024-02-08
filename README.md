# Q 1

We will preprocess the data and extract the data we want, according to the following sentence:

- **Score lead**. We believe that the difference in scores in the current game will significantly affect the player's mentality and indirectly affect the player's cash flow.

- **Stamina**. In the provided data set, we can measure the player's current physical strength through the distance traveled by the player.
- **Score streak**. We believe that whether consecutive points are scored in a game is also an important factor affecting a player's performance.
- **Mentality**. Losing points due to certain things during the game will affect the performance of the players, thereby indirectly affecting the performance.

Therefore, we will process the original data to obtain the following **evaluation indicators**:

|     evaluation indicators      |      Lable      |
| :----------------------------: | :-------------: |
|           Score lead           |   points_diff   |
| Running distance in this match | total_distance  |
|          Score streak          |  points_streak  |
|         unforced error         |     unf_err     |
|        Whether to serve        |     server      |
|     serve score(untouched)     |   serve_score   |
|      Last round duration       | elapsed_time_td |
|                                |                 |



![image-20240203013357618](C:\Users\40633\AppData\Roaming\Typora\typora-user-images\image-20240203013357618.png)

We comprehensively compared the training results of LGBM, XGBC, SVM, MLP, Logistic Regression, Decision Tree, Random Forest, Naive Bayes and other models.

It was found that the MLP model has the best prediction result, so we choose the MLP model for the 30th game 2023-wimbledon-1701 Make predictions and get performance graphs

# Q 2

A tennis coach is skeptical that “momentum” plays any role in the match. Instead, he postulates that swings in play and runs of success by one player are random. Use your model/metric to assess this claim.

In order to **refute** the coach's hypothesis, we used the **momentum prediction** results in Q1 for the first and game 2023-wimbledon-1301 to conduct **correlation analysis** with the real values, and obtained the following results:



# Q 3

Coaches would love to know if there are indicators that can help determine when the flow of play is about to change from favoring one player to the other.

- Using the data provided for at least one match, develop a model that predicts these swings in the match. What factors seem most related (if any)?
- Given the differential in past match “momentum” swings how do you advise a player going into a new match against a different player? 

Considering that simply using performance to describe momentum is not comprehensive enough, we considered several criteria based on the performance obtained from the Q1 model according to the following feature:

- **last_round_rally_cnt**:We consider this data from the perspective of physical exertion, mental endurance and concentration. The number of hits played by a player in the previous round will affect the player’s physical strength to a certain extent. At the same time, if the number of hits is larger, it will affect mental endurance and concentration. Degree will also have a certain impact

- **double_fault**:We believe that double faults will greatly affect the mentality of the players, so we take them into consideration

- **break_pt_missed**:We believe that losing points at match points will greatly affect a player's performance, so we take this into consideration

# 灵敏度分析

| distance_run         |       |
| -------------------- | ----- |
| elapsed_time         | p<0.7 |
| last_round_rally_cnt | p<0.1 |

