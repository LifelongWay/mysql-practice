#### setup
``` sql
CREATE TABLE students (sid CHAR(20),
name CHAR(20), login CHAR(10), gpa REAL);

CREATE TABLE enrolled (sid CHAR(20),
cid CHAR(10), grade CHAR(1));

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
- Add **Primary Key** constraints.
1.  Each student has 
   - unique sid identifying them"
   - unique login

``` sql
    -- Implementation
    alter table students 
    add constraint 
    primary key(sid), -- sid is PRIMARY KEY
    unique (login); -- login is CANDIDATE KEY
```

2. Only student listed in Students relation(table) is able to enroll\
to a course.
``` sql
    -- Implementation
    alter table students
    add constraint primary key(sid);

    alter table enrolled
    add constraint
    fk_students foreign key(sid) references students;
```
now, we aren't able to add students to **enrolled** if their **sid** isn't in\
**students** relation(table)
``` sql
INSERT INTO Enrolled (sid, cid, grade) VALUES
('S011', 'CSE111', 'A'),
('S012', 'CSE112', 'B'),
('S013', 'CSE113', 'C'),
('S014', 'CSE114', 'A'),
('S015', 'CSE115', 'B');

-- ERROR! (they're not in students)
```