### Integrity Constraints (IC).
- It's condition that **MUST** hold for ANY instance in db.
- It's **domain** constraints.
### 1. **UNIQUE KEY** - Can be applied to a column to make each value UNIQUE and NOT NULL;

- ADDING PRIMARY KEY CONSTR. AT **DEFINITION**
``` sql
    create table transactions(
        transaction_id int primary key, -- PRIMARY KEY ADDED
        amount decimal(5,2)
    );
```
``` sql
    alter table transactions
    add constraint 
    primary key(transaction_id);
```
#### 1.1 You can only have 1 primary key per table!
- TESTING PRIMARY KEY CONSTRAINT.
``` sql
-- ALLOWED ROWS
INSERT INTO transactions (transaction_id, amount) VALUES
(1, 100.50),
(2, 200.75),
(3, 150.25),
(4, 250.00),
(5, 99.99),
(6, 500.40),
(7, 75.10),
(8, 300.00),
(9, 125.80),
(10, 450.30);

-- TESTING
insert into transactions
values (3, 230.32);     -- FAILED TRANSACTION (not unique id!)

insert into transactions
values (NULL, 230.32)   -- FAILED TRANSACTION (null at id!)
```
- dropping primary key
``` sql
alter table transactions
drop primary key;
```
### 2. CANDIDATE KEY - has same restritions as primary, but
- One table can have multiple candidate keys.
- Added by UNIQUE constraint.

### 4. SUPER KEY
- #### any combination of columns that uniquely identifies a record (may have extra columns not necessary for uniqueness).

### 5. FOREIGN KEY
- #### It's a PRIMARY KEY of one table that can be also in different another tables.
- #### We will establish link between them

Example:
- #### adding foreign key
``` sql
    create table transactions(
        transaction_id int primary key, -- PRIMARY KEY ADDED
        amount decimal(5,2),
        customer_id int,
        -- HERE customer_id :
        -- WILL BE PRIMARY KEY OF ANOTHER TABLE
        -- AND AT SAME TIME FOREIGN KEY OF THIS TABLE

        -- add foreign key constraint
        foreign key(customer_id) references customers(customer_id);
    );

    create table customers(
        customer_id int primary key,
        first_name varchar(50),
        last_name varchar(50)
    );
```

- now we have foreign key in **transaction** linked to **customers**.
``` sql
    -- fill tables
    INSERT INTO transactions (transaction_id, amount, customer_id) VALUES
    (1, 150.00, 101),
    (2, 200.50, 102),
    (3, 250.75, 103),
    (4, 300.60, 104),
    (5, 120.40, 105),
    (6, 180.30, 106),
    (7, 500.00, 107),
    (8, 75.90, 108),
    (9, 110.20, 109),
    (10, 220.10, 110);

    INSERT INTO customers (customer_id, first_name, last_name) VALUES
    (101, 'John', 'Doe'),
    (102, 'Jane', 'Smith'),
    (103, 'Alice', 'Johnson'),
    (104, 'Bob', 'Brown'),
    (105, 'Charlie', 'Davis'),
    (106, 'Debbie', 'Miller'),
    (107, 'Eve', 'Wilson'),
    (108, 'Frank', 'Moore'),
    (109, 'Grace', 'Taylor'),
    (110, 'Hank', 'Anderson');

    -- you can see that all 10 transactions are also 
    -- recorded by customers table
    select first_name, customers.customer_id 
    from customers, transactions
    where customers.customer_id = transactions.customer_id;
```

- #### dropping foreign key
``` sql
    alter table transactions
    drop foreign key(name_of_foreign_key_constraint);
-- NOTE: name is by default found in schema view on left panel.
```
- #### adding foreign key with custom name (for later add).
``` sql 
    alter table transactions
    add constraint fk_customer_id -- name will call fk constr.
    foreign key(customer_id) references customers(customer_id);
```

### benefits of using this "linking"
- now, each customer_id in **transactions** table references **customers** table.
- now, we will not be able to destroy this link!\
I.e we can't now delete customer row in **customers** table\
if this customer_id is in **transactions**.
> useful to prevent losing info that's related with another tables.

i.e
``` sql
delete from customers
where customer_id = 101; -- NOT ALLOWED (have related data in transactions).
```

> However, we still can delte data that's not recorded in linked tables.
``` sql
insert into customers
values (111, "billi", "jean"); -- creates new record, which is NOT IN transactions.

delete from customers
where customer_id = 111; -- ALLOWED (doesn't hurt related table transactions ).
```