## Advanced Stuff

### List Installed Extensions

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

### Install Extension

As a requirement, install the `postgresql-contrib` package.

In Ubuntu can be done with:

```bash
$ sudo apt-get install postgresql-contrib
```

> Seen in [Stack Overflow](https://stackoverflow.com/questions/9025515/how-do-i-import-modules-or-install-extensions-in-postgresql-9-1)

#### PostgreSQL 9.1+

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