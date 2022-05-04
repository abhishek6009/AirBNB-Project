# AirBNB-Project

This project aims to create a regression model to predict/suggest a price for an AirBNB listing based on various available data. The data used consists of three tables:
- Calendar: Consists of price, availability, etc. of each listing over the course of the entire time period.
- Hosts: Details of each host, like name, date since they have been a host, location of the host, etc.
- Listings: Details of each listing, like latitude, longitude, number of bathrooms, beds, etc.

## Data Pre-Processing Highlights
- The column 'bathrooms_text' had small text snippets to indicate number of bathrooms. These were treated to convert them into appropriate numerical values.
- Missing values were treated in columns 'Bedrooms', 'Beds' and 'Price'.
- Dummy Encoding of categorical variables - 'Room Type' and 'Property Type'.
- Treating Datetime variables by converting them to UNIX timestamps so that they are numerical.

There is a complex treatment of a column 'Amenities' but it is not detailed here as the resulting columns were later removed due to not being useful for predictions. the details of the treatment can be found in the PPT.

## Model Building and Evaluation
After the final version of data has been created, we test a few different models and use the $R^2$ score and RMSE score to compare the models. These are the models, and their respective scores(Model - $R^2$ score - RMSE score):
- Linear Regression - 22.42% - 149.82
- Decision Tree Regressor - 98.64% - 19.82
- Decision Tree Regressor (max_depth of 15, max_features is 'sqrt') - 95.81% - 34.84
- **Random Forest Regressor (200 estimators) - 98.9% - 17.81**
- Random Forest (min_samples_split=100, max_features=‘sqrt’, max_samples=0.7) - 97.26% - 28.14
- AdaBoost Regressor - 5.45% - 165.40
- AdaBoost (base estimator was Decision Tree with max_depth 5) - 46.85% - 124.01
- Gradient Boosting Regressor - 79.17% - 77.64
- XGBoost Regressor - 98% - 24.06

As we can see, Random Forest was the best estimator, giving an $R^2$ score of nearly 99% and an RMSE of just $17.81. This is a very good predictor. To check for overfitting, the data was split into 20% test set, and these numbers are based on the test set. The numbers remained fairly similar over multiple splits of the dataset, hence it is safe to conclude that we do not have overfitting. 

## Top Predictors
Based on the Random Forest feature importances, we find that the following are the top 5 predictors, from most to least important (feature name - importance):
1. Property Type - Private Room in Townhouse - 0.276067
2. Property Type - Entire Villa - 0.142162
3. Accommodates - 0.075672
4. Bathrooms - 0.068826
5. Beds - 0.065905
