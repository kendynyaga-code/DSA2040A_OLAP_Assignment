# 🗄️ OLAP System with SQLite + Pandas

## 📌 Project Description

This project demonstrates the design and implementation of a **mini OLAP (Online Analytical Processing) system** using **SQLite, Pandas, and Seaborn/Matplotlib**.
It covers **ROLAP, MOLAP, and HOLAP architectures**, along with key **OLAP operations**: Slice, Dice, Roll-Up, and Drill-Down.
The project also provides visualizations to showcase insights from multidimensional data analysis.

---

## 🛠️ Schema Design (Star Schema)

The database follows a **Star Schema** with **dimension tables** and a **fact table**.

### **1. Dimension Tables**

#### `products`

| Column     | Type         | Description                                     |
| ---------- | ------------ | ----------------------------------------------- |
| product_id | INTEGER (PK) | Unique identifier for each product              |
| category   | TEXT         | Product category (Electronics, Furniture, etc.) |
| name       | TEXT         | Product name                                    |
| price      | DECIMAL      | Unit price of product                           |

#### `dates`

| Column     | Type      | Description           |
| ---------- | --------- | --------------------- |
| date       | DATE (PK) | Transaction date      |
| year       | INTEGER   | Year of sale          |
| quarter    | INTEGER   | Quarter of year (1–4) |
| month      | INTEGER   | Month number          |
| month_name | TEXT      | Month name            |

---

### **2. Fact Table**

#### `sales`

| Column     | Type         | Description                         |
| ---------- | ------------ | ----------------------------------- |
| sale_id    | INTEGER (PK) | Unique identifier for each sale     |
| date       | DATE (FK)    | Transaction date (links to `dates`) |
| product_id | INTEGER (FK) | Product sold (links to `products`)  |
| quantity   | INTEGER      | Quantity sold                       |
| revenue    | DECIMAL      | Total revenue (quantity × price)    |

---

## 🔍 OLAP Architectures Implemented

### **1. ROLAP (Relational OLAP)**

ROLAP queries are executed directly on the **SQLite database** using SQL.
Examples:

* **Average Revenue by Product Category**
* **Total Sales by Year**
* **Best-Selling Products in Each Category**

---

### **2. MOLAP (Multidimensional OLAP)**

MOLAP is implemented by building **data cubes in Pandas** after fetching data.
Examples:

* **Revenue Cube (Category × Year)**
* **Quantity Cube (Category × Year)**
  These cubes allow fast aggregation across multiple dimensions.

---

### **3. HOLAP (Hybrid OLAP)**

HOLAP combines SQL queries (ROLAP) with Pandas cubes (MOLAP).
Steps:

1. **SQL (ROLAP):** Fetch detailed data (e.g., sales in 2024).
2. **Pandas (MOLAP):** Build a cube summarizing **Revenue by Category × Month**.

---

## 🔄 OLAP Operations

1. **Slice**

   * Fix one dimension (e.g., sales in `2023` only).

2. **Dice**

   * Apply multiple filters (e.g., sales in `2023` AND category = Electronics).

3. **Roll-Up**

   * Aggregate from detailed → summarized (e.g., product → category → year).

4. **Drill-Down**

   * Break down summarized data into finer detail (e.g., Year → Quarter → Month).

---

## 📊 Visualizations

* **Bar Plot** → Average revenue by product category
* **Heatmap** → Revenue cube (Category × Year)
* **Line Plot** → Total revenue trends by year

---

## 🚀 How to Run

1. Clone this repository:

   ```bash
   git clone https://github.com/your-username/DSA2040A_OLAP_Assignment.git
   ```
2. Install dependencies:

   ```bash
   pip install pandas numpy matplotlib seaborn sqlite3
   ```
3. Run the Jupyter Notebook or Python script:

   ```bash
   python olap_system.py
   ```
