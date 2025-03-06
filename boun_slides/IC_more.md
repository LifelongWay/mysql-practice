### Integrity Constraints (IC) - (continuation of previous .md file)

- #### 4 actions
On trying to delete foreign key's row from its mother table, we will\
**by default** get rejection( NO ACTION ) <=> iff this row's key is referenced in another table.

But, we can override this behaviour.
**SQL supports all 4 options on deletes and updates. Default is NO ACTION (delete/update is rejected)**
- NO ACTION is equivalent to RESTRICT.

#### - Other ways:
  - CASCADE (also delete all tuples that refer to deleted tuple)
  - SET NULL / SET DEFAULT (sets foreign key value of referencing tuple)

    > For different actions:
    - ON DELETE CASCADE
    - ON UPDATE CASCADE
    - ON DELETE SET NULL
    - ON UPDATE SET DEFAULT

EXAMPLE:

- setup
``` sql
CREATE TABLE students (sid CHAR(20),
name CHAR(20), login CHAR(10), gpa REAL);

CREATE TABLE enrolled (sid CHAR(20),
cid CHAR(10), grade CHAR(1));

-- before adding foreign key
-- MUST HAVE PRIMARY KEY in referenced table.
alter table students
add constraint
primary key (sid);

-- now can set foreign key
alter table enrolled
add constraint 
fk_sid foreign key (sid) references students(sid);

INSERT INTO Students (sid, name, login, gpa) VALUES
('S001', 'John Doe', 'jdoe', 3.5),
('S002', 'Jane Smith', 'jsmith', 3.8),
('S003', 'Alice Johnson', 'ajohnson', 3.2),
('S004', 'Bob Brown', 'bbrown', 3.9),
('S005', 'Charlie Davis', 'cdavis', 2.8),
('S006', 'Debbie Miller', 'dmiller', 3.6),
('S007', 'Eve Wilson', 'ewilson', 3.7),
('S008', 'Frank Moore', 'fmoore', 3.4),
('S009', 'Grace Taylor', 'gtaylor', 3.1),
('S010', 'Hank Anderson', 'handerson', 3.5);

INSERT INTO Enrolled (sid, cid, grade) VALUES
('S001', 'CSE101', 'A'),
('S002', 'CSE102', 'B'),
('S003', 'CSE103', 'A'),
('S004', 'CSE104', 'C'),
('S005', 'CSE105', 'B'),
('S006', 'CSE106', 'A'),
('S007', 'CSE107', 'B'),
('S008', 'CSE108', 'A'),
('S009', 'CSE109', 'C'),
('S010', 'CSE110', 'B');
```

- **DEFAULT** - reject delete/update

``` sql
delete from students
where sid = "S001";
-- by default: delete REJECTED

update students 
set sid = "S011"
where sid = "S001";
-- by default: update foreign key val. REJECTED
```

- **CASCADED UPDATE**
``` sql
-- TO MODIFY already defined behavior
-- we will have to drop and readd constraint
alter table enrolled
drop constraint fk_sid;

alter table enrolled
add constraint 
    fk_sid foreign key(sid) 
        references students(sid) on update cascade;

-- now, UPDATING VALUE WILL UPDATE ALL RELATED TABLES
update students 
set sid = "S011"
where sid = "S001";

-- enrolled table will have changed value!
```

- **SETTING NULL**
    - it simply sets referenced foreign keys to NULL if referenced table changed its value!
