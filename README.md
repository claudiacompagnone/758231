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
The data was then split into two sets: 80% for training the models and 20% for testing their performance. The benchmark for our work was a simple Linear Regression model. Linear Regression was chosen as the baseline due to its simplicity and widespread use in predictive modeling. We then progressed to more complex models, including Ridge, Lasso, Random Forest, and XGBoost. These models were chosen due to their ability to handle complex datasets and deliver more accurate predictions.

Based on initial results, the XGBoost model, implemented with DMatrix data structure, stood out for its better handling of both sparse and dense datasets. This model was further refined by tuning its hyperparameters using Bayesian Optimization, a strategy known for effectively navigating the hyperparameter space to find the optimal model settings.

We used the R2 score as our evaluation metric. The R2 score, also known as the coefficient of determination, measures the proportion of variance in the dependent variable that can be predicted from the independent variables. It ranges from 0 to 1, where 1 indicates a perfect fit to the data. This metric was chosen because it provides a clear and interpretable measure of how well our models are performing in terms of variance explained.


### **Results:**
All models performed reasonably well, but the XGBoost model with DMatrix data structure and Bayesian hyperparameter optimization yielded the highest R2 score of 0.9912, indicating an excellent fit to the data.

To understand the contribution of each feature to the predictions, we performed feature importance analysis using SHAP (SHapley Additive exPlanations). This approach offers a unified measure of feature importance that allocates each feature an importance value for a particular prediction.

Through SHAP, we found that 'class', 'duration', and 'number of stops' were the most influential predictors of flight prices. This aligns with our initial findings during the Exploratory Data Analysis phase, confirming that these factors significantly impact the price of a flight ticket. The SHAP values also allowed us to understand the model on a granular level and interpret its predictions, providing valuable insights into the relationships between the predictors and the target variable.

### **Conclusions:**
The XGBoost model, with its high R2 score, provides a robust tool for predicting flight prices. This can offer valuable insights to customers and airlines, aiding in informed decision-making and strategic pricing. It's important to note, however, that while the model performs well on the given dataset, real-world conditions may introduce additional variables such as fuel prices and economic conditions. Future work could focus on incorporating these variables and expanding the dataset to improve the model's predictive accuracy and generalizability.
