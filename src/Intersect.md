# Intersect

The INTERSECT operator returns only the rows that are common to the results of the two input queries.

<div style="text-align: center">
    <img alt="Intersect" src="./images/intersect.png" width="250" />
</div>

```sql
SELECT country, region, city FROM HR.Employees
INTERSECT
SELECT country, region, city FROM Sales.Customers;
```

Instead of using the INTERSECT operator it is possible to use an alternative tool like an inner join or a correlated subquery, you need to add special treatment for NULLs—for example, assuming the alias E for Employees and C for


INTERSECT do not support ALL, but thanks to StackOverflow we can do that by ourself:

```sql
SELECT
  ROW_NUMBER()
    OVER(PARTITION BY country, region, city
         ORDER     BY (SELECT 0)) AS rownum,
  country, region, city
FROM HR.Employees

INTERSECT

SELECT
  ROW_NUMBER()
    OVER(PARTITION BY country, region, city
         ORDER     BY (SELECT 0)),
  country, region, city
FROM Sales.Customers;
```

