# 👟 Adidas_Sales_Analysis 
Power BI dashboard analysing Adidas sales in the USA (2020-2021)

## Overview
A Power BI project analysing Adidas sales data for 2020-2021. 
The dashboard explores key business areas such as regional performance, product profitability, sales method performance, sales trends over time and retailer analysis.

## Tools Used
- Power BI, DAX, Power Query


## Data Cleaning Steps
- Removed missing values
- Removed duplicates
- Fixed data types
- Standardised columns
- Extracted useful data and added it to additional columns to facilitate better analysis

## DAX Measures Used
- Total_Sales = SUM('Data Sales Adidas'[Total Sales])
- Total_Sales_Rounded = FORMAT(ROUND(SUM('Data Sales Adidas'[Total Sales]), 0), "#,##0")
- Total_Profit = SUM('Data Sales Adidas'[Operating Profit])
- Total_Units = SUM('Data Sales Adidas'[Units Sold])
- Avg_Margin = AVERAGE('Data Sales Adidas'[Operating Margin])
- Date Table = CALENDAR(MIN('Data Sales Adidas'[Invoice Date]), MAX('Data Sales Adidas'[Invoice Date]))
- Sales by Method = SUMX(FILTER('Data Sales Adidas', 'Data Sales Adidas'[Sales Method] = "Online"), 'Data Sales Adidas'[Total Sales])
- YoY Profit = CALCULATE([Total_Profit], SAMEPERIODLASTYEAR('Date Table'[Date]))
- YoY Profit Growth % = 
VAR CurrentYearProfit = CALCULATE([Total_Profit], 'Date Table'[Year] = 2021)
VAR LastYearProfit = CALCULATE([Total_Profit], 'Date Table'[Year] = 2020)

RETURN
DIVIDE(CurrentYearProfit - LastYearProfit, LastYearProfit)
- Top Retailer = CALCULATE(MAX('Data Sales Adidas'[Retailer]), FILTER('Data Sales Adidas', 'Data Sales Adidas'[Total Sales] = MAX('Data Sales Adidas'[Total Sales])))
- Top Retailer Sales = 
VAR SelectedRetailer = 
    CALCULATE(
        MAX('Data Sales Adidas'[Retailer]),
        FILTER(
            'Data Sales Adidas',
            'Data Sales Adidas'[Total Sales] = CALCULATE(MAX('Data Sales Adidas'[Total Sales]))
        )
    )
RETURN 
    CALCULATE(
        [Total_Sales],
        'Data Sales Adidas'[Retailer] = SelectedRetailer
    )


## Analysis and Charts
The report answers key business questions for Adidas, using interactive visuals and calculated measures, providing insights on:
- Products and regions that drive the most sales
    - Visualised with an interactive map with a custom tooltip, column charts and a scatter plot, as well as slicers for easy filtering by state, city and year
- Profitability across online vs offline sales methods
    - Doughnut chart
- Monthly sales trends and YoY comparisons
    - Conditionally formatted clustered bar chart, a card, line charts and a slicer
- Top-performing retailers and operating margins
    - Conditionally formatted clustered bar charts, cards and a table


## Dashboard Preview

<p align="center">
  <img src="![image](https://github.com/user-attachments/assets/73c6b9da-319d-401d-838d-8cecfbfadf98)" width="250"/>
  <img src="![image](https://github.com/user-attachments/assets/7535a811-3db4-4a46-a2e0-29eb255e3d8f)" width="250"/>
  <img src="![image](https://github.com/user-attachments/assets/fc6fa827-ee45-4e1a-894c-df6b25cb6cb5)" width="250"/>
  <img src="![image](https://github.com/user-attachments/assets/2cfd93e5-90b3-46cf-97c9-560b370e7b61)" width="250"/>
</p>


## Key Insights
- The West is the region with the most sales over the period, with Nevada being the leading state in 2020 and California in 2021 and for the total period
- Men's streetwear is the best-selling product, and women's apparel is the most profitable
- Less than a 3rd of the sales were made online (27.52%), with the remaining 72.48% being in-store and outlet
- 2021 has seen a significant growth in sales and profit compared to 2020, with 3.24% YoY growth. Women's apparel is the most profitable product at 4.1%.
- West Gear is the top retailer (243M), followed closely by Foot Locker (220M)


## Dataset Information

**Source:** [Adidas Sales Dataset (via Kaggle)](https://www.kaggle.com/datasets/heemalichaudhari/adidas-sales-dataset)   
**Years Covered:** 2020–2021   
**File Format:** CSV  
**Key Fields:** 
- Region/State/City, Product, Sales Method
- Units Sold, Total Sales, Operating Profit
- Retailer, Invoice Date





