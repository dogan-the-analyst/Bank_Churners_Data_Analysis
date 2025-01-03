# Bank Churn Data Analysis

This repository contains a comprehensive analysis of customer churn in the banking sector. The goal is to identify key characteristics and patterns that differentiate churned customers from non-churned ones, leveraging data visualization and statistical insights.

## Prerequisites

Ensure you have the following libraries installed:

- pandas
- numpy
- matplotlib
- seaborn
- plotly

## Analysis Steps

1. **Data Loading and Exploration**:
   - Load the dataset `BankChurners_v2.csv`.
   - Display the shape and first few rows of the dataset to understand its structure.

2. **Data Cleaning**:
   - Remove duplicates.
   - Handle missing values in the `Education_Level` column by filling them with "Unknown".

3. **Data Transformation and Binning**:
   - Binned the `Customer_Age` into categories.
   - Applied normalization and log transformation to the `Credit_Limit` column.

4. **Exploratory Data Analysis (EDA)**:
   - Investigate the distribution of churned vs. non-churned customers.
   - Analyze relationships between key numerical features like `Total_Trans_Amt` and `Total_Trans_Ct`.
   - Visualize age distribution, credit limit distribution, and transaction counts.

5. **Key Findings and Insights**:
   - "Attrited Customers" show lower transaction counts and amounts.
   - Differences in customer behaviors can be captured using features like `Credit_Limit`, `Total_Trans_Amt`, and `Total_Trans_Ct`.
   - Targeting churned customers with retention strategies could improve customer retention.

6. **Conclusion and Recommendations**:
   - Use customer segmentation to tailor marketing efforts.
   - Implement targeted campaigns focusing on high-value segments.
   - Focus on improving customer retention strategies for those showing signs of attrition.

## Data Visualization

- **Histograms**: Visualize age, credit limits, and transaction counts.
- **Pair Plots**: Examine relationships between numerical features.
- **KDE Plots**: Analyze the density of variables across churned and non-churned groups.

## Example Code

```python
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.graph_objs as go
from plotly.offline import iplot

# Load the dataset
df = pd.read_csv("BankChurners_v2.csv")

# Data cleaning
df.drop_duplicates(inplace=True)
df["Education_Level"] = df["Education_Level"].fillna("Unknown")

# Data transformation
df["Credit_Limit_Normalized"] = (df["Credit_Limit"] - df["Credit_Limit"].min()) / (df["Credit_Limit"].max() - df["Credit_Limit"].min())
df["Credit_Limit_Log_Transformed"] = np.log(df["Credit_Limit"])

# Exploratory Data Analysis
sns.histplot(df, x="Customer_Age")
sns.scatterplot(x="Total_Trans_Amt", y="Total_Trans_Ct", hue="Attrition_Flag")

# Insights
pivot_table = df.groupby(["Attrition_Flag"]).mean().T
pivot_table["Diff"] = pivot_table["Attrited Customer"] / pivot_table["Existing Customer"] - 1
pivot_table.sort_values("Diff")
```
