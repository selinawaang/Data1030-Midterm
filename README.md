# Data1030 Final Project: Injury Prediction for Distance Running Athletes

## Project overview:

The goal of this project is to predict whether an athlete will get injured on a given day based on their recent training history. This is a classification problem with the target variable being a binary variable indicating injury or no injury. The motivation behind this project is that sports teams want to prevent injury of their athletes, so it will be useful to know which factors contribute to injury, and signal athletes to take precautions to prevent injury.

The dataset used for this project is the replication data for the research paper "Replication Data for: Injury Prediction in Competitive Runners with Machine Learning" by Lovdal et al. from the Bernoulli Institute of the University of Groningen. It includes time-series data from 74 distance runners recorded over a period of 7 years. In total it has 72 features and 42,766 rows. The feature variables consist of the training log of the past 7 days leading up to the event day.

Because each athlete’s data will theoretically have a different distribution, to simplify this project, I only used data from one athlete to train a model that would predict injury for that single athlete, this gives a total of 730 datapoints.

I trained 4 different models: Logistic Regression, Random Forest Classifier, SVC and KNN. The most predictive model is Logistic Regression, which gives a mean F_2 score of 0.506 (0.5 standard deviations avobe baseline).

## Python and Package Versions:
Python version 3.10.5\
numpy version 1.22.4\
matplotlib version 3.5.2\
sklearn version 1.1.1\
pandas version 1.4.2\
xgboost version 1.5.1\
shap version 0.40.0

Refer to yaml file


## License:

