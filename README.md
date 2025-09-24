# E-commerce Database Schema

## 📖 Overview

This repository contains a complete **MySQL relational database schema** for a simple **E-commerce Store**. It is designed for academic and practical use cases, covering real-world features such as product management, user accounts, orders, payments, wishlists, and reviews.

The schema follows **best practices** in database normalization, uses **constraints** to ensure data integrity, and includes **sample seed data** to get started quickly.

---

## ⚙️ Features

* **Users & Authentication**: Customer and admin accounts with roles.
* **Product Catalog**: Products, suppliers, categories (with many-to-many mapping).
* **Orders & Payments**: Orders with order items, payments, shipping/billing addresses.
* **Wishlists & Reviews**: Customers can create wishlists and review products.
* **Audit Logs**: Stock change tracking via product stock audit table.
* **Referential Integrity**: Strong constraints with primary keys, foreign keys, and cascades.

---

## 🛠️ Getting Started

### 1. Requirements

* MySQL 8.0+ (or compatible version)
* MySQL Workbench (optional, for ER diagrams)
* Git (for cloning this repository)
* Docker (optional, run MySQL without installing locally)

### 2. Setup Instructions

```bash
# Clone the repository
git clone https://github.com/your-username/ecommerce-db.git
cd ecommerce-db

# Run the SQL script (replace 'your_user')
mysql -u your_user -p < ecommerce_db_schema.sql
```

This will:

* Create the database `ecommerce_store`
* Build all required tables and constraints
* Insert **sample seed data**

---

## 🗂️ Database Schema

Key entities include:

* **users** → customers & admins
* **products** ↔ **categories** (many-to-many)
* **orders** → **order\_items**, **payments**
* **wishlists** → **wishlist\_items**
* **reviews**, **addresses**, **suppliers**

For a detailed breakdown, see comments in `ecommerce_db_schema.sql`.

---

## 🧩 ER Diagram

To visualize the schema:

1. Open **MySQL Workbench** → `Database` → `Reverse Engineer` → select `ecommerce_store`.
2. Alternatively, use **draw\.io** or **Mermaid** and follow the entity relationship notes in the `.sql` file.

---

## 🔎 Example Queries

Here are some queries you can run on the seeded database:

### 1. List all products with their categories

```sql
SELECT p.name AS product, c.name AS category
FROM products p
JOIN product_categories pc ON p.product_id = pc.product_id
JOIN categories c ON pc.category_id = c.category_id;
```

### 2. Get all orders with customer details

```sql
SELECT o.order_id, u.email, o.order_total, o.status
FROM orders o
JOIN users u ON o.user_id = u.user_id;
```

### 3. Show reviews for a product

```sql
SELECT u.first_name, u.last_name, r.rating, r.title, r.body
FROM reviews r
JOIN users u ON r.user_id = u.user_id
WHERE r.product_id = 1;
```

### 4. Retrieve wishlist items for a customer

```sql
SELECT w.name AS wishlist, p.name AS product
FROM wishlists w
JOIN wishlist_items wi ON w.wishlist_id = wi.wishlist_id
JOIN products p ON wi.product_id = p.product_id
WHERE w.user_id = 1;
```





