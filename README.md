# DAX Queries for Power BI

Welcome to the guide on **DAX Queries for Power BI**! This README is designed to help you understand complex DAX queries in a simple and easy-to-follow format. We will cover essential DAX concepts, syntax, and examples to help you master querying in Power BI.

---

## What is DAX?
**DAX (Data Analysis Expressions)** is a formula language used in Power BI, Power Pivot, and SQL Server Analysis Services to perform calculations and data analysis on your data models. DAX enables you to create measures, calculated columns, and tables to extract meaningful insights.

---

## Key DAX Concepts

### 1. **Calculated Columns**
Calculated columns allow you to add new data to your existing table based on calculations or expressions.

#### Syntax:
```DAX
ColumnName = TableName[Column1] + TableName[Column2]
```

#### Example:
If you have a `Sales` table with `Price` and `Quantity` columns, you can calculate the total sales for each row:
```DAX
TotalSales = Sales[Price] * Sales[Quantity]
```

---

### 2. **Measures**
Measures are calculations used in aggregation (e.g., summing up, averaging) and are optimized for performance.

#### Syntax:
```DAX
MeasureName = SUM(TableName[ColumnName])
```

#### Example:
To calculate the total revenue from your `Sales` table:
```DAX
TotalRevenue = SUM(Sales[TotalSales])
```

---

### 3. **Filtering with CALCULATE**
The `CALCULATE` function modifies the filter context for calculations.

#### Syntax:
```DAX
CALCULATE(Expression, Filter1, Filter2, ...)
```

#### Example:
To calculate revenue only for "Electronics":
```DAX
ElectronicsRevenue = CALCULATE(SUM(Sales[TotalSales]), Sales[Category] = "Electronics")
```

---

### 4. **Time Intelligence Functions**
DAX provides functions to work with dates and time, such as year-to-date (YTD), month-to-date (MTD), and more.

#### Syntax:
```DAX
TOTALYTD(Expression, DatesColumn, [Filter])
```

#### Example:
To calculate year-to-date sales:
```DAX
YTD_Sales = TOTALYTD(SUM(Sales[TotalSales]), Sales[Date])
```

---

### 5. **IF Statements**
The `IF` function allows you to implement conditional logic in your queries.

#### Syntax:
```DAX
IF(Condition, Result_If_True, Result_If_False)
```

#### Example:
To create a column that flags sales over $500:
```DAX
HighValueSale = IF(Sales[TotalSales] > 500, "High", "Low")
```

---

### 6. **RELATED Function**
The `RELATED` function fetches data from a related table.

#### Syntax:
```DAX
RELATED(ColumnName)
```

#### Example:
If you have a `Products` table related to a `Sales` table, you can fetch the product category:
```DAX
ProductCategory = RELATED(Products[Category])
```

---

### 7. **ALL Function**
The `ALL` function removes filters from a column or table.

#### Syntax:
```DAX
ALL(TableName[ColumnName])
```

#### Example:
To calculate a percentage of total sales:
```DAX
SalesPercentage = DIVIDE(SUM(Sales[TotalSales]), CALCULATE(SUM(Sales[TotalSales]), ALL(Sales)))
```

---

### 8. **RANKX Function**
The `RANKX` function ranks rows in a table based on an expression.

#### Syntax:
```DAX
RANKX(Table, Expression, [Value], [Order])
```

#### Example:
To rank products by sales:
```DAX
SalesRank = RANKX(ALL(Sales[Product]), SUM(Sales[TotalSales]),, DESC)
```

---

### 9. **SUMX Function**
The `SUMX` function evaluates an expression for each row in a table and returns the sum of those values.

#### Syntax:
```DAX
SUMX(Table, Expression)
```

#### Example:
To calculate total sales for each region:
```DAX
RegionSales = SUMX(Sales, Sales[Price] * Sales[Quantity])
```

---

### 10. **LOOKUPVALUE Function**
The `LOOKUPVALUE` function returns the value of a column for a row that meets specified criteria.

#### Syntax:
```DAX
LOOKUPVALUE(Result_ColumnName, Search_ColumnName, Search_Value)
```

#### Example:
To fetch the manager name for a given employee:
```DAX
ManagerName = LOOKUPVALUE(Employees[Manager], Employees[EmployeeID], Sales[EmployeeID])
```

---

### 11. **DISTINCT Function**
The `DISTINCT` function returns a one-column table with unique values.

#### Syntax:
```DAX
DISTINCT(TableName[ColumnName])
```

#### Example:
To get a list of unique product categories:
```DAX
UniqueCategories = DISTINCT(Products[Category])
```

---

### 12. **VALUES Function**
The `VALUES` function returns a one-column table with unique values, including blank.

#### Syntax:
```DAX
VALUES(TableName[ColumnName])
```

#### Example:
To find distinct years in a date column:
```DAX
DistinctYears = VALUES(Sales[Year])
```

---

### 13. **CONCATENATE Function**
The `CONCATENATE` function joins two text strings into one.

#### Syntax:
```DAX
CONCATENATE(Text1, Text2)
```

#### Example:
To combine first and last names:
```DAX
FullName = CONCATENATE(Employees[FirstName], " " & Employees[LastName])
```

---

### 14. **CONCATENATEX Function**
The `CONCATENATEX` function concatenates the result of an expression evaluated for each row in a table.

#### Syntax:
```DAX
CONCATENATEX(Table, Expression, [Delimiter])
```

#### Example:
To concatenate product names with a comma:
```DAX
ProductList = CONCATENATEX(Products, Products[ProductName], ", ")
```

---

### 15. **COUNTROWS Function**
The `COUNTROWS` function counts the number of rows in a table.

#### Syntax:
```DAX
COUNTROWS(TableName)
```

#### Example:
To count the total number of orders:
```DAX
TotalOrders = COUNTROWS(Sales)
```

---

### 16. **COUNT Function**
The `COUNT` function counts the number of non-blank values in a column.

#### Syntax:
```DAX
COUNT(ColumnName)
```

#### Example:
To count the number of products sold:
```DAX
ProductsSold = COUNT(Sales[ProductID])
```

---

### 17. **AVERAGE Function**
The `AVERAGE` function calculates the average of a column.

#### Syntax:
```DAX
AVERAGE(ColumnName)
```

#### Example:
To find the average sales amount:
```DAX
AverageSales = AVERAGE(Sales[TotalSales])
```

---

### 18. **AVERAGEX Function**
The `AVERAGEX` function calculates the average of an expression evaluated for each row in a table.

#### Syntax:
```DAX
AVERAGEX(Table, Expression)
```

#### Example:
To calculate the average revenue per order:
```DAX
AverageRevenue = AVERAGEX(Sales, Sales[Price] * Sales[Quantity])
```

---

### 19. **DIVIDE Function**
The `DIVIDE` function performs division and handles divide-by-zero errors.

#### Syntax:
```DAX
DIVIDE(Numerator, Denominator, [AlternateResult])
```

#### Example:
To calculate profit margin:
```DAX
ProfitMargin = DIVIDE(Sales[Profit], Sales[TotalSales], 0)
```

---

### 20. **ISBLANK Function**
The `ISBLANK` function checks whether a value is blank.

#### Syntax:
```DAX
ISBLANK(Value)
```

#### Example:
To flag orders with no discount applied:
```DAX
NoDiscount = IF(ISBLANK(Sales[Discount]), "No", "Yes")
```

---

## Tips for Writing DAX Queries
- **Start simple**: Break down complex calculations into smaller steps.
- **Understand filter context**: Filters applied in visuals or relationships affect your calculations.
- **Test incrementally**: Use tools like DAX Studio for debugging.

---
