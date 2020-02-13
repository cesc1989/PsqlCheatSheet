# Advanced Stuff

## List Installed Extensions

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

## Install Extension

As a requirement, install the `postgresql-contrib` package.

In Ubuntu can be done with:

```bash
$ sudo apt-get install postgresql-contrib
```

> Seen in [Stack Overflow](https://stackoverflow.com/questions/9025515/how-do-i-import-modules-or-install-extensions-in-postgresql-9-1)

### PostgreSQL 9.1+

Use the `CREATE EXTENSION` command/query.

This is a [list of available modules](https://www.postgresql.org/docs/9.1/sql-createextension.html) to install:

```
adminpack , auth_delay , auto_explain , btree_gin , btree_gist
, chkpass , citext , cube , dblink , dict_int
, dict_xsyn , dummy_seclabel , earthdistance , file_fdw , fuzzystrmatch
, hstore , intagg , intarray , isn , lo
, ltree , oid2name , pageinspect , passwordcheck , pg_archivecleanup
, pgbench , pg_buffercache , pgcrypto , pg_freespacemap , pgrowlocks
, pg_standby , pg_stat_statements , pgstattuple , pg_test_fsync , pg_trgm
, pg_upgrade , seg , sepgsql , spi , sslinfo , tablefunc
, test_parser , tsearch2 , unaccent , uuid-ossp , vacuumlo
, xml2
```

Example:

```bash
CREATE EXTENSION [EXTESION_NAME]

CREATE EXTENSION unaccent;

CREATE EXTENSION "uuid-ossp";
```

## Export or Import Large Tables with `COPY`

The [`COPY` command](https://www.postgresql.org/docs/current/sql-copy.html)

> COPY moves data between PostgreSQL tables and standard file-system files. COPY TO copies the contents of a table to a file, while COPY FROM copies data from a file to a table (appending the data to whatever is in the table already). COPY TO can also copy the results of a SELECT query.

To import to a table from a large CSV file this way:

```
postgres=# \copy table_name FROM /path/to/file.csv WITH DELIMITER ',' CSV HEADER;
```

To export [to a CSV file](https://stackoverflow.com/questions/1120109/how-to-export-table-as-csv-with-headings-on-postgresql) from a table:

```
postgres=# \copy table_name TO '/path/to/file.csv' WITH (FORMAT CSV, HEADER);
```