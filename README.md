# course-data
=======
# Shop dataset

Sample data for the SQL and Python course. This is a small, synthetic e-commerce store, made-up customers, products, and orders, built for learning.

## What's here

Four CSV files, one per table, plus a ready-to-query DuckDB database and the script that builds it.

| File | Rows | What it is |
|---|---|---|
| `customers.csv` | 45 | People who have an account at the shop |
| `products.csv` | 45 | Things the shop sells, across five categories |
| `orders.csv` | 85 | Orders that customers placed |
| `order_items.csv` | 130 | The individual line items inside those orders |
| `shop.duckdb` | — | All four tables in one DuckDB database file |
| `shop_duckdb_setup.sql` | — | The script that builds the database from scratch |

## The columns

**customers**: `customer_id`, `first_name`, `last_name`, `email`, `city`, `state`, `signup_date`

**products**: `product_id`, `product_name`, `category`, `price`, `in_stock`

**orders**: `order_id`, `customer_id`, `order_date`, `status`, `total_amount`

**order_items**: `order_item_id`, `order_id`, `product_id`, `quantity`, `unit_price`

## How the tables connect

An order belongs to a customer (`orders.customer_id` points at `customers.customer_id`). Each order is made up of one or more line items (`order_items.order_id` points at `orders.order_id`), and each line item is one product (`order_items.product_id` points at `products.product_id`).

The five product categories are Electronics, Home, Office, Kitchen, and Fitness.

## Loading it

In Python with pandas, straight from this repo:

```python
import pandas as pd

BASE = "https://raw.githubusercontent.com/cjjohanson/course-data/main/"
customers = pd.read_csv(BASE + "customers.csv")
customers.head()
```

In DuckDB, either open `shop.duckdb` directly, or rebuild it from `shop_duckdb_setup.sql`.
