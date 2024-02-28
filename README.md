# Data1030 Final Project: Injury Prediction for Distance Running Athletes

## Project overview:

The goal of this project is to predict whether an athlete will get injured on a given day based on their recent training history. This is a classification problem with the target variable being a binary variable indicating injury or no injury. The motivation behind this project is that sports teams want to prevent injury of their athletes, so it will be useful to know which factors contribute to injury, and signal athletes to take precautions to prevent injury.

I trained 4 different models: Logistic Regression, Random Forest Classifier, SVC and KNN. The most predictive model is Logistic Regression, which gives a mean F_2 score of 0.506 (0.5 standard deviations avobe baseline).

Below is an overview of my procedure and key considerations. Please refer to the [final project report](https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/tree/main/report), and the [code file](https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/blob/main/src/running%20injury%20prediction%20one%20athlete.ipynb) for more details.

- **EDA:**
  - Choosing one athlete to predict: I examined the distributions of feature variables and picked the athlete with the highest fraction of injury out of all events attended to be the athlete my model is trained for. I decided to train a model for only one athlete because not only is my data a time-series, each athlete has a different distribution of training record data so combining these will violate the iid assumption.
- **Feature engineering:** The features contain training data for the past 7 days. I added the average and maximum values for the past 7 days as additional features to the dataset. Minimum values over the last 7 days are 0 for all features, so those were not included in the dataset. I also added a lag feature of the target variable, this feature indicates whether the athlete was injured on the previous event day.
- **Splittiing:** I split the data into training-validation-test sets in chronological order, and performed this splitting in 6 folds so I can test the model performance on different test sets to account for uncertainty. Please see report for more details on splitting.
- **Preprocessing:** I used the standard scalar for all the variables because they can all be treated as continuous variables, and most of them do not have a clear upper bound and have a long tail. The lag of the target variable was also transformed using the standard scalar to make it easier to interpret the coefficients of my linear model.
- **Evaluation metric:** I chose the F_2 score as my evaluation metric because my dataset is highly imbalanced, and also I would like to capture a large proportion of the conditional positive samples.
- **Training Pipeline**: For each algorithm, 
- **Results**:




## Python and Package Versions:
Python version 3.10.5\
numpy version 1.22.4\
matplotlib version 3.5.2\
sklearn version 1.1.1\
pandas version 1.4.2\
xgboost version 1.5.1\
shap version 0.40.0

Please refer to the [yaml file](data1030.yml)


## License:
Please refer to the [license file](LICENSE.md)

