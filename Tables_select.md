### Select - for quering data from table.
---
- **SELECT** all rows:
``` sql
SELECT * 
FROM employees;
```
- **SELECT** rows with specific fields:
``` sql
SELECT first_name, last_name
FROM employees;
```
> You can also change order.
``` sql
SELECT last_name, first_name;
FROM employees;
```

- **SELECT** rows with specific field values:
``` sql
-- ex1:
SELECT * 
FROM employees
WHERE first_name = "Spongebob";

-- ex2: no value check
SELECT *
FROM employees
WHERE hire_date IS NULL;
```
> = NULL doesn't work!\
> can use: IS NULL or IS NOT NULL.
