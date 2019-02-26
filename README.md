# music_box_project
The project of music app platform's churn prediction and music recommendation using spark 
# Introduction
This project used the large and unstructureed dataset of user's behavior history from music platform, then made the classifier of user's churn possibility using current popular machine learning algorithms and used matrix factorization method with PySpark ALS to recommend the most relevant songs according to user's behavior. 
### languages
Python, 
Shell Script, 
Sql
### libraries
PySpark, 
Scikit-learn
### computation
AWS
# Data Set Summary
The original data files which are downloaded from the website is constructed by three types files: play data, download data, search data which are specified by the date from 2017-03-31 - 2017-05-12. 
# Preprocessing and Feature Extraction
Unzipped the original files and integrated them into three files: play, download and search. Extracted the features: 'uid', 'device', 'song_id', 'date' and created a new feature 'event' to figure the three actions of users. Joined the three files into one 'event' file and cleaned the bots and outliers to be used by the user's churn prediction. Downsampled the file, in order to reduce the duration of computation. Created the churn label defined by that there were actions before 2017-04-29 no action after that date. Generated the features by frequency methods during 5 different time windows. 
# Churn prediction
Used three machine learning modules of pyspark to build the model: 'LogisticRegression', 'RandomForestClassifier'and  'GBTClassifier'. Random forest classifier got the highest test AUC score: 0.87. Among the feature importance of three different methods, 'play' behavior and 'search' behavior made much more contributions for user's churn tendency then 'download' behavior. 
# Music Recommender 
The original data doesn't contain explicit users' rating. Through counting the frequency during time windows for 'play', 'search' and 'download', user's implicit rating could be calculated. Since 'play' and 'download' times could reflect the user's interest directly, the weighted summation of these two statistics can be regarded as explicit rating to user. As normal, 'download' action and times of 'play' action reflect the degree of interest, thus, 'download' statistic has larger weight then 'play' statistic. The rating range is from 0 - 5, the rating larger then 5 will be truncated to 5. Trained the ALS of pysark on the training data, then get 1.4 RMSE on test data. Tested several examples, the result is acceptable. 
# Summary
As for churn prediction , 'search' and 'paly' statistics play the important roles; For music recommender, 'download' and times of 'play' statistics determine the explicit rating and ALS do well on this project. 
