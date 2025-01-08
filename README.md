# CoffeeShopSales_Power-BI
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
## Modelling:
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

![]()
