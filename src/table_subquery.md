# Derived table expression

* Derived tables (also known as table subqueries) are defined in the FROM clause of an outer query. Their scope of existence is the outer query. 
* As soon as the outer query is finished, the derived table is gone.

```sql
USE lessons;

SELECT *
    FROM (
        SELECT custid, companyname
        FROM Sales.Customers
        WHERE country = N'USA'
    ) AS USACusts;
```

* Order is not guaranteed. A table expression is supposed to represent a relational table, and the rows in a relational table have no guaranteed order.
* All columns must have names. All columns in a table must have names; therefore, you must assign column aliases to all expressions in the SELECT list of the query that is used to define a table expression.
* All column names must be unique. All column names in a table must be unique; therefore, a table expression that has multiple columns with the same name is invalid.

One of the way to use table expression:

This will throw an error:

```sql
SELECT
  YEAR(orderdate) AS orderyear,
  COUNT(DISTINCT custid) AS numcusts
FROM Sales.Orders
GROUP BY orderyear;
```

To solve this issue we can use table expression and name aliases:

```sql
SELECT orderyear, COUNT(DISTINCT custid) AS numcusts
FROM (
    SELECT YEAR(orderdate) AS orderyear, custid
    FROM Sales.Orders
) AS D
GROUP BY orderyear;
```

*Table expressions have neither a positive nor negative impact on performance when compared to the expanded query without the table expression.*

In the query that defines a derived table, we can refer to arguments.

```sql
DECLARE @empid AS INT = 3;

SELECT orderyear, COUNT(DISTINCT custid) AS numcusts
FROM (
    SELECT YEAR(orderdate) AS orderyear, custid
        FROM Sales.Orders
        WHERE empid = @empid
) AS D
GROUP BY orderyear;
```

## Nesting

If you need to define a derived table based on a query that itself is based on a derived table, you can nest those.

```sql
SELECT orderyear, numcusts
FROM (SELECT orderyear, COUNT(DISTINCT custid) AS numcusts
        FROM (SELECT YEAR(orderdate) AS orderyear, custid
                FROM Sales.Orders
            ) AS D1
            GROUP BY orderyear
    ) AS D2
WHERE numcusts > 70;
```