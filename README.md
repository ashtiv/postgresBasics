## 3. What is PostgreSQL All About?

PostgreSQL is a powerful and open-source  relational database  management system (RDBMS) that is known for its reliability, scalability, and extensibility. It was first released in 1989 and has since become one of the most popular  RDBMSs  in the world.

PostgreSQL supports a wide range of  programming languages, including C, C++, Java, Python, and Ruby, and provides built-in support for many features that are typically available only through add-ons in other databases, such as  JSON  and  XML  data types, full-text search, and advanced indexing.

PostgreSQL is also highly customizable, with a large number of extensions and plug-ins available to add functionality and improve performance.

## 4. Database Design

Database design is the process of creating a  database schema  that defines the structure and organization of the data stored in a database. A good  database design  can improve performance, reduce redundancy, and make it easier to maintain and update the database in the future.

There are several key concepts and terms that are important to understand when designing a database:

-   Entity: A thing or concept that we want to store data about, such as a person, product, or order.
-   Attribute: A characteristic of an entity, such as the name, age, or price of a product.
-   Primary key: A unique identifier for each entity that is used to distinguish it from other entities in the same table.
-   Foreign key: A reference to a primary key in another table that is used to establish relationships between entities.
-   Relationship: A connection between two entities that is defined by a  foreign key.

## Quiz 1: Database Terminology

Quiz questions to test your knowledge of  database terminology.

## 5. Creating Tables

In PostgreSQL, tables are created using the  `CREATE TABLE`  statement. The basic syntax for creating a table is as follows:

```
CREATE TABLE table_name (
  column1 datatype1 [constraints],
  column2 datatype2 [constraints],
  ...
);

```

Here is an example of creating a simple  `users`  table with two columns:

```
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(50) NOT NULL
);

```

In this example, we are creating a table called  `users`  with two columns:  `id`  and  `name`. The  `id`  column uses the  `SERIAL`  data type, which automatically generates a unique value for each new row. The  `PRIMARY KEY`  constraint indicates that the  `id`  column is the primary key for the table. The  `name`  column uses the  `VARCHAR`  data type with a length of 50 characters and the  `NOT NULL`  constraint, which means that a value must be provided for this column when inserting a new row.

## 6. Analyzing CREATE TABLE

In PostgreSQL, we can use the  `\d`  command to display information about a table, including its columns and constraints. For example, to display information about the  `users`  table we created in the previous step, we can run the following command:

sql

Copy

```
\d users

```

This will display the following output:

```
                                        Table "public.users"
 Column |         Type          | Collation | Nullable |               Default                
--------+-----------------------+-----------+----------+--------------------------------------
 id     | integer               |           | not null | nextval('users_id_seq'::regclass)
 name   | character varying(50) |           | not null | 
Indexes:
    "users_pkey" PRIMARY KEY, btree (id)

```

This output shows that the  `users`  table has two columns (`id`  and  `name`), with the  `id`  column being the primary key. It also shows that the  `id`  column uses the  `integer`  data type and the  `name`  column uses the  `character varying`  data type with a length of 50 characters.

## 7. Inserting Data Into a Table

In PostgreSQL, data is inserted into a table using the  `INSERT INTO`  statement. The basic syntax for inserting data is as follows:

```
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);

```

Here is an example of inserting a new row into the  `users`  table we created earlier:

```
INSERT INTO users (name) VALUES ('Alice');

```

This will insert a new row into the  `users`  table with a value of  `'Alice'`  for the  `name`  column. Since we did not provide a value for the  `id`  column, it will be automatically generated by the  `SERIAL`  data type.

## 8. Retrieving Data with SELECT

In PostgreSQL, data is retrieved from a table using the  `SELECT`  statement. The basic syntax for selecting data is as follows:

```
SELECT column1, column2, ... FROM table_name WHERE condition;

```

Here is an example of selecting all rows from the  `users`  table:

```
SELECT* FROM users;

```

This will retrieve all columns (`*`) from the  `users`  table.

## Coding Exercise 1: Create, Insert, and Select!

Let's practice creating a table, inserting data into it, and retrieving data from it.

1.  Create a new table called  `employees`  with the following columns:

-   `id`  (serial, primary key)
-   `name`  (varchar(50), not null)
-   `age`  (integer, not null)
-   `salary`  (numeric(10,2), not null)

2.  Insert the following data into the  `employees`  table:

-   Name:  Alice, Age: 25, Salary: 50000.00
-   Name:  Bob, Age: 30, Salary: 60000.00
-   Name: Charlie, Age: 35, Salary: 70000.00

3.  Retrieve all columns from the  `employees`  table.

## 9. Calculated Columns

In PostgreSQL, we can create calculated columns by using expressions in the  `SELECT`  statement. These expressions can perform calculations on existing columns or combine multiple columns into a new column.

Here is an example of creating a  calculated column  that calculates the total revenue for each order in an  `orders`  table:

```
SELECT order_id, quantity * price AS total_revenue FROM orders;

```

In this example, we are multiplying the  `quantity`  and  `price`  columns for each row and assigning the result to a new column called  `total_revenue`.

## 10. Calculating Phone Revenue

Let's practice creating a calculated column using a real-world example.

Suppose we have a  `sales`  table that contains information about phone sales, including the number of phones sold and the price per phone. We want to calculate the total revenue for each sale and display it in a new column called  `total`.

Here is an example of how we can do this:

```
SELECT sale_id, phone_price * phone_quantity AS total FROM sales;

```

In this example, we are multiplying the  `phone_price`  and  `phone_quantity`  columns for each row and assigning the result to a new column called  `total`.

## Coding Exercise 2: Using  Calculated Columns

Let's practice creating a calculated column.

Suppose we have a  `products`  table that contains information about products, including the price per unit and the number of units sold. We want to calculate the total revenue for each product and display it in a new column called  `revenue`.

1.  Create a new table called  `products`  with the following columns:

-   `id`  (serial, primary key)
-   `name`  (varchar(50), not null)
-   `price_per_unit`  (numeric(10,2), not null)
-   `units_sold`  (integer, not null)

2.  Insert the following data into the  `products`  table:

-   Name: Product A, Price per unit: 10.00, Units sold: 100
-   Name: Product B, Price per unit: 20.00, Units sold: 200
-   Name: Product C, Price per unit: 30.00, Units sold: 300

3.  Create a calculated column called  `revenue`  that calculates the total revenue for each product.
    
4.  Retrieve all columns from the  `products`  table.
    

## 11. Exercise Solution

Here is a possible solution to  Coding Exercise  2:

```
-- Step 1: Create a new table
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  price_per_unit NUMERIC(10,2) NOT NULL,
  units_sold INTEGER NOT NULL
);

-- Step 2: Insert data into the table
INSERT INTO products (name, price_per_unit, units_sold) VALUES
('Product A', 10.00, 100),
('Product B', 20.00, 200),
('Product C', 30.00, 300);

-- Step 3: Create a calculated column
SELECT id, name, price_per_unit, units_sold, price_per_unit * units_sold AS revenue FROM products;

-- Step 4: Retrieve all columns from the table
SELECT * FROM products;

```

This solution creates a  `products`  table with four columns (`id`,  `name`,  `price_per_unit`, and  `units_sold`), inserts three rows of data into the table, creates a calculated column called  `revenue`  that multiplies the  `price_per_unit`  and  `units_sold`  columns for each row, and retrieves all columns from the table.

## 12. String Operators and Functions

In PostgreSQL, we can use  string operators  and functions to manipulate strings and perform operations on them. Some common string operators and functions include:

-   `||`:  Concatenation  operator that combines two strings into one.
-   `LENGTH(string)`: Function that returns the length of a string.
-   `SUBSTR(string, start, length)`: Function

## 13. Filtering Rows with "Where"

In  PostgreSQL, we can use the  `WHERE`  keyword to filter rows based on a specified condition. The basic syntax for using  `WHERE`  is as follows:

```
SELECT column1, column2, ... FROM table_name WHERE condition;

```

Here is an example of using  `WHERE`  to filter rows from an  `employees`  table based on age:

```
SELECT * FROM employees WHERE age > 30;

```

This will retrieve all columns (`*`) from the  `employees`  table where the  `age`  column is greater than 30.

## 14. More on the "Where" Keyword

In addition to using  comparison operators  like  `>`  and  `<`, we can also use other operators in conjunction with  `WHERE`  to filter rows based on more complex conditions. Some common operators include:

-   `=`: Equal to
-   `<>`  or  `!=`: Not equal to
-   `LIKE`: Matches a pattern (use  `%`  as a wildcard)
-   `IN`: Matches any of a list of values
-   `NOT`: Negates a condition

Here are some examples of using these operators in  `WHERE`  clauses:

sql

Copy

```
SELECT * FROM employees WHERE name = 'Alice'; -- Matches rows where name is exactly 'Alice'
SELECT * FROM employees WHERE age <> 30; -- Matches rows where age is not equal to 30
SELECT * FROM employees WHERE name LIKE 'A%'; -- Matches rows where name starts with 'A'
SELECT * FROM employees WHERE age IN (25, 35); -- Matches rows where age is either 25 or 35
SELECT * FROM employees WHERE NOT (name = 'Bob' AND age = 30); -- Matches rows where name is not 'Bob' OR age is not 30

```

## 15. Compound "Where" Clauses

We can also use multiple conditions in a  `WHERE`  clause to create more  complex filters. We can use the  `AND`  and  `OR`  operators to combine conditions in a single  `WHERE`  clause.

Here is an example of using  `AND`  to filter rows from an  `employees`  table based on both name and age:

```
SELECT * FROM employees WHERE name = 'Alice' AND age > 25;

```

This will retrieve all columns (`*`) from the  `employees`  table where the  `name`  column is  `'Alice'`  and the  `age`  column is greater than 25.

Here is an example of using  `OR`  to filter rows based on two different conditions:

```
SELECT * FROM employees WHERE name = 'Alice' OR age > 30;

```

This will retrieve all columns (`*`) from the  `employees`  table where the  `name`  column is  `'Alice'`  or the  `age`  column is greater than 30.

## 16. A "Where" Exercise Overview

Let's practice using the  `WHERE`  keyword to filter rows from a table.

Suppose we have an  `orders`  table that contains information about customer orders, including the customer's name, the date the order was placed, and the total amount of the order. We want to retrieve all orders placed by customers named 'Alice' that were placed on or after January 1st, 2020.

## Coding Exercise 3: Practicing Where Statements

Write a  SQL query  that retrieves all columns from the  `orders`  table where the  `customer_name`  column is 'Alice' and the  `order_date`  column is greater than or equal to '2020-01-01'.

## 17. A "Where" Solution

Here is a possible solution to  Coding Exercise 3:

```
SELECT * FROM orders
WHERE customer_name = 'Alice'
AND order_date >= '2020-01-01';

```

This solution uses  `WHERE`  to filter rows from the  `orders`  table based on two conditions: that the  `customer_name`  column is  `'Alice'`  and that the  `order_date`  column is greater than or equal to  `'2020-01-01'`.

## 18. "Where" With Lists

We can also use the  `IN`  operator in a  `WHERE`  clause to filter rows based on a list of values. Here is an example of using  `IN`  to retrieve rows from a  `users`  table where the  `name`  column is either 'Alice' or 'Bob':
```
SELECT * FROM users WHERE name IN ('Alice', 'Bob');

```

## 19. A "Where" With Lists Solution

Let's practice using the  `IN`  operator in a  `WHERE`  clause.

Suppose we have a  `sales`  table that contains information about phone sales, including the  phone model  and the price per phone. We want to retrieve all rows from the  `sales`  table where the phone model is either 'iPhone' or 'Samsung'.

## Coding Exercise 4: A More Challenging 'Where'

Write a SQL query that retrieves all columnsfrom the  `sales`  table where the  `phone_model`  column is either 'iPhone' or 'Samsung'.

## 20. Calculations in "Where" Clauses

We can also perform calculations in a  `WHERE`  clause to filter rows based on the result of a calculation. For example, we can retrieve all rows from a  `sales`  table where the  `price_per_phone`  column is greater than $500:

```
SELECT * FROM sales WHERE price_per_phone > 500;

```

## 21. Solving Calculations

Let's practice using calculations in a  `WHERE`  clause.

Suppose we have a  `products`  table that contains information about products, including the  product name  and the price per unit. We want to retrieve all rows from the  `products`  table where the price per unit is less than $10.

## Coding Exercise 5: Trying Calculations in Where Clauses

Write a SQL query that retrieves all columns from the  `products`  table where the  `price_per_unit`  column is less than $10.

## 22. Updating Rows

In addition to retrieving rows from a table, we can also update rows using the  `UPDATE`  statement. The basic syntax for  `UPDATE`  is as follows:

```
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;

```

Here is an example of using  `UPDATE`  to set the  `price_per_phone`  of all rows in a  `sales`  table where the  `phone_model`  is 'iPhone' to $600:

```
UPDATE sales SET price_per_phone = 600 WHERE phone_model = 'iPhone';

```

## 23. Deleting Rows

We can also delete rows from a table using the  `DELETE`  statement. The basic syntax for  `DELETE`  is as follows:

```
DELETE FROM table_name WHERE condition;

```

Here is an example of using  `DELETE`  to delete all rows from a  `sales`  table where the  `phone_model`  is 'iPhone':

```
DELETE FROM sales WHERE phone_model = 'iPhone';

```

## Coding Exercise 6: Try Updating Records In a Table!

Let's practice using the  `UPDATE`  statement to modify rows in a table.

Suppose we have a  `users`  table that contains information about users, including their name and age. We want to update the age of the user named 'Alice' to 35.

## Coding Exercise 6: Try Updating Records In a Table!

Write a SQL query that updates the  `age`  column of the  `users`  table to 35 for the row where the  `name`  column is 'Alice'.

## 24. A Solution for Updating Rows

Here is a possible solution to  Coding Exercise 6:

```
UPDATE users SET age = 35 WHERE name = 'Alice';

```

This solution uses  `UPDATE`  to modify the  `age`  column of the  `users`  table to 35 where the  `name`  column is  `'Alice'`.

## Coding Exercise 7: Practice Deleting Records

Let's practice using the  `DELETE`  statement to delete rows from a table.

Suppose we have a  `customers`  table that contains information about customers, including their name and email address. We want to delete all rows from the  `customers`  table where the  email address  ends in '@example.com'.

## Coding Exercise 7: Practice Deleting Records

Write a SQL query that deletes all rows from the  `customers`  table where the  `email`  column ends in '@example.com'.

## 25. Solution for Deleting Rows

Here is a possible solution to  Coding Exercise 7:

```
DELETE FROM customers WHERE email LIKE '%@example.com';

```

This solution uses  `DELETE`  to remove all rows from the  `customers`  table where the  `email`  column ends in '@example.com'. The  `LIKE`  keyword is used with the  `%`  wildcard to match any email address that ends with '@example.com'.
