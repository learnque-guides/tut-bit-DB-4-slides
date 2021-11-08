# Exercise 2

Write a query that returns the maximum value in the orderdate column for each employee:

* Table involved: Sales.Orders table
* Desired output:

```sql
empid       maxorderdate
----------- -------------
3           2016-04-30
6           2016-04-23
9           2016-04-29
7           2016-05-06
1           2016-05-06
4           2016-05-06
2           2016-05-05
5           2016-04-22
8           2016-05-06

(9 row(s) affected)
```

Encapsulate the query that you get before in a derived table. Write a join query between the derived table and the Orders table to return the orders with the maximum order date for each employee:

* Table involved: Sales.Orders
* Output:

```sql
empid       orderdate   orderid     custid
----------- ----------- ----------- -----------
9           2016-04-29  11058       6
8           2016-05-06  11075       68
7           2016-05-06  11074       73
6           2016-04-23  11045       10
5           2016-04-22  11043       74
4           2016-05-06  11076       9
3           2016-04-30  11063       37
2           2016-05-05  11073       58
2           2016-05-05  11070       44
1           2016-05-06  11077       65

(10 row(s) affected)
```
