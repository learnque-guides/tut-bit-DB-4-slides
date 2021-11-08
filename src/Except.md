# Except

The **EXCEPT** operator implements set differences. It operates on the results of two input queries and returns rows that appear in the first input but not the second.

<div style="text-align: center">
    <img alt="Except" src="./images/except.png" width="250" />
</div>

```sql
SELECT country, region, city FROM HR.Employees
EXCEPT
SELECT country, region, city FROM Sales.Customers;
```

There are alternatives to the EXCEPT operator. One is an outer join that filters only outer rows, and another is to use the NOT EXISTS predicate.

The EXCEPT ALL operator is similar to the EXCEPT operator, but it also takes into account the number of occurrences of each row. If a row R appears x times in the first multiset and y times in the second, and x > y, R will appear x – y times in Query1 EXCEPT ALL Query2. In other words, EXCEPT ALL returns only occurrences of a row from the first multiset that do not have a corresponding occurrence in the second.

T-SQL do not support EXCEPT ALL but we can implemt it in the same way as we did with INTERSECT:

```sql
WITH EXCEPT_ALL
AS
(
  SELECT
    ROW_NUMBER()
      OVER(PARTITION BY country, region, city
           ORDER     BY (SELECT 0)) AS rownum,
    country, region, city
    FROM HR.Employees

  EXCEPT

  SELECT
    ROW_NUMBER()
      OVER(PARTITION BY country, region, city
           ORDER     BY (SELECT 0)),
    country, region, city
  FROM Sales.Customers
)
SELECT country, region, city
FROM EXCEPT_ALL;
```