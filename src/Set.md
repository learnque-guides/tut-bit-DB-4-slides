# Set

Set operators are operators that combine rows from two query result sets (or multisets). Some of the operators remove duplicates from the result, and hence return a set, whereas others don’t, and hence return a multiset. T-SQL supports the following operators: 
* UNION, 
* UNION ALL, 
* INTERSECT,
* EXCEPT.

Syntax:

```sql
Input Query1
<set_operator>
Input Query2
[ORDER BY ...];
```

*A set operator expects multisets as inputs, the two queries involved cannot have ORDER BY clauses.*

*Standard SQL supports two “flavors” of each operator—DISTINCT (the default) and ALL. The DISTINCT flavor eliminates duplicates and returns a set. ALL doesn’t attempt to remove duplicates and therefore returns a multiset.*