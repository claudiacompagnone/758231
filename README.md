# 758231

# **Title: Air transportation fare prediction**

**Team members:**
- Claudia Compagnone 758231
- Nicolò Rosso 758991
- Giovanni Raimondo Quaratino 759111



## **Introduction:**
The project aims to provide a predictive model for flight ticket prices for a leading Indian travel company. The model uses factors including airline, flight number, source and destination cities, departure and arrival times, ticket class, flight duration, number of stops, and the number of days left until departure to predict prices. The goal is to offer a reliable tool that can assist customers in their decision-making process and help airlines in devising strategic pricing policies.



## **Methods:**

### **Data Preprocessing:**

#### **Programming environment:**
We used Python as programming language and the web-based JupyterLab as IDE. We imported the following libraries: pandas 1.5.2, numpy 1.23.5, matplotlib 3.7.1, seaborn 0.12.2, dython 0.7.3, sklearn 1.2.0, xgboost 1.7.3, shap 0.41.0, bayesian-optimization 1.4.3.


#### **Data Cleaning:**
Once we read the csv file into a pandas DataFrame, we moved to the cleaning phase:
- we checked for duplicate and nan values in the dataset, but there were none.
- outliers, which can often skew the results of a model, were detected and removed using the Interquartile Range (IQR) method. In this method, a data point was considered an outlier if it was below (1st Quartile - 1.5IQR) or above (3rd Quartile + 1.5IQR). We removed a total of 123 outliers (going from 300153 to 300030 observations).
- we transformed the duration variable (originally in hours) into minutes.


#### **Exploratory Data Analysis (EDA):**
During EDA, we sought to visualize and understand the dataset's various features and their interrelationships. 
First of all, we realized a correlation matrix, that was useful in order to decide whether we could drop some variables which were too highly correlated and could raise collinearity-related problem. 

![Correlation Matrix](images/complete_correlation.png)

After visualizing the distribution of our variables, we investigated how they relate to price, in particular, we tried to answer the following questions:

**1. How is price affected by the days left until plane departure?**
![Line Plot](images/Line-plot.png)

**2. Is price affected by the source and destination city?**
![Relplot](images/Relplot.png)

**3. How does the airfare vary between Economy and Business class?**
![Bar Plot Class](images/Bar-plot-class.png)

**4. Is price affected by departure time and arrival time?**
![Bar Plot Dep](images/Bar-plot-dep.png)
![Bar Plot Arr](images/Bar-plot-arr.png)

**5. How does the airfare vary with the number of stops?**
![Bar Plot Stops](images/Bar-plot-stops.png)

We found that the price of a ticket had substantial correlations with the class of the ticket, the duration of the flight, and the number of stops. Longer flights and higher class types (business, first class) tend to cost more, which explained these correlations.


#### **Feature Selection and Additional Transformations:**
By looking at the correlation matrix, we noticed that the flight variable is perfectly positively correlated with airline, so we decided to simply drop it.
Finally, we converted into category type all the non-numeric variables of our dataset.


All the performed transformations were done to facilitate the models' understanding of the features and to establish more accurate relationships with the flight prices.



## **Experimental Design:**

#### **Train-Test split:**
The dataset was split into a training set (75%) and a test set (25%). 

#### **Baseline model:**
A **simple Linear Regression model** was used as the **baseline** due to its simplicity and common usage in predictive modeling. However, given the complexity and high-dimensionality of the dataset, more sophisticated machine learning models were employed, including Ridge, Lasso, SVR, Random Forest, and XGBoost.

#### **More flexible models of non-linear relationships between the predictors and the response variable:**
Regularization methods such as Ridge and Lasso Regression were used as they extend simple linear regression by adding a penalty term to the loss function, which helps to control overfitting and improve generalization. 
Then, we tried even to train a Support Vector Regression (SVR) model, but the performance was below the previous models so we rejected it.

#### **Ensemble learning methods:**
We then moved to ensemble learning models, combining decisions from multiple underlying models, and using a voting technique to determine the final prediction. In particular, we built and tuned a Random Forest and an Extreme Gradient Boosting (XGBoost) model. We decided to use these two algorithms because one implements Boosting and one Bagging technique to sample the dataset.
The Random Forest model was selected for its ability to handle a large number of features and its robustness to outliers and non-linear data.
The XGBoost model was particularly highlighted due to its effectiveness in handling both sparse and dense datasets. This model was further refined by tuning its hyperparameters using Bayesian Optimization. Bayesian Optimization is a sequential design strategy for global optimization of black-box functions that works by constructing a posterior distribution of functions to find the maximum of these functions efficiently.

#### **Evaluation metrics**
We chose to evaluate our models with three different metrics:
- **RMSE**: it is the square root of mean squared error (squared distance between actual and predicted values). The output value you get is in the same unit as the required output variable which makes interpretation of loss easier. **Important** the prices in our dataset are given in rupees (1 INR == 0.012 USD), the Indian currency, this is why the RMSE is so high.
- **MAPE**: the Mean Absolute Percentage Error is a measure of accuracy. It is the mean of all absolute percentage
errors between the predicted and actual values. As a rule of thumb, a good result for MAPE is < 20%.
- **R2**: it is a measure of goodness of fit (how well data are approximated by predictions). It measures the proportion of variance in the dependent variable that can be predicted from the independent variables, providing a clear and interpretable measure of the models' performance.



## **Results:**
All models performed reasonably well, but the XGBoost model with DMatrix data structure and Bayesian hyperparameter optimization yielded the highest R2 score of 0.9928, indicating an excellent fit to the data.

To understand the contribution of each feature to the predictions, we performed feature importance analysis using SHAP (SHapley Additive exPlanations). This approach offers a unified measure of feature importance that allocates each feature an importance value for a particular prediction.

Through Shap, we found that 'class', 'duration', and 'number of stops' were the most influential predictors of flight prices. This aligns with our initial findings during the Exploratory Data Analysis phase, confirming that these factors significantly impact the price of a flight ticket. The SHAP values also allowed us to understand the model on a granular level and interpret its predictions, providing valuable insights into the relationships between the predictors and the target variable.



## **Conclusions:**
The XGBoost model, with its high R2 score, provides a robust tool for predicting flight prices. This can offer valuable insights to customers and airlines, aiding in informed decision-making and strategic pricing. It's important to note, however, that while the model performs well on the given dataset, real-world conditions may introduce additional variables such as fuel prices and economic conditions. Future work could focus on incorporating these variables and expanding the dataset to improve the model's predictive accuracy and generalizability.
