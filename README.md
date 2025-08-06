FX Exchange Rate Prediction using Machine Learning 

## NON-TECHNICAL EXPLANATION
This project attempts to predict whether Asian currency exchange rates will go up or down the next day using machine learning. 
The system combines signals from four different trading strategies (including moving averages and technical indicators) to make predictions. 
Currency forecasting is notoriously difficult - even slightly beating a coin flip (50% accuracy) is considered successful. The models achieve around 51-52% accuracy, with the Random Forest model showing the most promise for potentially profitable trading strategies.

## DATA
The dataset consists of daily closing prices for 10 major currencies (focusing on Asian currencies plus EUR/USD) from January 1, 2004 to August 5, 2025. 
Data is sourced from Yahoo Finance API using the yfinance Python library. Missing values on public holidays are handled using a fill-forward method. From the raw price data, the system calculates:

- Trading signals from four different strategies
- Historical performance metrics (rolling Sharpe ratios)
- 63-day rolling volatility measures
Citation: Data sourced from Yahoo Finance API, subject to Yahoo's Terms of Service.

## MODEL 
Four machine learning approaches are tested:

- Random Forest with GridSearchCV - chosen for its robustness and ability to handle non-linear relationships
- XGBoost with GridSearchCV - selected for its gradient boosting capabilities and strong performance on structured data
- Neural Network with GridSearchCV - included to capture complex non-linear patterns
- Random Forest with manual parameter selection - designed to reduce overfitting by finding generalized parameters across all currencies

The models predict binary outcomes (up/down) for next-day currency movements using technical trading signals, historical strategy performance, and volatility measures as features.

## HYPERPARAMETER OPTIMSATION
GridSearchCV is used for hyperparameter optimization in models 1-3, with individual optimization conducted for each currency's model. 
For model 4, hyperparameters are manually selected within user-defined ranges to find a generalized specification across all currencies, aiming to reduce overfitting given the relatively small dataset. The degree of regularization can be adjusted by users to control model complexity and prevent overfitting to training data. 

The code contains two sets of parameters for the hyperparameter optimization. A standard setting (regularization = 0) and settings with calibration for more regularisaed hyperparameterisation (reguarlization =1). 

For the random forests, the hyperparmeter options that are adjusted include the number of estimators, the max depth of trees, the minimum samples in each split and leaf.
For XGBoost classifier, the hyperparameter options also include the learning rate, minimum child weights and subsample size, aswell as the regularisaiton of the classifier and the early stopping parameter.
For the neural network model, hyperparameter options focus on the number of hidden layers, the learning rate and the alpha L2 regularisation parameter. 

## RESULTS
Performance is measured using accuracy scores and Sharpe ratios from simulated trading strategies. Average test dataset performance across currencies:

Random Forest (GridSearchCV): 51.82% accuracy, 0.67 Sharpe ratio
XGBoost (GridSearchCV): 51.63% accuracy, 0.49 Sharpe ratio
Neural Network (GridSearchCV): 50.69% accuracy, 0.37 Sharpe ratio
Random Forest (manual): 51.15% accuracy, 0.31 Sharpe ratio

The Random Forest with GridSearchCV shows the most promise, though only this model approaches the ~0.7 Sharpe ratio threshold typically required for production trading strategies. 
Futher investigation of hyperparmeter optimisation and additional exogenous features is required to provide an implimentable trading strategy. 
