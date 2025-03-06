### Terminology
- database - similar to folder.
- table - similar to file within a folder.



- **Create** db:
``` sql
CREATE DATABASE myDB;
```
---

> - keyword aren't case-sensitive, so you can use lower-case if you want.

> - all stmts must end with semicolon.
---

- **Use** db:
``` sql
USE myDB;
```
> - also can be done by selecting "use as default schema".
---

- **Drop** db:
``` sql
DROP myDB;
```
> DB will be gone.
---

- **Set to Read-only**  mode:
``` sql
ALTER DATABASE myDB READ ONLY = 1;
```
> Modifications will be NOT ALLOWED.
<blockquote>

example:
1. CREATE DATABASE myDB1;\
2. USE DATABASE myDB1;\
3. ALTER DATABASE myDB1 READ ONLY = 1;\
4. DROP DATABASE myDB1; **-- ERROR**

> **DROP NOT ALLOWED due to READ-ONLY**!
- To Drop: - remove READ ONLY.
5. ALTER DATABASE myDB1 READ ONLY = 0;
6. DROP DATABASE myDB1; 
</blockquote>

--- 
