# Udacity-Data-Scientist-Capstone-Sparkify
## Welcome to my Capstone in python
### [Medium](https://ebenite2.medium.com/utilizing-k-means-clustering-to-determine-churn-rates-of-music-subscription-users-in-pyspark-ed0ebbf70991)

There are two jupyter notebooks to satisfy the requirements of this capstone project.  As the data is extremely large for a local instance, and my IBM cluster utilized all lite instances; I had to split the notebooks into two.  The first notebook is merely an exploratory phase, to understand the data, and to gain insights for how to compute the purpose of churn rates.  While the notebooks are related and utilize the same dataset, the library requirements do differ slightly.  Due to professional considerations, the dataset, and vectorized model data will not be published to github.

Libraries required:

* os, sys, requests
* pandas, numpy
* plotly, matplotlib
* pyspark

Motivation for the captsone outside the realm of completing the project requirements include, a lifelong desire to merge mathematics, and computer science in an applicable, and industrious way.  As technology has taken hold, it is machine learning which seems to satisfy this niche pursuit in a more than satisfactory way.

Github project consists of the following,
    
    jupyter notebook -- sparkify_capstone.ipynb:
    -----------------------------------------------
         * The jupyter notebook of python code used in numerical calcualtions.
         
    jupyter notebook -- exploratory analysis.ipynb:
    -----------------------------------------------
         * The jupyter notebook utilized for exploratory analysis.
 
    markdown -- README.md:
    ----------------------
         This markdown holds various information on the github repository.  My basic solution of the initial dataset were threefold,
            1.  Pysparks Machine Learning API requires vectorization
            2.  The data sets contains non numerical values, given this and the large data size, Pipeline is:
                    * StringIndexer => VectorAssembler => StandardScaler => ChiSqSelector => kMeans 
            
Reflection:
    The main difficulties in compiling this experiment and analysis was the computing resources required to implement the pyspark ML libraries.  We did utilize the IBM computing cloud, yet were limited to the free tier, and a monthly aggregation of instance hours.  Initially we tried to comput the analysis locally, yet had not the forethought to break the data set into a much smaller and manageable size.  Once, the data was broken into around 50 users, the local instances computed rather quickly and allowed for more breathing room when compiling the entire data set within the IBM cloud.  Another difficulty was the inability to apply the ParamGridBuilder either locally, or from within the IBM cloud.  Multiple questions were posed to the Mentor Udacity Resource, without an appropriate response.  Rather, I circumvented this scenario by implementing each parameter individually, and attaching the results to a list which was used to compare the hyper parameter improvements, or "lack thereof".
    
Improvement:
    There are several features which could be included to improve the current implementation.  The first of which would be to implement the regression withing the pyspark pipeline, as opposed to its current graphical solution utilized by the Pandas library.  Basing additional regression tests on multiple  sub section metrics of the data, might also implement improvement to the analysis, while simultaneously dealing with the issue, and current reasoning that each metric is based on a point in time.  A particular users' session Id, identifies their current play listing, and subscription status, and for essence we calculate the specific cluster they might inherit, at that point in time, and utilize a regression metric to identify that groups future subscription likleyhood.  Also, perhaps the paramGridBuilder could be further explored to improve the hyper parameter tuning, in a more advanced ml pipeline.  
    We might also consider a more accurate, data checking tests.  As opposed to just comparing the cluster prediction with the current 2-dimensional system of paid, and free users.  The data might be broken up, again as paid and free, yet also split the timeseries data into two sections, with just a single session ID, left to verify the results of the predefined analysis.
