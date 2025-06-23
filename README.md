# 👟 Adidas_Sales_Analysis 
Power BI dashboard analysing Adidas sales in the USA (2020-2021)

## Overview
A Power BI project analysing Adidas sales data for 2020-2021. 
The dashboard explores key business areas such as regional performance, product profitability, sales method performance, sales trends over time and retailer analysis.


## Tools Used
- Power BI, DAX, Power Query


## Dataset Information

**Source:** [Adidas Sales Dataset (via Kaggle)](https://www.kaggle.com/datasets/heemalichaudhari/adidas-sales-dataset)   
**Years Covered:** 2020–2021   
**File Format:** CSV  
**Key Fields:** 
- Region/State/City, Product, Sales Method
- Units Sold, Total Sales, Operating Profit
- Retailer, Invoice Date


## Data Cleaning Steps
- Removed missing values to ensure clean analysis
- Removed duplicates
- Corrected data types
- Standardised columns for consistency
- Extracted new fields (Year, Month) using Power Query to support time analysis


## DAX Measures Used
- **Total Sales**  
  Total_Sales = SUM('Data Sales Adidas'[Total Sales])  

- **Total Profit**  
  Total_Profit = SUM('Data Sales Adidas'[Operating Profit])  

- **Units & Margins**  
  Total_Units = SUM('Data Sales Adidas'[Units Sold])  
  Avg_Margin = AVERAGE('Data Sales Adidas'[Operating Margin])  

- **Sales by Method**  
  Sales by Method = SUMX(FILTER('Data Sales Adidas', 'Data Sales Adidas'[Sales Method] = "Online"), 'Data Sales Adidas'[Total Sales])  

- **Date Table**  
  Date Table = CALENDAR(MIN('Data Sales Adidas'[Invoice Date]), MAX('Data Sales Adidas'[Invoice Date]))  

- **Year-on-Year Profit % Growth**  
  YoY Profit Growth % =   
  VAR CurrentYearProfit = CALCULATE([Total_Profit], 'Date Table'[Year] = 2021)  
  VAR LastYearProfit = CALCULATE([Total_Profit], 'Date Table'[Year] = 2020)  
  RETURN DIVIDE(CurrentYearProfit - LastYearProfit, LastYearProfit)  

- **Top Retailer & Sales**  
  Top Retailer Sales =   
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
    - Visualised with an interactive map with a custom tooltip, column charts and a scatter plot, as well as slicers for easy filtering by state, city, year or product
- Profitability across online vs offline sales methods
    - Doughnut chart showing shares
- Monthly sales trends and YoY comparisons
    - Conditionally formatted clustered bar chart, a card, line charts and a slicer for retailers
- Top-performing retailers and operating margins
    - Conditionally formatted clustered bar charts, cards and a table


## Key Insights
- The West is the region with the most sales over the period, with Nevada dominating in 2020 and California in 2021 and overall
- Men's streetwear is the best-selling product, and women's apparel is the most profitable
- Less than a 3rd of the sales were made online (27.52%), with the remaining 72.48% being in-store and outlet, highlighting the improtance of in-store presence
- Sales and profit grew by 3.24% YoY from 2020 to 2021, suggesting a recovery or growth trend
- West Gear is the top retailer (243M), followed closely by Foot Locker (220M)


## Dashboard Preview

<p align="center">
  <img src="https://github.com/user-attachments/assets/73c6b9da-319d-401d-838d-8cecfbfadf98" width="300" alt="Regional Performance Page" />
  <img src="https://github.com/user-attachments/assets/7535a811-3db4-4a46-a2e0-29eb255e3d8f" width="300" alt="Product and Sales Method Analysis Page" />
  <br>
  <img src="https://github.com/user-attachments/assets/fc6fa827-ee45-4e1a-894c-df6b25cb6cb5" width="300" alt="Trends Over Time Page" />
  <img src="https://github.com/user-attachments/assets/2cfd93e5-90b3-46cf-97c9-560b370e7b61" width="300" alt="Top Retailer Page" />
</p>

