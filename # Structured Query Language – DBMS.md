# Structured Query Language – DBMS
結構化查詢語言（Structured Query Language，簡稱 SQL）是一種用於管理和操作關聯性數據庫管理系統（DBMS）的語言。以下是一個簡單的介紹 SQL 的方式：

## 1. **資料庫**：首先，理解資料庫是一個組織和存儲數據的容器。DBMS 是用於管理這些數據庫的軟體。

## 2. **資料表**：資料庫內的數據以資料表的形式存儲。資料表就像 Excel 表格一樣，包含了列和行，每列代表一個屬性（例如姓名、年齡、地址），每行代表一條記錄。

## 3. **SQL 查詢**：SQL 用於查詢和操作資料表中的數據。它提供了幾個關鍵的指令：
  - **SELECT**：用於檢索資料，你可以指定你想要的列，也可以使用條件過濾數據。
  例子:SELECT * FROM employee;
  - **INSERT**：用於將新數據插入資料表。
  例子:INSERT INTO employee VALUES (105, 'Lau', 'Andy', '14-JUL-79', 32000);
  - **UPDATE**：用於更新現有數據表中的數據。
  例子:
  - **DELETE**：用於刪除資料表中的數據。
  例子:DELETE FROM employees WHERE age > 65

## 4. **條件**：SQL 查詢可以包含條件，這些條件用於篩選符合特定條件的數據。例如，你可以使用 WHERE 子句來限制只檢索特定年齡的人。
## 5. **聚合函數**：SQL 還提供了一些聚合函數，例如 SUM、COUNT、AVG 和 MAX，用於對數據進行統計運算。
以下是一個簡單的 SQL 查詢示例，假設我們有一個名為 "users" 的資料表：

```sql
-- 檢索所有使用者的姓名和年齡
SELECT name, age
FROM users;

-- 檢索年齡大於 30 歲的使用者
SELECT name, age
FROM users
WHERE age > 30;

-- 計算使用者的總數
SELECT COUNT(*)
FROM users;
```

# `CONSTRAINT` 是 SQL 中用於實施數據完整性的關鍵字，它用於定義資料表中的約束條件，以確保數據庫中的數據符合特定的規則和要求。以下是 `CONSTRAINT` 的一些常見用法：

## 1. **主鍵約束 (PRIMARY KEY)**：主鍵約束用於確保資料表中的每一行都具有唯一的識別標誌。主鍵通常是一個或多個列，並且不能包含空值。主鍵可以確保每行數據都可以唯一識別。
```sql
 CONSTRAINT pk_employee PRIMARY KEY (ID),
 ```

## 2. **外鍵約束 (FOREIGN KEY)**：外鍵約束用於確保兩個資料表之間的關聯性。外鍵通常與其他資料表的主鍵關聯，以確保參考完整性。外鍵約束可以防止無效的參照。

   ```sql
   CREATE TABLE orders (
       order_id INT PRIMARY KEY,
       user_id INT,
       order_date DATE,
       CONSTRAINT orders FOREIGN KEY (user_id) REFERENCES users(user_id)
   );
   ```

## 3. **唯一約束 (UNIQUE)**：唯一約束確保資料表中的一列或多列的值是唯一的，但與主鍵不同，唯一約束允許包含空值。

   ```sql
   CREATE TABLE products (
       CONSTRAINT product_id PRIMARY KEY,
       product_code VARCHAR(20) UNIQUE,
       product_name VARCHAR(255)
   );
   ```

## 4. **檢查約束 (CHECK)**：檢查約束用於確保插入或更新的數據符合特定的條件。這可以用來限制某一列的數值範圍或其他約束。

   ```sql
   CREATE TABLE employees (
       CONSTRAINT employee_id INT PRIMARY KEY,
       employee_name VARCHAR(255),
       salary DECIMAL(10, 2) CHECK (salary >= 0)
   );
   ```

## 5. **DEFAULT 約束 (DEFAULT)**：DEFAULT 約束用於為新插入的行提供默認值。如果插入語句未指定某一列的值，則將使用默認值。

   ```sql
   CREATE TABLE messages (
       CONSTRAINT message_id INT PRIMARY KEY,
       message_text VARCHAR(255) DEFAULT 'No message'
   );
   ```

這些約束可以保護數據庫中的數據完整性，確保數據符合預期的要求，並幫助防止無效或不合規格的數據進入資料庫。
---------------------------------------------------------------------------
# Structured Query Language (SQL) 中的 DDL 是指數據定義語言（Data Definition Language）。DDL 用於創建、修改和刪除數據庫對象，例如數據表、索引、視圖和其他數據庫結構。以下是一些 DDL 的常見操作：

## 1. **創建表格（CREATE TABLE）**：

   使用 DDL 可以創建新的數據表。以下是一個示例：

   ```sql
   CREATE TABLE employees (
       employee_id INT PRIMARY KEY,
       first_name VARCHAR(50),
       last_name VARCHAR(50),
       hire_date DATE
   );
   ```

## 2. **修改表格（ALTER TABLE）**：

   使用 DDL 可以修改現有的數據表。例如，添加新列、刪除列或修改列的數據類型。以下是一個示例：

   ```sql
   ALTER TABLE employees
   ADD email VARCHAR(100);
   ```

## 3. **刪除表格（DROP TABLE）**：

   使用 DDL 可以刪除不再需要的數據表。請注意，這是一個危險的操作，它將永久刪除表格及其所有數據。以下是一個示例：

   ```sql
   DROP TABLE employees;
   ```

## 4. **創建索引（CREATE INDEX）**：

   DDL 也可以用於創建索引，以加速數據查詢。以下是一個示例：

   ```sql
   CREATE INDEX idx_last_name ON employees(last_name);
   ```

## 5. **刪除索引（DROP INDEX）**：

   使用 DDL 可以刪除不再需要的索引。以下是一個示例：

   ```sql
   DROP INDEX idx_last_name;
   ```

## 6. **創建視圖（CREATE VIEW）**：

   DDL 用於創建虛擬表格，稱為視圖，這些視圖基於現有的數據表。以下是一個示例：

   ```sql
   CREATE VIEW employee_summary AS
   SELECT employee_id, first_name, last_name
   FROM employees
   WHERE hire_date >= '2020-01-01';
   ```

## 7. **刪除視圖（DROP VIEW）**：

   使用 DDL 可以刪除不再需要的視圖。以下是一個示例：

   ```sql
   DROP VIEW employee_summary;
   ```
# 經常在 DDL 操作中使用：

1. **PRIMARY KEY**：用於定義主鍵約束，唯一標識數據表中的每一行。

2. **FOREIGN KEY**：用於定義外鍵約束，建立表之間的關聯性。

3. **UNIQUE**：用於定義唯一約束，確保某一列（或一組列）的值是唯一的。

4. **CHECK**：用於定義檢查約束，確保數據滿足特定的條件或規則。

5. **INDEX**：用於創建索引，以加速數據查詢操作。

6. **TABLE**：用於定義表格，包括列名和數據類型。

7. **COLUMN**：用於描述表格中的單個列，包括列名、數據類型和約束。

8. **ALTER**：用於修改現有數據庫對象（如表格、列或約束）的結構。

9. **DROP**：用於刪除數據庫對象，包括表格、索引、視圖等。

10. **VIEW**：用於創建虛擬表格，基於現有表格的查詢結果。

11. **SEQUENCE**：用於創建序列，生成唯一的數字值，通常用於主鍵列的自動增長。

12. **DEFAULT**：用於指定列的默認值。

13. **CASCADE**：用於指定在刪除或修改數據表時如何處理相關的約束和數據。

