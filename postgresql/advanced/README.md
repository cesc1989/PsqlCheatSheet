## Advanced Stuff

### List installed extensions

> Seen in [Stack Overflow](https://stackoverflow.com/questions/21799956/using-psql-how-do-i-list-extensions-installed-in-a-database).

You can do it in psql CLI:

```bash
\dx

List of installed extensions
  Name   | Version |   Schema   |         Description          
---------+---------+------------+------------------------------
 plpgsql | 1.0     | pg_catalog | PL/pgSQL procedural language
(1 row)
```

Or with a SQL query:

```bash
SELECT *
FROM pg_extension;

extname | extowner | extnamespace | extrelocatable | extversion | extconfig | extcondition 
---------+----------+--------------+----------------+------------+-----------+--------------
 plpgsql |       10 |           11 | f              | 1.0        |           | 
(1 row)
```