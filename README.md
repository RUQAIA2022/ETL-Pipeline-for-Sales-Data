# ETL-Pipeline-for-Sales-Data

This project implements an ETL (Extract, Transform, Load) pipeline to process sales data from multiple CSV files and load it into a MySQL database with proper normalization.

## Features

- **Data Extraction**:
  - Combines data from three CSV files (`store_sales_1.csv`, `store_sales_2.csv`, `store_sales_3.csv`)
  
- **Data Transformation**:
  - Handles missing values:
    - Drops records with missing `CustomerID`
    - Fills missing quantities with `1`
    - Replaces missing unit prices with the mode value
  - Converts currency from USD to OMR (Omani Rial)
  - Standardizes text formatting (trim whitespace, title case)
  - Creates normalized database structure with 4 tables

- **Data Loading**:
  - Automatically creates database tables
  - Establishes proper relationships between tables
  - Handles data type conversions

## Database Schema


    PRODUCT ||--o{ SALE : has
    CUSTOMER ||--o{ SALE : makes
    STORE ||--o{ SALE : contains
    PRODUCT {
        int ProductID PK
        varchar(255) ProductName
    }
    CUSTOMER {
        varchar(50) CustomerID PK
        varchar(255) CustomerName
        varchar(255) ContactInfo
    }
    STORE {
        varchar(50) StoreID PK
        varchar(255) StoreName
        varchar(255) Location
    }
    SALE {
        int SaleID PK
        int ProductID FK
        varchar(50) CustomerID FK
        varchar(50) StoreID FK
        int Qty
        float Unit_Price
        datetime SaleDate
        varchar(10) CurrencyType
    }
