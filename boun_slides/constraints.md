### CONSTRAINTS

- ### UNIQUE
>- all values in a column MUST BE different.
``` sql
-- UNIQUE when creating
create table products (
    product_id int,
    product_name varchar(25) unique, -- HERE UNIQUE 
    price decimal(4, 2)
);

-- UNIQUE after creating( can do it later)
alter table products
add constraint
unique(product_name);
```

> testing
``` sql
    insert into products
    values
    (100, "hamburger", 3.99),
    (101, "fries", 1.89),
    (102, "soda", 1.00),
    (103, "ice cream", 1.49),
    (104, "fries", 1.75);   -- DUPLICATE with (101)
```
> ERROR! -Query failed!
---

- ### NOT NULL
> every value in column MUST NOT BE NULL
``` sql
-- UNIQUE when creating
create table products (
    product_id int,
    product_name varchar(25) unique,
    price decimal(4, 2) not null    -- HERE NOT NULL
);

-- UNIQUE after creating( can do it later ) , but not allowed if already have null 
alter table products
modify price decimal(4, 2) not null; 
```
>> different from unique constr. adding\

> testing 
``` sql
insert into products
values (1, "kebab", null)
```
> Error! Price can't be null! 

---

- ### CHECK (general constraints)
- can be named(identified) or unnamed.
> Impose range restriction of variable value
``` sql
create table employees
(
    employee_id int,
    first_name varchar(50), 
    last_name varchar(50),
    hourly_pay decimal(5,2),
    hire_date date,
    check( hourly_pay >= 10.0) -- UNIdentified check constraint
    constraint chk_hourly_pay check(hourly_pay) -- Identified check constraint
);
```
- - Adding later
``` sql
alter table employees
 add constraint chk_hourly_pay check(hourly_pay >= 10);
```
- - Removing
``` sql
-- general way
alter table employees
  drop constraint chk_hourly_pay;

-- specific way for check
alter table employees
  drop check chk_hourly_pay;
```