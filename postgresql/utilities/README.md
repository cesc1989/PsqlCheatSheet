# Utilities

This section covers some utility commands to do useful things with your database.

## Start/stop PostgreSQL server in macOS

### Start Manually

```bash
$ pg_ctl -D /usr/local/var/postgres start
```

### Sop Manually

```bash
$ pg_ctl -D /usr/local/var/postgres stop
```

## Terminate Connections Using PostgreSQL Database

Access the `psql` console

    $ psql --host [host_name] --username [username]

connect to the desired database with the `\c` command

    postgres=# \c [db_name];

and then execute the next query:

    db_name=# SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE pid <> pg_backend_pid() AND datname = 'db_name';

## Find out how many connections are using the database

Access the `psql` console

    $ psql [db_name] --host [host_name] --username [username]

and then execute following query:

    db_name=# SELECT COUNT(*) FROM pg_stat_activity WHERE pid <> pg_backend_pid() AND usename = current_user;
