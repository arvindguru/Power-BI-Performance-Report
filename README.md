# Plant Co. Gross Profit Performance 2023

## Overview
This Power BI report provides an in-depth analysis of the gross profit performance for Plant Co. in the year 2023. It focuses on key performance metrics such as year-to-date (YTD) gross profit, prior year-to-date (PYTD) comparisons, and gross profit percentage (GP%). The report is designed to help stakeholders monitor financial performance, track profitability trends, and analyze profitability across different products, regions, and time periods.

## Key Features
- **YTD and PYTD Gross Profit**: Displays year-to-date gross profit compared to the prior year-to-date, highlighting the difference (YTD vs PYTD).
- **Gross Profit Segmentation**: Provides insights into gross profit based on month, region, and product category.
- **Bottom 10 Countries**: A treemap visual showcasing the bottom 10 countries by YTD performance.
- **Gross Profit Trends**: Month-by-month trend analysis of gross profit for different product types (Indoor, Landscape, Outdoor).
- **Profitability Segmentation**: A scatter plot showing account profitability segmentation by GP% and Gross Profit (SW_YTD).
- **KPIs**: Key performance indicators (KPIs) showing YTD, PYTD, and GP% for quick reference.

## Data Source
- **Fact_Sales**: Captures individual sales transactions with fields like `Date_Time`, `SalesAmount`, `GrossProfit`, `Product_Type`, and `Country`.
- **Dim_Date**: The date dimension table used for time series analysis, supporting YTD and PYTD calculations.
- **Dim_Product**: The product dimension table categorizes the product types (Indoor, Outdoor, Landscape).
- **Dim_Region**: A geographic dimension table mapping countries to regions.

## Visualizations
### 1. **Bottom 10 YTD vs PYTD - Country**
- **Type**: Treemap
- **Purpose**: Displays the bottom 10 countries by gross profit performance. The size of each block represents the total YTD profit or loss for each country.
- **Insight**: Helps identify countries that are underperforming compared to others, with China being the largest loss in the given period.

### 2. **Gross Profit YTD vs PYTD by Month - Country - Product**
- **Type**: Waterfall Chart
- **Purpose**: Shows the monthly changes in gross profit across different countries and product categories. The green bars represent an increase in profit, while red bars represent a decrease.
- **Insight**: Provides a clear month-over-month breakdown of performance, identifying the months with the most significant changes.

### 3. **Gross Profit YTD & PYTD by Month**
- **Type**: Line & Stacked Column Chart
- **Purpose**: Displays the YTD gross profit and compares it to PYTD for different months of the year. A line graph overlays the gross profit trends for a clearer view.
- **Insight**: Tracks the performance of different product types (Indoor, Landscape, Outdoor) over the months and compares it to the previous year.

### 4. **Account Profitability Segmentation | GP% and Gross Profit**
- **Type**: Scatter Chart
- **Purpose**: Shows account segmentation based on gross profit and GP% for each account, allowing users to analyze which accounts are contributing the most to profitability.
- **Insight**: The scatter plot helps identify outliers, such as accounts with high gross profit but low GP%, or vice versa.

### 5. **KPIs:**
- **Type**: Card
- **YTD**: $5.15M
- **YTD vs PYTD**: -$265.29K
- **PYTD**: $5.42M
- **GP%**: 39.62%
- These KPIs provide an at-a-glance summary of the gross profit performance.

### DAX Formulas
Here are some of the DAX formulas used in the report to show a few:

- **Gross Profit YTD**:
  ```DAX
  YTD Gross Profit = TOTALYTD([Gross Profit],Fact_Sales[Date_Time])  
- **Gross Profit PYTD**:
  ```DAX
  PYTD Gross Profit = CALCULATE([Gross Profit],SAMEPERIODLASTYEAR(Dim_date[Date]),Dim_date[Checkdate] = TRUE)
- **Switch PYTD**:
  ```DAX
  SW_PYTD = 
    VAR selected_value = SELECTEDVALUE(Slc_value[Values])
    VAR result = SWITCH(
        selected_value,
        "Sales", [PYTD Sales],
        "Quantity", [PYTD Quantity],
        "Gross Profit", [PYTD Gross Profit],
        BLANK()
    )
    RETURN result
- **Switch YTD vs PYTD**:
  ```DAX
  YTD vs PYTD = Measures_[SW_YTD] - Measures_[SW_PYTD]
- **Gross Profit in %**:
  ```DAX
  GP% = DIVIDE([Gross Profit],[Sales])
- **Waterfall dynamic title**:
  ```DAX
  _Waterfall title = 
    SELECTEDVALUE(Slc_value[Values]) & " YTD vs PYTD | " &
    SELECTEDVALUE(Dim_date[Date].[Month]) & " | " &
    SELECTEDVALUE(Dim_Account[country]) & " | " &
    SELECTEDVALUE(Dim_Product[Product_Type])
## Screenshots

### Gross Profit For The Year 2023
![1](https://github.com/user-attachments/assets/ed9abea4-72b1-4799-9497-02fcbbe08e66)

### Gross Profit for 2023 with a drill-down by product type in a waterfall chart
![1 4](https://github.com/user-attachments/assets/1eda0222-ba2e-42ef-b3de-77b2d1add5ab)

### Gross Profit YTD & PYTD | Month
![3](https://github.com/user-attachments/assets/aee864cb-9cc3-451c-a10f-0c6449449877)

## How to Use
- Download the .pbix file from this repository.
- Open the file using Power BI Desktop.
- Explore the dashboard using slicers and interactive visuals.
- Use filters to drill down into specific data points, such as product categories or regions.








