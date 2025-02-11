# 📊 Power BI Dashboard - Sales Performance Analysis

## 📌 Project Overview
This Power BI dashboard provides an interactive analysis of sales performance, comparing **Year-to-Date (YTD) vs. Prior Year-to-Date (PYTD)** values. It helps in tracking **gross profit, sales quantity, and profitability trends** across different months, product types, and accounts.

## 📂 Data Sources & Structure
- **Dataset:** Sales data including revenue, profit, and account performance.
- **Main Fields:**
  - `Date` (Month-Year format)
  - `Country` (Sales region)
  - `Product Type` (Indoor, Landscape, Outdoor)
  - `Sales` (YTD & PYTD values)
  - `Gross Profit (GP%)`
  - `Account-Based Sales Performance`

## 📊 Key Insights & Visuals
1. **KPI Cards**
   - **YTD Sales:** $13.00M
   - **PYTD Sales:** $13.51M
   - **YTD vs PYTD Difference:** -$512.26K
   - **Gross Profit % (GP%):** 0.40

2. **YTD vs. PYTD by Month**
   - Highlights **monthly increases and decreases in sales.**
   - Key months with major fluctuations are visually represented in red (decrease) and green (increase).

3. **Sales Breakdown by Country**
   - **China, Poland, and Sweden** are among the bottom regions with lowest sales.
   - **Treemap visualization** categorizes sales across multiple countries.

4. **Product Type Analysis**
   - Sales breakdown across **Indoor, Landscape, and Outdoor** product categories.
   - Compares YTD and PYTD values to show performance trends.

5. **Account-Wise Sales & GP% Analysis**
   - Scatter plot to analyze **sales trends across different accounts**.
   - Shows correlation between `S_YTD` (Sales YTD) and `GP%` (Gross Profit %).

## 🔢 Key DAX Measures Used
1. **YTD Calculation**
   ```DAX
   YTD_GrossProfit = TOTALYTD([Gross_Profit],Fact_sales[Date_Time])
   YTD_Quantity = TOTALYTD([Quantity],Fact_sales[Date_Time])
   YTD_Sales = TOTALYTD([Sales],Fact_sales[Date_Time])

2. **SWITCH Calculation**
 ```S_PYTD =
VAR selected_value = SELECTEDVALUE(Slc_Values[Values]) 
 VAR result = SWITCH(selected_value,
    "Sales", [PYTD_Sales],
    "Quantity",[PYTD_Quantity],
    "Gross Profit",[PYTD_GrossProfit],
    BLANK()
    )
    RETURN
    result


    S_YTD = 
VAR selected_value = SELECTEDVALUE(Slc_Values[Values])
VAR result = SWITCH(selected_value,
    "Sales", [YTD_Sales],
    "Quantity",[YTD_Quantity],
    "Gross Profit",[YTD_GrossProfit],
    BLANK()
    )
    RETURN
    result

    YTD vs PYTD = [S_YTD] - [S_PYTD]```

  3.**PYTD**
   DAX
   ``` PYTD_GrossProfit = 
CALCULATE(
    [Gross_Profit], 
    SAMEPERIODLASTYEAR(Dim_Date[Date]), 
    Dim_Date[Inpast] = TRUE
)

PYTD_Quantity = 
CALCULATE(
    [Quantity], 
    SAMEPERIODLASTYEAR(Dim_Date[Date]), 
    Dim_Date[Inpast] = TRUE
)

PYTD_Sales = 
CALCULATE(
    [Sales], 
    SAMEPERIODLASTYEAR(Dim_Date[Date]), 
    Dim_Date[Inpast] = TRUE
)

    
