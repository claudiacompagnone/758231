# 758231

## **Title:**
*Air transportation fare prediction*


**Team members:**
- Claudia Compagnone 758231
- Nicolò Rosso 758991
- Giovanni Raimondo Quaratino 759111



### **Introduction:**
The project aims to provide a predictive model for flight ticket prices for a leading Indian travel company. The model uses factors including airline, flight number, source and destination cities, departure and arrival times, ticket class, flight duration, number of stops, and the number of days left until departure to predict prices. The goal is to offer a reliable tool that can assist customers in their decision-making process and help airlines in devising strategic pricing policies.


### **Methods:**

#### **Data Preprocessing:**
The dataset provided required preprocessing for optimal use. Missing values, if any, were treated depending on the data type: for numerical variables, we used median imputation, while for categorical variables, the mode was used for imputation.

Outliers, which can often skew the results of a model, were detected and removed using the Interquartile Range (IQR) method. In this method, a data point was considered an outlier if it was below (1st Quartile - 1.5IQR) or above (3rd Quartile + 1.5IQR).

#### **Exploratory Data Analysis (EDA):**
During EDA, we sought to visualize and understand the dataset's various features and their interrelationships. We found that the price of a ticket had substantial correlations with the class of the ticket, the duration of the flight, and the number of stops. Longer flights and higher class types (business, first class) tend to cost more, which explained these correlations. Multiple-stop flights were usually cheaper, showing an inverse correlation with price.

#### **Data Preprocessing:**

Feature engineering and transformation were crucial steps in preparing the data for model training. The categorical variable 'stops' was converted into a numerical variable, while the flight duration was changed from hours and minutes to total minutes. These transformations were done to facilitate the models' understanding of these features and to establish more accurate relationships with the flight prices.

### **Experimental Design:**
The dataset was split into a training set (75%) and a test set (25%). A simple Linear Regression model was used as the baseline due to its simplicity and common usage in predictive modeling. However, given the complexity and high-dimensionality of the dataset, more sophisticated machine learning models were employed, including Ridge, Lasso, Random Forest, and XGBoost.

Ridge and Lasso Regression were used as they extend simple linear regression by adding a penalty term to the loss function, which helps to control overfitting and improve generalization. The Random Forest model was selected for its ability to handle a large number of features and its robustness to outliers and non-linear data.

The XGBoost model was particularly highlighted due to its effectiveness in handling both sparse and dense datasets. This model was further refined by tuning its hyperparameters using Bayesian Optimization. Bayesian Optimization is a sequential design strategy for global optimization of black-box functions that works by constructing a posterior distribution of functions to find the maximum of these functions efficiently.

The R2 score was chosen as the evaluation metric. It measures the proportion of variance in the dependent variable that can be predicted from the independent variables, providing a clear and interpretable measure of the models' performance.


### **Results:**
All models performed reasonably well, but the XGBoost model with DMatrix data structure and Bayesian hyperparameter optimization yielded the highest R2 score of 0.9928, indicating an excellent fit to the data.

To understand the contribution of each feature to the predictions, we performed feature importance analysis using SHAP (SHapley Additive exPlanations). This approach offers a unified measure of feature importance that allocates each feature an importance value for a particular prediction.

Through SHAP, we found that 'class', 'duration', and 'number of stops' were the most influential predictors of flight prices. This aligns with our initial findings during the Exploratory Data Analysis phase, confirming that these factors significantly impact the price of a flight ticket. The SHAP values also allowed us to understand the model on a granular level and interpret its predictions, providing valuable insights into the relationships between the predictors and the target variable.

### **Conclusions:**
The XGBoost model, with its high R2 score, provides a robust tool for predicting flight prices. This can offer valuable insights to customers and airlines, aiding in informed decision-making and strategic pricing. It's important to note, however, that while the model performs well on the given dataset, real-world conditions may introduce additional variables such as fuel prices and economic conditions. Future work could focus on incorporating these variables and expanding the dataset to improve the model's predictive accuracy and generalizability.
