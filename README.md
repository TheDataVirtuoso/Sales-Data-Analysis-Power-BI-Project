# Sales Data Analysis

### Report Link :https://drive.google.com/file/d/1c3_ZIKjVXvIwrflrXtSzulbII_zZIdYe/view?usp=sharing

## Problem Statement

The goal of this project is to develop a comprehensive sales and profitability analysis system that allows business users to gain actionable insights into their financial performance over a specified period. This system aims to achieve the following objectives:



### - Objectives
- Calculate Total Sales:
 Accurately compute and display the total sales value for a selected period to provide a clear understanding of the overall revenue generated.

- Calculate Profit:
 Determine and visualize the total profit achieved based on the sales data, offering insights into the financial performance of the business.


- Analyze Orders
 Examine the number of orders placed during the selected period to identify sales patterns and order trends.

- Calculate Profit Margin:
Calculate and visualize the profit margin percentage to assess the profitability of products or services.

- Compare Sales by Product with Previous Year: 
 Evaluate the sales performance of each product by comparing the selected period's sales to those of the previous year, highlighting growth or decline trends.

- Compare Sales by Months with Previous Year: 
 Analyze sales performance across different months, comparing the selected period with the previous year to identify regions with significant changes.

- Display Top 5 Cities: 
 Create visualizations to showcase the top 5 cities based on sales, allowing users to quickly identify the most lucrative locations.

- Compare Profit by Channel with Previous Year: 
 Compare the profit generated by each sales channel between the selected period and the previous year, highlighting improvements or challenges in profitability.

- Analyze Sales by Customer and Compare with Previous Year: 
 Analyze sales data by customer to highlight the performance of individual customers and compare it to the previous year.

- Create Slicers for Date, City, Product, and Channel: 
 Develop interactive slicers for selecting specific dates, cities, products, and channels to enable dynamic filtering and personalized analysis.
 

### 2. DATA COLLECTION

- Data Source: Used a excel as a data connector to collect data.
- Loading Data: Loaded the data into Power BI for further processing and analysis.
  
  - Customers Data
  - Products Data
  - Region Data
  - Sales Data

### 3. DATA TRANSFORMATION

- Ensure Correct Data Types:
Verified that all data types are in the correct format.


- Data Validation:
Ensure that every row and Column has correct data

- Data Cleaning:
Rename the Column OrderDate to Order_Date

Calculating sales

    Add a Custom Column In Power Query:
    Order Quantity * Unit Selling Price
    Rename to Sales
    Convert to Decimal no.
    
Calculating Total Costs

    Add a Custom Column In Power Query:
    Unit Cost * Order Quantity
    Rename to Total Costs
    Convert to Decimal no.

Creating the Date Table using the following DAX:

    DAX DateTable = 
    ADDCOLUMNS (
    //CALENDAR(DATE(2020,1,1), DATE(2024,12,31)),
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Quarter", "Q" & FORMAT(CEILING(MONTH([Date])/3, 1), "#"),
    "Quarter No", CEILING(MONTH([Date])/3, 1),
    "Month No", MONTH([Date]),
    "Month Name", FORMAT([Date], "MMMM"),
    "Month Short Name", FORMAT([Date], "MMM"),
    "Month Short Name Plus Year", FORMAT([Date], "MMM,yy"),
    "DateSort", FORMAT([Date], "yyyyMMdd"),
    "Day Name", FORMAT([Date], "dddd"),
    "Details", FORMAT([Date], "dd-MMM-yyyy"),
    "Day Number", DAY ( [Date] )
    )

Mark the table as the Date table

 ### 4. DATA MODELLING
Creating relationships between the Sales Data table with: Products Data, Region Data and Customers Data

 ### 4. DAX MEASURES
Creating the following DAX Measures:

- Profit

Adding a   Column in the Sales Data table to calculate Profit:

     Profit = Sales_Data[Sales]-Sales_Data[Total_Costs]
        
- Sales


      Sales = SUM(Sales_Data[Sales])

- Sales Previous Year

      Sales PY = CALCULATE([Sales], SAMEPERIODLASTYEAR(DateTable[Date]))

- Sales vs PY

      Sales vs PY = [Sales] - [Sales PY]

- Sales vs py %

      Sales vs py % = DIVIDE([Sales vs PY],[Sales],0)

-  Products Sold

       Products Sold = SUM(Sales_Data[Order Quantity])

- Profit

      Profit = SUM(Sales_Data[Profit]

- Profit Last Year


  
      Profit LY = CALCULATE([Profit], SAMEPERIODLASTYEAR(DateTable[Date]))

- Profit Vs LY


      Profit Vs LY = [Profit]- [Profit LY]

- Profit Vs LY%


      Profit vs LY % = [Profit Vs LY]/[Profit]

- Profit Margin


      Profit Margin = DIVIDE([Profit],[Sales],0)

- Total Cost


      Total Cost = SUM(Sales_Data[Total Cost])                  
 ### 5. DATA VISUALIZATION
1. Key Performance Indicators (KPIs):

- Sales: 
Calculated and displayed total sales.

- Profit: 
 Calculated and displayed total profit.

- Profit Margin: 
 Calculated and displayed profit margin percentage.

- Product Sold:  
 Tracked and displayed the number of products sold.


snap of KPI's

![Screenshot 2024-05-25 102327](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/11b3f44a-c975-4f42-84ba-7b81bd83c29e)

2.  Slicers
 
     Implemented slicers for filtering data by Year, City, Product Name, and Channel to enable dynamic and personalized analysis.

Snap of Slicers:
![Screenshot 2024-05-25 102444](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/e2213ffb-e924-4f7d-aaf4-70981e1b3e9a)


3.  Combo Chart:    
          

       Created a combo chart to display sales in the current year (CY) and the previous year (PY), allowing for a visual comparison of sales performance over time.

Snap of Combo chart
![Screenshot 2024-05-25 102539](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/7e6ca6da-4105-4012-b0c1-5bcd70208c77)

4. Line Chart:

Developed a line chart to show sales trends in the CY and PY, providing a clear visualization of sales patterns over time.


Snap of Line Chart

![Screenshot 2024-05-25 102602](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/dfa862bf-6ffb-4ec5-a5bc-ca937a1498db)


5. Donut Chart:

Created a donut chart to display the top 5 cities by sales, highlighting the most lucrative locations.


Snap of Donut Chart

![Screenshot 2024-05-25 102640](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/95e2f9be-41de-4add-b757-2b4229f5756c)



6. Area Chart:

Designed an area chart to show CY profit, PY profit, and channel profit margin, offering a comprehensive view of profitability over time and by channel.


Snap of Area Chart

![Screenshot 2024-05-25 102711](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/6443649d-b1f1-4798-927d-f892b3a8bad3)


7. Clustered Bar Chart:

Developed a clustered bar chart to compare sales in the CY and PY by customer name, identifying key customers and their sales performance year over year.


Snap of Clustered Bar Chart
![Screenshot 2024-05-25 102731](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/1e65c74c-ff41-4b81-b787-89d47443d09f)


 Build Aesthetics:

Canvas Background:
I changed the canvas background using MS PowerPoint to enhance the visual appeal.

I ensured that the background complemented the overall theme and was not too distracting.

 Interactivity:

Edit Interactions:
I enabled edit interactions to ensure every visual was interactive with each other.
This ensured that selections in one visual filtered the data in the other visuals, providing a more dynamic and insightful user experience.

 # Report Snapshot (Power BI DESKTOP)

 
![SALES REPORT](https://github.com/TheDataVirtuoso/Patient-Waitlist--Power-BI-project/assets/87636760/89972367-da4a-4b36-9f65-8cd3f997436f)


# Insights 

A One page report was created on Power BI Desktop 

Following inferences can be drawn from the report;

### Financial Performance Summary

    Total Sales: $154.6 million

    Total Profit: $57.8 million

    Profit Margin: 37.4%

    Products Sold: 67.6K units

    Top Sales by City: Christchurch: $11.5 million

    Top Customer by Sales: Medline Customer:
    
    Top Product by Sales: Product 7: $8.3 million

    Top Channel by Sales and Profit:
    
             Wholesale: Sales of $83 million and profit of $30.7 million
    Lowest Sales and Profit Channel:

             Export: Sales of $22.6M and profit of $8.6M 

    Sales Performance:

        Overall sales decreased by more than 10%
        A drop in sales for all the top 7 products
        Four key customers are leading to the drop in sales

    Profit Margin by Channel:

        Higher profit margin in the Export channel

# Recommendations

### [1] Investigate the Decline in Sales:



  Root Cause Analysis: Conduct a thorough analysis to understand why there is a significant decrease in sales, especially focusing on the top 7 products and the four key customers contributing to this decline.

Customer Feedback: Collect feedback from these customers to identify any issues or dissatisfaction that may be causing the drop.



  ### [2] Revise Marketing and Sales Strategies:
  
Targeted Campaigns: Develop targeted marketing campaigns aimed at reviving sales of the top 7 products and re-engaging the four key customers


Promotions and Discounts: Offer promotions or discounts on products experiencing a decline in sales to stimulate demand.

 ### [3] Optimize Product Portfolio:
Product Analysis: Evaluate the performance of all products, not just the top sellers, to identify any potential areas for improvement or discontinuation.

New Product Development: Consider developing or introducing new products to diversify the product portfolio and attract new customers.


### [4]Expand Profitable Channels:

Wholesale Focus: Since the Wholesale channel is performing well, explore opportunities to further expand this channel.

Optimize Export Channel: Although the Export channel has the lowest sales and profit, its higher profit margin suggests potential. Investigate ways to boost sales in this channel without compromising the profit margin.

### [5] Enhance Customer Relationships:

Customer Loyalty Programs: Implement loyalty programs to retain key customers and incentivize repeat purchases.

Personalized Communication: Utilize personalized communication strategies to strengthen relationships with high-value customers.
    

### [6] Improve Sales in Underperforming Regions:

Regional Strategies: Develop tailored strategies for regions with declining sales to address specific local market conditions.

Top City Performance: Leverage the success of Christchurch to replicate strategies in other cities.

