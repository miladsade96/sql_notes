# Retrieving Data From A Single Table

## SELECT:
The `SELECT` clause in `SQL` is used to specify the columns that you want to retrieve from a table

#### Selecting a database to query:
```mysql
USE database_Name;
```

---

#### Selecting all columns from a table:
```mysql
SELECT * FROM customers_table;
```

---

#### Filtering data using *WHERE* clause:
```mysql
SELECT * FROM customers_table WHERE customer_id = 1;
```

---

#### Sorting data based on a specific column:
```mysql
SELECT * FROM customers_table ORDER BY first_name;
```

---

#### Commenting out queries using --:
```mysql
-- SELECT * FROM customers_table;
```

---

#### Selecting specific columns to get from a table:
```mysql
SELECT first_name, last_name, points FROM customers_table;
```

---

#### Executing an arithmetic expression based on the column of the table:
```mysql
--- Order of math operators matter
SELECT first_name, last_name, points, points * 10 + 100 FROM customers_table;
```

---

#### Specifying an alias to arithmetic expression:
```mysql
SELECT 
    first_name,
    last_name,
    points,
    points * 10 + 100 AS discount_factor
FROM customers_table;
--- Alias name should be sourounded by quotes in case there is a space between
```

---

#### Selecting a unique list of values in the column:
```mysql
SELECT DISTINCT state FROM customers_table;
```

---

## WHERE:
The `WHERE` clause in `SQL` is used to filter the results of a query based on specific conditions. It allows you to specify criteria that must be met for a row to be included in the result set.

#### Selecting all customers with *points* greater than 3000:
```mysql
SELECT * FROM customers_table WHERE points > 3000;

-- Other operators: >   >=  <   <=  =   !=  <>
```

---

#### Selecting only customers that are located in virginia:
```mysql
SELECT * FROM customers_table WHERE state = "VA";
-- String "VA" is not case sensitive
```

---

#### Selecting all customers that are located outside of virginia:
```mysql
SELECT * from customers_table WHERE state != "VA";
-- != and <> are equivalent
```

---

#### Selecting only customers are born after january first 1990:
```mysql
SELECT *
FROM customers_table
WHERE birth_date > "1990-01-01";    -- Date default format in sql: yyyy-mm-dd
```
---

## AND, OR, NOT:
`AND`, `OR`, and `NOT` are logical operators used in `SQL` to combine multiple conditions in the `WHERE` clause.

#### Selecting all customers that are born after january first 1990 and have points more than 1000:
```mysql
Select * From customers_table WHERE birth_date > "1990-01-01" AND points > 1000;

-- Both conditions should be true
```

---

#### Selecting all customers that are born after january first 1990 or have points more than 1000:
```mysql
Select * FROM customers_table WHERE birth_date > "1990-01-01" OR points > 1000;

-- At least one of the conditions should be true
```

---

#### Selecting all customers that are born either after 1990 or they have more than 1000 points and live in virginia:
```mysql
SELECT * from customers_table WHERE birth_date > "1990-01-01" OR points > 1000 AND state = "VA";

-- AND operator always evaluated before OR
```

---

#### Selecting all customers that are not born after january first 1990 or not have points more than 1000:
```mysql
Select * FROM customers_table WHERE NOT (birth_date > "1990-01-01" OR points > 1000);

-- Equivalent to below:

Select * FROM customers_table WHERE birth_date <= "1990-01-01" AND points <= 1000;
```

---

## IN:
The `IN` operator in `SQL` is used to check if a value exists within a list of values. It's a convenient way to simplify queries that involve multiple `OR` conditions.

#### Selecting all customers that are located in virginia or georgia or florida:
```mysql
SELECT * FROM customers_table WHERE state = "VA" OR state = "GA" OR state = "FL";

-- Equivalent to below using IN operator:

Select * FROM customers_table WHERE state IN ("VA", "GA", "FL");
```

---

#### Selecting all customers that are not located in virginia or georgia or florida:
```mysql
SELECT * FROM customers_table WHERE state NOT IN ("VA", "GA", "FL");
```

---

## BETWEEN:
The `BETWEEN` operator in `SQL` is used to check if a value falls within a specified range. It's a convenient way to simplify queries that involve multiple comparison operators.

#### Selecting all customers that have more than 1000 and less than 3000 points:
```mysql
SELECT * FROM customers_table where points BETWEEN 1000 AND 3000;

-- Range is inclusive ---> 1000 <= points <= 3000 
```

---

## LIKE:
The `LIKE` operator in `SQL` is used for pattern matching. It allows you to search for rows that contain specific patterns within a column.

#### Selecting only customers who's last name starts with `b`:
```mysql
SELECT * FROM customers_table WHERE last_name LIKE "b%";

-- % means any number of characters - case insensitive
```

---

#### Selecting only customers who's last name starts with `brush`:
```mysql
SELECT * FROM customers_table WHERE last_name LIKE "brush%";
```

---

#### Selecting all customers who have `b` somewhere in their last name:
```mysql
SELECT * FROM cusomers_table WHERE last_name LIKE "%b%";
```

---

#### Selecting only customers who's last name ends with `y`:
```mysql
SELECT * FROM customers_table WHERE last_name LIKE "%y";
```

---

#### Selecting only customers whose length of their last name is 6 characters and ends with `y`;
```mysql
SELECT * FROM customers_table WHERE last_name LIKE "_____y";

-- _ means a single character
```

---

#### Selecting only customers whose length of their last name is 6 characters and starts with `b` and ends with `y`;
```mysql
SELECT * FROM customers_table WHERE last_name LIKE "b____y";
```

---

## REGEXP:
The `REGEXP` operator is a powerful tool for pattern matching in `SQL`, providing more flexibility and advanced features compared to the `LIKE` operator. While its availability and syntax may vary slightly across different database systems, the core concept remains consistent.

#### Selecting all customers who have `field` in their last name:
```mysql
SELECT * FROM custoemrs_table WHERE last_name LIKE "%field%"

-- Equivalent to below:

SELECT * FROM customers_table WHERE last_name REGEXP "field";
```

---

#### Selecting all customers whose last name starts with `field`:
```mysql
SELECT * From customers_table WHERE last_name REGEXP "^field";
```

---

#### Selecting all customers whose last_name ends with `field`:
```mysql
SELECT * FROM customers_table WHERE last_name REGEXP "field$";
```

---

#### Selecting all customers who have words `field` or `mac` in their last name:
```mysql
SELECT * FROM customers_table WHERE last_name REGEXP "field|mac";
```

---

#### Selecting all customers who have words `field` or `mac` or `rose` in their last name:
```mysql
SELECT * FROM customers_table WHERE last_name REGEXP "field|mac|rose";
```

---

#### Selecting all customers whose last name ends with word `field` or have words `mac` or `rose` in their last name:
```mysql
SELECT * FROM customers_table WHERE last_name REGEXP "field$|mac|rose";
```

---

#### Selecting all customers who have words `ge` or `ie` or `me` in their last name:
```mysql
SELECT * FROM customers_table WHERE last_name REGEXP "[gim]e";
```

---

#### Selecting all customers who have range of characters from `a` to `h` before character `e` in their last name:
```mysql
SELECT * FROM customers_table WHERE last_name REGEXP "[a-h]e";
```

---

## IS NULL:
The `IS NULL` operator in SQL is used to check if a value is null. A null value represents the absence of data.

#### Selecting all customers that do not have a phone number:
```mysql
SELECT * FROM customers_table WHERE phone IS NULL;
```

---

#### Selecting all customers that do have a phone number:
```mysql
SELECT * FROM customers_table WHERE phone IS NOT NULL;
```

---

## ORDER BY:
The `ORDER BY` clause in SQL is used to sort the results of a query based on one or more columns. It allows you to arrange the rows in `ascending` or `descending` order.

#### Selecting all customers and sort them based on their `first name` in ascending order:
```mysql
SELECT * FROM customers_table ORDER BY first_name;
```

---

#### Selecting all customers and sort them based on their `first name` in descending order:
```mysql
SELECT * FROM customers_table ORDER BY first_name DESC;
```

---

#### Selecting all customers and sort them based on their `state` in ascending order and for each `state` sort them based on their `first name` in ascending order:
```mysql
SELECT * FROM customers_table ORDER BY state, first_name;
```

---

#### Selecting all customers and sort them based on their `state` in descending order and for each `state` sort them based on their `first name` in descending order:
```mysql
SELECT * FROM customers_table ORDER BY state DESC , first_name DESC;
```

---

#### Selecting first name and last name of all customers and sort them based on their birthdate:
```mysql
SELECT first_name, last_name FROM customers_table ORDER BY birth_date;
```

---

#### Selecting and sorting customers based on an alias:
```mysql
SELECT first_name, last_name, 10 AS points FROM customers_table ORDER BY points, first_name;
```

---

## LIMIT:
The `LIMIT` clause in `SQL` is used to specify the maximum number of rows to return from a query. It's particularly useful when dealing with `large datasets` or when you only need a subset of the results.

#### Selecting only 3 customers from customers table:
```mysql
SELECT * FROM customers_table LIMIT 3;
```

---

#### Implementing the pagination in sql so that skip first 6 records and get other 3 records after skip section:
```mysql
SELECT * FROM customers_table LIMIT 6, 3;
```
