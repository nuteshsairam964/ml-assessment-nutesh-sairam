## B1. Problem Formulation

(a)

This can be formulated as a supervised machine learning regression problem.

Target variable: items_sold
Input features: store_id, store_size, location_type, promotion_type, competition_density, is_weekend, is_festival, temporal features (month, day, etc.)

Since the goal is to predict a continuous numerical value (items sold), this is a regression problem.

(b)

Using items_sold is more reliable than revenue because:

Revenue can be influenced by price variations, discounts, or inflation
Items sold directly reflects customer demand and promotion effectiveness

- This illustrates the principle of:
Choosing a target variable that directly aligns with the business objective

(c)

Instead of a single global model, we can use:

Segmented models (cluster-based or location-based models)

Reason:

Stores in urban, semi-urban, and rural areas behave differently
Promotions impact varies across regions

- This improves prediction accuracy and personalization

  ## B2. Data and EDA Strategy
(a)

We would join datasets using:

store_id → for store attributes
transaction_date → for calendar data
promotion details via common keys

- Final dataset grain:

One row per store per day (or per transaction_date)

Aggregations:

Daily/monthly sales per store
Promotion usage counts
Average competition density

b)

EDA steps:

Distribution of target (items_sold)
Check skewness and outliers
Helps decide transformations
Sales vs Promotion Type
Identify which promotions perform better
Helps feature importance
Time-based trends
Monthly/weekly patterns
Helps feature engineering (seasonality)
Location-wise performance
Compare urban vs rural stores
Helps segmentation strategy
(c)

Imbalance issue:

80% no promotion → model may bias toward "no promotion"

Solution:

Use balanced sampling
Add promotion indicator features
Use evaluation metrics carefully
Possibly apply weighting techniques

## B3. Model Evaluation and Deployment
(a)

Train-test split:

Use time-based split (not random)
Train on past data, test on future data

Reason:

Prevents data leakage
Reflects real-world scenario

Metrics:

RMSE → penalizes large errors
MAE → interpretable average error
(b)

Feature importance helps explain decisions:

Identify which features influenced prediction (e.g., month, promotion type)
Seasonal trends (December vs March) explain different recommendations

- This improves model interpretability for business teams

(c)

Deployment process:

Save model using pickle or joblib
Load model monthly
Input new store + promotion data
Generate predictions

Monitoring:

Track RMSE over time
Detect performance drop
Retrain model when needed