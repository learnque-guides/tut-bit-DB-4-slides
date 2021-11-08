# Exercise 5

Create an inline TVF that accepts as inputs a supplier ID (@supid AS INT) and a requested number of products (@n AS INT). The function should return @n products with the highest unit prices (ordered in descending order) that are supplied by the specified supplier ID.

* Table involved: Production.Products
* When:

```sql
SELECT * FROM Production.TopProducts(5, 2);
```

* Output:

```
productid   productname        unitprice
----------- ------------------ ---------------
12          Product OSFNS      38.00
11          Product QMVUN      21.00

(2 row(s) affected)
```