
# 📘 SQL BASICS – COMPLETE GUIDE (With Examples & Output)

This guide explains common SQL queries using simple **users** and **orders** tables.

---

## 🗂️ Sample Tables

### **users**

| user_id | name  | email                                       |
| ------: | ----- | ------------------------------------------- |
|       1 | Alice | [alice@gmail.com](mailto:alice@gmail.com)   |
|       2 | Bob   | [bob@gmail.com](mailto:bob@gmail.com)       |
|       3 | Alice | [alice2@gmail.com](mailto:alice2@gmail.com) |

### **orders**

| order_id | user_id | product_name | amount |
| -------: | ------: | ------------ | -----: |
|      101 |       1 | Laptop       |  75000 |
|      102 |       1 | Mouse        |   2000 |
|      103 |       2 | Mobile       |  25000 |
|      104 |       4 | Tablet       |  30000 |

---

## 1️⃣ SELECT

Used to fetch all columns from a table.

```sql
SELECT * FROM users;
```

**Output**

| user_id | name  | email                                       |
| ------: | ----- | ------------------------------------------- |
|       1 | Alice | [alice@gmail.com](mailto:alice@gmail.com)   |
|       2 | Bob   | [bob@gmail.com](mailto:bob@gmail.com)       |
|       3 | Alice | [alice2@gmail.com](mailto:alice2@gmail.com) |

---

## 2️⃣ SELECT Specific Columns

```sql
SELECT name, email FROM users;
```

**Output**

| name  | email                                       |
| ----- | ------------------------------------------- |
| Alice | [alice@gmail.com](mailto:alice@gmail.com)   |
| Bob   | [bob@gmail.com](mailto:bob@gmail.com)       |
| Alice | [alice2@gmail.com](mailto:alice2@gmail.com) |

---

## 3️⃣ WHERE

Filters rows based on condition.

```sql
SELECT * FROM orders WHERE amount > 30000;
```

**Output**

| order_id | user_id | product_name | amount |
| -------: | ------: | ------------ | -----: |
|      101 |       1 | Laptop       |  75000 |

---

## 4️⃣ DISTINCT

Removes duplicate values.

```sql
SELECT DISTINCT name FROM users;
```

**Output**

| name  |
| ----- |
| Alice |
| Bob   |


### Query

```sql
SELECT DISTINCT name FROM users;
```

### Output

| name  |
| ----- |
| Alice |
| Bob   |

### Explanation

* The **`DISTINCT`** keyword removes **duplicate values** from the selected column.
* In the `users` table, **Alice appears twice**, but `DISTINCT` ensures it is shown **only once**.
* The database first looks at all `name` values, removes duplicates, then returns the result.

---

## 5️⃣ ORDER BY

Sorts data (ASC by default).

```sql
SELECT * FROM orders ORDER BY amount DESC;
```

**Output**

| order_id | product_name | amount |
| -------: | ------------ | -----: |
|      101 | Laptop       |  75000 |
|      104 | Tablet       |  30000 |
|      103 | Mobile       |  25000 |
|      102 | Mouse        |   2000 |

---

## 6️⃣ LIMIT

Restricts number of rows returned.

```sql
SELECT * FROM orders LIMIT 2;
```

**Output**

| order_id | product_name | amount |
| -------: | ------------ | -----: |
|      101 | Laptop       |  75000 |
|      102 | Mouse        |   2000 |

---

## 7️⃣ COUNT

Counts number of rows.

```sql
SELECT COUNT(*) AS total_orders FROM orders;
```

**Output**

| total_orders |
| ------------ |
| 4            |

---

## 8️⃣ SUM

Calculates total of a column.

```sql
SELECT SUM(amount) AS total_amount FROM orders;
```

**Output**

| total_amount |
| ------------ |
| 132000       |

---

## 9️⃣ GROUP BY

Groups rows for aggregation.

```sql
SELECT name, COUNT(user_id) AS total_users
FROM users
GROUP BY name;
```

**Output**

| user_name | total_users |
| ------: | -----------: |
|   Alice |            2 |
|     Bob |            1 |



---

## 🔟 HAVING

Filters **grouped data** (used with aggregates).

```sql
SELECT user_id, SUM(amount) AS total_spent
FROM orders
GROUP BY user_id
HAVING SUM(amount) >= 30000;
```

**Output**

| user_id | total_spent |
| ------: | ----------: |
|       1 |       77000 |
|       4 |       30000 |

👉 **Note**:

* `WHERE` → filters rows
* `HAVING` → filters aggregated results

---

## 1️⃣1️⃣ INNER JOIN

Returns only matching records.

```sql
SELECT u.name, o.product_name, o.amount
FROM users u
INNER JOIN orders o
ON u.user_id = o.user_id;
```

**Output**

| name  | product_name | amount |
| ----- | ------------ | -----: |
| Alice | Laptop       |  75000 |
| Alice | Mouse        |   2000 |
| Bob   | Mobile       |  25000 |

---

## 1️⃣2️⃣ LEFT JOIN

All rows from left table + matching right.

```sql
SELECT u.name, o.product_name
FROM users u
LEFT JOIN orders o
ON u.user_id = o.user_id;
```

**Output**

| name  | product_name |
| ----- | ------------ |
| Alice | Laptop       |
| Alice | Mouse        |
| Bob   | Mobile       |
| Alice | NULL         |

---

## 1️⃣3️⃣ RIGHT JOIN

All rows from right table + matching left.

```sql
SELECT u.name, o.product_name
FROM users u
RIGHT JOIN orders o
ON u.user_id = o.user_id;
```

**Output**

| name  | product_name |
| ----- | ------------ |
| Alice | Laptop       |
| Alice | Mouse        |
| Bob   | Mobile       |
| NULL  | Tablet       |

---

## 1️⃣4️⃣ UPDATE

Updates existing data.

```sql
UPDATE users
SET email = 'alice_new@gmail.com'
WHERE user_id = 1;
```

✔ Alice’s email is updated.

---

## 1️⃣5️⃣ DELETE

Deletes selected rows.

```sql
DELETE FROM orders WHERE order_id = 102;
```

✔ Mouse order deleted.

---

## 1️⃣6️⃣ TRUNCATE

Deletes **all rows**, keeps table structure.

```sql
TRUNCATE TABLE orders;
```

✔ Fast and irreversible.

---

## 1️⃣7️⃣ DROP

Deletes table permanently.

```sql
DROP TABLE users;
```

❌ Table + data removed forever.

---

##  SUMMARY

* **SELECT** → fetch data
* **WHERE** → filter rows
* **DISTINCT** → remove duplicates
* **GROUP BY** → aggregate data
* **HAVING** → filter aggregated data
* **JOIN** → combine multiple tables
* **TRUNCATE vs DELETE** → structure kept vs row-based
* **DROP** → removes table completely

---

### Find customers with total spend > 10,000 in 2024    
    
```
SELECT customer_id
FROM orders
WHERE order_date >= DATE '2024-01-01'
  AND order_date <  DATE '2025-01-01'
GROUP BY customer_id
HAVING SUM(amount) > 10000;
```