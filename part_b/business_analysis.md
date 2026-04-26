# Part B — Business Case Analysis

## B1. Problem Formulation

### (a)
The objective is to predict the number of items sold for a store under a given promotion.  
The target variable is **items_sold**, while input features include store attributes (store size, location type), promotion type, competition density, and time-based features such as month, weekends, and festivals.

This is a **supervised regression problem** because the output is a continuous numerical value and predictions are made using historical labelled data.



### (b)
Using revenue alone can be misleading because it is influenced by pricing and discount levels. For example, a high discount may increase revenue but not reflect actual customer demand.

but In contrast, **items sold directly measures customer response** to a promotion, making it a more reliable indicator of effectiveness.

This shows an important machine learning principle: the target variable should align closely with the real business objective being optimised.



### (c)
Using a single global model may not capture differences across stores.

A better approach is to:
 Segment stores based on characteristics such as location or store size, or  
 Use a cluster-based or hierarchical modelling approach  

For example, urban stores may respond differently to promotions compared to rural stores. This helps the model capture location-specific behaviour patterns.



## B2. Data and EDA Strategy

### (a)
The datasets can be joined using common keys such as **store_id** and **date**.

The final dataset should be structured at a **store–month level**, where each row represents one store’s performance under a specific promotion during a given time period.

Aggregations may include:
- Total items sold  
- Number of transactions  
- Average basket size  
- Promotion applied  

This ensures consistent granularity and avoids duplication.



### (b)
Before modelling, the following analyses would be performed:

 **Distribution of items_sold** to identify skewness and outliers  
 **Bar chart of sales by promotion type** to compare effectiveness  
 **Time-series plot** to detect seasonal trends (e.g., festivals, peak months)  
 **Correlation heatmap** to understand relationships between variables  

These insights help guide feature engineering, such as creating seasonal features and selecting important variables.



### (c)
Since 80% of transactions occur without promotions, the dataset is imbalanced.

This may bias the model towards predicting lower sales values associated with non-promotional periods.

To address this:
- Add a binary feature showing whether a promotion is applied  
- Use sampling techniques to balance promotional data  
- Apply weighting to give more importance to promotional cases  



## B3. Model Evaluation and Deployment

### (a)
A **time-based split** should be used, where earlier data is used for training and more recent data is used for testing.

A random split is not appropriate because it can cause data leakage, where future information influences the training process.

Evaluation metrics:
 **RMSE** to penalise large prediction errors  
 **MAE** to measure average prediction error  

These metrics help evaluate how close predictions are to actual sales.



### (b)
Feature Importance can help explain why different promotions are recommended for the same store at different time frames.

For example:
 Seasonal features such as month or festival indicators may influence promotion effectiveness  
 Location based features may affect customer behaviour  

This can be communicated to the marketing team using feature importance charts and simple explanations linking key factors to model decisions.



### (c)
The trained model can be saved using tools like **joblib** or **pickle**.

Each month:
 fesh new data is collected  
 The same preprocessing pipeline is applied  
 The model generates predictions for each store  

Monitoring should include:
 Tracking RMSE and MAE over time  
 Comparing predicted vs actual sales  
 Setting thresholds to detect performance degradation  

If performance decreases significantly, the model should be retrained using updated data.

This approach ensures better real-world applicability.
