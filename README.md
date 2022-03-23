<h1> ReadMe </h1>

<h2> Introduction </h2>
This project is my on the capstone project of Udacity's Data Scientist NanoDegree Programme.

The corresponding blog post could be found here https://astraro.github.io/euro2020/.

The goal of this project is to investigate if a machine learning algorithm can help me to perform better in a soccer betting game w.r.t. the UEFA Euro 2020. The betting game took place on the platform www.kicktipp.de and the contestants were my workmates.

In the betting game we have to make two kinds of bets:
<ol>
  <li>Guessing the results of all the games in UEFA Euro 2020. For a correct guess we obtain four points. For a correct goal difference we obtain three points (in case of a draw that is already covered by the correct result), and for a correct tendency we obtain two points. In the knockout-phase the results we have to guess the results after a possible penalty shootout.</li>
  <li> Moreover, there are some bonus points. We have to guess the winners of the six groups, the participants of the semi-finals and the champion of the tournament.</li>
</ol>

This project consists of four parts:
<ol>
  <li>The first part is a <em>crawling</em>-step. In the crawling step we crawl the pages of the UEFA regarding the matches played in the Euro 2020 qualifying, and the UEFA nations leagues 2018/19 and 2020/21. Moreover, we also crawl the matches played in UEFA Euro 2020 to grab the results of the matches played in this tournament. The pages of the UEFA contain statistics about the games played like attempts of each team, completed passes, ball possessions, ...</li>
  <li>The second part is about <em>feature engineering</em>. From the crawling step we know only attemps, completed passes in the games played. We cannot use this features for the prediction, because at the time we have to bet the match did not start. Therefore, we compute rolling (weighted) averages w.r.t. different time spans of the features in the matches played before. Moreover, here is some data exploration contained.</li>
  <li>The third part is about <em>traing the model</em>. We use a simple random forest. The training is done using gridsearch. As parameters for gridsearch we use the depth of the random forest and the different kinds of rolling averages as features.</li>
  <li>The final part is about <em>predicting</em> the matches and <em>evaluating</em> the performance of the model. The prediction of the matches is a bit more complex in this project since we do not have a classification problem, but have to optimize the chosen bet w.r.t. to an objective function. In order to do this, we use the probability distribution for the goals scored by each time given by our model and then choose the result, which maximizes the expected points.
  
  Moreover, to make predictions for the bonus points we have to take a different approach. In order to do this, we make a Monte Carlo simulation of the tournament, where the matches are simulated according to the model.
  </li>
</ol>

<h2> Requirements and Interactions with the Project</h2>
This project is structured into three folders: <em>code</em>, <em>data</em> and <em>models</em>. The folder <em>code</em> contains four notebooks: <em>crawling_data.ipynb</em>, <em>feature_engineering_v2.ipynb</em>, <em>model_building_v2.ipynb</em>, and <em>evaluation_model.ipynb</em>. The folder data contains four Excel files: The files <em>matches_euro_2020.xlsx</em> and <em>matches_training_ml.xlsx</em> stem from the crawling step and contain the results of the Euro 2020 and the matches with the features played before the tournament. In the feature engineering step the Excel files <em>20220323_features_matches_training.xlsx</em> and <em>20220322_features_last_match.xlsx</em> are generated. These files serve as base for training the model and for predicting the matches in Euro 2020. The models generated in the model building step are stored in the folder models. In this project we use the model <em>model.pkl</em>.

The project requires only standard libraries:
<ol>
  <li> The crawling step especially uses <em>requests</em>, and <em>BeautifulSoup</em> to perform the crawling and to parse the data from the HTML code. Moreover, we use                  <em>pandas</em> to store the data and some additional libraries like <em>os</em>, <em>time</em>, <em>json</em> and <em>urllib</em>.</li>
  <li> The feature engineering relies mostly on <em>pandas</em>.</li>
  <li> The model building step is based on <em>sklearn</em> and the model is stored using <em>pickle</em>.</li>
  <li> The model evaluation uses <em>random</em> to simulate the games.</li>
</ol>
