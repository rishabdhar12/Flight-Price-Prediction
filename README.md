# Flight-Price-Prediction


* Created a tool that estimates Flight Prices to help users look for best prices when booking flight tickets.
* Engineered features from the Departure Time, Date of Journey, to quantify the data and make it more understandable.
* Optimized multiple Regression models using GridsearchCV to reach the best model.
* Built a client facing API using flask

# Codes and Resources Used


* Python Version: 3.8.5
* Packages: pandas, numpy, sklearn, matplotlib, seaborn, flask, json, pickle
* For Web Framework Requirements: pip install -r requirements.txt
* Dataset: https://www.kaggle.com/nikhilmittal/flight-fare-prediction-mh
* Flask Productionization: https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2



# Problem Statement

Flight ticket prices can be something hard to guess, today we might see a price, check out the price of the same flight tomorrow, it will be a different story. We might have often heard travelers saying that flight ticket prices are so unpredictable. As data scientists, we are gonna prove that given the right data anything can be predicted. Here you will be provided with prices of flight tickets for various airlines between the months of March and June of 2019 and between various cities. Size of training set: 10683 records

* Size of test set: 2671 records
* FEATURES: Airline: The name of the airline.
* Date_of_Journey: The date of the journey
* Source: The source from which the service begins.
* Destination: The destination where the service ends.
* Route: The route taken by the flight to reach the destination.
* Dep_Time: The time when the journey starts from the source.
* Arrival_Time: Time of arrival at the destination.
* Duration: Total duration of the flight.
* Total_Stops: Total stops between the source and destination.
* Additional_Info: Additional information about the flight
* Price: The price of the ticket

# Cleaning the Data
I needed to clean it up so that it was usable for our model. I made the following changes and created the following variables:

* Made Columns for Day and Month out of Date of Journey
* Calculated the total flight duration
* Removed the null values
* Removed the outliers

# EDA

![alt text](https://github.com/rishabdhar12/Flight-Price-Prediction/blob/main/Images/airline.png)

![alt text](https://github.com/rishabdhar12/Flight-Price-Prediction/blob/main/Images/describe.png)

![alt text](https://github.com/rishabdhar12/Flight-Price-Prediction/blob/main/Images/month.png)


# Model Building

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 30%.

I tried forteen different models and evaluated them using Root Mean Squared Error. I chose RMSE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.

Different models I tried:

* LinearRegression :  2779.0455708889144
* ElasticNet : 3379.6819876610443
* Lasso :  2759.449381312224
* Ridge :  2710.8476127741037
* KNeighborsRegressor :  3249.005561971264
* DecisionTreeRegressor :  2017.530360334335
* RandomForestRegressor :  1662.7359733973055
* SVR :  4246.460099935076
* AdaBoostRegressor :  3135.985374101527
* GradientBoostingRegressor :  1904.7364927923986
* ExtraTreeRegressor :  2432.1393735590073
* HuberRegressor :  3108.870789540331
* XGBRegressor :  1603.7426369307445
* BayesianRidge :  2773.275561516677

XGBRegressor, RandomForestRegressor and GradientBoostingRegressor gave the lowest RMSE so I chose these model and performed hyper parameter tuning

![alt text](https://github.com/rishabdhar12/Flight-Price-Prediction/blob/main/Images/hyperparameter.png)


USing hyperparameter tuning on GradientBoostingRegressor further increased the accuracy.

# Model Accuracy

GradientBoostingRegressor : 
* MAE: 959.8979539240587
* MSE: 2705023.0432436923
* RMSE: 1644.6954256772565


# Productionization

In this step, I built a flask API endpoint that was hosted on a local webserver. The API endpoint takes in a request with a list of values from a flight and returns an estimated price.


























