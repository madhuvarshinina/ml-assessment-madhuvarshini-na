## B1. Problem Formulation
(a)

The goal is to predict the number of items sold for a given store and promotion.
The target variable is items_sold, while input features include store attributes (store size, location type), promotion type, competition density, and temporal features such as month, weekends, and festivals.
This is a supervised regression problem, since we are predicting a continuous numerical value based on historical data.

(b)

Using revenue alone can be misleading, as it is influenced by pricing and discount levels. A high revenue does not necessarily indicate strong customer engagement.
In contrast, items sold directly reflects customer response to promotions, making it a more reliable measure of promotion effectiveness.
This highlights an important principle in machine learning: the target variable should align closely with the actual business objective being optimised.

(c)

Instead of using a single global model, a better approach would be to use segmented models based on store characteristics, such as location or store size.
Alternatively, a hierarchical or cluster-based modelling approach can be used to group similar stores and train models accordingly.
This ensures that differences in customer behaviour across regions are properly captured.

## B2. Data and EDA Strategy
(a)

The datasets would be joined using common keys such as store_id and date.
The final dataset would be aggregated at the store-month level, where each row represents the performance of a store under a specific promotion during a given time period.
Aggregations may include total items sold, average basket size, and number of transactions.
This ensures consistency in granularity and avoids duplication issues during modelling.

(b)

Before modelling, several exploratory analyses would be performed:

A distribution plot of items sold to understand variability and detect outliers
A bar chart comparing average sales across different promotion types to identify effective promotions
A time series plot to observe seasonal patterns or trends
A correlation heatmap to identify relationships between numerical features

These insights would guide feature engineering, such as creating seasonal features or refining promotion-related variables.

(c)

Since 80% of transactions occur without promotions, the dataset is imbalanced.
This could bias the model towards predicting lower sales values associated with non-promotional periods.
To address this, techniques such as stratified sampling, weighting promotional data, or creating separate features indicating promotion presence can be used.

## B3. Model Evaluation and Deployment
(a)

The data should be split using a time-based approach, where earlier data is used for training and more recent data is used for testing.
A random split is inappropriate because it can lead to data leakage, where future information influences the model during training.

Evaluation metrics should include:

RMSE to measure large prediction errors
MAE to understand average prediction deviation

These metrics help assess how accurately the model predicts actual sales in a business context.

(b)

Feature importance can be used to understand why different promotions are recommended for the same store across months.
For example, seasonal features such as month or festival indicators may have high importance, leading the model to favour certain promotions during specific periods.

This explanation can be communicated to the marketing team by showing which factors influenced each decision, making the model’s recommendations more transparent and actionable.

(c)

The trained model can be saved using tools like joblib or pickle.
Each month, new data would be preprocessed using the same pipeline and passed into the model to generate predictions.

Monitoring should include tracking prediction errors over time and comparing predicted vs actual sales.
If performance degrades significantly, it indicates the need for retraining the model using more recent data.
