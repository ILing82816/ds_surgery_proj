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
  

## Model Building
First, I normalized the data. I also split the data into train and tests sets with a test size of 20%.  
I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.  
I tried three different models:  
* **Linear Regression** - Baseline for the model
* **Long Short-term Memory (LSTM)** - Because the history of oil price would affect current oil price, I thought a memorable model like long short-term memory would be effective.
* **Prophet** - Again, with the time series data, I thought that this would be a good fit. Also, prophet can predict not only one period but more.   

## Model performance
Depend on the trend of oil price in the future, investors decide the strategies of investment. Although the Linear Regression model far outperformed the other approaches on the test and validation sets, the Prophet model is more practical.
* **Prophet:** MAE = 14.56   
![alt text](https://github.com/ILing82816/ds_oil_price_proj/blob/master/Figure/prediction_prophet.png "prophet")   
* **Linear Regression:** MAE = 0.82  
![alt text](https://github.com/ILing82816/ds_oil_price_proj/blob/master/Figure/prediction_linear.png "linear")  
* **Long Short-term Memory (LSTM):** MAE = 1.08  
![alt text](https://github.com/ILing82816/ds_oil_price_proj/blob/master/Figure/prediction_LSTM.png "LSTM")

## Productionization
In this step, I built a flask API endpoint that was hosted on a local webserver by following along with the tutorial in the reference section above. The API endpoint takes in a request with the day of prediction and returns a list of estimated WTI Price.
