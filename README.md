<h1>Statistical Analysis on Retail Sales Using Hypothesis Testing</h1>

<h2>Overview :</h2>

This repository contains a statistical analysis project that applies hypothesis testing techniques on a retail sales dataset. The goal of this project is to understand how different business factors such as region, category, and discount strategies influence sales performance and customer behavior.

This project demonstrates the complete data analysis workflow, including data exploration, data visualization, hypothesis testing, and interpretation of statistical results.

<h2>Tools used for the analysis :</h2>

1. Python
2. Pandas Library
3. Matplotlib Library
4. Seaborn Library
5. SciPy Library
6. Statsmodels Library
7. Jupyter Notebooks
8. Visual Studio Code

<h2>Importing Libraries :</h2>

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import scipy.stats as stats
from scipy.stats import ttest_1samp
from scipy.stats import ttest_ind
from scipy.stats import ttest_rel
from scipy.stats import f_oneway
from scipy.stats import chi2_contingency
from statsmodels.stats.multicomp import pairwise_tukeyhsd
```

<h2>Loading dataset :</h2>

```python
data = pd.read_excel("C:\\Users\\ADMIN\\Saikat VS\\Hypothesis Testing\\Raw Sales Data.xlsx")
data
```

<h2>Exploratory Data Analysis :</h2>

```python
sns.boxplot(x='Region', y='Discount', data=data)
```
![boxplot]()
Description : Boxplot helps in visualizing the distribution, spread and outliers in Discounts across Different Regions.

<h2>Two Sample T-Test :</h2>

```python
df_data = data[data['Region'].isin(["East","West"])]
df_East_region_sales = df_data[df_data['Region']=="East"]['Sales']
df_West_region_sales = df_data[df_data['Region']=="West"]['Sales']
ttest, p_value = ttest_ind(a = df_East_region_sales, b = df_West_region_sales, equal_var=False)
print("P Value = ",p_value)
```
![p value]()

<h2>Result Interpretation :</h2>

```python
if p_value<0.05:
    print("Reject Null Hypothesis")
else:
    print("Fail to Reject Null Hypothesis")
```
![Result]()
Insight : The Test showed No statistically significant Difference in Average Sales between East and West Regions.

<h2>Chi - Square Test :</h2>

```python
df_observed= pd.crosstab(data['Region'],data['Category'])
Chi2, p_value, dof, expected = chi2_contingency(df_observed)
alpha = 0.05
print("Chi-Square: ",Chi2,
      "\nP value: ",p_value,
      "\nDegree of Freedom: ",dof,
      "\nAlpha: ",alpha
      )
```
![print]()

<h2>Result Interpretation :</h2>

```python
if p_value<0.05:
    print("Reject Null Hypothesis")
else:
    print("Fail to Reject Null Hypothesis")
```
![result]()
Insight : There is No significant Association between Region and Category, indicating independence between these variables.

<h2>ANNOVA :</h2>

```python
South = data[data['Region']=="South"]['Discount'].dropna()
Central = data[data['Region']=="Central"]['Discount'].dropna()
West = data[data['Region']=="West"]['Discount'].dropna()
East = data[data['Region']=="East"]['Discount'].dropna()
f_statistics, p_value = f_oneway(South, West, Central, East)
print("Value of F-Statistics = ",f_statistics,
      "\nP Value = ",p_value)
```
![result]()

<h2>Result Interpretation :</h2>

```python
if p_value<0.05:
    print("Reject Null Hypothesis")
else:
    print("Fail to Reject Null Hypothesis")
```
![result]()
Insight : There is a statistically significant Difference in Discount Distribution Across The Four Regions.

<h2>Tukey’s Honest Significant Difference (HSD) Test :</h2>

As the 'P Value' is <0.05 so Tukey’s Honest Significant Difference Test is performed.

```python
tukey = pairwise_tukeyhsd(endog=data['Discount'], groups=data['Region'], alpha=0.05)
print(tukey)
```
![result]()
Insight : This test identifies which Specific Regions Differ significantly from Each Other in terms of Discounts.

<h2>Key Insights of the Research</h2>

1. Sales performance is similar across regions
2. Category distribution is independent of region
3. Discount strategies vary significantly across regions
4. Central region shows higher discount variability

<h2>Challenges Faced :</h2>

1. Handling mixed data formats (especially Date columns)
2. Understanding correct application of statistical tests
3. Interpreting statistical outputs into business insights

<h2>Conclusion :</h2>

This project demonstrates how hypothesis testing techniques such as T-Test, Chi-Square, ANOVA, and Tukey HSD can be used to extract meaningful business insights from retail sales data.

The analysis highlights how statistical methods can support decision-making in pricing strategies, regional performance evaluation, and business optimization.

This project strengthens skills in data analysis, statistical thinking, and real-world business problem solving using Python.
