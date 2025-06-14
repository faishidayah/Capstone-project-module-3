# Capstone project module 3


## Business Problem Understanding
### 1. Background
California is one of the most dynamic and exciting real estate markets in the world. California has the largest economy in the United States and is one of the strongest economies in the world. Some of the key sectors that form the backbone of the California economy are Technology, Agriculture, Entertainment and Media. With over 39 million people, the demand for both residential and commercial properties continues to grow. However, it also faces significant challenges including the combination of high prices, stringent regulations and environmental risks, therefore property pricing requires a well thought out strategy.
### 2. Problem Statement
The company wants to set competitive and attractive property prices in the California market while ensuring optimal profit margins, but also considering buyer appeal.
### 3. Goals
Based on these problems, companies need a tool that can help them predict house prices accurately. Features owned by a house such as the location of the house, the average age of the house, the total number of rooms, the total number of bedrooms and others can increase the accuracy of house price predictions, so that they can provide optimal profits for the company and attractive prices for buyers.
### 4. Analitical Approach
Conducting data analysis to determine the relationship between variables and find patterns of existing features that differentiate one house from another. Then building machine learning that will be a tool used by companies to predict house prices accurately.
### 5. Metrics Evaluation
Evaluation metrics that will be used include the following:
- MAE ==> Average absolute value of error. Gives an idea of ​​how big the average error is in the same unit as the target.
- MAPE ==> Average percentage of absolute error between actual and predicted values. Useful for evaluating model performance at various scales.
- RMSE ==> Square root of Mean Squared Error. Measures the average error with a penalty for large errors.
- 
## Data Understanding
Column Description:
longitude ==> A measure of how far west a house is; higher values ​​mean further west
latitude ==> A measure of how far north a house is; higher values ​​mean further north
housingMedianAge ==> The average age of a house in a block; lower values ​​mean newer buildings
totalRooms ==> The total number of rooms in a block
totalBedrooms ==> The total number of bedrooms in a block
population ==> The total number of people living in a block
households ==> The total number of households, a group of people living in a single housing unit, for a block
medianIncome ==> The median income for households in a block of houses (measured in tens of thousands of US Dollars)
medianHouseValue ==> The median home value for households in a block (measured in US Dollars)
oceanProximity ==> The location of a house in relation to the ocean

## Data Preprocesing
1. Missing value handling
2. Duplicate data
3. Outliers handling
4. feature engineering
adding 3 columns :
- rooms_per_household ==> average rooms per household
- bedrooms_per_room ==> average bedrooms per household
- pop_per_house ==> average population per household
removing columns:
- total_rooms
- total_bedrooms
- population
5. data correlation

## Modelling 
1. One hot encoding ocean_proximity column
2. Data Splitting
- train size ==> 80%
- test size ==> 20%
- random state ==> 42
3. Model selection
The model used is XGBoost because it gets the best score based on benchmarking
4. Tuning
The tuning hyperparameters to be used are:
- max_depth ==> 7
- learning rate ==> 0.1
- n_estimators ==> 188
- subsample ==> 0.9
- gamma ==> 3
- cosample_bytree 0.7
- reg_alpha 0.05994842503189409
5. Comparison of scores before and after tuning:
After tuning, the RMSE, MAE and MAPE scores decreased, which means that the model experienced an increase in performance, although not significant.
- RMSE 42548.726617 ==> 41424.476807 
- MAE 28985.347693 ==> 27738.313086 
- MAPE 0.170032 ==> 0.161551
  
## Conclusion
- based on the modeling that has been done, the features __'ocean_proximity'__ and __'median_income'__ are the features that have the most influence on __'median_house_value'__
- The evaluation metrics used are MAE, MAPE and RMSE. MAE score ==> 27738.31 and MAPE ==> 16.1%, so we can conclude that the average price prediction of the model will miss around 16% or 27738.31 USD from the actual price. The model created is used to predict property/house prices in California but has limitations where the model can only predict __'median_house_value'__ in the range of 14,999 to 480275.0 USD.
- but it is also possible that the model's prediction will miss further from its actual value, either overestimation or underestimation. This is due to the limited features contained in the dataset so that the model only has a little important information that can help explain the target value.
  
## Recommendation
1. for dataset:
- there are only a few features that are highly correlated with the target, therefore it is necessary to add several features such as __building area__, __land area__, __house facilities__, and distance of housing to public facilities (__city center__, __airport__, __mall__ and others)
- this dataset is information from the 1990 California census. to predict current housing prices, more updated data is needed. because the dataset is 34 years old, of course housing prices have been affected by inflation
2. for machine learning models:
- tuning using __GridSearch__ then hyperparameter optimization using __Optuna__ or __Bayesian Optimization__ for a faster and more efficient optimization process
3. for developers:
- for maximum profit, developers need to consider the location of the house construction. the closer the location of the house/property to the sea, the higher the price of the house/property.
