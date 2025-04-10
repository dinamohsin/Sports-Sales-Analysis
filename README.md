
![LOGO](https://github.com/user-attachments/assets/a2cee876-6c53-4aaf-9824-4de1c6a39366)

# **Sports Sales Analysis - Data Analysis (Python & Power BI)**

This project involves analyzing **Sports-Product** data using **Python**, **Power BI**, and **Excel datasets** to extract insights and visualize key business metrics. The focus is on understanding **sales trends**, **profitability**, and **product performance** through a comprehensive data analysis.

![Insights](https://github.com/user-attachments/assets/2d13be27-1b86-4f2c-8934-a6cd07fc517b)
![Details](https://github.com/user-attachments/assets/e1aee0f5-dde3-45e6-9794-eb97dbc0f001)

## Table of Contents
- [1. Data Analysis Workflow](#1-data-analysis-workflow)
- [2. Project Goal](#2-project-goal)
- [3. Dashboard Requirements](#3-dashboard-requirements)
- [4. Dataset Details & Preparation](#4-dataset-details--preparation)
- [5. Data Cleaning & Transformation](#5-data-cleaning--transformation)
- [6. Power BI Visualizations](#6-power-bi-visualizations)
- [7. Python Analysis](#7-python-analysis)
- [8. Business Insights, Recommendations & Conclusion](#8-business-insights-recommendations--conclusion)
- [9. Technologies Used](#9-technologies-used)
- [10. Final Thoughts](#10-final-thoughts)

---

## **1. Data Analysis Workflow**  
The analysis follows a structured workflow:  

### Step 1: Data Cleaning and Preparation  
- **Data types** were checked and verified for correctness in the dataset.  
- Fixed a column name error: `"Operating Proft"` was corrected to `"Operating Profit"`.  
- Ensured there were no **null values** or **duplicates** in the dataset.  

### Step 2: Loading Data into Power BI  
- After cleaning, the dataset was loaded into **Power BI** for visualization.  

### Step 3: Developing KPIs and Metrics  
Several key performance indicators (KPIs) were calculated:  
- **Total Sales**  
- **Total Profit**  
- **Units Sold**  
- **Total Products**  

### Step 4: Creating Visualizations in Power BI  
Various visualizations were built to represent business insights:  
- **Total Sales & Profit by Region and Quarter**  
- **Top 5 States by Total Sales**  
- **Total Sales by Region**  
- **Product Sales by Month**  
- **Total Sales by Sales Method**  
- **Total Profit by Sales Method**  
- **Unit Sold by Sales Method**  
- **Total Sales by Product**  
- **Average Price Per Unit by Product** (calculated as:  
  `Avg Price Per Unit = SUM(SportProducts[Total Sales]) / SUM(SportProducts[Units Sold])`)  

---

## **2. Project Goal**  
The main objective of this project is to analyze **Sports Product Sales** data to extract insights related to profitability, pricing, and sales performance. The focus is to visualize key business metrics using **Power BI** to aid decision-making.

The goal is to answer specific business questions like:  
- **How are sales distributed across regions and sales methods?**  
- **What are the trends in sales and profit over time?**  
- **How do product prices vary and impact sales?**

---

## **3. Dashboard Requirements**  
- **Sales & Profit Analysis** by Region and Quarter  
- **Top Products and States** by Total Sales  
- **Revenue and Profit Trends**  
- **Unit Sales by Different Methods**  
- **Product Sales and Pricing Analysis**

---

## **4. Dataset Details & Preparation**  
The dataset used for this analysis consists of sales data for sports products, including details on product sales, regions, pricing, and units sold. The data is stored in **Excel**, and all data cleaning, transformation, and analysis were conducted using **Power BI**.

---

## **5. Data Cleaning & Transformation**  
- Corrected column names and ensured data integrity by removing null values and duplicates.  
- Fixed the column name issue from `"Operating Proft"` to `"Operating Profit"`.  
- Used Power BI's data transformation tools to reshape and clean the data.  

---

## **6. Power BI Visualizations**  
After preparing the data, **Power BI** was used to create various visualizations to analyze and present the findings:  
- **Total Sales & Profit by Region and Quarter**: This chart provides insights into how sales and profit are distributed across different regions and quarters.  
- **Top 5 States by Total Sales**: Displays the states with the highest total sales.  
- **Total Sales by Region**: Visualizes the total sales by each region.  
- **Product Sales by Month**: Shows the sales performance for each product by month.  
- **Total Sales by Sales Method**: Analyzes how different sales methods contribute to the overall sales.  
- **Total Profit by Sales Method**: Provides insights into how sales methods influence profit.  
- **Unit Sold by Sales Method**: Analyzes units sold by different sales methods.  
- **Total Sales by Product**: Visualizes the sales of individual products.  
- **Average Price Per Unit by Product**: Shows the average price per unit for each product, calculated using the formula mentioned earlier.  

---

## **7. Python Analysis**

After loading the data into **Python** using **Pandas**, the following steps were performed:

### Step 1: **Data Type Summary**
We created a function `data_type_summary(df)` to display the **data types** of the columns and identify which columns are categorical and which are numerical. This helped us understand the structure of the data.

### Step 2: **Categorical Columns & Unique Values**
We wrote code to identify the **categorical columns** and display the **unique values** within those columns. This step is important for further analysis, especially for grouping and segmentation.

### Step 3: **Date Conversion**
We converted the `'Invoice Date'` column into a **datetime** format to facilitate time-based analysis:
```python
# Convert 'Invoice Date' to datetime
df['Invoice Date'] = pd.to_datetime(df['Invoice Date'])
```

### Step 4: **Data Type Conversion**
Several columns were converted to the appropriate data types:

```python
# Convert the 'Retailer ID' column to string type
df['Retailer ID'] = df['Retailer ID'].astype(str)

# Rename 'Operating Proft' column to 'Operating Profit'
df = df.rename(columns={'Operating Proft': 'Operating Profit'})
```

## Step 5: Extracting Year and Quarter
We extracted year and quarter information from the 'Invoice Date' column for time-based analysis:

```python
# Extracting year and quarter from invoice date
df['Year'] = df['Invoice Date'].dt.year
df['QuarterNum'] = df['Invoice Date'].dt.quarter
df['Quarter'] = 'Q' + df['QuarterNum'].astype(str)

# Creating a new column combining year and quarter
df['Year_Quarter'] = df['Year'].astype(str) + '-' + df['Quarter']
```

## Step 6: KPI Metrics Calculation
We calculated several Key Performance Indicators (KPIs):

```python
# KPI METRICS
total_sales = df['Total Sales'].sum()
total_profit = df['Operating Profit'].sum()
total_units_sold = df['Units Sold'].sum()
total_products = df['Product'].count()

print("--- KPI Summary ---")
print(f"Total Sales: ${total_sales:,.2f}")
print(f"Total Profit: ${total_profit:,.2f}")
print(f"Total Units Sold: {total_units_sold:,}")
print(f"Number of Product Records: {total_products:,.0f}")

avg_sales = df['Total Sales'].mean()
avg_profit = df['Operating Profit'].mean()
avg_units = df['Units Sold'].mean()
avg_price = df['Price per Unit'].mean()
avg_margin = df['Operating Margin'].mean()

print("\n--- KPI Averages ---")
print(f"Average Sales: ${avg_sales:,.2f}")
print(f"Average Profit: ${avg_profit:,.2f}")
print(f"Average Units Sold: {avg_units:.2f}")
print(f"Average Price per Unit: ${avg_price:.2f}")
print(f"Average Margin: {avg_margin:.2%}")
```

## Step 7: Custom Formatter for Plotting
For visualizations, we created a custom function to format large numbers in millions or thousands:

```python
from matplotlib.ticker import FuncFormatter

# --- Custom formatter to display values in millions, thousands, or as is --- 
def custom_formatter(x, pos):
    if x >= 1_000_000:
        return f'{x/1_000_000:.1f}M'  # For millions
    elif x >= 1_000:
        return f'{x/1_000:.0f}K'  # For thousands
    else:
        return f'{x:.0f}'  # For values less than 1,000
```

## 8. Business Insights, Recommendations & Conclusion

📌 **Revenue Trends**:  
- Sales and profits are positively correlated, indicating a steady demand for products across regions.  
- Certain regions show higher sales and profit margins, suggesting potential areas for targeted marketing.

📌 **Pricing Analysis**:  
- **Avg Price Per Unit** shows a direct relationship between product pricing and sales performance.  
- Consider adjusting pricing strategies for specific products based on the findings.

📌 **Sales Method Insights**:  
- **Sales Methods** significantly impact both sales and profit. Analyzing these trends will help optimize future sales strategies.

---

## 9. Technologies Used
- **Python** (for data cleaning, transformation, and KPI calculation)  
- **Power BI** (for data visualization and dashboard creation)  
- **Excel** (for initial dataset preparation and cleaning)  
- **Data Transformation & Cleaning** (using Power BI tools)

---

## 10. Final Thoughts  
This project demonstrates a comprehensive approach to analyzing sports product sales data, from cleaning and preparing the data to creating insightful visualizations. By utilizing **Power BI**, key business metrics were visualized effectively, helping to answer important business questions and providing recommendations for improving sales strategies.



