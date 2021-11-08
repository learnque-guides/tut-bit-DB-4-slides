# Common table expression

* Common table expressions (CTEs) are another standard form of table expression similar to derived tables.
* CTEs are defined by using a WITH statement and have the following general form:

```sql
WITH <CTE_Name>[(<target_column_list>)]
AS (
  <inner_query_defining_CTE>
)
<outer_query_against_CTE>;
```

* As with derived tables, as soon as the outer query finishes, the CTE goes out of scope.

CTE gives an advantage over derived table queries.

One advantage is that if you need to refer to one CTE from another, you don’t nest them; rather, you separate them by commas.

```sql
WITH C1 AS
(
    SELECT YEAR(orderdate) AS orderyear, custid
    FROM Sales.Orders
),
C2 AS
(
    SELECT orderyear, COUNT(DISTINCT custid) AS numcusts
    FROM C1
    GROUP BY orderyear
)
SELECT orderyear, numcusts
FROM C2
WHERE numcusts > 70;
```