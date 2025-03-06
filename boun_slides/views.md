## Views  - a virtual table based on result set of query stmt.
> - fields in a virtual are fields from one or more real tables in db.

OUR EXAMPLE:
``` sql
create table employees(
employee_id int, first_name varchar(50), 
last_name varchar(50), hourly_pay decimal(5, 2), 
job varchar(50), hire_date date
);

INSERT INTO employees (employee_id, first_name, last_name, hourly_pay, hire_date)
VALUES 
(2, "Squidward", "Tentacles" , 15.00, "2023-01-3"),
(3, "Spongebob", "Squarepants", 12.50, "2023-01-05"),
(4, "Patrick", "Star", 12.50, "2023-01-05");

-- note:  unfilled attributes will be NULL -- NO NULL constr. (won't be available.)
```

USAGES:

1. NO REDUNDANCY

    - We may want to create table of only names and last names in **employees** table. \
      By using view -> no redundancy will happen.
    > Instead of repeating data of table, just use view to this table.

    - **CREATING** view of that view.
    ``` sql
        CREATE VIEW employee_attendance AS
        SELECT first_name, last_name
        FROM employees;

        -- since it has properties of normal table
        -- treat as ordinary table
        select * from employee_attendance;
    ```
    > Note we can also change column names of VIEW (OPTIONAL)
    ``` sql
        CREATE VIEW employee_attendance (fname, lname) AS
        SELECT first_name, last_name
        FROM employees;
    ```
    - **DROPING** view
    ``` sql
        drop view employe_attendance;
    ```



2. Security - we can hidde unwanted details about object by making view.

``` sql
    -- Create student table and fill it.
    CREATE TABLE students(sid INT, name VARCHAR(20), login VARCHAR(20), gpa DECIMAL(4, 1));

    INSERT INTO students
    VALUES
    (53666, "Jones", "jones@cs", 3.4),
    (53688, "Smith", "smith@ee", 3.2),
    (53650, "Smith", "smith@math", 3.8),
    (53800, "Ahmed", "ahme@gmail.com", 3.7);

    -- View creation with optional column. name change
    -- though we set to same naming!
    CREATE VIEW HighHonorStudents(name, cid) AS
    select s.name, s.sid
    from students s
    where s.gpa > 3.5;
```

2.1 Note, view doens't copy data, it is just referencing to tables it's based on.\
Thus, if we change tables it's combined of, view will give us still up-to-date results!
``` sql
    INSERT INTO students
    VALUES (53801, "Nikolas", "niko@gmail.com", 3.9);
    SELECT * FROM highHonorStudents;
```