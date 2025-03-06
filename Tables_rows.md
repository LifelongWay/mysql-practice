## - INSERT INTO/UPDATE SET/DELETE FROM 

- **INSERT** a ROW into a table:
``` sql
CREATE TABLE employees (
    employee_id INT,
    first_name VARCHAR(50), 
    last_name VARCHAR(50),
    hourly_pay DECIMAL(),
    hire_date DATE
);

INSERT INTO employees
VALUES(1, "Eugene", "Krabs", 25.50, "2023-01-02"); 
```
> NOTE: must **FOLLOW ORDER OF ATTRIBUTES** and **domains**

- **INSERT** multiple ROWS:
``` sql
INSERT INTO employees
VALUES 
(2, "Squidward", "Tentacles" , 15.00, "2023-01-3"),
(3, "Spongebob", "Squarepants", 12.50, "2023-01-05"),
(4, "Patrick", "Star", 12.50, "2023-01-05"),
```
- **INSERTING** INCOMPLETE(MISSING DATAROW)
``` sql
INSERT INTO employees
VALUES
(5, "Sandy", "Cheeks", 17.25);
```
> GIVES ERROR: not match with schema field count.

SOLUTION: - specify fields of schema before add!
``` sql
INSERT INTO employees (employee_id, first_name, last_name)
VALUES (6, "Sheldon", "Plankton");
```
> NOTE: now, we add to columns separately, not entire row to table. -> that's why we don't get error!

Not specified fields will be empty!

---
- **UPDATE/SET** row attr. value(s):
``` sql
-- one value updated
UPDATE employees
SET hourly_pay = 10.25
WHERE employee_id = 6;

-- multiple values updated
UPDATE employees
SET hourly_pay = 10.50
    hire_date = "2023-01-07"
WHERE employee_id = 6;
```

- **UPDATE/SET** ALL ROWS(DANGEROUS):
> simply don't specify which rows by **removing WHERE**.
```sql
-- will set same attribute value to all rows.
UPDATE employees
SET hourly_pay = 10.50
    hire_date = "2023-01-07"
```
---

- **DELETEING** rows from table:
``` sql 
DELETE FROM employees
WHERE employee_id = 66;
```
> NOTE: not specifying WHERE will delete ALL ROWS!

But, table will still exist.
To delete it completely, just DROP it!