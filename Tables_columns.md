- About data types:
  1. VARCHAR(MAX_LENGTH).
  2. DECIMAL(MAX_LENGTH, PRECISION).
  3. DATE - for date.
  4. DATETIME - for date with time.

---
- **CREATE** table:
``` sql
CREATE TABLE employees (
    employee_id INT,
    first_name VARCHAR(50), 
    last_name VARCHAR(50),
    hourly_pay DECIMAL(),
    hire_date DATE
);
```
---

- **SELECT** table:
``` sql
SELECT * FROM employees;
```
> here * means "ALL"
- **RENAME** table:
``` sql
RENAME TABLE employees TO workers;
```
- **DROP** table:
``` sql
DROP TABLE employees;
```
---
- **ALTER** table to **ADD**:
``` sql
ALTER TABLE employees
ADD phone_number VARCHAR(15);
```

- **ALTER** table to **rename** added schema field:
``` sql
ALTER TABLE employees
RENAME COLUMN phone_number TO email;
```

- **ALTER** to **change datatype**
``` sql
ALTER TABLE employees
MODIFY COLUMN email VARCHAR(100);
```
> - need to refresh schemas

- **Change order** in schema:
``` sql 
ALTER TABLE employees
MODIFY first_name VARCHAR(50)
AFTER last_name; 

-- To show change
-- SELECT * FROM employees;
```
> NOTE: we need to write datatype of col-mn we move.

- **ALTER** to **DROP** schema field(i.e col-mn):
``` sql
ALTER TABLE employees
DROP COLUMN email;
```