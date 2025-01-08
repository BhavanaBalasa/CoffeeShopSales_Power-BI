# CoffeeShopSales_Power-BI
## Description:
   This project involved designing and implementing an advanced-level Power BI Sales Analysis Dashboard for a dataset with over 149,000 transactions from multiple coffee shop locations. Developed complex DAX measures for dynamic and insightful KPIs, Utilized a variety of charts to present data in a visually appealing and easy-to-understand format, implemented custom tooltips to provide additional context for visualizations,Created a Date Table with rich dimensions to analyze sales trends at various levels (daily, monthly, yearly).
## Bussiness Problem:
    Coffee shop businesses thrive on understanding customer behavior, product performance, and sales trends across locations. 
    With 149,116 detailed transaction records, this dataset provides an opportunity to gain insights into sales performance, 
    customer preferences, and operational efficiency at various coffee shop locations.
## About Dataset
    The dataset titled "Coffee Shop Sales" is structured with 149,116 entries, detailing transactions at various coffee shop locations.
    Here's a breakdown of the information available in the dataset:
- 	transaction_id: A unique identifier for each transaction.
- 	transaction_date: The date when the transaction occurred.
- 	transaction_time: The time at which the transaction took place.
- 	transaction_qty: Quantity of the product purchased in each transaction.
- 	store_id: A unique identifier for the store where the transaction took place.
- 	store_location: The physical location of the store.
- 	product_id: A unique identifier for the product sold.
- 	unit_price: The price per unit of the product.
   	product_category: The broad category of the product (e.g., Coffee, Tea, Drinking Chocolate).
- 	product_type: More specific type of product within the category (e.g., Gourmet brewed coffee, Brewed Chai tea).
- 	product_detail: Detailed description of the product (e.g., Ethiopia Rg, Spicy Eye Opener Chai Lg).
## Data Cleaning:
    The dataset required minimal cleaning, with the primary focus being the correction of data types for several columns to ensure proper analysis.
    Below is a summary of the data type adjustments:
### Conversion of Dates and Times:
-    transaction_date: Converted from string to datetime format for proper time-based analysis.
-    transaction_time: Converted from string to time format to allow aggregation by time of day.
### Numeric Conversions:
-   transaction_qty: Ensured this column is in integer format.
-   unit_price: Converted to float for calculations and analysis.
### Categorical Columns:
-   store_id, store_location, product_id, product_category, product_type, and product_detail: Converted to categorical data type to optimize memory usage and improve processing efficiency.
## Data Modeling:
### Date Table Creation and Relationship Setup in Power BI
    To enable efficient time-based analysis of the sales data, a Date Table was created in Power BI using DAX. 
    This table includes several useful columns to support detailed reporting and analysis.
### Dax:
    DateTable = CALENDAR(MIN(TransactionTable[transaction_date]), MAX(TransactionTable[transaction_date]))
    Month = FORMAT('Date Table'[Date],"mmm")
    Month number = MONTH('Date Table'[Date])
    Month Year = FORMAT('Date Table'[Date],"mmm yyyy")
    Day Name = FORMAT('Date Table'[Date],"DDD")
    Week num = WEEKNUM('Date Table'[Date],2)
    Day No = DAY('Date Table'[Date])
    Week Day Num = WEEKDAY('Date Table'[Date],2)
    WeekDay/Weekend = IF('Date Table'[Day Name] = "Sat" || 'Date Table'[Day Name] = "Sun","Weekend","Weekday")
### Created Relationships with the Transaction Table
-   Established a one-to-many relationship between the Date column in the Date Table and the transaction_date column in the Transaction Table.
-   Ensured the relationship is active and enabled cross-filtering for seamless analysis.

![](https://github.com/BhavanaBalasa/CoffeeShopSales_Power-BI/blob/main/PowerBI%20Model.png)

## Calculated Measures Creation in Power BI Used in Report:
    To derive meaningful insights and support dynamic reporting, numerous calculated measures were created using DAX. These measures provide key performance indicators (KPIs) and used in different charts some of them are:
-  Mom Growth & Diff Orders = 
    VAR month_diff=[CM Orders]-[PM Orders]
    VAR mom_per=month_diff/[PM Orders]
    VAR _sign=IF(mom_per>0,"+","")
    VAR sign_trend=IF(mom_per>0,"▲","▼")
    RETURN
    IF([PM Orders],
    sign_trend & " " & _sign & FORMAT(mom_per,"#0.0%") & " | " & _sign & FORMAT(month_diff/1000,"0.0K") & " " & "vs LM","No PM Data")
-  MoM Growth & Diff Qty = 
    VAR month_diff=[CM Qty]-[PM Qty]
    VAR month_diff_per=month_diff/[PM Qty]
    VAR _sign=IF(month_diff>0,"+","")
    VAR sign_trend=IF(month_diff>0,"▲","▼")
    RETURN
    IF([PM Qty],
    sign_trend & " " & _sign & FORMAT(month_diff_per,"#0.0%") & " " & "|" & " " & _sign & FORMAT(month_diff/1000,"#0.0K") & " vs LM","No PM Data")
## Final Report:

![](https://github.com/BhavanaBalasa/CoffeeShopSales_Power-BI/blob/main/CoffeeSalesReport.png)

## Learnings:
-  Different ways of using DAX to represent the data and provide insights to the customer.
-  To represent the charts in a meaningful.
-  In-depth properties under each chart to format them. 
