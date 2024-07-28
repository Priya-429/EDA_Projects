
# Diwali Sales Analysis

This project aims to perform an exploratory data analysis (EDA) on a dataset of Diwali sales, which includes various customer attributes and their purchase details. The analysis helps in understanding customer behavior, identifying potential customers, and improving sales by planning inventory based on the most selling product categories and products.

## Project Overview

The dataset contains information about customer demographics, their purchases, and the amount spent. The project involves data cleaning, manipulation, and visualization to derive meaningful insights.

## Dataset

The dataset consists of more than 10,000 rows with the following columns:
- `User_ID`: Unique identifier for each customer
- `Cust_name`: Name of the customer
- `Product_ID`: Unique identifier for each product
- `Gender`: Gender of the customer
- `Age Group`: Age group of the customer
- `Age`: Actual age of the customer
- `Marital_Status`: Marital status of the customer (0 for unmarried, 1 for married)
- `State`: State of residence of the customer
- `Zone`: Geographical zone of the state
- `Occupation`: Occupation of the customer
- `Product_Category`: Category of the product
- `Orders`: Number of orders placed by the customer
- `Amount`: Total amount spent by the customer

## Project Learnings

1. **Performed Data Cleaning and Manipulations**
   - Handled missing values and duplicates.
   - Standardized categorical variables.
   - Converted data types where necessary.
   - Dropped unrelated/blank columns.
   - Renamed columns for better readability.

2. **Performed EDA using Pandas, Matplotlib, and Seaborn Libraries**
   - Generated descriptive statistics.
   - Visualized data distributions and relationships between variables.
   - Created insightful plots to understand customer behavior and sales patterns.

3. **Improved Customer Experience**
   - Identified potential customers across different states, occupations, genders, and age groups.

4. **Improved Sales**
   - Identified most selling product categories and products.
   - Provided recommendations for inventory planning to meet demand.

## Tools and Libraries Used

- **Pandas**: For data manipulation and analysis.
- **Numpy**: For numerical operations.
- **Matplotlib**: For creating static, interactive, and animated visualizations.
- **Seaborn**: For making statistical graphics in Python.

## Code Snippets

### Import Libraries

```python
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
```

### Load Data

```python
df = pd.read_csv('Diwali Sales Data.csv', encoding='unicode_escape')
```

### Data Cleaning and Manipulation

```python
# Drop unrelated/blank columns
df.drop(['Status', 'unnamed1'], axis=1, inplace=True)

# Check for and drop null values
df.dropna(inplace=True)

# Change data type
df['Amount'] = df['Amount'].astype('int')

# Rename columns
df.rename(columns={'Marital_Status':'Shaadi'}, inplace=True)
```

### Descriptive Statistics

```python
df.describe()
df[['Age', 'Orders', 'Amount']].describe()
```

### Visualizations

- **Bar Chart for Gender Count**

```python
ax = sns.countplot(x='Gender', data=df)
for bars in ax.containers:
    ax.bar_label(bars)
```

- **Bar Chart for Gender vs Total Amount**

```python
sales_gen = df.groupby(['Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.barplot(x='Gender', y='Amount', data=sales_gen)
```

- **Bar Chart for Age Group and Gender Count**

```python
ax = sns.countplot(x='Age Group', hue='Gender', data=df)
for bars in ax.containers:
    ax.bar_label(bars)
```

- **Bar Chart for Total Amount vs Age Group**

```python
sales_age = df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.barplot(x='Age Group', y='Amount', data=sales_age)
```

- **Top 10 States by Number of Orders**

```python
sales_state = df.groupby(['State'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.set(rc={'figure.figsize':(15,5)})
sns.barplot(x='State', y='Orders', data=sales_state)
```

- **Top 10 States by Amount Spent**

```python
sales_state = df.groupby(['State'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
sns.set(rc={'figure.figsize':(15,5)})
sns.barplot(x='State', y='Amount', data=sales_state)
```

- **Bar Chart for Marital Status Count**

```python
ax = sns.countplot(x='Marital_Status', data=df)
sns.set(rc={'figure.figsize':(7,5)})
for bars in ax.containers:
    ax.bar_label(bars)
```

- **Amount Spent by Marital Status and Gender**

```python
sales_state = df.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.set(rc={'figure.figsize':(6,5)})
sns.barplot(x='Marital_Status', y='Amount', hue='Gender', data=sales_state)
```

- **Bar Chart for Occupation Count**

```python
sns.set(rc={'figure.figsize':(20,5)})
ax = sns.countplot(x='Occupation', data=df)
for bars in ax.containers:
    ax.bar_label(bars)
```

- **Amount Spent by Occupation**

```python
sales_state = df.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.set(rc={'figure.figsize':(20,5)})
sns.barplot(x='Occupation', y='Amount', data=sales_state)
```

- **Bar Chart for Product Category Count**

```python
sns.set(rc={'figure.figsize':(20,5)})
ax = sns.countplot(x='Product_Category', data=df)
for bars in ax.containers:
    ax.bar_label(bars)
```

- **Amount Spent by Product Category**

```python
sales_state = df.groupby(['Product_Category'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
sns.set(rc={'figure.figsize':(20,5)})
sns.barplot(x='Product_Category', y='Amount', data=sales_state)
```

- **Top 10 Most Sold Products by Orders**

```python
sales_state = df.groupby(['Product_ID'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.set(rc={'figure.figsize':(20,5)})
sns.barplot(x='Product_ID', y='Orders', data=sales_state)
```

- **Top 10 Most Sold Products (Bar Chart)**

```python
fig1, ax1 = plt.subplots(figsize=(12,7))
df.groupby('Product_ID')['Orders'].sum().nlargest(10).sort_values(ascending=False).plot(kind='bar')
```

## How to Run the Project

1. Clone the repository or download the project files.
2. Ensure you have the necessary Python libraries installed:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
3. Open the Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
4. Navigate to the project directory and open `Diwali_Sales_Analysis.ipynb`.
5. Run the notebook cells to see the analysis and visualizations.

## Conclusion and Recommendations

- **Summary of Key Findings**: 
  - Detailed insights on customer demographics and their spending patterns.
  - Identification of high-spending customer segments.

- **Actionable Recommendations**:
  - Develop targeted marketing strategies for high-spending customer segments.
  - Plan inventory based on the demand for the most selling products.

## Jupyter Notebook

You can access the Jupyter Notebook used for this analysis [here](http://localhost:8888/notebooks/Downloads/Python_Diwali_Sales_Analysis-main/Diwali_Sales_Analysis.ipynb).
