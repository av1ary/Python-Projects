Data analytics and science portfolio for learning or Demonstrating End-to-End Capabilities.
The portfolio in this repo is presented as Jupyter Notebooks, SQL scripts, or .pbix files.

Note: Projects are built using synthetic or web-sourced datasets.

Projects:

1. [Client Segmentation & Behavior](RFM,_Cohort_and_CLTV_Analysis.ipynb)
   
3. [Clients' repayment abilities prediction](Loan_Default_Prediction.ipynb)
   
5. [Sales Forecasting](Sales_Forecasting.ipynb)
   
This project is a  Sales Forecasting system built on the Brazilian E-Commerce Public Dataset (Olist) on Kaggle. It focuses on predicting weekly product demand across different regions and categories to help businesses optimise inventory and understand regional market dynamics. The general idea was to recreate the ecom/marketplace basic model for a storage inventory optimisation system. So if a seller has a stable demand in several regions, the marketplace would predict it and store enough products.

**Purpose**
Regional Demand Prediction: Predicting demand at the regional level for sellers and products using price elasticity.

**Data**
The project utilises the Olist Brazilian E-Commerce dataset from Kaggle, which contains approximately 100,000 orders from 2016 to 2018. Target is the number of products sold by the seller in the region.

**Methods**
Data preparation:
Filtering for "delivered" orders, aggregating transactional data into weekly buckets, and handling high-cardinality categorical variables using label/category encoding and creating a synthetic twin with zero sales.

Feature Engineering:
Seasonality: Created sine/cosine transformations for months and weeks to capture cyclical trends.
Relevant Trends: Added Lag features (sales from previous weeks) and Rolling Window features (moving averages) to capture momentum.
Zero Sales: created features to detect zero sales by trends and history.
Elasticity Features: Calculated two "Relative Price" (how a product's price compares to its category average) and "Price Dynamics" - price changes last week.

Modeling:
Model: LightGBM (LGBM), chosen for its efficiency with large datasets and ability to handle categorical features.
Optimisation: Automated hyperparameter tuning using Optuna to minimise RMSE using OPTUNA.
Feature selection: Optimised the number of features by dropping insignificant columns using SHAP.

Validation:
A Time-series split was used, where the most recent weeks were reserved for testing to simulate a real-world forecasting scenario in ecom/marketplace.

**Key Insights**
Price Matters: The model confirms that "Relative Price" within a category is a major driver of demand—customers in this marketplace are highly price-sensitive.

Elasticity Works: Adding features that represent economic elasticity (relationship between price and demand) improved model accuracy (RMSE) significantly.

Regional Dominance: EDA showed a heavy concentration of sales in specific Brazilian states (like São Paulo), which the model uses to refine regional forecasts.
