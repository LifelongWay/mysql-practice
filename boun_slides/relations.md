- Creating 2 Relations (tables):
    1. Students (table)
        ``` sql
        CREATE TABLE students(sid INT, name VARCHAR(20), login VARCHAR(20), gpa DECIMAL(4, 1));

        INSERT INTO students
        VALUES
        (53666, "Jones", "jones@cs", 3.4),
        (53688, "Smith", "smith@ee", 3.2),
        (53650, "Smith", "smith@math", 3.8);
        ```


    2. Enrolled (table)

        ``` sql
        CREATE TABLE enrolled(
        sid INT,
        cid VARCHAR(20),
        grade VARCHAR(2)
        );

        INSERT INTO enrolled
        VALUES 
        (53666, "Cmpe321", "AA"),
        (53688, "Math201", "BA"),
        (53688, "Cmpe150", "BA"),
        (53688, "Bio101", "BB");
        ```

- Quering multiple relations
  1. Query for getting (student, course_name) where student got AA grade.(Student must be enrolled!)

        ``` sql
            -- WITHOUT ALIAS
            SELECT students.name, enrolled.cid 
            FROM students, enrolled
            WHERE enrolled.grade = "AA" AND students.sid = enrolled.sid;

            -- WITH ALIAS
            SELECT S.name, E.cid
            FROM students AS S, enrolled AS E
            WHERE E.grade = "AA" AND S.sid = E.sid;
        ```
    