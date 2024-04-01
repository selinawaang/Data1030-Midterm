# Data1030 Final Project: Injury Prediction for Distance Running Athletes

## Project overview:

The goal of this project is to predict whether an athlete will get injured on a given day based on their recent training history. This is a classification problem with the target variable being a binary variable indicating injury or no injury. The motivation behind this project is that sports teams want to prevent injury of their athletes, so it will be useful to know which factors contribute to injury, and signal athletes to take precautions to prevent injury.

I trained 4 different models: Logistic Regression, Random Forest Classifier, SVC and KNN. The most predictive model is Logistic Regression, which gives a mean F_2 score of 0.506 (0.5 standard deviations avobe baseline). 

The three biggest challenges I faced while working on this project were working with imbalanced data, dealing with overfitting, and setting up train-val-test sets for a time-series data.

Below is an overview of my procedure and key considerations. Please refer to the [final project report](https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/tree/main/report), and the [code file](https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/blob/main/src/running%20injury%20prediction%20one%20athlete.ipynb) for more details.

- **EDA:**
  - Choosing one athlete to predict: I examined the distributions of feature variables and picked the athlete with the highest fraction of injury out of all events attended to be the athlete my model is trained for. I decided to train a model for only one athlete because not only is my data a time-series, each athlete has a different distribution of training record data so combining these will violate the iid assumption.
- **Feature engineering:** The features contain training data for the past 7 days. I added the average and maximum values for the past 7 days as additional features to the dataset. Minimum values over the last 7 days are 0 for all features, so those were not included in the dataset. I also added a lag feature of the target variable, this feature indicates whether the athlete was injured on the previous event day.
- **Splitting:** I split the data into training-validation-test sets in chronological order, and performed this splitting in 6 folds so I can test the model performance on different test sets to account for uncertainty. Please see report for more details on splitting.
- **Preprocessing:** I used the standard scalar for all the variables because they can all be treated as continuous variables, and most of them do not have a clear upper bound and have a long tail. The lag of the target variable was also transformed using the standard scalar to make it easier to interpret the coefficients of my linear model.
- **Evaluation metric:** I chose the F_2 score as my evaluation metric because my dataset is highly imbalanced, and also I would like to capture a large proportion of the conditional positive samples.
- **Training Pipeline:** For each algorithm, we trained the model on the training set, used the validation set to choose the est set of hyperparameters, and then predicted on the test set to calculate the test F_2 score. I repeat this process 6 times for each algorithm, giving 6 F_2 scores on 6 different test sets.
- **Results**: Below are the results for each algorithm. I chose logistic regression as my final model, but in hindsight I would have chosen random forest because it has significantly lower standard deviation meaning that its performance is more constant across different testing periods.
<img alt="image" src="https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/assets/80374850/e6c0b131-1076-435d-8acf-b04fece9872c">

- **Model Interpretation and Feature Importance:**
    - **Global feature importance:** Global feature importance was calculated in three ways: permutation importance, size of the coefficients, and SHAP global importance. In each of these calculations, the lag feature of the target variable was consistently ranked as the most important feature, and its importance is significantly larger than other features, meaning that the model relied most heavily on whether the athlete was injured during the previous event day to predict whether the athlete is injured on a given day. This makes sense as many of the class 1 (injury class) points in the dataset occur on consecutive event days. The one feature that was surprising was ‘perceived recovery’ which has high importance but a positive coefficient, which means that the model is more likely to predict injury if the athlete’s own perception of recovery is high. This suggests that perhaps the coach should not use the athlete’s own judgement of recovery as an indication of whether they will be injured.

      <img width="291" alt="image" src="https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/assets/80374850/e7e31445-b537-430d-9e38-044298218719">
      <img width="428" alt="image" src="https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/assets/80374850/3a8ac018-d257-415e-9220-1381e2776c18">
  - **Local feature importance:** I examined 4 different datapoints (indexed 0, 1, 8 and 14) in the test set for local feature importance using SHAP values, two of which are displayed below.
      - Observation 0 is a true positive and an injury was present on the previous event day, so not surprisingly the lag feature of the target variable that is pushing this datapoint towards being in class 1.<img width="468" alt="image" src="https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/assets/80374850/f8729620-273d-45a4-a9fd-81b89835c743">
      - Observation 1 was a false positive, and the prediction for this point was also largely due to the lag of the feature variable. From this observation we can see that the model seems to rely too much on the lag feature, which leads to misclassifying points into class 1 when they are preceded by an event day with injury.<img width="468" alt="image" src="https://github.com/selinawaang/Injury-Prediction-for-Distance-Running-Athletes/assets/80374850/d06d641f-192f-45b7-8e08-0aa38bdb1a34">


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

