# Data Catalog: Gold Layer

## Overview
The **Gold Layer** represents the business-ready data in the data warehouse. It is designed to support analytics, dashboarding, and decision-making. This layer contains **dimension tables** and **fact tables**, typically organized in a **Star Schema** format.

---

### 1. `gold.dim_customers`
**Purpose:**  
Stores enriched customer details, including demographic and geographic attributes, for use in analytics and reporting.

**Columns:**

| Column Name     | Data Type     | Description                                                                                   |
|-----------------|---------------|-----------------------------------------------------------------------------------------------|
| `customer_key`  | INT           | Surrogate key uniquely identifying each customer.                                             |
| `customer_id`   | INT           | Unique identifier assigned to each customer.                                                  |
| `customer_number` | NVARCHAR(50) | Alphanumeric customer reference used for tracking.                                            |
| `first_name`    | NVARCHAR(50)  | Customer's first name.                                                                        |
| `last_name`     | NVARCHAR(50)  | Customer's last (family) name.                                                                |
| `country`       | NVARCHAR(50)  | Customer's country of residence (e.g., 'Australia').                                          |
| `marital_status`| NVARCHAR(50)  | Marital status of the customer (e.g., 'Married', 'Single').                                   |
| `gender`        | NVARCHAR(50)  | Gender of the customer (e.g., 'Male', 'Female', 'n/a').                                       |
| `birthdate`     | DATE          | Customer's date of birth (`YYYY-MM-DD`).                                                      |
| `create_date`   | DATE          | Record creation date in the source system.                                                    |

---

### 2. `gold.dim_products`
**Purpose:**  
Contains product-related metadata and classifications to support product-level analysis.

**Columns:**

| Column Name          | Data Type     | Description                                                                                   |
|----------------------|---------------|-----------------------------------------------------------------------------------------------|
| `product_key`        | INT           | Surrogate key uniquely identifying each product.                                              |
| `product_id`         | INT           | Internal unique identifier for the product.                                                   |
| `product_number`     | NVARCHAR(50)  | Structured alphanumeric code used for inventory or tracking.                                  |
| `product_name`       | NVARCHAR(50)  | Full descriptive name of the product.                                                         |
| `category_id`        | NVARCHAR(50)  | Unique identifier for the product category.                                                   |
| `category`           | NVARCHAR(50)  | High-level product grouping (e.g., 'Bikes').                                                  |
| `subcategory`        | NVARCHAR(50)  | More specific classification within the category.                                             |
| `maintenance_required`| NVARCHAR(50) | Indicates whether the product needs maintenance (`Yes` / `No`).                               |
| `cost`               | INT           | Base cost of the product in whole currency units.                                             |
| `product_line`       | NVARCHAR(50)  | Product series or line (e.g., 'Mountain', 'Road').                                            |
| `start_date`         | DATE          | Product availability start date.                                                              |

---

### 3. `gold.fact_sales`
**Purpose:**  
Captures transactional sales data for revenue analysis, performance tracking, and forecasting.

**Columns:**

| Column Name     | Data Type     | Description                                                                                   |
|-----------------|---------------|-----------------------------------------------------------------------------------------------|
| `order_number`  | NVARCHAR(50)  | Unique identifier for each sales order (e.g., 'SO54496').                                     |
| `product_key`   | INT           | Foreign key to the product dimension.                                                         |
| `customer_key`  | INT           | Foreign key to the customer dimension.                                                        |
| `order_date`    | DATE          | Date when the order was placed.                                                               |
| `shipping_date` | DATE          | Date when the order was shipped.                                                              |
| `due_date`      | DATE          | Payment due date for the order.                                                               |
| `sales_amount`  | INT           | Total sales value for the line item.                                                          |
| `quantity`      | INT           | Number of product units sold in the order.                                                    |
| `price`         | INT           | Price per unit of the product.                                                                |
