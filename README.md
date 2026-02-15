**Executive Summary: BigMart Sales Predictive Analysis**

**1. Project Objective:** The goal of this analysis was to develop a machine learning model to predict sales for 1,559 products across 10 different BigMart outlets. By identifying the key properties of products and stores that drive revenue, BigMart can optimize inventory and marketing strategies to increase overall sales.

**2. Exploratory Data Analysis (EDA) & Data Cleaning:** Initial data checks on the 2013 sales dataset revealed several areas requiring intervention:
  •	Missing Value Imputation:
    o	Item_Weight: Multiple techniques were assessed (Mean, Median, KNN, and Interpolation). Interpolation was selected as the final method as it most closely preserved the original distribution of the variable.
    o	Outlet_Size: Rather than using a global mode, missing values were replaced with the median size based on Store Type. This correctly identified that "Grocery" and "Supermarket Type 1" stores were predominantly "Small," whereas the global mode was "Medium."
  •	Data Standardization: The Item_Fat_Content feature contained redundant labels (e.g., "LF", "low fat", and "Low Fat"). These were standardized into two clean categories: Low Fat and Regular.
  •	Sales Distribution: Five categories Fruits & Vegetables, Snack Foods, Household, Frozen Foods, and Dairy account for approximately 60% of total sales, confirming the store's primary identity as a grocery-focused supermarket.
  •	Granularity: The dataset is unique at the Item_Identifier and Outlet_Identifier level, with no duplicate entries found.

**3. Model Pipeline & Development**
To prepare the data for regression, a robust preprocessing pipeline was implemented:
  •	Feature Encoding: Categorical variables were transformed into dummy variables using pandas.get_dummies. To prevent the "dummy variable trap" (multicollinearity), the first category for each feature was dropped.
  •	Data Splitting: The dataset was split into 70% Training (5.9K entries) and 30% Testing (2.5K entries). Stratified bins of the dependent variable (Item_Outlet_Sales) were used during the split to ensure a balanced distribution of sales values in both sets.

**Model Performance Comparison**
Four algorithms were evaluated using R-squared, MAPE, RMSE, and MAE:
  1.	Linear Regression: Provided a baseline for linear relationships.
  2.	Random Forest: Captured non-linear interactions between features.
  3.	XGBoost: Optimized via Grid Search for hyperparameter tuning. Features were refined to include only high-impact variables (e.g., Item MRP, Store Age, Visibility, and Outlet Type).
  4.	Decision Tree Regressor: Tested with various depths (3, 4, and 5).

**4. Final Solution & Results**
Across all models, the R-squared values ranged between 58% and 60%. Crucially, performance remained stable between the training and testing phases, indicating the models generalized well without overfitting.

**Selected Model: Decision Tree Regressor (Max Depth = 4)**

While XGBoost showed slightly superior statistical metrics (R-square and MAPE), the Decision Tree with a Max Depth of 4 was selected as the final solution. This model provided the highest accuracy in the hackathon challenge while maintaining high interpretability for business stakeholders.

**Key Sales Drivers**
The model identified the following features as the primary drivers of sales:
•	Item MRP (The most significant predictor)
•	Store Age and Outlet Type (Supermarket Type 1 vs. others)
•	Outlet Size (Specifically Medium and Small)
•	Item Visibility
