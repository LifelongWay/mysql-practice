### Alias - (AS - keyword).
> NOTE: SOMETIMES AS DOESN"T WORK - instead just delete AS and use as it's there!
- Used to give temporary name for
  1. table 
  2. column
- Exist only within query.

- Alias Column 
``` sql 
SELECT column_name AS alias_name
FROM table_name;

--  USE ?
```
- Alias Table
``` sql
SELECT alias_name.table_name
FROM table_name AS alias_name;

-- ex:
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE 
c.CustomerName='Around the Horn' 
AND c.CustomerID=o.CustomerID;
```
ALIAS WITHOUT (AS) -- IN my version of mysql
``` sql
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers c, Orders o
WHERE 
c.CustomerName='Around the Horn' 
AND c.CustomerID=o.CustomerID;
```

- If we didn't use alias in last ex, then it'll be:
``` sql
SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName='Around the Horn' 
AND Customers.CustomerID=Orders.CustomerID;
```