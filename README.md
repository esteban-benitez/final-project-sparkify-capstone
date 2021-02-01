# Udacity-Data-Scientist-Capstone-Sparkify
## Welcome to my Capstone in python
### [Medium](https://ebenite2.medium.com/utilizing-k-means-clustering-to-determine-churn-rates-of-music-subscription-users-in-pyspark-ed0ebbf70991)

There are two jupyter notebooks to satisfy the requirements of this capstone project.  As the data is extremely large for a local instance, and my IBM cluster utilized all lite instances; I had to split the notebooks into two.  The first notebook is merely an exploratory phase, to understand the data, and to gain insights for how to compute the purpose of churn rates.  While the notebooks are related and utilize the same dataset, the library requirements do differ slightly.  Due to professional considerations, the dataset, and vectorized model data will not be published to github.

#### Libraries required:

* pyspark.sql: SparkSession, functions.col, functions as F, min, max, count, array
* pyspark.ml: 
    Pipeline, regression.GeneralizedLinearRegression, feature.VectorAssembler, StringIndexer
    clustering.KMeans, evaluation.RegressionEvaluator, MultiClassificaitonEvaluator, ClusteringEvaluator
    Tuning.CrossValidator, ParamGridBuilder
* pandas, numpy
* plotly, matplotlib

##### Motivation:

Motivation for the captsone outside the realm of completing the project requirements include, a lifelong desire to merge mathematics, and computer science in an applicable, and industrious way.  As technology has taken hold, it is machine learning which seems to satisfy this niche pursuit in a more than satisfactory way.  The general pursuit of the Sparkify project is to determine marketing campaigns in specific customer targeting scenarios at point in time, such that customer's grouped based on their subscription type, might improve the companies bottom line.  We aim to predict the customer's subscription status, in order to increase, or maintain the number of paid subscriptions.

#### Github project consists of the following,
    
    jupyter notebook -- sparkify_capstone.ipynb:
    -----------------------------------------------
         * The jupyter notebook of python code used in numerical calcualtions.  Here we apply the kmeans clustering algorithm, after which is applied we break the
         groups out on their respective prediction cluster, and separate the free from the paid users.  The GeneralizedLinearRegression is then applied to each of 3
         clusters between the paid and the freed, with the necessary root mean squared error used to judge the accuracy of the GLM Model, and specified hyper
         tuning.
         
    jupyter notebook -- exploratory analysis.ipynb:
    -----------------------------------------------
         * The jupyter notebook utilized for exploratory analysis.  Plot out the visualization based on length of sessions between the paid and free users.  As such
         we look for visual discrepencies between normality, and non parametric methods.  We also utilize the correlations between to justify that each metric can 
         a quanititative effect on the level index.
 
    markdown -- README.md:
    ----------------------
         This markdown holds various information on the github repository.  My basic solution of the initial dataset were threefold,
            1.  Pysparks Machine Learning API requires vectorization
            2.  The data sets contains non numerical values, given this and the large data size, Pipeline is:
                    * StringIndexer => VectorAssembler => kMeans 
            3.  Filter data set based on clustering prediction
                    * VectorAssembler => GeneralizedLinearRegression
                    
                    
#### Summary of Results:
We processed 543705 rows of data and when broken into three k = 3 clusters, the evaluation accuracy is only 54%, which should be expected, given that the data contains only two groups, “paid”, and “free”. When evaluated with only 2 clustering groups, k = 2 we achieve a 27% accuracy rating, which is indicative of proper clustering placements. The clustering evaluator for k = 3, provides a score of -0.07212799045115308, for k = 2, 0.015491645537876866.

    Free Users:
    -----------
    Cluster 0 has a slope of -2.530473632235824e-10 indicating: 
         These users will stay
    Cluster 1 has a slope of -3.179434015818414e-10 indicating: 
         these users might downgrade
    Cluster 2 has a slope of -7.591706795140503e-10 indicating: 
         these might leave altogether
    Paid Users:
    -----------
    Cluster 0 has a slope of -1.9949623791887178e-10 indicating: 
         these users might upgrade
    Cluster 1 has a slope of -2.493610749731137e-10 indicating: 
         these will continue free service
    Cluster 2 has a slope of -5.059036390144245e-10 indicating: 
         these users probably leave the service altogether

The model is evaluated for it's accuracy of predicting the regression based analysis of predicting the length of each user's session, utilizing the root mean squared error, such that the smaller value indicates higher accuracy of the model.  The hyper parameter tuning was conducted on Gaussian, and Gamma distributions.

    Free:
               Gaussian           Gamma
    Cluster 0: 97.32010175753923  97.32234392541109
    Cluster 1: 93.11747843700327  93.10982280439835
    Cluster 2: 116.64181787949359 116.60559496512755
    --------------------------------------------------------------------Paid:
               Gaussian           Gamma
    Cluster 0: 95.14288236629696  95.14288234267099
    Cluster 1: 94.02797858398525  94.02797495408264
    Cluster 2: 115.00386573617652 115.00460904112288
    
To quantify the accuracy of the multiclass model where the user can either downgrade, upgrade, or drop service completely, is only interrogated based on two metrics for their level of subscription, free, and paid.  When evaluated with only 2 clustering groups, k = 2 we achieve a 27% accuracy rating, which is indicative of proper clustering placements. The clustering evaluator for k = 3, provides a score of -0.07212799045115308, for k = 2, 0.015491645537876866.


#### Reflection:
   
The main difficulties in compiling this experiment and analysis was the computing resources required to implement the pyspark ML libraries.  We did utilize the IBM computing cloud, yet were limited to the free tier, and a monthly aggregation of instance hours.  Initially we tried to comput the analysis locally, yet had not the forethought to break the data set into a much smaller and manageable size.  Once, the data was broken into around 50 users, the local instances computed rather quickly and allowed for more breathing room when compiling the entire data set within the IBM cloud.  Another difficulty was the inability to apply the ParamGridBuilder either locally, or from within the IBM cloud.  Multiple questions were posed to the Mentor Udacity Resource, without an appropriate response.  Rather, I circumvented this scenario by implementing each parameter individually, and attaching the results to a list which was used to compare the hyper parameter improvements, or "lack thereof".
    
#### Improvement:

There are several features which could be included to improve the current implementation.  The first of which would be to implement the regression withing the pyspark pipeline, as opposed to its current graphical solution utilized by the Pandas library.  Basing additional regression tests on multiple  sub section metrics of the data, might also implement improvement to the analysis, while simultaneously dealing with the issue, and current reasoning that each metric is based on a point in time.  A particular users' session Id, identifies their current play listing, and subscription status, and for essence we calculate the specific cluster they might inherit, at that point in time, and utilize a regression metric to identify that groups future subscription likleyhood.  Also, perhaps the paramGridBuilder could be further explored to improve the hyper parameter tuning, in a more advanced ml pipeline.  

We might also consider a more accurate, data checking tests.  As opposed to just comparing the cluster prediction with the current 2-dimensional system of paid, and free users.  The data might be broken up, again as paid and free, yet also split the timeseries data into two sections, with just a single session ID, left to verify the results of the predefined analysis.

#### Acknowledgements:

We would like to say thank you to Udacity for the large library of information, and dedicated lessons created to teach the necessary skills to become a Data Scientist.  Also the support, and recomendation to scour blogs, apis, additional documentation, how-tos, etc to supplement your curriculum.  Additional thanks to the project reviewers, and mentors who answered questions swiftly.  In addition to those that came before, we extends thanks to Apache Spark for implementing the distributed system environment and contributing to open source.  We also commend the following authors for their contributions to the science of data:
    
[1] Firdaus, Afrizal. "Bisecting Kmeans Clustering." Medium, Medium, 9 May 2020, medium.com/@afrizalfir/bisecting-kmeans-clustering-5bc17603b8a2.
[2] KAUSHIK, SAURAV. "Clustering: Types Of Clustering: Clustering Applications." Analytics Vidhya, 18 Oct. 2020, www.analyticsvidhya.com/blog/2016/11/an-introduction-to-clustering-and-different-methods-of-clustering/.
[3] Stephanie Glen. "RMSE: Root Mean Square Error" From StatisticsHowTo.com: Elementary Statistics for the rest of us! https://www.statisticshowto.com/probability-and-statistics/regression-analysis/rmse-root-mean-square-error/
[4] Wikipedia contributors. (2021, January 26). Normal distribution. In Wikipedia, The Free Encyclopedia. Retrieved 01:55, February 1, 2021, from https://en.wikipedia.org/w/index.php?title=Normal_distribution&oldid=1002951236
