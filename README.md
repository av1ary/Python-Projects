Data analytics and science portfolio for learning or Demonstrating End-to-End Capabilities.
The portfolio in this repo is presented as Jupyter Notebooks, SQL scripts, or .pbix files.

Note: Projects are built using synthetic or web-sourced datasets.

Projects:

1. [Client Segmentation & Behavior](RFM,_Cohort_and_CLTV_Analysis.ipynb)

   The project provides basic analytical models to understand customer behaviour and predict long-term value in an e-commerce context. The project is written for junior analysts to onboard as far as possible into the ecom context. By transitioning from historical snapshots (RFM) to predictive modelling (CLTV), the analysis enables data-driven marketing strategies, and its advanced versions are used in the companies I worked/work for.

**Data Handling**

Outliers: A crucial step was the decision to clamp outliers rather than delete them. Since extreme purchase values significantly skew Customer Lifetime Value (CLTV) models, capping these values ensured the model remained stable without losing the record of high-value transactions. In Data Analyst courses, this step is not explained.

Integrity Checks: The project strictly removed "cancellations" (Invoice numbers starting with 'c') and records with zero or negative prices/quantities, ensuring that the financial metrics reflected actual realised revenue. In reality, such problems should be solved by data engineers. 

**Strategic Customer Segmentation (RFM)**
The project uses Recency, Frequency, and Monetary scores to categorise customers into actionable marketing segments.
In the real world, Frequency and Monetary features should be observed on dynamic dashboards, for if customer will spend less money or buy less often, the company would react. 

**Predictive Lifetime Value (CLTV)**

Beyond looking at the past, the project used the BG/NBD and Gamma-Gamma models to forecast future behaviour over the next 3 months. Interestingly, the analysis revealed that segments like "Promising" and "Need Attention" actually have higher predicted future value ($477 and $422, respectively) compared to "Loyal Customers" ($37). This suggests that "Loyal" customers may have already peaked, while "Promising" ones represent the best growth opportunity.

**Cohort Retention Analysis**

Time-Based Behavior: By grouping customers by their first purchase month, the analysis tracked how well the business retains users over time. In a better version, the MAU is divided by subscription methods, social features and so on. Cohort charts typically reveal the specific month where retention drops most sharply, identifying critical windows for sending  personalized coupons.
   
2. [Clients' repayment abilities prediction](Loan_Default_Prediction.ipynb)
   
The Loan Default Prediction project is a  machine learning pipeline designed to predict whether a borrower will struggle to repay a loan (it is a default). This project is based on the "Home Credit Default Risk" Kaggle competition and focuses on building a robust classification model using complex, multi-table data.

**Purpose**

To build a predictive model that estimates the probability of loan default (binary classification), helping financial institutions assess credit risk more accurately.

**Methodology**

Exploratory Data Analysis (EDA): Deep dive into feature distributions, missing value patterns, and correlations with the target variable to understand the drivers of default.

Feature Engineering:

Manual Engineering: Creating domain-specific ratios like Credit-to-Income, Annuity-to-Income, and Employment-to-Age ratios.

Polynomial Features: Generating interaction terms for high-impact variables (e.g., EXT_SOURCE scores) to capture non-linear relationships.

Automated Engineering: Utilising Featuretools with DFS to  aggregate and transform data.

Machine Learning Models:

Baselines: Established using Random Forest to evaluate the impact of different feature sets.

Advanced Gradient Boosting: Implementation of LightGBM for high-performance training and handling of large-scale data.

Optimisation: Employing Optuna for automated hyperparameter tuning and Stratified K-Fold Cross-Validation to ensure the model generalises well to unseen data
   
3. [Sales Forecasting](Sales_Forecasting.ipynb)
   
This project is a  Sales Forecasting system built on the Brazilian E-Commerce Public Dataset (Olist) on Kaggle. It focuses on predicting weekly product demand across different regions and categories to help businesses optimise inventory and understand regional market dynamics. The general idea was to recreate the ecom/marketplace basic model for a storage inventory optimisation system. So if a seller has a stable demand in several regions, the marketplace would predict it and store enough products.

**Purpose**

Regional Demand Prediction: Predicting demand at the regional level for sellers and products using price elasticity.

**Data**

The project utilises the Olist Brazilian E-Commerce dataset from Kaggle, which contains approximately 100,000 orders from 2016 to 2018. Target is the number of products sold by the seller in the region.

**Methodology**

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
