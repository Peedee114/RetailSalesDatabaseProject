# Retail Sales Analytics Dashboard (SQL Server + Power BI)

## Dashboard Preview

![Retail Dashboard](RetailSalesDatabaseProject/RetailDashboard.png)
## Overview

This project demonstrates how relational sales data stored in a SQL database can be transformed into an interactive analytics dashboard. The workflow covers database design, data modelling, and business intelligence visualisation.

A small retail dataset was created using SQL Server and then connected to Power BI to produce a dashboard that highlights sales performance across regions, products, and time.

The goal of the project is to show how transactional data can be structured and analysed to generate meaningful business insights.

---

# Technologies Used

## Database

* Microsoft SQL Server
* SQL Server Management Studio (SSMS)

These tools were used to:

* Design the relational database schema
* Create tables and relationships
* Insert sample transactional data
* Store and manage the dataset used in the dashboard

## Data Visualisation

* Power BI Desktop

Power BI was used to:

* Connect to the SQL Server database
* Create relationships between tables
* Define business measures
* Build an interactive dashboard for analysis

---

# Database Schema

The project simulates a simplified retail sales system using four tables.

### Tables

| Table        | Description                        |
| ------------ | ---------------------------------- |
| Customers    | Stores customer information        |
| Products     | Stores product catalogue data      |
| Orders       | Stores order records               |
| OrderDetails | Stores the items within each order |

This structure follows a typical **transactional retail schema** where customers place orders and each order contains one or more products.

---

# SQL Code

## Creating the Tables

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY IDENTITY(1,1),
    CustomerName VARCHAR(100),
    Region VARCHAR(50),
    JoinDate DATE
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY(1,1),
    ProductName VARCHAR(100),
    Category VARCHAR(50),
    Price DECIMAL(10,2)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY IDENTITY(1,1),
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

CREATE TABLE OrderDetails (
    OrderDetailID INT PRIMARY KEY IDENTITY(1,1),
    OrderID INT,
    ProductID INT,
    Quantity INT,
    TotalAmount DECIMAL(10,2),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```

---

## Inserting Sample Data

```sql
INSERT INTO Customers (CustomerName, Region, JoinDate)
VALUES
('Alice Smith','London','2023-01-10'),
('John Lee','Manchester','2023-02-15'),
('Sarah Khan','Birmingham','2023-03-20');

INSERT INTO Products (ProductName, Category, Price)
VALUES
('Laptop','Electronics',900),
('Phone','Electronics',600),
('Desk Chair','Furniture',150);

INSERT INTO Orders (CustomerID, OrderDate)
VALUES
(1,'2024-01-05'),
(2,'2024-01-12'),
(3,'2024-02-02');

INSERT INTO OrderDetails (OrderID, ProductID, Quantity, TotalAmount)
VALUES
(1,1,1,900),
(2,2,2,1200),
(3,3,3,450);
```

---

# Data Model

The following relationships were created in Power BI to connect the tables and enable analysis across the dataset.

```
Customers.CustomerID → Orders.CustomerID

Orders.OrderID → OrderDetails.OrderID

Products.ProductID → OrderDetails.ProductID
```

This relational structure allows metrics such as revenue, orders, and product performance to be calculated across multiple dimensions including region, time, and product.

---

# Dashboard Features

The Power BI dashboard provides a simple overview of retail performance.

## Key Metrics

* Total Revenue
* Total Orders
* Total Units Sold

## Visualisations

* Revenue over time (line chart)
* Sales by region (bar chart)
* Top performing products (table)

These visuals provide quick insight into product demand and regional sales distribution.

---

# Dashboard Filters

Interactive filters were added to allow users to explore the data dynamically.

### Region Filter

Allows users to filter the dashboard to view sales performance for specific regions.

### Order Date Filter

Allows analysis of sales metrics across different time periods.

All dashboard visuals update automatically when filters are applied.

---

---

# Dashboard File

The Power BI dashboard file is located in the following directory:

```
RetailSalesDatabaseProject/RetailSalesDashboard.pbix
```

Open this file using **Power BI Desktop** to explore or modify the dashboard.

---

# Dashboard Preview

A screenshot of the dashboard can be found here:

```
RetailSalesDatabaseProject/RetailDashboard.png
```

---

# Key Concepts Demonstrated

This project highlights several important data and analytics concepts:

* Relational database design
* SQL table creation and data insertion
* Data modelling and relationships
* Connecting Power BI to SQL Server
* Building business intelligence dashboards
* Creating interactive filters and visualisations

---

# Potential Improvements

Possible future enhancements include:

* Expanding the dataset with larger or synthetic sales data
* Adding calculated metrics such as profit margins
* Implementing category-level product analysis
* Adding drill-through reports in Power BI
* Publishing the dashboard to Power BI Service
