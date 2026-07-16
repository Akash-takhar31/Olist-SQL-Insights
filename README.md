#  Olist Business Intelligence Analysis

Business intelligence project analyzing the Brazilian e-commerce platform **Olist**, answering **39 business questions using SQL** and preparing the ground for a **Power BI dashboard** highlighting key KPIs and indicators.

## About the Project

Olist is a Brazilian marketplace that connects small businesses to major sales channels. This project digs into Olist's public e-commerce dataset to answer real business questions — revenue, delivery performance, customer behavior, seller performance, and review scores — entirely through SQL queries, followed by a Power BI dashboard summarizing the most relevant KPIs.

## What You'll Find Here

- **Aggregate functions**: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `ROUND`, `EXTRACT`, `TO_CHAR`, etc.
- **Clauses**: `SELECT`, `WHERE`, `HAVING`, `GROUP BY`, `ORDER BY`, `LEFT JOIN`, `INNER JOIN`, `CASE WHEN`, `LIMIT`.
- **Window functions**: `RANK`, `ROW_NUMBER`, `OVER`, `PARTITION BY`.
- **CTEs and subqueries** for multi-step, readable analysis.

## Data Schema

![Olist data schema](data_schema.png)

The dataset is relational, composed of multiple tables connected primarily through `order_id`, `customer_id`, `product_id`, and `seller_id`.

## Dataset Description

| Table | Description |
|---|---|
| **Customers** | Customer identifiers and location. Distinguishes `customer_id` (per order) from `customer_unique_id` (per person). |
| **Geolocation** | Brazilian zip code prefixes with lat/lng coordinates — used for maps and seller–customer distance calculations. |
| **Order Items** | Items purchased per order, including price and freight value (freight is split across items in multi-item orders). |
| **Payments** | Payment method, installments, and transaction value per order (an order can have multiple payments). |
| **Order Reviews** | Customer satisfaction survey results, including review score (1–5) and comments. |
| **Orders** | The core table — order status and full timestamp lifecycle (purchase, approval, carrier handoff, delivery, estimated delivery). |
| **Products** | Product category (in Portuguese), plus dimensions, weight, and content-length metadata. |
| **Sellers** | Seller identifiers and location. |

<details>
<summary><strong>Full column-level reference</strong></summary>

**Customers**
- `customer_id`: Key to the orders dataset; unique per order.
- `customer_unique_id`: Unique identifier of a customer across orders.
- `customer_zip_code_prefix`: First five digits of the customer's zip code.
- `customer_city` / `customer_state`

**Geolocation**
- `geolocation_zip_code_prefix`, `geolocation_lat`, `geolocation_lng`, `geolocation_city`, `geolocation_state`

**Order Items**
- `order_id`, `order_item_id`, `product_id`, `seller_id`
- `shipping_limit_date`: Seller's deadline to hand the order to the logistics partner.
- `price`, `freight_value`

**Payments**
- `order_id`, `payment_sequential`, `payment_type`, `payment_installments`, `payment_value`

**Order Reviews**
- `review_id`, `order_id`, `review_score`
- `review_comment_title`, `review_comment_message` (Portuguese)
- `review_creation_date`, `review_answer_timestamp`

**Orders**
- `order_id`, `customer_id`, `order_status`
- `order_purchase_timestamp`, `order_approved_at`
- `order_delivered_carrier_date`, `order_delivered_customer_date`, `order_estimated_delivery_date`

**Products**
- `product_id`, `product_category_name`
- `product_name_length`, `product_description_length`, `product_photos_qty`
- `product_weight_g`, `product_length_cm`, `product_height_cm`, `product_width_cm`

**Sellers**
- `seller_id`, `seller_zip_code_prefix`, `seller_city`, `seller_state`

</details>

## Business Questions

The analysis walks through 39 business questions, spanning descriptive statistics, trend analysis, and correlation checks, such as:

- How many unique customers and orders are there, and what is the total revenue?
- Which cities, states, and product categories drive the most orders and sales?
- What are the order, review, delivery, and payment trends over time?
- How many orders were delivered late, early, or on the estimated date?
- Is there a relationship between delivery delays, seller/customer distance, payment installments, and review scores?
- Which sellers and product categories are the most profitable and best reviewed?

The complete bilingual (English/Portuguese) list of all 39 questions is available in [`business_questions.txt`](business_questions.txt), with the corresponding SQL implementations in [`olist_queries.sql`](olist_queries.sql) / [`SQL_queries.txt`](SQL_queries.txt).

## Repository Structure

```
Olist-Data-Analysis/
├── README.md                 # Project overview and documentation
├── business_questions.txt    # The 39 business questions (EN + PT)
├── olist_queries.sql         # SQL solutions to the business questions
├── SQL_queries.txt           # SQL queries in plain text format
└── data_schema.png           # Entity-relationship diagram of the dataset
```

## Tools & Technologies

- **SQL** (PostgreSQL-flavored syntax: `EXTRACT`, `TO_CHAR`, window functions)
- **Power BI** for the KPI dashboard

## Dataset Source

The data was collected from Kaggle's [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce?select=olist_order_items_dataset.csv).
