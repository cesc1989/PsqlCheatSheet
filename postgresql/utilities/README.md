# Utilities

This section covers some utility commands to do useful things with your database.

## Start/stop PostgreSQL server in macOS

### Run as a system service

Check out instructions with `brew info postgres`

```bash
postgresql: stable 11.3 (bottled), HEAD
Object-relational database system
https://www.postgresql.org/
Conflicts with:
  postgres-xc (because postgresql and postgres-xc install the same binaries.)
/usr/local/Cellar/postgresql/11.3 (3,187 files, 35.5MB) *
  Poured from bottle on 2019-05-13 at 17:41:03
From: https://github.com/Homebrew/homebrew-core/blob/master/Formula/postgresql.rb
==> Dependencies
Build: pkg-config ✔
Required: icu4c ✔, openssl ✔, readline ✔
==> Options
--HEAD
	Install HEAD version
==> Caveats
To migrate existing data from a previous major version of PostgreSQL run:
  brew postgresql-upgrade-database

To have launchd start postgresql now and restart at login:
  brew services start postgresql
Or, if you don't want/need a background service you can just run:
  pg_ctl -D /usr/local/var/postgres start
==> Analytics
install: 95,429 (30 days), 251,748 (90 days), 806,525 (365 days)
install_on_request: 86,856 (30 days), 228,361 (90 days), 713,206 (365 days)
build_error: 0 (30 days)
```

Notice instruction `brew services start postgresql`

### Start Manually

```bash
$ pg_ctl -D /usr/local/var/postgres start
```

### Stop Manually

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
