# Shop dataset

Sample data for the SQL and Python course. It's a small e-commerce shop, customers, products, orders, and the line items inside those orders. None of it is real data.

## What's here

| File | Rows | What it is |
|---|---|---|
| `customers.csv` | 408 | People who have an account at the shop |
| `products.csv` | 120 | Things the shop sells, across five categories |
| `orders.csv` | 1,000 | Orders customers placed |
| `order_items.csv` | 2,993 | The individual line items inside those orders |
| `shop.duckdb` | — | All four tables in one DuckDB database file |
| `shop_duckdb_setup.sql` | — | The script that builds the database from scratch |

## The columns

**customers**: `customer_id`, `first_name`, `last_name`, `email`, `city`, `state`, `signup_date`, `phone`, `total_spent`

**products**: `product_id`, `product_name`, `category`, `price`, `in_stock`

**orders**: `order_id`, `customer_id`, `order_date`, `status`, `total_amount`

**order_items**: `order_item_id`, `order_id`, `product_id`, `quantity`, `unit_price`

## How the tables connect

An order belongs to a customer (`orders.customer_id` points at `customers.customer_id`). Each order is made of one or more line items (`order_items.order_id` points at `orders.order_id`), and each line item is one product (`order_items.product_id` points at `products.product_id`).

The five product categories are Electronics, Home, Office, Kitchen, and Fitness.

## Loading it

**Python, from the CSVs (the beginner path).** No download needed, pandas reads straight from this repo:

```python
import pandas as pd

BASE = "https://raw.githubusercontent.com/cjjohanson/course-data/main/"
customers = pd.read_csv(BASE + "customers.csv")
customers.head()
```

**Python, connected to the database (recommended).** This is the path I'd steer you toward. You query a real database straight from Python, which is the closest thing to how the job actually works, and it lets you use SQL and pandas side by side instead of picking one. It's a step up from reading flat CSVs, and worth it. Download `shop.duckdb`, `pip install duckdb`, and query it as a real database:

```python
import duckdb

con = duckdb.connect("shop.duckdb")
con.execute("SELECT * FROM customers LIMIT 5").df()
```

**SQL.** Open `shop.duckdb` directly in a tool like DBeaver, or rebuild it from scratch by running `shop_duckdb_setup.sql`.
