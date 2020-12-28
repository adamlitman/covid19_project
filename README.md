# California Covid-19 Regression (python): Project Overview
- Created a regression model for predicting the number of new daily deaths from Covid-19 in California
- Gathered 8 open datasets from CA.gov covering 277 days from March 18th through December 19th
- Cleaned the data by handling null values and dropping sparsely populated columns; Added new columns to distinguish new daily counts from running totals across columns
- Explored and visualized the data using multiple plot types in seaborn and matplotlib, including correlation among predictor variables
- Built and tested multiple regression types to find the optimal model (Multiple Linear Regression, Elastic Net, Random Forest, Gradient Boost)

# Sources and Code Used
- Data Source: https://data.ca.gov/dataset?groups=covid-19
- Python Packages Used: pandas, missingno, numpy, matplotlib, seaborn, sklearn

# Dataset Overview
Pulled the following 10 datasets from CA.gov, each of which contained daily reported data spanning 277 days (between 277 and 298,000 rows of data per csv file). Larger datasets reported at the county or hospital level, others reported at the state level.

- Statewide Cases/Deaths
- Statewide Testing
- Hospital Reporting
- Health Care Facility Beds
- Nursing Home Reporting
- Case Data by Age
- Case Data by Demographic
- Case Data by Sex

# Data Cleaning
- For all county/hospital level reporting, aggregated data to the state level each day
- If data was presented as a cumulative total, added columns to isolate new cases per day
- Renamed all columns for easier interpretation and analysis
- Merged the 8 independant dataframes into 1
- Filled NA values in each column by calculating a daily case weighted average for each corresponding row

Visual of Missing Values per Column

![image_nulls](/na_values.png)

# Exploratory Data Analysis
Highlights from EDA

![image_scatter](/scatterplot.png)
![image_hist](/histogram.png)
![image_corr](/corr_matrix.png)
![image_ecdf](/ECDF.png)

# Model Building and Optimization
The goal of model building was to design a regression model to accurately predict the daily death count based on the various case/testing/hospital variables.

Started by choosing relevant predictor variables and splitting the data into training and test sets with a test size of 20%.

Tested 4 different regression models and used GridSearchCV to tune parameters for the 2 tree based models. Calculated both R-squared and Root-Mean-Square Error to evaluate the fit of each model.

- Multiple Linear Regression: R-squared = 0.649, RMSE = 35.899 
- Elastic Net Regression: R-squared = 0.548, RMSE = 40.759
- Random Forest Regression: R-squared = 0.682, RMSE = 34.187
- Gradient Boost Regression: R-squared = 0.750, RMSE = 30.316

Based on both R-squared and RMSE, the gradient boost model clearly performed best. 

These features contributed most to the gradient boost model performance:

![image_features](/features.png)
