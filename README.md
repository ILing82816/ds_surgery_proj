# Data Science Length of Stay Post-surgery Prediction: Project Overview 
* Created a tool that predicting data science the lenght of stay post-surgery to identify the risk of surgery (Accuray 86%) to help doctors evaluate the risk of surgery in the future.
* Used a real, anonymized dataset provided by UPMC regarding surgical procedures between June 2017 and June 2018.
* Filled missing features by mode or mean value.
* Optimized Logistic Regressor, Random Forest, XGBoost, and LightGBM using Hyperopt to reach the best model.
* Displyed a variable importance using shap.

## Code and Resources Used
**Python Version:** 3.7  
**Packages:** pandas, numpy, sklearn, xgboost, lightgbm, hyperopt, matplotlib, seaborn, pickle, shap   

## Data
The data is already divided into training and test populations:
* Surgery Informations
* Hospital Examing Informations
* Office Visit Examing Informations

## Data Cleaning
I needed to clean it up so that it was usable for our model. I made the following changes and created the following variables:
* Removed rows that someone didn't visit office.
* Removed variables that have over 95% Nan values, and drop the repeat informations
* Filled Nan values by mode or mean
* Add column for the age of people is classed to youmg, mid_age, old, older
* Transformed the lenght of stay post-surgery into long or short stay
* Convert object to numeric data by one-hot encoding.

## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the pivot tables.  
![](https://github.com/ILing82816/ds_surgery_proj/blob/master/Figure/Female.PNG) 
![](https://github.com/ILing82816/ds_surgery_proj/blob/master/Figure/age.PNG) 
![](https://github.com/ILing82816/ds_surgery_proj/blob/master/Figure/area_age.PNG) 

## Model Building
First, I normalized the data. I also split the data into train and validation sets with a validation size of 20%.  
I tried four different models and evaluated them using ROC curve. I chose ROC curve because it is relatively easy to interpret and check overfitting for this type of model.  
I tried four different models:  
* **Logistic Regression** - Baseline for the model
* **Ensemble model (Random Forest, XGBoost, LightGBM)** - Because of the ensemble model improving weak classifiers, I thought Random Forest, XGBoost and LightGBM would be effective.   

## Model performance
The LightGBM model far outperformed the other approaches on the test and validation sets.
* **LightGBM:** Accuracy on train sets = 86%, Accuracy on validation sets = 84%       
![alt text](https://github.com/ILing82816/ds_oil_price_proj/blob/master/Figure/prediction_prophet.png "prophet")   
* **Logistic Regression:** Accuracy on train sets and on validation sets = 74%    
![alt text](https://github.com/ILing82816/ds_oil_price_proj/blob/master/Figure/prediction_linear.png "linear")  
* **Random Forest:** Accuracy on train sets = 81%, Accuracy on validation sets = 79%   
![alt text](https://github.com/ILing82816/ds_oil_price_proj/blob/master/Figure/prediction_LSTM.png "LSTM")
* **XGBoost:** Accuracy on train sets = 87%, Accuracy on validation sets = 83%   
![alt text](https://github.com/ILing82816/ds_oil_price_proj/blob/master/Figure/prediction_LSTM.png "LSTM")

## Productionization
In this step, I built a flask API endpoint that was hosted on a local webserver by following along with the tutorial in the reference section above. The API endpoint takes in a request with the day of prediction and returns a list of estimated WTI Price.
